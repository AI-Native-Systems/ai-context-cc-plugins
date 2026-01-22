# Security Policy

## Reporting Vulnerabilities

If you discover a security vulnerability in the AI Context Plugin, please report it responsibly:

1. **Do not** open a public issue
2. Email security concerns to the maintainers
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

**Response time:** We aim to respond within 48 hours.

## Security Architecture

### No External Dependencies

This plugin contains no external runtime dependencies. All functionality is self-contained within Claude Code.

### No Data Collection

- Your `.ai-context` files stay local
- No telemetry or analytics
- No data is sent to external servers

### No Network Calls

The plugin makes no network calls. All API communication is handled by Claude Code itself.

### Open Source Transparency

All code is open source. You can audit:
- Command definitions in `commands/`
- Skill definitions in `skills/`
- Schema in `schemas/`

## Security Best Practices

### For Users

1. **Review generated context** - Always review `.ai-context` before committing
2. **Don't include secrets** - Never put API keys, passwords, or tokens in context files
3. **Caution areas** - Use the `caution` field to mark sensitive code
4. **.gitignore patterns** - Consider what should be ignored

### For Context Files

The `.ai-context` file should NOT contain:
- API keys or secrets
- Passwords or credentials
- Personal identifiable information (PII)
- Internal URLs not meant to be shared

It SHOULD contain:
- Public conventions and patterns
- Domain terminology (non-sensitive)
- Architectural decisions
- Warning areas for careful handling

### Contact Field Warning

The `active_work.contact` field should use **team or role designations**, not personal information:

```yaml
# BAD - exposes personal information
active_work:
  - area: "auth refactor"
    contact: "john.smith@company.com"  # Don't do this!

# GOOD - uses team designation
active_work:
  - area: "auth refactor"
    contact: "auth-team"  # Safe for public repos
```

## Sensitive Information Handling

### Caution Areas

Use the `caution` field to mark sensitive areas:

```yaml
caution:
  - path: "src/lib/payments/*"
    reason: "Payment processing - PCI compliance"
    severity: "critical"
    requires:
      - "security review"
      - "team lead approval"

  - path: "src/auth/*"
    reason: "Authentication code - security sensitive"
    severity: "warning"
```

### Avoid Patterns

Use `preferences.avoid` to prevent insecure patterns:

```yaml
preferences:
  avoid:
    - pattern: "eval()"
      reason: "Security risk - code injection"
    - pattern: "innerHTML"
      reason: "XSS vulnerability - use textContent"
```

## Threat Model

### What This Plugin Does NOT Do

- Execute arbitrary code
- Access network resources
- Read files outside the project
- Modify files without user action
- Store data externally

### What This Plugin Does

- Read project files to infer context
- Write `.ai-context` and related files
- Parse YAML configuration
- Generate markdown documentation

### Attack Surface

The plugin's attack surface is minimal:
- **Input:** User responses to questions, codebase files
- **Output:** YAML and markdown files in project directory
- **Execution:** Only through Claude Code's controlled environment

## Version Support

We support security updates for:
- Current major version
- Previous major version (6 months after new major release)

## Changelog

Security-related changes will be noted in release notes with `[SECURITY]` prefix.
