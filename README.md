# Oplane for Cursor

AI-powered security analysis for your codebase: threat modeling, implementation assessment, and PR security review, inside Cursor.

## What it does

This plugin connects Cursor to [Oplane](https://www.oplane.com), giving you:

- **Codebase analysis**: identify security threats across your entire project
- **PR review**: analyze pull requests for security implications
- **Implementation assessment**: check if security requirements are properly implemented
- **Severity management**: adjust requirement severity based on your risk context

Results are saved to Oplane and visible in the [Gravity web interface](https://gravity.oplane.io).

## Prerequisites

- [Cursor](https://cursor.com)
- An [Oplane account](https://gravity.oplane.io)

## Installation

Open **Customize** in the Cursor sidebar, search for **Oplane**, select **Install**, and choose a project or user scope. You can also find it in the [Cursor Marketplace](https://cursor.com/marketplace).

## Authentication

The Oplane MCP server signs you in with OAuth, so there are no tokens to copy. Open **Cursor Settings > MCP**, find the Oplane server, and sign in when prompted. Tokens are issued and refreshed automatically.

For CI pipelines and other automation where nobody signs in, use an Oplane application key instead, see [Applications](https://www.oplane.com/docs/administration/applications).

## Usage

### Analyze a codebase

Type `/analyze` in the Agent chat, or ask the agent to analyze the project for security threats with Oplane. Optionally focus on a specific area:

```
/analyze authentication and session management
```

### Analyze a pull request

Type `/analyze-pr` in the Agent chat, and add context about the change:

```
/analyze-pr PR #123 adds OAuth login flow
```

### Security agent

The plugin also includes a `security-analyzer` agent for an in-depth, self-directed security review of the codebase.

## Recommended setup: CLAUDE.md / AGENTS.md

The single highest-impact step is making threat modeling a standing instruction your agent
reads every session, so security-relevant changes are modeled before each commit or PR,
not just reviewed after a PR opens. Add this to your project's `CLAUDE.md` (and/or
`AGENTS.md`):

```
For changes that could affect security, you MUST threat-model the change using Oplane MCP
before committing. Threat-model the actual diff (e.g. the PR threat model), not a written
summary of it - a model built from your own description only re-tests risks you already
considered. Explicitly consider untrusted-input-inbound (log/audit/template/SQL injection
from external data), not only outward data leakage.
```

## Available tools

The plugin connects your agent to the Oplane MCP server, which provides the tools the skills
use (create a threat model, get implementation advice, record assessments, and more). For the
full list, see the [MCP tool reference](https://www.oplane.com/docs/reference/mcp-tools).

## What the plugin sends

The plugin connects your agent to Oplane's MCP server at `https://gravity.oplane.io/mcp/`.
When you run an analysis, your agent sends Oplane:

- titles and descriptions of the code or change it is threat modeling, which can include
  short code excerpts
- git details such as the repository URL, branch, commit SHA and pull request URL
- the assessment it records for each security requirement, with file and line references

The plugin sends nothing to any other service. It has no hooks or scripts that run on your
machine: the skills and the agent are instructions your agent follows. Oplane stores the
results in your account, as described in the
[privacy policy](https://www.oplane.com/legal/privacy-policy).

## Support

See the [Oplane agent plugins documentation](https://www.oplane.com/docs/reference/agent-plugins) or email [support@oplane.io](mailto:support@oplane.io).

## License

Apache License 2.0. See [LICENSE](LICENSE).
