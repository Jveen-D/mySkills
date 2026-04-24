---
name: electron
description: |
  Electron 框架用于使用 JavaScript、HTML 和 CSS 构建跨平台桌面应用，
  覆盖架构、IPC、安全、打包、自动更新以及后端集成模式。

  USE WHEN: 用户提到 “Electron”“桌面应用”“跨平台应用”，或询问 “IPC”“主进程”“渲染进程”“Electron 打包”“自动更新”“代码签名”“Electron 安全”

  DO NOT USE FOR: Tauri 应用 - 请改用 `tauri` skill
allowed-tools: Read, Grep, Glob, Write, Edit
---
# Electron 核心知识

> **深入资料**：如需完整 API 文档，可使用 `mcp__documentation__fetch_docs`，并指定 technology 为 `electron`。

## 何时不应使用本 Skill

- **Tauri 应用** - Rust 桌面应用应使用 `tauri` skill
- **纯 Web 应用** - Electron 面向桌面应用，而不是 Web 部署
- **移动应用** - Electron 不原生支持 iOS/Android
- **CLI 工具** - 命令行程序请直接使用 Node.js

---

## 架构

### 进程模型

```
┌─────────────────────────────────────────────────────────────┐
│                         主进程                              │
│  - Node.js 运行时（完整访问权限）                           │
│  - Electron API（app、BrowserWindow、ipcMain、dialog）      │
└──────────────────────────┬──────────────────────────────────┘
                           │ IPC 通道
┌──────────────────────────▼──────────────────────────────────┐
│                        Preload 脚本                         │
│  - 在渲染进程之前执行                                        │
│  - 通过 contextBridge 暴露安全 API                          │
└──────────────────────────┬──────────────────────────────────┘
                           │ contextBridge.exposeInMainWorld()
┌──────────────────────────▼──────────────────────────────────┐
│                        渲染进程                              │
│  - Chromium 运行时（标准 Web API）                          │
│  - 默认不直接访问 Node.js                                   │
│  - 通过 preload 暴露的 window.electronAPI                  │
└─────────────────────────────────────────────────────────────┘
```

### 项目结构

```
electron-app/
├── src/
│   ├── main/                    # 主进程
│   │   ├── index.ts             # 入口文件
│   │   ├── window.ts            # 窗口管理
│   │   ├── ipc/                 # IPC 处理器
│   │   └── updater.ts           # 自动更新
│   ├── preload/
│   │   ├── index.ts             # 主 preload
│   │   └── types.d.ts           # 类型声明
│   └── renderer/                # 前端应用
├── resources/                   # 应用图标
├── electron-builder.yml         # 打包配置
└── package.json
```

---

## IPC 通信要点

### Preload 脚本

```typescript
// src/preload/index.ts
import { contextBridge, ipcRenderer } from 'electron';

const electronAPI = {
  openFile: () => ipcRenderer.invoke('dialog:openFile'),
  saveFile: (content: string) => ipcRenderer.invoke('dialog:saveFile', content),
  getVersion: () => ipcRenderer.invoke('app:getVersion'),
};

contextBridge.exposeInMainWorld('electronAPI', electronAPI);

// 事件订阅
contextBridge.exposeInMainWorld('electronEvents', {
  onMenuAction: (callback: (action: string) => void) => {
    const handler = (_e: any, action: string) => callback(action);
    ipcRenderer.on('menu:action', handler);
    return () => ipcRenderer.removeListener('menu:action', handler);
  },
});
```

### 主进程处理器

```typescript
// src/main/ipc/index.ts
import { ipcMain, dialog, app } from 'electron';

export function registerIpcHandlers() {
  ipcMain.handle('dialog:openFile', async () => {
    const result = await dialog.showOpenDialog({
      properties: ['openFile'],
    });
    return result.canceled ? null : result.filePaths[0];
  });

  ipcMain.handle('app:getVersion', () => app.getVersion());
}
```

> **完整参考**：详见 [ipc-security.md](ipc-security.md)，其中包含完整 IPC 模式与类型安全方案。

---

## 安全基础

### 安全的 BrowserWindow 配置

```typescript
const win = new BrowserWindow({
  webPreferences: {
    preload: path.join(__dirname, 'preload.js'),
    contextIsolation: true,      // 必须开启
    nodeIntegration: false,      // 必须关闭
    sandbox: true,               // 推荐开启
    webSecurity: true,           // 永远不要关闭
  },
});

// 内容安全策略（CSP）
win.webContents.session.webRequest.onHeadersReceived((details, callback) => {
  callback({
    responseHeaders: {
      ...details.responseHeaders,
      'Content-Security-Policy': [
        "default-src 'self'",
        "script-src 'self'",
        "connect-src 'self' https://api.example.com",
      ].join('; '),
    },
  });
});
```

### 安全检查清单

