# CompanyOS for Claude

CompanyOS brings your team's company knowledge, Procedures and Templates into Claude. This plugin
connects Claude to your CompanyOS Workspace and adds three commands.

## What it does

- Connects Claude to CompanyOS at `https://app.companyos.cc/api/mcp`. You see exactly what you can see in CompanyOS: Company Files, your own Personal Files, published Procedures and Templates, and your own drafts.
- Adds commands to run a Procedure, change one, and search your files with citations.

You need a CompanyOS account that is a Member of a Workspace. Start at [companyos.cc](https://companyos.cc).

## Install

**Claude Code**

```bash
claude plugin marketplace add meduza-digital/companyos-plugins
claude plugin install companyos@companyos
```

**claude.ai and the Claude desktop app**

Open **Customize → Plugins**, add the marketplace `meduza-digital/companyos-plugins` (or find CompanyOS in the directory), and install **CompanyOS**. Then connect it from the plugin's **Connectors** tab.

## Sign in

The first time Claude uses CompanyOS it opens the CompanyOS sign-in. In Claude Code, run `/mcp`, choose `companyos`, and sign in. If you belong to more than one Workspace, pick one. There is no API key, client ID or secret.

## Commands

| Command | What it does |
| --- | --- |
| `/companyos:use-procedure [procedure name or what you need]` | Finds the matching Procedure, asks you to pick when several match, and runs its steps with cited Company Files. |
| `/companyos:update-procedure [procedure name] [what to change]` | Shows the proposed change to a Procedure you may edit and saves it only after you say yes. Offers to create a personal Procedure when none matches. |
| `/companyos:search [question]` | Answers from your Company Files and Personal Files, citing each source, and says so when nothing matches. |

In claude.ai chat, Claude uses these skills when your request fits, even without typing the command.

## Data handling

- The plugin contains instructions and a server address only. It runs no code on your machine and stores nothing.
- Requests go to CompanyOS (`app.companyos.cc`) under your own sign-in. CompanyOS enforces the same file visibility as the web app.
- The commands read. Only `/companyos:update-procedure` writes, and only after you confirm the exact change. Sharing a Procedure with the Workspace waits for Owner approval.
- Privacy policy: <https://companyos.cc/privacy/>. Terms: <https://companyos.cc/terms/>.

## Support

Email [support@companyos.cc](mailto:support@companyos.cc) or visit <https://companyos.cc/support/>. Docs: <https://companyos.cc/docs/connect-claude/>.
