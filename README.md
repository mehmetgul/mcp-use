<div align="center">
&nbsp;

<div align="center">
  <a href="https://mcp-use.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="./static/logo_white.svg">
      <source media="(prefers-color-scheme: light)" srcset="./static/logo_black.svg">
      <img alt="mcp use logo" src="./static/logo_black.svg" width="50%" >
    </picture>
  </a>
</div>
&nbsp;

<p align="center" style="max-width:600px; margin-bottom:40px">
  <b>mcp-use</b> is the fullstack MCP framework. Build MCP Servers for AI Agents or MCP Apps for ChatGPT / Claude and MCP Clients.</p>
<p align="center">
    <a href="https://mcp-use.com/docs" alt="Documentation">
        <img src="https://img.shields.io/badge/mcp--use-docs-blue?labelColor=white" /></a>
    <a href="https://manufact.com" alt="Website">
        <img src="https://img.shields.io/badge/made by-manufact.com-blue" /></a>
    <a href="https://github.com/mcp-use/mcp-use/blob/main/LICENSE" alt="License">
        <img src="https://img.shields.io/github/license/mcp-use/mcp-use" /></a>
    <a href="https://discord.gg/XkNkSkMz3V" alt="Discord">
        <img src="https://dcbadge.limes.pink/api/server/XkNkSkMz3V?style=flat" /></a>
    <br/>
    <a href="https://mcp-use.com/docs/python" alt="Python docs">
        <img src="https://img.shields.io/badge/pyhton-docs-blue?labelColor=white&logo=python" alt="Badge"></a>
    <a href="https://pypi.org/project/mcp_use/" alt="PyPI Version">
        <img src="https://img.shields.io/pypi/v/mcp_use.svg"/></a>
    <a href="https://pypi.org/project/mcp_use/" alt="PyPI Downloads">
        <img src="https://static.pepy.tech/badge/mcp-use" /></a>
    <a href="https://github.com/mcp-use/mcp-use/actions/workflows/conformance.yml" alt="Python MCP Conformance">
        <img src="https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/tonxxd/6edf670f0446dc9f7a1f32d6bfda2b70/raw/python-conformance.json" /></a>
    <br/>
    <a href="https://mcp-use.com/docs/typescript" alt="Typescript Documentation">
        <img src="https://img.shields.io/badge/typescript-docs-blue?labelColor=white&logo=typescript" alt="Badge"></a>
    <a href="https://www.npmjs.com/package/mcp-use" alt="NPM Version">
        <img src="https://img.shields.io/npm/v/mcp-use.svg"/></a>
    <a href="https://www.npmjs.com/package/mcp-use" alt="NPM Downloads">
        <img src="https://img.shields.io/npm/dw/mcp-use.svg"/></a>
    <a href="https://github.com/mcp-use/mcp-use/actions/workflows/conformance.yml" alt="TypeScript MCP Conformance">
        <img src="https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/tonxxd/6edf670f0446dc9f7a1f32d6bfda2b70/raw/typescript-conformance.json" /></a>
    <br/>
</p>
</div>

---

## What you can do

