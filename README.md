# AI Context Plugin for Claude Code

**Generate and manage `.ai-context` files for AI-assisted development.**

This plugin helps you create structured context files that help AI assistants understand your project deeply - including conventions, domain terminology, architecture, and sensitive areas.

## The Problem

AI assistants often struggle with project-specific knowledge:
- They don't know your naming conventions
- They miss domain-specific terminology
- They can't see your architectural decisions
- They don't know which areas need extra care

## The Solution

The AI Context Plugin creates and maintains `.ai-context` files - structured YAML documents that capture everything an AI needs to know about your project:

- **Project metadata** - Stack, framework, dependencies
- **Domain knowledge** - Terms, entities, relationships
- **Conventions** - Naming patterns, file organization
- **Preferences** - Tooling choices, patterns to avoid
- **Caution areas** - Sensitive code with severity levels
- **Testing** - Frameworks, commands, patterns

## Quick Start

```bash
# Add the marketplace
/plugin marketplace add AI-Native-Systems/ai-context-cc-plugins

# Install the plugin
/plugin install ai-context@ans

# Initialize context for your project
/ai-context:init
```

## Commands

| Command | Description |
|---------|-------------|
| `/ai-context:init` | Create `.ai-context` for new or existing projects |
| `/ai-context:update` | Update context based on recent codebase changes |
| `/ai-context:digest` | Generate human-readable markdown summary |

## Skills (Auto-Triggered)

Skills are automatically invoked by Claude based on trigger phrases:

| Skill | Trigger Phrases | Purpose |
|-------|-----------------|---------|
| **context-init** | "context init", "create ai context", "initialize context" | Create context files |
| **context-update** | "update context", "sync context", "refresh ai context" | Keep context synced |
| **context-digest** | "context digest", "generate digest", "onboarding doc" | Generate readable summaries |

## How It Works

### 1. Context Init

For **existing projects**, the plugin:
1. Scans your codebase (package.json, configs, directory structure)
2. Detects stack, framework, and conventions
3. Asks you to confirm inferences
4. Fills gaps with targeted questions
5. Generates `.ai-context` YAML file
6. Sets up auto-loading via SessionStart hooks

For **new projects**, it guides you through setup questions.

### 2. Context Update

When your codebase evolves:
1. Detects changes via git history or file scanning
2. Identifies new dependencies, patterns, structure changes
3. Shows a diff of proposed updates
4. Makes surgical edits while preserving user-authored content

### 3. Context Digest

Transforms `.ai-context` into `AI-CONTEXT-DIGEST.md`:
- Human-readable markdown
- Perfect for team onboarding
- Tables, headers, and scannable format
- Skip empty sections automatically

## Example `.ai-context` Output

```yaml
version: "1.0"

project:
  name: "my-app"
  description: "E-commerce platform"
  type: "web-app"
  stack:
    - TypeScript
    - Next.js
    - Tailwind CSS
    - Prisma

domain:
  industry: "e-commerce"
  terms:
    - term: "SKU"
      meaning: "Stock Keeping Unit - unique product identifier"
    - term: "Cart"
      meaning: "Temporary collection of items before checkout"

structure:
  conventions:
    components: "src/components/{Name}/{Name}.tsx"
    tests: "co-located as {Name}.test.tsx"

preferences:
  state_management: "zustand"
  styling: "tailwind"
  avoid:
    - pattern: "class components"
      reason: "Use functional components with hooks"

caution:
  - path: "src/lib/payments/*"
    reason: "Payment processing - PCI compliance required"
    severity: "critical"

testing:
  framework: "vitest"
  run_command: "npm test"

history:
  created: "2024-01-15"
  last_updated: "2024-01-21"
```

## Schema

The plugin includes a comprehensive JSON Schema (`schemas/ai-context.schema.json`) that defines all supported fields:

- Project types: `web-app`, `api`, `cli`, `library`, `mobile-app`, `desktop-app`, `monorepo`, `microservices`
- Component statuses: `stable`, `unstable`, `deprecated`, `experimental`
- Severity levels: `info`, `warning`, `critical`
- Naming conventions: `camelCase`, `snake_case`, `PascalCase`, `kebab-case`

## Auto-Loading

The plugin sets up automatic context loading via:

1. **SessionStart hook** in `.claude/settings.json` (primary)
2. **CLAUDE.md** reference (fallback for other AI tools)

This ensures AI assistants always have your project context.

## Security & Trust

- **No external dependencies** - All functionality is self-contained
- **No data collection** - Your context stays local
- **No network calls** - Except for Claude API (handled by Claude Code)
- **Open source** - Full transparency

## Requirements

- Claude Code 1.0 or later
- No external dependencies

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.

---

Built for the [ans marketplace](https://github.com/AI-Native-Systems/ai-context-cc-plugins)

---

Built by [AI Native Systems™](https://ainativesystems.io)