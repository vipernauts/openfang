# Usage Statement & Legal Compliance Notice

**Author:** vipernauts (Hans)
**Date:** 2026-03-14
**Last reviewed:** 2026-03-14

---

## Purpose of This Fork

This is a private fork of [OpenFang](https://github.com/RightNow-AI/openfang) (MIT license) maintained for personal use as a productivity tool — specifically as a personal AI secretary that routes messages from messaging platforms (Signal, Telegram, etc.) to LLM backends for automated handling.

## LLM Provider Configuration

This fork uses OpenFang's built-in `claude-code` driver, which invokes the official Claude Code CLI binary (`claude -p`) as a subprocess. This is the same binary distributed by Anthropic at [claude.ai/install.sh](https://claude.ai/install.sh).

**What this means:**
- All Claude interactions go through the **official Claude Code CLI binary**
- Authentication uses the user's existing **Claude Code Max subscription** (20x plan)
- No OAuth tokens are extracted, intercepted, or proxied
- No custom API harness is used — the CLI is called as a standard subprocess
- No claude.ai login credentials are offered to third parties
- This tool is not a "third-party harness" — it delegates to the official binary

**What this does NOT do:**
- Does not intercept or spoof Claude Code OAuth tokens
- Does not bypass Anthropic's CLI telemetry or session management
- Does not resell, redistribute, or offer Claude API access to any third party
- Does not use Claude's API outside the official CLI path
- Does not train AI models on Claude's outputs
- Does not impersonate humans — all AI-generated messages are from an explicitly personal agent

## Compliance Analysis

A detailed legal/policy analysis of OpenFang's compatibility with Anthropic's Terms of Service was conducted on 2026-03-14. The analysis reviewed:

- [Anthropic Consumer Terms of Service](https://www.anthropic.com/legal/consumer-terms)
- [Anthropic Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms)
- [Anthropic Acceptable Use Policy](https://www.anthropic.com/legal/aup)
- [Claude Agent SDK documentation](https://platform.claude.com/docs/en/agent-sdk/overview) (for the third-party auth restriction)
- [Claude Code CLI reference](https://code.claude.com/docs/en/cli-reference) (for the `-p` flag as a supported non-interactive mode)

### Key findings:

1. **Using Claude Code CLI via subprocess is a supported use pattern.** The `-p` / `--print` flag is explicitly documented for non-interactive, scripted usage. OpenFang's `claude-code` driver uses this flag.

2. **This is not a "third-party harness."** Anthropic's January 2026 crackdown targeted tools that extracted OAuth tokens from claude.ai sessions and made direct API calls pretending to be Claude Code. OpenFang does not do this — it runs the actual binary.

3. **Development of this fork uses Claude Code Max.** Using Claude Code to write, debug, and maintain software is the tool's intended purpose. The type of software being developed (an agent framework) is not restricted — Anthropic's own Agent SDK encourages building autonomous agents.

4. **No commercial redistribution.** This fork is for personal use. It is not offered as a product or service to third parties.

5. **AUP compliance.** The agents configured in this fork comply with Anthropic's Acceptable Use Policy. No mass surveillance, influence operations, impersonation, or unauthorized access.

### Full analysis document:

The complete 380-line legal/policy analysis with clause-by-clause review is archived at:
- Local: `~/Documents/research/2026-03-14-anthropic-tos-analysis-openfang-openclaw.md`
- Obsidian vault: `research/2026-03-14-anthropic-tos-analysis-openfang-openclaw.md`

## Configuration Reference

```toml
# OpenFang config using Claude Code CLI as LLM backend
[default_model]
provider = "claude-code"
base_url = "/usr/local/bin/claude"  # Path to official Anthropic CLI binary

# Channel: personal Signal integration
[signal]
api_url = "http://localhost:8080"   # signal-cli REST API
phone_number = "+XXXXXXXXXXX"       # Bot's registered number
allowed_users = ["+XXXXXXXXXXX"]    # Only the owner — not a public service
```

## Upstream Sync Policy

This fork pulls from `origin` (RightNow-AI/openfang) daily. Local changes are limited to:
- This file (`USAGE_STATEMENT.md`)
- Personal agent configurations in `agents/`
- Configuration in `openfang.toml`
- Any `.gitignore` additions for local secrets

No upstream code is modified. If upstream changes conflict with local config, upstream wins.

---

*This document exists for transparency and personal record-keeping. It is not legal advice.*
