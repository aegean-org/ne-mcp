# NoteExpress MCP CLI 安装说明

## 目标

启动命令必须最终为：

```bash
C:\\absolute\\path\\to\\ne-mcp-xxx.exe
```

---

## 决策逻辑

1. 先判断当前操作系统和 CPU 架构，是否为Windows 64 位（x64）。
2. 从 GitHub Releases 下载对应平台压缩包，解压后直接运行本地二进制。

## 平台判断
- Windows x64: `win32-x64`
---

## 下载

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

## MCP 配置输出

如果使用本地二进制，改为：

- /absolute/path/to/ne-mcp 为解压后的文件地址

```json
{
  "mcpServers": {
    "ne-mcp": {
      "command": "/absolute/path/to/ne-mcp",
    }
  }
}
```

Windows 本地二进制时，`command` 改为 Windows路径
