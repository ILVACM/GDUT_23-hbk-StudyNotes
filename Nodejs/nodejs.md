# Node.js 基础与配置

> Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行时环境，使 JavaScript 能够脱离浏览器在服务器端运行。

-----------------------------------------------------------------

## 基本概念

### 1.1 定义

Node.js 并非一门新语言，而是 JavaScript 的运行环境（Runtime）。它允许开发者使用 JavaScript 编写后端服务、命令行工具及高性能网络应用。

### 1.2 核心特点

- **非阻塞 I/O (Non-blocking I/O)**：采用异步事件驱动模型，在处理高并发 I/O 操作（如网络请求、文件读写）时效率极高。
- **单线程 (Single-threaded)**：主线程为单线程，通过事件循环（Event Loop）处理并发，避免了多线程上下文切换的开销。
- **跨平台**：支持 Windows、Linux、macOS 等主流操作系统。

### 1.3 应用场景

- Web 后端服务器（API 接口、微服务）
- 前端工程化工具链（Webpack, Vite, ESLint）
- 实时通讯应用（聊天室、在线协作）
- 跨平台桌面应用（Electron）

-----------------------------------------------------------------

## Windows 环境安装配置

### 2.1 版本管理工具：nvm-windows

推荐使用 `nvm-windows` (Node Version Manager) 进行多版本管理，便于在不同项目间切换 Node.js 版本。

### 2.2 安装步骤

1. 从 [GitHub Releases](https://github.com/coreybutler/nvm-windows/releases) 下载 `nvm-setup.exe`。
2. 运行安装包，建议保持默认路径或自定义无中文路径。
3. 打开 PowerShell，执行以下命令安装 LTS 版本：

```powershell
nvm install 24.15.0
nvm use 24.15.0
node -v
npm -v
```

-----------------------------------------------------------------

## 镜像源配置

### 3.1 为什么选择淘宝镜像 (npmmirror)

- **同步速度快**：与官方 registry 同步延迟通常小于 10 分钟。
- **稳定性高**：由阿里云专业团队维护，提供全球 CDN 加速。
- **生态完善**：国内 npm 生态的事实标准，社区支持度高。

### 3.2 配置命令

将 npm 默认仓库地址切换为淘宝镜像：

```powershell
npm config set registry https://registry.npmmirror.com
npm config get registry
```

-----------------------------------------------------------------

## 常见问题与解决方案

### 4.1 nvm 提示 "Version not installed"

- **现象**：执行 `nvm use <version>` 时报错，但 `nvm install` 显示成功。
- **原因**：PowerShell 权限不足导致 symlink 创建失败，或 `settings.txt` 路径配置错误。
- **解决**：
  1. 以**管理员身份**运行 PowerShell。
  2. 检查 `C:\Users\<User>\AppData\Roaming\nvm\settings.txt`，确保 `path` 指向有效目录且无空格。
  3. 重新执行 `nvm use <version>`。

### 4.2 PowerShell 禁止运行脚本 (PSSecurityException)

- **现象**：执行 npm 命令时报错 `无法加载文件 ... 因为在此系统上禁止运行脚本`。
- **原因**：Windows PowerShell 默认执行策略为 `Restricted`。
- **解决**：修改当前用户执行策略为 `RemoteSigned`。

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

-----------------------------------------------------------------

## 版本对比与选择

### 5.1 LTS 版本状态对比 (2026.04)

| 版本 | 代号 | 状态 | 支持截止 | 推荐指数 |
| :--- | :--- | :--- | :--- | :--- |
| **v24.x** | Krypton | Active LTS | 2027-11 | ⭐⭐⭐⭐⭐ |
| v22.x | Jod | Maintenance LTS | 2026-04 | ⭐⭐⭐ |
| v20.x | Iron | Maintenance LTS | 2026-04 | ⭐⭐ |

### 5.2 选型建议

- **首选推荐**：**Node.js v24.15.0 (LTS)**。处于 Active LTS 阶段，拥有最长的安全维护周期和最完善的第三方库兼容性。
- **避坑指南**：避免使用奇数版本（Current 版）用于生产环境；v20/v22 即将停止维护，新项目不建议选用。
