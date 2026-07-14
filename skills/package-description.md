---
summary: "Template and instructions for writing package description documents"
---

# Skill: Write a package description

Instructions for creating a package description document in
`packages/<package-name>.md`.

## Template

When describing a package, gather and organize the following information:

```markdown
# <Package name>

- **Repository**: <URL>
- **Language**: <Primary language(s)>
- **Status**: active | maintenance | experimental | deprecated
- **Last reviewed**: YYYY-MM-DD

## Purpose

One paragraph: what does this package do and who uses it?

## Key features

Bullet list of main capabilities.

## Architecture

Brief description of the internal organization: main modules, key classes
or functions, data flow.

## Dependencies

### Depends on (our packages)
- List of internal packages this depends on, and how

### Depended on by (our packages)
- List of packages that depend on this one

### Key external dependencies
- Major third-party libraries (not exhaustive, just the important ones)

## API surface

Brief description of the public API: main entry points, key functions,
data structures. Focus on what other packages or users interact with.

## Known issues and technical debt

Current problems, planned refactors, or known limitations.

## Instructions for AI assistants

When asked to create a package description:

1. Read the package's source code, README, and any existing documentation
2. Fill in as much of the template as you can verify from the code
3. Mark anything uncertain with `[TODO: verify]`
4. Save to `packages/<package-name>.md`
