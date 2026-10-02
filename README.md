# Speechdub plugin skills

Agent **skills** that teach assistants when and how to use [Speechdub](https://www.speechdub.com) document and speech tools over the public MCP connection. This repo holds workflow text only; live tools and user sign-in are provided by Speechdub’s hosted MCP server.

| Resource | URL |
|----------|-----|
| Product | [speechdub.com](https://www.speechdub.com) |
| Agents & integrations | [speechdub.com/agents](https://www.speechdub.com/agents) |
| MCP endpoint (Streamable HTTP) | `https://mcp.speechdub.com/mcp` |

Users connect through the plugin or MCP client UI and sign in with their Speechdub account. This repository does not contain credentials or server code.

## Layout

```
.codex-plugin/plugin.json
skills/
  browse-speechdub-library/SKILL.md
  import-to-speechdub/SKILL.md
  edit-speechdub-document/SKILL.md
  speechdub-text-to-speech/SKILL.md
```

## Skills

| Skill | When to use |
|-------|-------------|
| `browse-speechdub-library` | List or read saved documents |
| `import-to-speechdub` | Create documents from pasted text |
| `edit-speechdub-document` | Update title, body, language, archive, or delete |
| `speechdub-text-to-speech` | List voices (`F1`-`F5`, `M1`-`M5`) and synthesize audio |

Each skill documents MCP tools named `speechdub_*` on the hosted server. REST examples live in [speechdub-public-api](https://github.com/speechdub/speechdub-public-api).

## Bundle for upload

Directory resubmission uses the plugin root: `.codex-plugin/plugin.json`, `assets/`, and `skills/`. Keep the existing package `name`. Do not put the README or `.git` in the zip.

```bash
zip -r speechdub-plugin.zip .codex-plugin assets skills
```

Single skill:

```bash
zip -r import-to-speechdub.zip skills/import-to-speechdub
```

## Repository

[github.com/speechdub/speechdub-skills](https://github.com/speechdub/speechdub-skills)

```bash
git clone https://github.com/speechdub/speechdub-skills.git
```
