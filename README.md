# Speechdub plugin skills

Bundled **skills** for the [Speechdub](https://www.speechdub.com) plugin in the OpenAI universal plugin directory (Codex and supported assistant surfaces). Live tools and sign-in use the hosted MCP server (OAuth), not this repository.

| Surface | URL |
|---------|-----|
| MCP (Streamable HTTP) | `https://mcp.speechdub.com/mcp` |
| OAuth authorization server | `https://app.speechdub.com/.well-known/oauth-authorization-server` |
| Protected resource metadata | `https://mcp.speechdub.com/.well-known/oauth-protected-resource` |
| Agents hub | [speechdub.com/agents](https://www.speechdub.com/agents) |

End users authenticate with their Speechdub account (OAuth). No API key is pasted in the plugin UI.

## Layout

```
.codex-plugin/plugin.json
skills/
  browse-speechdub-library/SKILL.md
  import-to-speechdub/SKILL.md
  edit-speechdub-document/SKILL.md
  speechdub-text-to-speech/SKILL.md
```

MCP server implementation: [speechdub-app](https://github.com/speechdub/speechdub-app) (`apps/mcp`).

## Plugin portal

1. **MCP**: URL `https://mcp.speechdub.com/mcp`, OAuth via metadata discovery.
2. **Skills**: upload `speechdub-plugin-skills.zip` (see below) or the `skills/` folder.
3. **Domain verification**: `GET https://mcp.speechdub.com/.well-known/openai-apps-challenge` (token on the MCP deployment).

### Upload zip

```bash
zip -r speechdub-plugin-skills.zip . -x "*.zip" -x ".git/*"
```

## GitHub

[github.com/speechdub/speechdb-skills](https://github.com/speechdub/speechdb-skills)

```bash
git clone https://github.com/speechdub/speechdb-skills.git
```

## Skills

| Skill | When to use |
|-------|-------------|
| `browse-speechdub-library` | List or read saved documents |
| `import-to-speechdub` | Create documents from pasted text |
| `edit-speechdub-document` | Update title/body/language or delete |
| `speechdub-text-to-speech` | List voices and synthesize audio |

Each skill references MCP tools `speechdub_*` on the hosted server.
