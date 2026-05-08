# NoteExpress MCP

## 项目简介

NoteExpress MCP，旨在通过模型上下文协议（Model Context Protocol，MCP）将NoteExpress本地数据库与不同 AI 助手衔接，支持自然语言驱动的专业学术查询。

## 功能特性
**目前仅支持只读，后续版本会加上写入数据功能**
- **文献检索**：按关键词搜索题录（标题、作者、正文等），支持分页
- **PDF 正文**：从题录关联的 PDF 附件中提取可读文本
- **文件夹 / 分类**：浏览 NE 分类树，并按文件夹列出条目
- **笔记与题录详情**：读取笔记内容、题录元数据及附件信息（只读，不在 NE 内新建或修改文献）

## 系统要求

- 需安装 **NoteExpress（论文管理软件）**，推荐在本机曾打开过至少一个文献库  
  官网：<https://www.inoteexpress.com/>
- **操作系统**：**Windows 64 位（x64）**（与本 MCP 发行包一致）
- **可选**：安装 **Node.js**（用于 `npm` / `npx` 方式拉起 MCP）

## 快速上手指南

### 给 CLI 工具自动安装

如果您正在使用 Claude Code、Codex 等支持读取安装说明的 CLI 工具，可以直接复制下面这段话给工具，让它自行读取安装文档并配置 MCP：

```text
帮我安装NoteExpress MCP，安装说明地址：
https://raw.githubusercontent.com/aegean-org/ne-mcp/main/INSTALL.md
```

### 手动安装

GitHub Releases 页面下载最新压缩包
```text
https://github.com/aegean-org/ne-mcp/releases/latest
```

之后将解压后的地址写入mcp配置文件
- /absolute/path/to/ne-mcp 为解压后的文件地址

```json
{
  "mcpServers": {
    "ne-mcp": {
      "command": "/absolute/path/to/ne-mcp",
    }
  }
}

#### 使用示例

- 「帮我查一下 NoteExpress 里包含『深度学习』关键词的文献有哪些」
- 「列出『参考文献』文件夹下面最近的题录」
- 「这篇文献关联的 PDF 正文里提到了哪些方法？」

##### 功能点
文献检索、分类浏览、PDF 正文提取等等

#### 可用工具（节选）

服务提供多个 **`ne.*`** 只读工具，以下为常用能力分类（完整列表见仓库 `README.md`）。

**库发现**

| 工具 | 说明 |
|------|------|
| `ne.get_default_library` | 当前默认 / 最近使用的文献库路径 |
| `ne.list_known_libraries` | 本机可能被 NE 使用的库路径汇总 |

**条目与检索**

| 工具 | 说明 |
|------|------|
| `ne.search_items` | 关键词搜索题录与正文等 |
| `ne.list_items` | 分页浏览与筛选 |
| `ne.get_item` | 按 ID 读取题录详情（含附件等） |

**笔记与 PDF**

| 工具 | 说明 |
|------|------|
| `ne.get_note` | 读取笔记 |
| `ne.get_item_pdf_content` | 提取关联 PDF 全文文本 |

**分类与配置**

| 工具 | 说明 |
|------|------|
| `ne.get_category_tree` | 分类树 |
| `ne.get_category_items` | 某文件夹下条目列表 |
| `ne.get_db_settings` | 库内配置项 |
| `ne.list_resources` | 附件 / 链接资源列表 |

### 支持的 AI 客户端

使用 Stdio 传输，可与支持 MCP 的客户端配合使用，例如：

- **Claude Desktop / Claude Code**
- **Cursor IDE**
- **Cherry Studio** 等支持 Stdio MCP 的应用

### 获取帮助

如有问题或建议，请到 GitHub 仓库提交 Issue：

<https://github.com/aegean-org/ne-mcp/issues>

更完整的命令行参数、开发编译说明见仓库根目录 **`README.md`**。
