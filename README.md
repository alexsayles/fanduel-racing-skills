# FanDuel Racing — Shared Claude Skills

Shared Claude Code skills for the FanDuel Racing product team.

## Setup

1. Clone this repo:
   ```bash
   git clone https://github.com/<your-org>/fanduel-racing-skills.git ~/fanduel-racing-skills
   ```

2. Add the skills directory to your Claude Code settings (`~/.claude/settings.json`):
   ```json
   {
     "skills": ["~/fanduel-racing-skills/skills"]
   }
   ```

3. Restart Claude Code. Type `/` to see all available skills.

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| Amplitude Specs | `/amplitude-specs` | Generate Amplitude event tracking specs for Racing features, publish to Confluence |

## Adding Skills

1. Create a new directory under `skills/` with the skill name (kebab-case).
2. Add a `SKILL.md` file inside it — see existing skills for the format.
3. Open a PR, get it merged, and teammates pull the latest.
