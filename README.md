# 考古文献解析 MCP Server

Parse archaeological documents (PDF, images, Office files) to Markdown via [MinerU](https://mineru.net) cloud API.

**Works out of the box — no API key required.** Optional Pro token for larger files and batch parsing.

## Install

```bash
# With uv (recommended)
uv pip install archaeo-doc-parser

# Or from source
git clone https://github.com/alexxhchen-nu/archaeo-doc-parser
cd archaeo-doc-parser
uv pip install -e .
```

## Usage

### As CLI

```bash
# stdio mode (for MCP clients)
archaeo-doc-parser

# HTTP mode (for remote access)
archaeo-doc-parser --transport http --port 8000

# Or run directly
uv run archaeo-doc-parser
```

### MCP Client Configuration

#### Claude Desktop (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "archaeo-doc-parser": {
      "command": "uv",
      "args": ["run", "archaeo-doc-parser"]
    }
  }
}
```

With Pro token:
```json
{
  "mcpServers": {
    "archaeo-doc-parser": {
      "command": "uv",
      "args": ["run", "archaeo-doc-parser"],
      "env": {
        "MINERU_TOKEN": "your-token-here"
      }
    }
  }
}
```

#### Cursor / Kimi Code

Same pattern — point the MCP server command to `uv run archaeo-doc-parser`.

## Tools

| Tool | Description | Free | Pro |
|------|-------------|------|-----|
| `parse_document` | Parse URL or local file → Markdown | 10MB / 20 pages | 200MB / 200 pages |
| `parse_batch` | Batch parse multiple URLs → JSON | ❌ | ✅ |
| `get_task_status` | Check async task progress | ❌ | ✅ |
| `get_supported_formats` | List supported formats and limits | ✅ | ✅ |
| `parse_tombs` | Extract tomb data from archaeological reports | ✅ | ✅ |

## Supported Formats

- **Documents**: PDF, DOCX, PPTX, XLSX
- **Images**: PNG, JPG, JPEG, JP2, WebP, GIF, BMP
- **OCR Languages**: Chinese (`ch`), English (`en`), Japanese (`japan`), Korean (`korean`), and more

## Pro Token

Get one at https://mineru.net → API管理 (API Management).

Unlocks:
- 200MB file size / 200 pages (vs 10MB / 20)
- Batch parsing
- Task status polling
- JSON, DOCX, HTML, LaTeX output formats

Each user can set their own `MINERU_TOKEN` in their MCP client's `env` block.

## License

MIT
