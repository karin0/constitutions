# CONSTITUTIONS

The rules for changing this repository are in [AGENTS.md](AGENTS.md).

## Install

```bash
git clone https://github.com/karin0/constitutions ~/.constitutions
mkdir -p ~/.claude/rules
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.claude/rules/
```

Pi:

```bash
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.pi/agent/AGENTS.md
```

DeepSeek Harness:

```bash
ln -s ~/.constitutions/CONSTITUTIONS.md ~/.dsh/AGENTS.md
```
