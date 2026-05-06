# Orchesty Worker — AI Instructions

This package (`@orchesty/nodejs-ai`) provides the AI coding rules used when building an Orchesty integration worker. The rules teach AI assistants how to build Applications, Connectors, Batches, CustomNodes, tests, and topology files for the Orchesty platform.

## Installation

In your worker repo:

```bash
npm install --save-dev @orchesty/nodejs-ai
```

The rule files are then available at `node_modules/@orchesty/nodejs-ai/rules/`.

## Rules

| File | Purpose |
|------|---------|
| `orchesty-project.mdc` | Architecture, component registration, payload flow |
| `orchesty-naming.mdc` | Naming conventions, directory structure |
| `orchesty-connectors.mdc` | Connector, batch, and custom node patterns |
| `orchesty-applications.mdc` | Application (auth provider) patterns |
| `orchesty-testing.mdc` | Testing patterns, NodeTester, mock fixtures |
| `orchesty-topologies.mdc` | Topology JSON file format |

Each rule file uses YAML frontmatter (`alwaysApply`, `globs`, `description`) to indicate when it applies.

## Tool-Specific Rule Setup

Detect which AI tool you are running in and follow the corresponding setup so the rules integrate natively with the tool's rule engine. **Do this once after installing the package**, and re-run the relevant copy/concat step after `npm update @orchesty/nodejs-ai` to pick up rule changes.

### Cursor

Copy the rule files so Cursor's native rule engine picks them up:

```bash
mkdir -p .cursor/rules
cp node_modules/@orchesty/nodejs-ai/rules/*.mdc .cursor/rules/
```

### Claude Code

Create a `CLAUDE.md` file in the project root. Read each file in `node_modules/@orchesty/nodejs-ai/rules/` and concatenate their contents (without the YAML frontmatter) into `CLAUDE.md`, separated by headings.

### Windsurf

Create a `.windsurfrules` file in the project root. Read each file in `node_modules/@orchesty/nodejs-ai/rules/` and concatenate their contents (without the YAML frontmatter) into `.windsurfrules`.

### GitHub Copilot

Create `.github/copilot-instructions.md`. Read each file in `node_modules/@orchesty/nodejs-ai/rules/` and concatenate their contents (without the YAML frontmatter) into that file.

### Cline / Roo Code

Copy the rule files into a `.clinerules/` directory:

```bash
mkdir -p .clinerules
cp node_modules/@orchesty/nodejs-ai/rules/*.mdc .clinerules/
```

### Aider

Create `.aider.conf.yml` that loads the rule files as read-only context:

```yaml
read:
  - node_modules/@orchesty/nodejs-ai/rules/orchesty-project.mdc
  - node_modules/@orchesty/nodejs-ai/rules/orchesty-naming.mdc
  - node_modules/@orchesty/nodejs-ai/rules/orchesty-connectors.mdc
  - node_modules/@orchesty/nodejs-ai/rules/orchesty-applications.mdc
  - node_modules/@orchesty/nodejs-ai/rules/orchesty-testing.mdc
  - node_modules/@orchesty/nodejs-ai/rules/orchesty-topologies.mdc
```

### Other tools

If your tool is not listed above, read all files in `node_modules/@orchesty/nodejs-ai/rules/` at the start of each session and treat their contents as mandatory coding rules.

## Updating

When a new version of `@orchesty/nodejs-ai` is released:

```bash
npm update @orchesty/nodejs-ai
```

Then re-run the copy/concat step for your AI tool so the materialized rules in `.cursor/rules/`, `CLAUDE.md`, `.windsurfrules`, etc. reflect the latest content.

## References

- [Orchesty Docs](https://docs.orchesty.io/category/get-started/)
- [Connector Examples](https://github.com/Orchesty/orchesty-nodejs-connectors/tree/master/lib)
- [Pre-built connector packages](https://www.npmjs.com/search?q=%40orchesty%2Fconnector)
