# Installing Enhance Prompt for Codex

Enable enhance-prompt skill in Codex via native skill discovery.

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/VoDaiLocz/Enhance-Prompt.git ~/.codex/enhance-prompt
   ```

2. **Create the skills symlink:**
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/enhance-prompt/skills ~/.agents/skills/enhance-prompt
   ```

   **Windows (PowerShell):**
   ```powershell
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills"
   cmd /c mklink /J "$env:USERPROFILE\.agents\skills\enhance-prompt" "$env:USERPROFILE\.codex\enhance-prompt\skills"
   ```

3. **Restart Codex** to discover the skill.

## Verify

```bash
ls ~/.agents/skills/enhance-prompt
```

You should see a symlink pointing to the skills directory.

## Usage

Ask Codex something that triggers the skill:

```
/enhance-prompt Fix the login bug
```

Or tell the agent:
```
Use the enhance-prompt skill to improve this prompt: "optimize the database"
```

## Updating

```bash
cd ~/.codex/enhance-prompt && git pull
```

## Uninstalling

```bash
rm ~/.agents/skills/enhance-prompt
rm -rf ~/.codex/enhance-prompt
```
