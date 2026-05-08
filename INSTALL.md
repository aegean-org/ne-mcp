# NoteExpress MCP（ne-mcp-server）安装说明

本文件说明如何在 **Windows** 上安装并对接支持 MCP 的客户端（如 Claude Code、Cursor 等），使 AI 能通过 MCP 协议只读访问本机 **NoteExpress** 文献库（`.ndb`）。

---

## 环境与前置条件

| 项目 | 说明 |
|------|------|
| 操作系统 | **Windows 64 位（x64）**；NoteExpress 与本服务均面向 Windows |
| NoteExpress | 建议已安装并至少打开过一次文献库，便于自动发现库路径 |
| 可选：Node.js | 若使用 **npm / npx** 方式安装运行，需已安装 Node.js（自带 `npx`） |

---

## 安装方式概览

推荐顺序：

1. 若已安装 **Node.js**，优先使用官方 npm 包 **`@aegean-org/ne-mcp`**，由 `npx` 自动拉取 Windows 平台二进制。
2. 若 **未安装 Node.js**（或无法使用 npm）：打开 **[GitHub Releases 最新版](https://github.com/aegean-org/ne-mcp/releases/latest)**，下载当前版本提供的 **Windows 安装包（通常为 zip）**，解压后得到 **`ne-mcp-server-amd64.exe`**，在 MCP 配置里填写该文件的**绝对路径**（见下文「方式二」）。

---

## 方式一：通过 npm（推荐）

包名：**`@aegean-org/ne-mcp`**（发布于 **https://registry.npmjs.org**）。

无需全局安装；首次由 MCP 客户端或终端拉起时，会从 npm 拉取 **可选依赖** `@aegean-org/ne-mcp-win32-x64`，其中包含与本机架构匹配的 `ne-mcp-server-amd64.exe`。

日常使用 **无需填写任何启动参数**；默认会自动尝试发现 NoteExpress 最近使用的文献库。

### MCP 配置示例（npx）

```json
{
  "mcpServers": {
    "ne-mcp-server": {
      "command": "npx",
      "args": ["-y", "@aegean-org/ne-mcp"]
    }
  }
}
```

---

## 方式二：GitHub Releases 安装包（无 Node.js 时）

当本机 **没有 Node.js** 或不便使用 **npm / npx** 时，请从官方发布页下载 Windows 包：

**[https://github.com/aegean-org/ne-mcp/releases/latest](https://github.com/aegean-org/ne-mcp/releases/latest)**

在 **Assets** 中选择适用于 Windows 的压缩包（如 `*.zip`），下载后解压，其中应包含：

**`ne-mcp-server-amd64.exe`**

将该文件放到固定目录（例如 `%USERPROFILE%\AppData\Local\ne-mcp-server\ne-mcp-server-amd64.exe`），随后在 MCP 配置中指向该路径即可。

### MCP 配置示例（本地 exe）

```json
{
  "mcpServers": {
    "ne-mcp-server": {
      "command": "C:\\Users\\你的用户名\\AppData\\Local\\ne-mcp-server\\ne-mcp-server-amd64.exe"
    }
  }
}
```

路径请改为本机实际绝对路径，Windows 下建议使用**双反斜杠** `\\` 或按客户端要求的 JSON 转义规则书写。

---
