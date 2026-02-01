# MCP File CRUD Server

A lightweight [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server that provides file system CRUD operations for LLM applications like Claude Desktop.

## Features

- 📂 **List Files** - Browse directory contents with file sizes and types
- 📖 **Read Files** - Read text file contents
- ✏️ **Write Files** - Create or update files (auto-creates directories)
- 🗑️ **Delete Files** - Remove files or empty directories
- 🔒 **Security** - Path traversal protection to prevent unauthorized access

## Installation

```bash
# Clone the repository
git clone https://github.com/As1fNaz1r/mcp-file-crud.git
cd mcp-file-crud

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Usage

### With Claude Desktop

Add to your Claude Desktop config (`~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "file-crud": {
      "command": "python",
      "args": ["/path/to/mcp-file-crud/server.py"],
      "env": {
        "DATA_DIR": "/path/to/your/data/folder"
      }
    }
  }
}
```

### Standalone

```bash
# Set the data directory (defaults to /data)
export DATA_DIR=/path/to/your/files

# Run the server
python server.py
```

## Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| `list_files` | List files in a directory | `path` (optional) - subdirectory path |
| `read_file` | Read file contents | `file_path` - relative path to file |
| `write_file` | Write content to file | `file_path`, `content` |
| `delete_file` | Delete a file or directory | `file_path` - relative path |

## Security

- All file operations are restricted to the configured `DATA_DIR`
- Path traversal attacks (e.g., `../`) are blocked
- Symlink resolution prevents escape attempts

## Requirements

- Python 3.10+
- `mcp>=1.0.0`

## License

MIT
