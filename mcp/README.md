Archon: https://github.com/coleam00/archon.git

PowerPoint: https://github.com/GongRzhe/Office-PowerPoint-MCP-Server.git

Check node version compatibility issues in the mcp logs through claude desktop

TODO: upgrade n8n account to get api key?

https://github.com/czlonkowski/n8n-mcp
"n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true",
        "N8N_API_URL": "https://your-n8n-instance.com",
        "N8N_API_KEY": "your-api-key"
      }
    }