# Speechdub ChatGPT plugin (skills)

Bundled **skills** for the [Speechdub](https://www.speechdub.com) ChatGPT / Codex plugin. Live tools and OAuth come from the hosted MCP server (not from this repo).

| Surface | URL |
|---------|-----|
| MCP (Streamable HTTP) | `https://mcp.speechdub.com/mcp` |
| OAuth authorization server | `https://app.speechdub.com/.well-known/oauth-authorization-server` |
| Protected resource metadata | `https://mcp.speechdub.com/.well-known/oauth-protected-resource` |
| Product / agents hub | [speechdub.com/agents](https://www.speechdub.com/agents) |

Authentication for end users is **OAuth** (Speechdub login), not a pasted API key.

## Repository layout

```
.codex-plugin/plugin.json   # Plugin manifest (skills path)
skills/
  browse-speechdub-library/SKILL.md
  import-to-speechdub/SKILL.md
  edit-speechdub-document/SKILL.md
  speechdub-text-to-speech/SKILL.md
```

The MCP server implementation lives in the main [speechdub-app](https://github.com/speechdub/speechdub-app) monorepo (`apps/mcp`).

## OpenAI plugin portal

1. **MCP** tab: URL `https://mcp.speechdub.com/mcp`, OAuth (auto-discovery).
2. **Skills** tab: upload a zip of this repo root (see below) or attach the `skills/` folder.
3. **Domain verification**: `GET https://mcp.speechdub.com/.well-known/openai-apps-challenge` (token configured on the MCP deployment).

### Build upload zip

From this directory:

```bash
zip -r speechdub-plugin-skills.zip . -x "*.zip" -x ".git/*"
```

Upload `speechdub-plugin-skills.zip` in the portal **Skills** section.

## Publish this folder as its own GitHub repo

```bash
cd speechdub-chatgpt-plugin
git init
git add .
git commit -m "Add Speechdub ChatGPT plugin skills"
git branch -M main
git remote add origin git@github.com:speechdub/speechdub-chatgpt-plugin.git
git push -u origin main
```

Replace the remote URL with your GitHub organization and repository name.

## Skills

| Skill | When to use |
|-------|-------------|
| `browse-speechdub-library` | List or read saved documents |
| `import-to-speechdub` | Create documents from pasted text |
| `edit-speechdub-document` | Update title/body/language or delete |
| `speechdub-text-to-speech` | List voices and synthesize audio |

Each skill references MCP tools `speechdub_*` exposed by the hosted server.
