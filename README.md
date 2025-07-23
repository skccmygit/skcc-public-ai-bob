# skcc-public-ai-bob
Public AI Best of Breeds



MCP

```

{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-postgres",
        "postgresql://ags_developer:Dev@123@skax-ags-mgmt-dev-pgsql.postgres.database.azure.com:5432/agsdb?sslmode=require"
      ]
    },
    "TalkToFigma": {
      "command": "bunx",
      "args": [
        "cursor-talk-to-figma-mcp@latest"
      ]
    },
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    },
    "taskmaster-ai": {
      "command": "npx",
      "args": ["-y", "--package=task-master-ai", "task-master-ai"],
      "env": {
          "ANTHROPIC_API_KEY": "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",
          "PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
          "OPENAI_API_KEY": "YOUR_OPENAI_KEY_HERE",
          "GOOGLE_API_KEY": "AIzaSyC6a65wNkDFJp2HnzG37aN7qczidH_njxU",
          "MISTRAL_API_KEY": "YOUR_MISTRAL_KEY_HERE",
          "OPENROUTER_API_KEY": "YOUR_OPENROUTER_KEY_HERE",
          "XAI_API_KEY": "YOUR_XAI_KEY_HERE",
          "AZURE_OPENAI_API_KEY": "YOUR_AZURE_KEY_HERE"
      }
    }
  }
}
