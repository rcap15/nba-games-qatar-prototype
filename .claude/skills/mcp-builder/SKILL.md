---
name: mcp-builder
description: Build Model Context Protocol (MCP) servers that allow LLMs to interact with external services. Four-phase process: research → implement → review → evaluate. Use when creating or extending MCP servers for Claude or other LLM integrations.
license: Complete terms in LICENSE.txt
---

# MCP Builder

Builds high-quality Model Context Protocol servers. Server quality is measured by how effectively it enables LLMs to accomplish practical tasks.

## Four-Phase Development

### Phase 1: Research and Planning

- Study MCP protocol documentation and design principles
- Understand the target service's API thoroughly
- Plan tool interface design: what actions matter to LLMs?
- Choose implementation language: **TypeScript preferred** (better SDK quality and ecosystem compatibility)

### Phase 2: Implementation

**Project structure:**
```
src/
  index.ts          # server entry point
  tools/            # individual tool definitions
  resources/        # resource endpoints
  auth.ts           # authentication handling
package.json
tsconfig.json
```

**Tool design principles:**
- Balance comprehensive API coverage with specialized workflow tools
- Name tools with consistent, action-oriented patterns: `get_`, `list_`, `create_`, `update_`, `delete_`
- Provide clear, specific error messages — LLMs need actionable guidance
- Schema all inputs with proper types and descriptions

**Authentication:**
- Handle auth in a dedicated module
- Support environment variable configuration
- Fail clearly when credentials are missing or invalid

### Phase 3: Review and Testing

- Run `npx @modelcontextprotocol/inspector` to inspect the server
- Verify TypeScript compilation with no errors
- Test each tool against the real API
- Check error handling for invalid inputs and API failures

### Phase 4: Evaluation

Write 10 test questions that cover realistic LLM use cases:
- Simple lookups
- Multi-step workflows
- Edge cases and error conditions
- Questions that require combining multiple tools

Verify an LLM can answer each question using only your server.

## TypeScript Template

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

const server = new McpServer({ name: "my-server", version: "1.0.0" });

server.tool(
  "get_item",
  "Retrieves an item by ID",
  { id: z.string().describe("The item ID") },
  async ({ id }) => {
    // implementation
    return { content: [{ type: "text", text: JSON.stringify(result) }] };
  }
);

const transport = new StdioServerTransport();
await server.connect(transport);
```

## Key Design Guidelines

- Prefer fewer, more powerful tools over many narrow ones
- Include all context an LLM needs to understand what a tool does
- Return structured data in a format LLMs can parse and reason about
- Never expose credentials in tool output
