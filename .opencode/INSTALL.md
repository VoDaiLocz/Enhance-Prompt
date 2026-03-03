# Installing Enhance Prompt for OpenCode

## Prerequisites

- [OpenCode.ai](https://opencode.ai) installed
- Git installed

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/VoDaiLocz/Enhance-Prompt.git ~/.config/opencode/enhance-prompt
```

### 2. Symlink Skills

```bash
mkdir -p ~/.config/opencode/skills
ln -s ~/.config/opencode/enhance-prompt/skills ~/.config/opencode/skills/enhance-prompt
```

### 3. Restart OpenCode

Restart OpenCode. Verify by asking: `"do you know how to use enhance-prompt?"`

## Usage

### Load the skill

```
use skill tool to load enhance-prompt/enhance-prompt
```

### Use the slash command

```
/enhance-prompt Fix the login bug
```

## Updating

```bash
cd ~/.config/opencode/enhance-prompt && git pull
```

## Troubleshooting

### Skill not found

1. Check symlink: `ls -l ~/.config/opencode/skills/enhance-prompt`
2. Verify it points to: `~/.config/opencode/enhance-prompt/skills`
3. Use `skill` tool to list discovered skills

## Getting Help

- Issues: https://github.com/VoDaiLocz/Enhance-Prompt/issues
