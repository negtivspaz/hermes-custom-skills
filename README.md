# hermes-custom-skills

> Production-ready skills for the [Hermes](https://hermes.ai) agent platform — designed for autonomous workflow automation, content generation, and intelligent task orchestration.

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Hermes Skills](https://img.shields.io/badge/hermes%20skills-2-blue)](#available-skills)

---

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Available Skills](#available-skills)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [Related Repositories](#related-repositories)
- [License](#license)

---

## Overview

This repository hosts production-ready **Hermes skills** — self-contained agent instruction sets (`SKILL.md`) that drive Hermes agents through specific workflows.

**Skills** are declarative specifications that define:
- Agent capabilities and tools required
- Input/output contracts
- Workflow procedures with verification steps
- Environment variables and dependencies

Each skill is optimized for the Hermes agent execution model and integrates with Hermes' built-in tool ecosystem.

---

## Prerequisites

- [Hermes CLI](https://hermes.ai/docs/cli) installed and authenticated
- Hermes agent runtime (local or managed)
- API access as required per skill:
  - Web research: BRAVE_API_KEY, FIRECRAWL_API_KEY
  - Additional tools as noted in individual `SKILL.md` files

---

## Available Skills

### Content & Information

| Skill | Description | Language | Tools Required |
|-------|-------------|----------|-----------------|
| [`ai-newsletter-prompt`](./ai-newsletter-prompt/SKILL.md) | Generate daily AI news newsletter from fresh web sources | English | web_search, web_fetch |
| [`ai-newsletter-prompt-chn`](./ai-newsletter-prompt-chn/SKILL.md) | Generate daily AI news newsletter for Chinese audience | 中文 | web_search, web_fetch |

---

## Installation

### From this Repository

```bash
# Clone the repository
git clone https://github.com/negtivspaz/hermes-custom-skills.git
cd hermes-custom-skills

# Install a skill from a local path
hermes skill install ./ai-newsletter-prompt

# Or use the CLI directly
hermes run ./ai-newsletter-prompt
```

### From a Skill Directory

```bash
# Navigate to skill directory
cd ai-newsletter-prompt

# Execute the skill
hermes run .
```

---

## Usage

Each skill is invoked through the Hermes CLI or agent context. Refer to the individual `SKILL.md` for the full input/output contract and workflow details.

### Interactive Execution

```bash
# Run a skill interactively (prompts for inputs)
hermes run ai-newsletter-prompt
```

### Inline Inputs

```bash
# Pass inputs directly
hermes run ai-newsletter-prompt --input 'search_query="latest AI breakthroughs" target_news_count=15'
```

### Agent Context

Within a Hermes agent workflow, invoke a skill by name:

```
Use the ai-newsletter-prompt skill to generate a daily briefing.
```

---

## Skill Structure

Each skill directory contains:

- **`SKILL.md`** — Skill definition with metadata, inputs, outputs, and detailed workflow procedures
- **`README.md`** (optional) — Human-readable documentation and examples
- **`/scripts`** (optional) — Supporting Python/shell scripts for complex operations

### Example Skill.md Structure

```yaml
---
name: skill-name
description: What this skill does
version: 1.0.0
author: Name (github url)
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [tag1, tag2]
    requires_toolsets: [toolset1]
    requires_tools: [tool1, tool2]
    required_environment_variables:
      - name: ENV_VAR_NAME
        prompt: User-facing prompt
        help: Helper text
        required_for: What feature needs this
---

# Skill Title

[Detailed documentation...]
```

---

## Environment Variables

Most skills require external API keys. Set these before running:

```bash
export BRAVE_API_KEY="your-brave-api-key"
export FIRECRAWL_API_KEY="your-firecrawl-api-key"
```

For production use, configure these in your Hermes agent configuration or secrets manager.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding new skills, testing, and submitting pull requests.

---

## Related Repositories

- [**claude-custom-skills**](https://github.com/j3ffyang/claude-custom-skills) — Claude Code IDE automation skills
- [**openclaw-custom-skills**](https://github.com/j3ffyang/openclaw-custom-skills) — OpenClaw workflow automation skills

---

## License

This project is licensed under the [MIT License](LICENSE).

Individual skills may carry their own license declarations inside their `SKILL.md`.
