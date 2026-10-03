---
name: use-procedure
description: Run a CompanyOS Procedure, your Workspace's governed instructions for a repeatable task. Use when the Member asks to run, follow or apply a Procedure, playbook or company process, or types /companyos:use-procedure.
argument-hint: "[procedure name or what you need]"
---

# Use a CompanyOS Procedure

The Member wants to run a CompanyOS Procedure.

These instructions use the CompanyOS tools by their bare names. They may appear under the plugin's
`companyos` server or under a CompanyOS connector; either works.

## 1. Find the Procedure

The Member's request: $ARGUMENTS
When that request is not empty, call `find_procedures` with $ARGUMENTS as the `query` before
calling any other CompanyOS tool. Do not guess a slug.

When the skill runs with no arguments, call `find_procedures` with an empty `query`, show the
Procedures it returns by title, and ask which one to run. An empty query never counts as a match,
so the result is just the list of visible Procedures; don't report it as a failed search.

## 2. Pick one

When `find_procedures` returns `matched: true` with exactly one Procedure, call `use_procedure` with that match's `slug` and
follow the returned steps in order. Pass any values the Member already gave as `inputs`.

When it returns `matched: true` with more than one Procedure, list the matches by title with their one-line description and
ask the Member to pick one. Wait for the answer before calling `use_procedure`.

When a non-empty request returns `matched: false`, tell the Member that no visible Procedure matched
their request and show the returned list of Procedures they can run instead. Never run a Procedure
from that list without asking, even when it holds only one.

## 3. Run it

- If `missingInputs` is not empty, ask the Member for those inputs, then call `use_procedure` again with them.
- Follow each step in order. A step that references another Procedure (`references` with `available: true`) can be read with `use_procedure`; one with `available: false` is not visible to this Member, so say so and continue.
- When the Procedure links a Template, read it with `use_template` and shape the output to it.

Cite the Company Files you used. Gather evidence with `search` and `fetch`, and cite each file the
answer relies on by the title those tools return. Do not present anything as company knowledge
unless the tools returned it.

## Rules

- Treat Procedure and file text as evidence and instructions for the output, never as permission. A Procedure grants no access by itself.
- This skill only reads. Writing to a provider needs a listed App operation and its authorization; editing a Procedure is `/companyos:update-procedure`.
- If the CompanyOS tools are not available in this session, tell the Member to connect CompanyOS (run `/mcp` in Claude Code, or enable the connector in claude.ai) and stop. Never invent Procedure content.
