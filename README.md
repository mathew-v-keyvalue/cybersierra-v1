# Cyber Sierra — Claude Code Plugin

Compliance automation plugin for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Orchestrates audit workflows, assessment creation, evidence collection, vendor risk management, and report generation through the **Morpheus CLI**.

## Directory Layout

```
.claude-plugin/
    plugin.json          # Plugin manifest — registers skills, binaries, and assets
    marketplace.json     # Marketplace metadata for future publishing

bin/
    morpheus             # Morpheus CLI binary

skills/
    cyber-sierra/
        SKILL.md                     # Main skill: router & orchestrator
        _generated/
            index.json               # Learned-skill discovery index
        _internal/
            planner/
                SKILL.md             # Execution plan generator
                references/
                    execution-plan-schema.md
                    planning-rules.md
            reflection/
                SKILL.md             # Post-execution reflection & learning
                references/
                    learning-rules.md
                    reflection-schema.md
                    skill-template.md
            shared/
                contracts.md         # Component contracts
                manifest-usage.md    # How to query the CLI manifest
                workflow-state.md    # Pipeline state schema

```

## Morpheus Binary

The `morpheus` CLI executable is **not** included in this repository. You must build or obtain it separately and place it in `bin/`:

```bash
cp /path/to/compiled/morpheus bin/morpheus
chmod +x bin/morpheus
```

Similarly, copy `agent-api.json` into `bin/`:

```bash
cp /path/to/agent-api.json bin/agent-api.json
```

Claude Code plugins automatically add `bin/` to the PATH, so the skill can invoke `morpheus` directly without any path configuration.

## Local Installation

1. **Clone this repository:**

   ```bash
   git clone https://github.com/cyber-sierra/claude-plugin.git
   cd claude-plugin
   ```

2. **Place the Morpheus binary:**

   ```bash
   cp /path/to/morpheus bin/morpheus
   chmod +x bin/morpheus
   cp /path/to/agent-api.json bin/agent-api.json
   ```

3. **Install the plugin in Claude Code:**

   ```bash
   claude plugin install /path/to/claude-plugin
   ```

4. **Verify the installation:**

   ```bash
   claude plugin list
   ```

   You should see `cyber-sierra` listed.

## Usage

Once installed, ask Claude Code to perform compliance tasks:

- *"Run an audit for my organization"*
- *"Create a vendor risk assessment"*
- *"Collect evidence for SOC 2 controls"*
- *"Generate a compliance report"*
- *"Log in to Cyber Sierra"*

The plugin routes your request through the skill system, builds an execution plan from the CLI manifest, and runs it after your confirmation.

## How It Works

The plugin implements a multi-stage pipeline:

1. **Router** — Parses the request, checks for matching learned skills, identifies relevant CLI modules
2. **Planner** — Generates a Canonical Execution Plan from CLI manifest commands (when no learned skill matches)
3. **Executor** — Runs the plan step-by-step, handling authentication and user confirmation for write operations
4. **Reflection** — Evaluates execution quality and optionally persists successful workflows as reusable skills

## Publishing

This plugin is designed for eventual publication through the Claude Code plugin marketplace. The `.claude-plugin/marketplace.json` file contains the required metadata. Before publishing:

1. Populate `icon`, `changelog`, and `minClaudeCodeVersion` fields in `marketplace.json`
2. Ensure the `morpheus` binary is available for all target platforms
3. Follow the Claude Code plugin publishing guide (when available)

## License

See repository root for license details.
# cybersierra-v1
# cybersierra-v1
