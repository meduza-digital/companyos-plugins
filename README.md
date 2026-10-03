# CompanyOS plugins

This folder is the source of the public repository
[`meduza-digital/companyos-plugins`](https://github.com/meduza-digital/companyos-plugins). Edit plugins
here; the `plugins-publish` workflow copies this folder to the root of that repository.

## Layout

One folder per host and plugin: `plugins/<host>/<plugin>/`. Each folder is one plugin as its host
and its directory expect it, so it can be submitted on its own.

| Path | What it is |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude marketplace `companyos`. Lists `./claude/companyos` |
| `claude/companyos/` | Claude plugin `companyos`: `.claude-plugin/plugin.json`, `.mcp.json`, `skills/` |
| `chatgpt/companyos/` | Planned ChatGPT/Codex plugin. Not built yet |
| `.agents/plugins/marketplace.json` | Planned ChatGPT/Codex marketplace that will list `./chatgpt/companyos` |

The ChatGPT/Codex plugin will use OpenAI's portable format: a root `plugin.json`, `skills/` with the
same `SKILL.md` files, and `mcp.json` pointing at `https://app.companyos.cc/api/mcp`. See
<https://developers.openai.com/plugins/build/plugins>.

## Install from a checkout

```bash
claude plugin validate --strict plugins/claude/companyos
claude plugin marketplace add ./plugins
claude plugin install companyos@companyos
```

## Release

1. Change the plugin and bump `version` in `claude/companyos/.claude-plugin/plugin.json`. Users and the directory only pick up a new version.
2. Run `bun test tooling/plugins.test.ts` and `claude plugin validate --strict plugins/claude/companyos`.
3. Merge to `main`.
4. Run the **Publish plugins** workflow (`plugins-publish`) from `main` in GitHub Actions. It tests, copies this folder to the public repository, and pushes one commit naming the source SHA. Anthropic's directory picks that commit up from there.

The workflow needs the repository secret `PLUGINS_DEPLOY_KEY`, a deploy key with write access to
`meduza-digital/companyos-plugins`.
