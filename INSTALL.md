# NoteExpress MCP CLI 安装说明

## 目标

启动命令必须最终为以下两种之一：

```bash
npx -y @aegean-org/ne-mcp
```

或本地二进制：

```bash
C:\\absolute\\path\\to\\ne-mcp.exe
```

---

## 决策逻辑

1. 先判断当前操作系统和 CPU 架构，是否为Windows 64 位（x64）。
2. 再检查 `node` 与 `npx` 是否已安装且可执行。
3. 如果 `node` 和 `npx` 可用，优先使用 npm 包启动，不下载 GitHub release。
4. 如果 `node` 或 `npx` 不可用，则从 GitHub Releases 下载对应平台压缩包，解压后直接运行本地二进制。

## 平台判断
- Windows x64: `win32-x64`
---

## Node.js 可用时

直接使用：

```bash
npx -y @aegean-org/ne-mcp
```

不要额外安装全局包，也不要改写参数顺序。

## Node.js 不可用时

GitHub Releases 页面：

```text
https://github.com/aegean-org/ne-mcp/releases/latest
```

直接下载地址模板：

```text
https://github.com/aegean-org/ne-mcp/releases/latest/download/<asset>
```

资产映射：

- `win32-x64` -> `ne-mcp-windows-amd64.7z`

将压缩包解压到用户可写目录，例如：

- Windows: `%USERPROFILE%\\AppData\\Local\\ne-mcp\\`

解压后的目标文件名必须为：

- Windows: `ne-mcp.exe`

## MCP 配置输出

如果目标 CLI 支持直接添加 stdio MCP server：

- 有 Node.js 时，command 使用 `npx`，args 使用 `["-y", "@aegean-org/ne-mcp"]`
- 无 Node.js 时，command 使用本地二进制绝对路径

如果目标 CLI 需要 JSON 配置，输出：

```json
{
  "mcpServers": {
    "ne-mcp": {
      "command": "npx",
      "args": ["-y", "@aegean-org/ne-mcp"]
    }
  }
}
```

如果使用本地二进制，改为：

```json
{
  "mcpServers": {
    "ne-mcp": {
      "command": "/absolute/path/to/ne-mcp",
    }
  }
}
```

Windows 本地二进制时，`command` 改为 `C:\\absolute\\path\\to\\ne-mcp.exe`。
