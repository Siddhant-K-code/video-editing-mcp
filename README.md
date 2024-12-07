# Video Jungle MCP server
 
Upload, edit, and generate videos from everyone's favorite LLM

[![PyPI version](https://badge.fury.io/py/video-editor-mcp.svg)](https://pypi.org/project/video-editor-mcp/)

## Components

### Resources

The server implements an interface to upload, generate, and edit videos with:
- Custom vj:// URI scheme for accessing individual videos and project
- Each project resource has a name, description

### Prompts

Coming soon.

### Tools

The server implements a few tools:
- add-video: Add a video from a URL
  - Returns an vj:// URI to reference the Video file
- search-videos: Search videos using embeddings
  - Returns video matches based upon embeddings and keywords
- generate-edit-from-videos
  - Generates a rendered video edit from a set of video files
- generate-edit-from-single-video
  - Generate an edit from a single input video file

## Configuration

You must login to [Video Jungle settings](https://app.video-jungle.com/profile/settings), and get your API key. Use this to start Video Jungle MCP:

```bash
$ uv run video-jungle-mcp YOURAPIKEY
```

## Quickstart

### Install

#### Claude Desktop

You'll need to adjust your `claude_desktop_config.json` manually:

On MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

<details>
  <summary>Development/Unpublished Servers Configuration</summary>
  ```
  "mcpServers": {
    "video-jungle-mcp": {
      "command": "uv",
      "args": [
        "--directory",
        "/Users/stankley/Development/video-jungle-mcp",
        "run",
        "video-jungle-mcp",
        "YOURAPIKEY"
      ]
    }
  }
  ```
</details>

<details>
  <summary>Published Servers Configuration</summary>
  ```
  "mcpServers": {
    "video-jungle-mcp": {
      "command": "uvx",
      "args": [
        "video-jungle-mcp",
        "YOURAPIKEY"
      ]
    }
  }
  ```
</details>

## Development

### Building and Publishing

To prepare the package for distribution:

1. Sync dependencies and update lockfile:
```bash
uv sync
```

2. Build package distributions:
```bash
uv build
```

This will create source and wheel distributions in the `dist/` directory.

3. Publish to PyPI:
```bash
uv publish
```

Note: You'll need to set PyPI credentials via environment variables or command flags:
- Token: `--token` or `UV_PUBLISH_TOKEN`
- Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).


You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory /Users/stankley/Development/video-jungle-mcp run video-jungle-mcp
```


Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.

Additionally, I've added logging to `app.log` in the project directory. You can add logging to diagnose API calls via a:

```
logging.info("this is a test log")
```

A reasonable way to follow along as you're workin on the project is to open a terminal session and do a:

```bash
$ tail -f app.log
```