- [ ] `contextIsolation: true` - 将 preload 与渲染进程隔离
- [ ] `nodeIntegration: false` - 渲染进程不暴露 Node.js API
- [ ] `sandbox: true` - 启用操作系统级进程沙箱
- [ ] 绝不向渲染进程暴露原始 `ipcRenderer`
- [ ] 在 `ipcMain.handle()` 中校验**所有输入**
- [ ] 凭据使用 `safeStorage` API 保存

> **完整参考**：详见 [ipc-security.md](ipc-security.md)，其中包含完整安全配置。

---

## 打包快速开始

### Electron Builder（`electron-builder.yml`）

```yaml
appId: com.company.app
productName: My Application

mac:
  hardenedRuntime: true
  target: [dmg, zip]

win:
  target: [nsis, portable]

linux:
  target: [AppImage, deb]

publish:
  provider: github
  owner: company
  repo: app
```

### 自动更新

```typescript
import { autoUpdater } from 'electron-updater';

autoUpdater.on('update-available', (info) => {
  dialog.showMessageBox({
    message: `Version ${info.version} available`,
    buttons: ['Download', 'Later'],
  }).then(({ response }) => {
    if (response === 0) autoUpdater.downloadUpdate();
  });
});

autoUpdater.on('update-downloaded', () => {
  autoUpdater.quitAndInstall();
});

// 启动时检查更新
autoUpdater.checkForUpdates();
```

> **完整参考**：详见 [packaging.md](packaging.md)，其中包含完整 Forge 与 Builder 配置。

---

## 后端集成

### 本地 SQLite 数据库

```typescript
import Database from 'better-sqlite3';
import { app } from 'electron';

const db = new Database(path.join(app.getPath('userData'), 'app.db'));
db.pragma('journal_mode = WAL');

export const itemsRepo = {
  getAll: () => db.prepare('SELECT * FROM items').all(),
  create: (data) => db.prepare('INSERT INTO items (name) VALUES (?)').run(data.name),
};
```

### 安全的 Token 存储

```typescript
import { safeStorage } from 'electron';
import Store from 'electron-store';

const store = new Store({ name: 'auth' });

export const tokenStore = {
  setToken(token: string): void {
    if (safeStorage.isEncryptionAvailable()) {
      const encrypted = safeStorage.encryptString(token);
      store.set('accessToken', encrypted.toString('base64'));
    }
  },
  getToken(): string | null {
    const stored = store.get('accessToken') as string;
    if (safeStorage.isEncryptionAvailable()) {
      return safeStorage.decryptString(Buffer.from(stored, 'base64'));
    }
    return stored;
  },
};
```

> **完整参考**：详见 [backend.md](backend.md)，其中包含嵌入式服务、离线优先模式和 WebSocket 集成。

---

## 生产检查清单

### 构建与打包
- [ ] 所有平台都已配置代码签名
- [ ] 已启用 macOS notarization
- [ ] 已启用 ASAR 打包

### 安全
- [ ] 已强制启用所有安全默认项
- [ ] 已配置 CSP 头
- [ ] IPC 处理器会校验所有输入
- [ ] 凭据使用 `safeStorage`

### 性能
- [ ] 启动时间 < 3 秒
- [ ] 已建立内存占用基线

### 监控指标

| 指标 | 警告 | 严重 |
|------|------|------|
| 启动时间 | > 3s | > 5s |
| 内存占用 | > 300MB | > 500MB |
| 崩溃率 | > 0.1% | > 1% |

---

## 反模式

| 反模式 | 问题 | 解决方案 |
|--------|------|----------|
| `nodeIntegration: true` | 严重安全风险 | 使用 `contextIsolation: true` + preload |
| `webSecurity: false` | 会导致 XSS 风险 | 绝不要关闭 |
| 暴露原始 `ipcRenderer` | 安全漏洞 | 使用 `contextBridge.exposeInMainWorld()` |
| 不做输入校验 | 易受注入攻击 | 在 `ipcMain.handle()` 中校验 |
| 硬编码凭据 | 会暴露在 ASAR 中 | 使用 `safeStorage` API |
| `ipcRenderer.sendSync` | 阻塞渲染进程 | 使用异步 `invoke()` |

---

## 快速排障

| 问题 | 解决方法 |
|------|----------|
| `require is not defined` | 使用 preload + `contextBridge` |
| IPC 返回 `undefined` | 检查通道名是否一致 |
| 启动白屏 | 查看 DevTools 控制台 |
| 自动更新不检查 | 确认应用已代码签名 |
| 内存占用过高 | 检查是否存在无上限缓存 |
| macOS 无法启动 | 完成 notarization |

---

## 参考文件

| 文件 | 内容 |
|------|------|
| [ipc-security.md](ipc-security.md) | 类型安全 IPC、安全配置 |
| [packaging.md](packaging.md) | Electron Forge、Builder、自动更新 |
| [backend.md](backend.md) | SQLite、Express、离线优先、WebSocket |

---

## 外部文档

- [Electron 官方文档](https://www.electronjs.org/docs/latest/)
- [Electron Security](https://www.electronjs.org/docs/latest/tutorial/security)
- [Electron Forge](https://www.electronforge.io/)
- [electron-builder](https://www.electron.build/)
