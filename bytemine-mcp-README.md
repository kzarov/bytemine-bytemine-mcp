# Bytemine MCP Server

Connect [Bytemine's](https://bytemine.ai) B2B contact database of **130M+ verified professionals** directly to Claude, Cursor, Windsurf, and other AI assistants via the [Model Context Protocol](https://modelcontextprotocol.io).

## Tools

### `people_search`

Search contacts by job title, company, location, industry, seniority, department, company size, and more.

**Filters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `api_key` | string | **Required.** Your Bytemine workspace API key |
| `titleFunction` | string[] | Job title keywords, e.g. `["CEO", "CTO"]` |
| `companyName` | string[] | Company names, e.g. `["Google", "Meta"]` |
| `city` | string[] | Cities, e.g. `["New York"]` |
| `state` | string[] | States, e.g. `["CA", "NY"]` |
| `country` | string[] | Countries, e.g. `["United States"]` |
| `industry` | string[] | Industries, e.g. `["Technology"]` |
| `seniority` | string[] | `"c_suite"`, `"vp"`, `"director"`, `"manager"`, `"senior"`, `"entry"` |
| `department` | string[] | Departments, e.g. `["Engineering"]` |
| `employeeRange` | string[] | `"1-10"`, `"11-50"`, `"51-200"`, `"201-500"`, `"501-1000"`, `"1001-5000"`, `"5001-10000"`, `"10001+"` |
| `hasWorkEmail` | boolean | Only contacts with verified work email |
| `hasPhoneCell` | boolean | Only contacts with mobile phone |
| `hasPhoneDirect` | boolean | Only contacts with direct dial |
| `limit` | number | Max results (1–100, default 25) |
| `start` | number | Pagination offset (default 0) |

**Credits:** 1 per search

---

### `contact_enrich`

Get verified email addresses, phone numbers, and full profile data for a contact.

| Parameter | Type | Description |
|-----------|------|-------------|
| `api_key` | string | **Required.** Your Bytemine workspace API key |
| `pid` | string | Contact PID from `people_search` results |
| `linkedin_url` | string | LinkedIn profile URL, e.g. `https://linkedin.com/in/johndoe` |

Provide either `pid` or `linkedin_url`.

**Returns:** Work email, personal email, direct dial, mobile, work phone, LinkedIn URL, company details, seniority, department.

**Credits:** 1 per successful match

---

## Setup

### Claude Desktop

1. Get your API key at [bytemine.ai](https://bytemine.ai) → Developer Suite → API Keys
2. Open Claude Desktop → **Settings → Developer → Edit Config**
3. Add the following to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "bytemine": {
      "url": "https://bvjmtgaxijpyasjtaqiv.supabase.co/functions/v1/mcp-server"
    }
  }
}
```

4. Restart Claude Desktop. You'll see a 🔨 icon when tools are detected.

### Other Clients

Any MCP client that supports **Streamable HTTP** transport can connect using the server URL above. Compatible with Cursor, Windsurf, Cline, Continue, and MCP Inspector.

---

## Example Prompts

Try these in Claude after setup:

- *"Find me CTOs at healthcare companies in New York"*
- *"Search for Marketing Directors at SaaS companies with 50-200 employees"*
- *"Enrich this LinkedIn profile: linkedin.com/in/johndoe"*
- *"Find VPs of Engineering in San Francisco with direct phone numbers"*

---

## Authentication

Every tool call requires your Bytemine workspace API key passed as the `api_key` parameter. Credits are deducted from your workspace balance automatically.

Get your API key: [bytemine.ai](https://bytemine.ai) → Developer Suite → API Keys

---

## Links

- **Website:** [bytemine.ai](https://bytemine.ai)
- **API Docs:** [bytemine.ai/developer-hub](https://bytemine.ai/developer-hub)
- **MCP Setup Guide:** [bytemine.ai/developer-hub?tab=mcp](https://bytemine.ai/developer-hub?tab=mcp)

## License

MIT
