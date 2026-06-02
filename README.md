# grok-connectors

Collection of Grok/xAI tool connectors, MCP integrations, browser-to-api workflows, and utilities for agent systems like Hermes and OpenClaw. Designed for self-hosted environments (Unraid, Home Assistant, Ubuntu) with privacy-focused, copy-paste ready examples.

## Overview

This repository centralises documentation and examples for the available tool connectors and skills in the Grok/xAI ecosystem. Use these to build or extend agent workflows, connect to services, and integrate with your local infrastructure like Unraid Docker containers and Home Assistant automations.

**Note:** These are system-level tools and skills. They are not public APIs but can inspire custom implementations or direct use via connected interfaces in supported agents.

## Available Tool Connectors

Core tools for search, browsing, media, file operations, and more:

- **web_search**: Query the web with operators. Returns results with citations.
- **browse_page**: Fetch and summarise specific webpage content based on instructions.
- **x_keyword_search** / **x_semantic_search**: Advanced X (Twitter) post search (keyword or semantic). Supports filters, limits, modes (Top/Latest).
- **x_user_search** / **x_thread_fetch**: Find X users or fetch full thread context.
- **search_images** / **generate_image** / **edit_image**: Image search (saves to disk), generation (Grok Imagine), and editing.
- **read_file** / **edit_file** / **write_file**: Local filesystem operations in the sandbox environment.
- **bash**: Execute shell commands in the persistent sandbox (with timeout, background options).
- **search_connected_tools** / **call_connected_tool**: Discover and invoke tools for your connected services (GitHub, Notion, Google Drive/Calendar/Gmail, monday.com).

All support parallel calls where applicable. Results include structured data for chaining in agents.

## Skills

Specialised capabilities (read SKILL.md in each for full instructions):

- **docx**: Create, read, edit Word documents (.docx). Professional formatting, headings, tables, images.
- **pdf**: Full PDF handling – extract text/tables, merge, split, rotate, watermark, OCR, fill forms, encrypt.
- **pptx**: PowerPoint creation/editing, slides, layouts, speaker notes.
- **xlsx**: Spreadsheet creation, editing, formulas, charts, data cleaning.
- **ffmpeg**: Media processing – video/audio convert, trim, extract frames, subtitles, GIFs, compression.
- **browser-to-api**: Convert interactive browser workflows (navigation, clicks, forms, scraping) into structured API endpoints/functions with JSON I/O. Ideal for reliable automation without persistent browser state.
- **ai-coding-prompt**: Generate optimised prompts for coding assistants (Claude, GPT, Grok, etc.). Outputs clean markdown code blocks.
- **daily-news**: Produce custom daily briefings (e.g. tech intelligence HTML).
- **memory-edit**: Policy for storing/updating user memory.md (personal facts, preferences).
- **skill-creator**: Guide for creating/updating custom skills.

## MCP & Agent Integrations (Hermes, OpenClaw, etc.)

For multi-model orchestration and MCP (context/tool calling) in agents:

- Use the above tools as building blocks for custom MCP servers or connectors.
- Examples integrate with Unraid (Docker, scripts like StandFirm, ProxyNet/Traefik), Home Assistant (YAML automations calling external endpoints or webhooks), and local services (MariaDB, SSH, SMB).
- Recommended pattern: Self-host MCP-compatible endpoints on your Unraid box for low-latency, private tool use in agents like Hermes.

Copy-paste ready Home Assistant example (automation to trigger a connector-style action via webhook):

```yaml
alias: "Trigger Grok Connector via Webhook"
description: "Example for calling external connector or agent endpoint"
trigger:
  - platform: webhook
    webhook_id: grok_connector_trigger
condition: []
action:
  - service: rest_command.call_connector
    data:
      endpoint: "https://your-unraid-ip:port/connector-endpoint"
      payload:
        query: "Latest X posts about Adelaide tech"
mode: single
```

(Replace with your actual endpoint; secure with authentication.)

## Unraid & Self-Hosting Notes

- Run companion containers for any custom MCP servers or browser-to-api endpoints.
- Use Traefik/ProxyNet for secure exposure.
- Store generated files (images, docs) in mounted volumes accessible to your agents.
- Git clone this repo into your Unraid appdata or a project share for versioning.

## Getting Started

1. Clone: `git clone https://github.com/LordVaderXIII/grok-connectors.git`
2. Review SKILL.md files in relevant skills (via source or docs).
3. For connected services: Use search_connected_tools to discover, then call_connected_tool with exact args from schema.
4. Build agents that chain tools (parallel where possible) for complex workflows.

## Limitations & Best Practices

- Tools run in a sandboxed environment; file ops are local to the session.
- For production agents, self-host equivalents with proper auth, rate limiting, and logging.
- Always verify outputs; chain with verification steps.
- Privacy: Connected services use your authenticated sessions – review permissions.

Contributions or custom extensions welcome via PRs. Tailor to your stack (Unraid, HA, Windows, Tesla integration, etc.).

---

*Initialised for Reuben's agent and self-hosting projects. Adapt as needed.*