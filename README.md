# @orchesty/nodejs-ai

AI coding rules for building [Orchesty](https://docs.orchesty.io/) Node.js integration workers. Designed to be installed as a dev dependency in an Orchesty worker repository so that AI assistants (Cursor, Claude Code, Windsurf, GitHub Copilot, Cline, Aider, ...) follow the same conventions when generating Applications, Connectors, Batches, CustomNodes, tests, and topology files.

## Installation

```bash
npm install --save-dev @orchesty/nodejs-ai
```

The rule files are then available at `node_modules/@orchesty/nodejs-ai/rules/`.

## Setup

See [AI-INSTRUCTIONS.md](AI-INSTRUCTIONS.md) for per-tool setup (Cursor, Claude Code, Windsurf, Copilot, Cline, Aider). Each tool needs the rules wired into its native rule engine — typically a one-time copy or concat command.

## Rules

| File | Purpose |
|------|---------|
| `orchesty-project.mdc` | Architecture, component registration, payload flow |
| `orchesty-naming.mdc` | Naming conventions, directory structure |
| `orchesty-connectors.mdc` | Connector, batch, and custom node patterns |
| `orchesty-applications.mdc` | Application (auth provider) patterns |
| `orchesty-testing.mdc` | Testing patterns, NodeTester, mock fixtures |
| `orchesty-topologies.mdc` | Topology JSON file format |

Each file uses YAML frontmatter (`alwaysApply`, `globs`, `description`) so Cursor's native rule engine can scope rules to the right files automatically.

## Updating

```bash
npm update @orchesty/nodejs-ai
```

Re-run the copy/concat step from [AI-INSTRUCTIONS.md](AI-INSTRUCTIONS.md) afterwards so the materialized rules in `.cursor/rules/`, `CLAUDE.md`, `.windsurfrules`, etc. reflect the latest content.

## License

Apache-2.0