- **Build** — mcp-use SDK: MCP Servers and MCP Apps
- **Preview** — mcp-use Inspector: Test and debug your servers
- **Deploy** — [Manufact](https://manufact.com): MCP Cloud — connect your GitHub repo and have it up and running in production with observability, metrics, logs, branch-deployments, and more

---

## Links

- [Docs](https://mcp-use.com/docs)
- Quickstarts: [TypeScript](https://mcp-use.com/docs/typescript/getting-started/quickstart) | [Python](https://mcp-use.com/docs/python/getting-started/quickstart)
- [Skills (for coding agents)](https://skills.sh/?q=mcp-use)

Since this is a monorepo, see the sub-package READMEs for detailed docs:

- [Python library →](./libraries/python/)
- [TypeScript library →](./libraries/typescript/)

---

## Quick Start — MCP Servers

### <img src="./static/typescript.svg" height="14" style="margin-right:4px; top:-1px; position:relative;" align="center" /> TypeScript

Scaffold a new project:

```bash
npx create-mcp-use-app my-server
```

Or create a server manually:

```typescript
import { MCPServer, text } from "mcp-use/server";
import { z } from "zod";

const server = new MCPServer({
  name: "my-server",
  version: "1.0.0",
});

server.tool({
  name: "get_weather",
  description: "Get weather for a city",
  schema: z.object({ city: z.string() }),
}, async ({ city }) => {
  return text(`Temperature: 72°F, Condition: sunny, City: ${city}`);
});

await server.listen(3000);
// Inspector at http://localhost:3000/inspector
```

[**→ Full TypeScript Server Documentation**](https://mcp-use.com/docs/typescript/server/getting-started)

### <img src="./static/python.svg" height="14" style="margin-right:4px; top:-1px; position:relative;" align="center" /> Python

```bash
pip install mcp-use
```

```python
from mcp_use import MCPServer

server = MCPServer(
    name="my-server",
    version="1.0.0",
)

@server.tool()
def get_weather(city: str) -> dict:
    """Get weather for a city"""
    return {"temperature": 72, "condition": "sunny", "city": city}

if __name__ == "__main__":
    server.run()
```

[**→ Full Python Server Documentation**](https://mcp-use.com/docs/python/server/index)

---

## MCP Apps

MCP Apps let you build interactive widgets that work across Claude, ChatGPT, and other MCP clients — write once, run everywhere.

```typescript
import { MCPServer, text } from "mcp-use/server";
import { z } from "zod";

const server = new MCPServer({
  name: "weather-app",
  version: "1.0.0",
  mcpApps: true,
});

server.tool({
  name: "get_weather",
  description: "Get weather for a city",
  schema: z.object({ city: z.string() }),
  widget: "weather-widget",
}, async ({ city }) => {
  return text(`Temperature: 72°F, Condition: sunny, City: ${city}`);
});

await server.listen(3000);
```

[**→ MCP Apps Documentation**](https://mcp-use.com/docs/typescript/server/ui-widgets)

---

## Inspector

The mcp-use Inspector lets you test and debug your MCP servers interactively.

**Auto-included** when using `server.listen()`:

```typescript
server.listen(3000);
// Inspector at http://localhost:3000/inspector
```

**Standalone** — inspect any MCP server:

```bash
npx @mcp-use/inspector --url http://localhost:3000/sse
```

[**→ Inspector Documentation**](https://mcp-use.com/docs/inspector/index)

---

## Deploy

Deploy your MCP server to production:

```bash
npx @mcp-use/cli login
npx @mcp-use/cli deploy
```

Or connect your GitHub repo on [manufact.com](https://manufact.com) — production-ready with observability, metrics, logs, and branch-deployments.

---

## Package Overview

This monorepo contains multiple packages for both Python and TypeScript:

### Python Packages

| Package     | Description                           | Version                                                                                 |
| ----------- | ------------------------------------- | --------------------------------------------------------------------------------------- |
| **mcp-use** | Complete MCP client and agent library | [![PyPI](https://img.shields.io/pypi/v/mcp_use.svg)](https://pypi.org/project/mcp_use/) |

### TypeScript Packages

| Package                | Description                                     | Version                                                                                                         |
| ---------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **mcp-use**            | Core framework for clients, agents, and servers | [![npm](https://img.shields.io/npm/v/mcp-use.svg)](https://www.npmjs.com/package/mcp-use)                       |
| **@mcp-use/cli**       | Build tool with hot reload and auto-inspector   | [![npm](https://img.shields.io/npm/v/@mcp-use/cli.svg)](https://www.npmjs.com/package/@mcp-use/cli)             |
| **@mcp-use/inspector** | Web-based debugger for MCP servers              | [![npm](https://img.shields.io/npm/v/@mcp-use/inspector.svg)](https://www.npmjs.com/package/@mcp-use/inspector) |
| **create-mcp-use-app** | Project scaffolding tool                        | [![npm](https://img.shields.io/npm/v/create-mcp-use-app.svg)](https://www.npmjs.com/package/create-mcp-use-app) |

---

## Legacy: MCP Agent & Client

mcp-use also provides a full MCP Agent and Client implementation.

<details>
<summary>Build an AI Agent</summary>

### <img src="./static/python.svg" height="14" style="margin-right:4px; top:-1px; position:relative;" align="center" /> Python

```bash
pip install mcp-use langchain-openai
```

```python
import asyncio
from langchain_openai import ChatOpenAI
from mcp_use import MCPAgent, MCPClient

async def main():
    config = {
        "mcpServers": {
            "filesystem": {
                "command": "npx",
                "args": ["-y", "@modelcontextprotocol/server-filesystem", "/tmp"]
            }
        }
    }

    client = MCPClient.from_dict(config)
    llm = ChatOpenAI(model="gpt-4o")
    agent = MCPAgent(llm=llm, client=client)

    result = await agent.run("List all files in the directory")
    print(result)

asyncio.run(main())
```

[**→ Full Python Agent Documentation**](./libraries/python/README.md#quick-start)

### <img src="./static/typescript.svg" height="14" style="margin-right:4px; top:-1px; position:relative;" align="center" /> TypeScript

```bash
npm install mcp-use @langchain/openai
```

```typescript
import { ChatOpenAI } from "@langchain/openai";
import { MCPAgent, MCPClient } from "mcp-use";

async function main() {
  const config = {
    mcpServers: {
      filesystem: {
        command: "npx",
        args: ["-y", "@modelcontextprotocol/server-filesystem", "/tmp"],
      },
    },
  };

  const client = MCPClient.fromDict(config);
  const llm = new ChatOpenAI({ modelName: "gpt-4o" });
  const agent = new MCPAgent({ llm, client });

  const result = await agent.run("List all files in the directory");
  console.log(result);
}

main();
```

[**→ Full TypeScript Agent Documentation**](./libraries/typescript/README.md#-quick-start)

</details>

<details>
<summary>Use MCP Client</summary>

### <img src="./static/python.svg" height="14" style="margin-right:4px; top:-1px; position:relative;" align="center" /> Python

```python
import asyncio
from mcp_use import MCPClient

async def main():
    config = {
        "mcpServers": {
            "calculator": {
                "command": "npx",
                "args": ["-y", "@modelcontextprotocol/server-everything"]
            }
        }
    }

    client = MCPClient.from_dict(config)
    await client.create_all_sessions()

    session = client.get_session("calculator")
    result = await session.call_tool(name="add", arguments={"a": 5, "b": 3})

    print(f"Result: {result.content[0].text}")
    await client.close_all_sessions()

asyncio.run(main())
```

[**→ Python Client Documentation**](./libraries/python/README.md#direct-tool-calls-without-llm)

### <img src="./static/typescript.svg" height="14" style="margin-right:4px; top:-1px; position:relative;" align="center" /> TypeScript

```typescript
import { MCPClient } from "mcp-use";

async function main() {
  const config = {
    mcpServers: {
      calculator: {
        command: "npx",
        args: ["-y", "@modelcontextprotocol/server-everything"],
      },
    },
  };

  const client = new MCPClient(config);
  await client.createAllSessions();

  const session = client.getSession("calculator");
  const result = await session.callTool("add", { a: 5, b: 3 });

  console.log(`Result: ${result.content[0].text}`);
  await client.closeAllSessions();
}

main();
```

[**→ TypeScript Client Documentation**](./libraries/typescript/README.md#basic-usage)

</details>

---

## Community & Support

- **Discord**: [Join our community](https://discord.gg/XkNkSkMz3V)
- **GitHub Issues**: [Report bugs or request features](https://github.com/mcp-use/mcp-use/issues)
- **Documentation**: [mcp-use.com/docs](https://mcp-use.com/docs)
- **Website**: [manufact.com](https://manufact.com)
- **Twitter**: Follow [@pietrozullo](https://x.com/pietrozullo) and [@pederzh](https://x.com/pederzh)
- **Contributing**: See [CONTRIBUTING.md](https://github.com/mcp-use/mcp-use/blob/main/CONTRIBUTING.md)
- **License**: MIT © [MCP-Use Contributors](https://github.com/mcp-use/mcp-use/graphs/contributors)

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mcp-use/mcp-use&type=Date)](https://www.star-history.com/#mcp-use/mcp-use&Date)

---

## Contributors

Thanks to all our amazing contributors!

### Core Contributors

1. **Pietro** ([@pietrozullo](https://github.com/pietrozullo))
2. **Luigi** ([@pederzh](https://github.com/pederzh))
3. **Enrico** ([@tonxxd](https://github.com/tonxxd))

<br>

<a href="https://github.com/mcp-use/mcp-use/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mcp-use/mcp-use" />
</a>

---

<div align="center">
  <strong>Built with ❤️ by the MCP-Use community</strong>
  <br/>
  <sub>San Francisco | Zürich</sub>
</div>
