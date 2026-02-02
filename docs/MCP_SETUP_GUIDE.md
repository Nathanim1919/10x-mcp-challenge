# MCP (Model Context Protocol) Setup Guide for Cursor

This guide documents the process of setting up MCP servers in Cursor IDE, specifically for the 10 Academy Tenx MCP server.

## What is MCP?

Model Context Protocol (MCP) is an open standard that enables AI models to interact with external tools and services through a unified interface. It follows a client-server architecture where:

- **MCP Client**: Your IDE (Cursor, VS Code, Claude Code)
- **MCP Server**: External service providing tools, prompts, and resources

## MCP Capabilities

MCP servers can provide:
- **Tools**: Functions the AI can call (e.g., database queries, API calls)
- **Prompts**: Pre-defined prompt templates
- **Resources**: External data sources
- **Sampling**: Request completions from the AI
- **Authentication**: Secure access to services

## Configuration Locations

### Cursor IDE

| Location | Scope | Description |
|----------|-------|-------------|
| `~/.cursor/mcp.json` | User-wide | Applies to all projects |
| `.cursor/mcp.json` | Project | Applies to current project only |

### VS Code

| Location | Scope |
|----------|-------|
| User settings | User-wide |
| `.vscode/mcp.json` | Project |

### Claude Code

| Location | Scope |
|----------|-------|
| `~/.mcp.json` | User-wide |
| `.mcp.json` | Project |

## Configuration Format

MCP servers are configured using JSON:

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "@package/name"],
      "env": {
        "API_KEY": "${ENV_VAR_NAME}"
      }
    }
  }
}
```

### Configuration Properties

| Property | Description | Example |
|----------|-------------|---------|
| `command` | Executable to run | `"npx"`, `"node"`, `"python"` |
| `args` | Command arguments | `["-y", "@package/name"]` |
| `env` | Environment variables | `{"API_KEY": "value"}` |

## Tenx MCP Server Setup

### Step 1: Obtain Credentials

Contact 10 Academy to receive:
- Tenx MCP server package name
- API key or authentication credentials
- Any additional configuration requirements

### Step 2: Create Configuration

Create or edit `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "tenx": {
      "command": "npx",
      "args": ["-y", "@10academy/tenx-mcp"],
      "env": {
        "TENX_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Step 3: Verify Connection

1. Restart Cursor IDE
2. Open a new chat session
3. The MCP server should connect automatically
4. Check for any connection errors in the output

### Step 4: Test Functionality

Try using MCP tools in your chat:
- Ask the agent to use Tenx-specific features
- Verify that interactions are being logged

## Troubleshooting

### Common Issues

#### Server Not Starting

**Symptoms:** MCP server doesn't appear in available tools

**Solutions:**
1. Check the package name is correct
2. Verify npm/npx is installed and accessible
3. Check environment variables are set correctly
4. Look for error messages in Cursor's output panel

#### Authentication Errors

**Symptoms:** Server starts but operations fail

**Solutions:**
1. Verify API key is correct
2. Check if key has expired
3. Ensure proper permissions are granted

#### Connection Timeout

**Symptoms:** Server takes too long to respond

**Solutions:**
1. Check network connectivity
2. Verify server endpoint is accessible
3. Increase timeout settings if available

### Debug Mode

To enable verbose logging:

```json
{
  "mcpServers": {
    "tenx": {
      "command": "npx",
      "args": ["-y", "@10academy/tenx-mcp", "--verbose"],
      "env": {
        "TENX_API_KEY": "your-api-key",
        "DEBUG": "true"
      }
    }
  }
}
```

## Alternative Installation Methods

### Docker

```json
{
  "mcpServers": {
    "tenx": {
      "command": "docker",
      "args": ["run", "-i", "10academy/tenx-mcp"],
      "env": {
        "TENX_API_KEY": "your-api-key"
      }
    }
  }
}
```

### Local Installation

```bash
# Install globally
npm install -g @10academy/tenx-mcp

# Configure to use local installation
{
  "mcpServers": {
    "tenx": {
      "command": "tenx-mcp",
      "args": [],
      "env": {
        "TENX_API_KEY": "your-api-key"
      }
    }
  }
}
```

## Security Considerations

### Best Practices

1. **Never commit API keys** to version control
2. **Use environment variables** for sensitive data
3. **Review server permissions** before installation
4. **Keep servers updated** for security patches

### Environment Variables

Instead of hardcoding keys:

```json
{
  "mcpServers": {
    "tenx": {
      "command": "npx",
      "args": ["-y", "@10academy/tenx-mcp"],
      "env": {
        "TENX_API_KEY": "${TENX_API_KEY}"
      }
    }
  }
}
```

Then set in your shell:
```bash
export TENX_API_KEY="your-actual-key"
```

## Verifying MCP Connection

### Check Server Status

In Cursor, you can verify MCP servers are connected by:
1. Opening the Command Palette (Ctrl+Shift+P / Cmd+Shift+P)
2. Searching for "MCP" related commands
3. Checking the MCP server status

### Test with Simple Query

Ask the agent:
```
Can you list the available MCP tools?
```

The agent should be able to see and use Tenx MCP tools if properly configured.

## Resources

- [Cursor MCP Documentation](https://cursor.com/docs/context/model-context-protocol)
- [MCP Specification](https://modelcontextprotocol.io/)
- [VS Code MCP Guide](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)

---

*This guide is part of the TRP 1 MCP Setup Challenge documentation.*

