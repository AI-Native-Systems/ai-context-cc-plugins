# Contributing to AI Context Plugin

Thank you for your interest in contributing! This document provides guidelines for contributing to the AI Context Plugin.

## Getting Started

### Prerequisites

- Claude Code 1.0 or later
- Git

### Local Development

1. **Fork and clone the repository**
   ```bash
   git clone https://github.com/agenisea/ai-context-cc-plugins.git
   cd ai-context-plugin
   ```

2. **Add local marketplace for testing**
   ```bash
   /plugin marketplace add ./
   ```

3. **Install for testing**
   ```bash
   /plugin install ai-context@ans
   ```

4. **Test the commands**
   ```bash
   /ai-context:init
   /ai-context:update
   /ai-context:digest
   ```

## How to Contribute

### Reporting Bugs

1. Check existing issues first
2. Create a new issue with:
   - Clear title describing the problem
   - Steps to reproduce
   - Expected vs actual behavior
   - Claude Code version
   - OS and environment details

### Suggesting Features

1. Check existing issues/discussions
2. Create a feature request with:
   - Clear description of the feature
   - Use case and motivation
   - Potential implementation approach (optional)

### Pull Requests

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Follow existing code style
   - Update documentation if needed
   - Keep changes focused and atomic

4. **Test your changes**
   - Test all three commands
   - Verify schema validation still works
   - Check edge cases

5. **Submit PR**
   - Clear title and description
   - Reference any related issues
   - Explain what changed and why

## Code Style

### Skill/Command Definitions

- Use YAML frontmatter for metadata
- Include clear `description` field
- Document all boundaries and focus areas
- Keep workflows organized in phases

### Schema Changes

- Follow JSON Schema Draft 7 format
- Add descriptions to all fields
- Include sensible defaults where appropriate
- Update documentation for new fields

### Documentation

- Keep README up to date
- Use clear, concise language
- Include examples where helpful

## Areas for Contribution

### High Impact

- **Schema improvements** - New fields for common use cases
- **Better inference** - Smarter detection of conventions
- **Multi-language support** - Improve detection for more languages
- **IDE integrations** - Context awareness in other tools

### Medium Impact

- **Examples** - Sample `.ai-context` files for various project types
- **Documentation** - Tutorials, guides, best practices
- **Validation** - Better error messages and suggestions

### Good First Issues

- Typo fixes
- Documentation improvements
- Additional keywords in schema
- Test coverage improvements

## Plugin Structure

```
ai-context-plugin/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace entry point
├── claude-code/plugins/ai-context/
│   ├── .claude-plugin/
│   │   └── plugin.json           # Plugin manifest
│   ├── commands/                 # Command definitions
│   │   ├── context-init.md
│   │   ├── context-update.md
│   │   └── context-digest.md
│   └── skills/                   # Auto-triggered skills
│       ├── context-init/SKILL.md
│       ├── context-update/SKILL.md
│       └── context-digest/SKILL.md
├── schemas/
│   └── ai-context.schema.json    # JSON Schema for .ai-context
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
└── package.json
```

## Questions?

- Open an issue for questions
- Tag with `question` label

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
