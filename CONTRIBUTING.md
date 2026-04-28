# Contributing to hermes-custom-skills

Thank you for your interest in contributing! This guide will help you add new Hermes skills and submit pull requests.

---

## Table of Contents

- [Before You Start](#before-you-start)
- [Adding a New Skill](#adding-a-new-skill)
- [SKILL.md Format](#skillmd-format)
- [Testing Your Skill](#testing-your-skill)
- [Submitting a Pull Request](#submitting-a-pull-request)
- [Code Review Process](#code-review-process)
- [License](#license)

---

## Before You Start

1. **Fork** this repository
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/<your-username>/hermes-custom-skills.git
   cd hermes-custom-skills
   ```
3. **Create a feature branch**:
   ```bash
   git checkout -b feat/my-skill-name
   ```

---

## Adding a New Skill

### Step 1: Create the Skill Directory

```bash
mkdir my-skill-name
cd my-skill-name
```

### Step 2: Write the SKILL.md

Create a `SKILL.md` file that defines your skill. Use the template below as a starting point.

### Step 3: (Optional) Add Supporting Files

- **`README.md`** — Human-readable documentation, examples, and use cases
- **`/scripts`** — Helper scripts (Python, shell, etc.)
- **`/examples`** — Example inputs/outputs and sample invocations

### Step 4: Test Locally

```bash
# Test the skill definition syntax
hermes skill validate ./my-skill-name/SKILL.md

# Run the skill interactively
hermes run ./my-skill-name

# Test with inline inputs (if applicable)
hermes run ./my-skill-name --input 'param1=value1 param2=value2'
```

---

## SKILL.md Format

Every skill **must** have a valid `SKILL.md` file. Here's the required structure:

```yaml
---
name: skill-identifier
description: >
  A clear, one-line description of what this skill does.
  Can span multiple lines (use > for text wrapping).
version: 1.0.0
author: Your Name (https://github.com/your-handle)
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [tag1, tag2, tag3]
    requires_toolsets: [web, file, compute]
    requires_tools: [tool_name_1, tool_name_2]
    required_environment_variables:
      - name: API_KEY_NAME
        prompt: "Prompt shown to user when requesting this variable"
        help: "Additional help text explaining what this variable is for"
        required_for: "What feature/step requires this"
---

# Skill Title

A brief overview of what this skill does.

## When to Use

Describe the ideal use case(s) for this skill.

## When NOT to Use

List scenarios where this skill should not be used (helps avoid misuse).

## Inputs

Define all input parameters with:
- `parameter_name` — Type and description
  - Default: (if applicable)
  - Required: yes/no
  - Bounds: min..max (if numeric)

Example:
```
- `search_query` — String, the search terms to use
  - Default: "latest news"
  - Required: yes
```

## Outputs

Define all return values with:
- `output_name` — Type and description

Example:
```
- `results` — Array of objects, each containing:
  - `title` (string)
  - `url` (string)
  - `summary` (string)
```

## Procedure

Step-by-step workflow. Use numbered steps and be explicit:

1. Resolve inputs and validate bounds.
2. Initialize state (e.g., counters, seen URLs).
3. Fetch data.
4. Filter and rank results.
5. Return outputs.

Include verification logic, error handling, and edge cases.

## Verification

Define acceptance criteria for results:
- URLs must be valid
- Summaries must be non-empty
- Data must be fresh (within N days)

## Error Handling

Describe how to handle:
- Missing required inputs
- API failures
- Invalid results
- Timeout scenarios

```

### Required Metadata Fields

| Field | Purpose | Example |
|-------|---------|---------|
| `name` | Unique skill identifier (snake_case) | `ai-newsletter-daily` |
| `description` | One-line summary | `Generate a daily AI news digest` |
| `version` | Semantic version | `1.0.0` |
| `author` | Skill creator | `Jane Doe (https://github.com/janedoe)` |
| `platforms` | Supported OS | `[linux, macos, windows]` |
| `metadata.hermes.tags` | Searchable tags | `[AI, News, Content]` |
| `metadata.hermes.requires_tools` | Tools this skill needs | `[web_search, web_fetch]` |

---

## Testing Your Skill

### Pre-Submission Checklist

- [ ] Skill runs without errors: `hermes run ./my-skill-name`
- [ ] All inputs have defaults or are marked required
- [ ] All outputs are properly documented
- [ ] Workflow steps are clear and testable
- [ ] Verification steps are explicit
- [ ] Error handling is documented
- [ ] Environment variables are defined in metadata
- [ ] `SKILL.md` passes validation: `hermes skill validate ./my-skill-name/SKILL.md`

### Testing with Sample Data

```bash
# Test with inline inputs
hermes run ./my-skill-name --input 'param1="test" param2=5'

# Test with sample file
hermes run ./my-skill-name --input-file examples/sample-input.json

# Verify output structure
hermes run ./my-skill-name --output-format json | jq .
```

---

## Submitting a Pull Request

### PR Title Format

Use one of these prefixes:

- **`feat:` — New skill**
  - `feat: add weather-forecast-agent`
- **`improve:` — Enhance existing skill**
  - `improve: optimize ai-newsletter performance`
- **`fix:` — Bug fix**
  - `fix: handle missing dates in ai-newsletter`
- **`docs:` — Documentation only**
  - `docs: add examples to ai-newsletter README`

### PR Checklist

Before submitting, ensure:

- [ ] Fork is up to date with `main`
- [ ] Commits are clean and atomic
- [ ] Commit messages follow the format above
- [ ] All tests pass locally
- [ ] README is updated (if applicable)
- [ ] No breaking changes (or clearly documented)

### PR Description Template

```markdown
## Description

Brief explanation of what this PR adds or changes.

## Type of Change

- [ ] New skill
- [ ] Enhancement to existing skill
- [ ] Bug fix
- [ ] Documentation

## Testing Done

Describe how you tested this skill:
- Tested with sample inputs: [describe]
- Verified outputs: [describe]
- Tested error cases: [describe]

## Related Issues

Closes #(issue number) if applicable.

## Checklist

- [ ] SKILL.md is valid and complete
- [ ] README or examples added (if new skill)
- [ ] Tested locally with `hermes run`
- [ ] No breaking changes
- [ ] License header included (MIT)
```

---

## Code Review Process

1. **Automated checks** — We run validation on all PRs:
   - SKILL.md syntax validation
   - Metadata completeness check
   - License verification

2. **Maintainer review** — A maintainer will:
   - Check workflow logic and correctness
   - Verify inputs/outputs match documentation
   - Ensure error handling is robust
   - Test the skill end-to-end

3. **Feedback & revisions** — We may request changes. Please respond within 5 days.

4. **Merge** — Once approved, your PR will be merged to `main`.

---

## Style Guidelines

- **Skill names**: Use lowercase, hyphen-separated (e.g., `ai-newsletter-daily`)
- **SKILL.md**: Use clear, imperative language ("Fetch data", "Filter results", not "Data is fetched")
- **Comments**: Keep sparse; the workflow should be self-documenting
- **Errors**: Be explicit about failure modes and recovery strategies

---

## Questions?

- Check existing skills in this repo for examples
- Review the [Hermes documentation](https://hermes.ai/docs)
- Open a discussion or issue with questions

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License (same as this project).

Thank you for improving hermes-custom-skills! 🙏
