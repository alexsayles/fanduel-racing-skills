# FanDuel Racing — Shared Claude Skills

Shared Claude Code skills for the FanDuel Racing product team.

## Setup

1. Clone this repo:
   ```bash
   git clone https://github.com/alexsayles/fanduel-racing-skills.git
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
| Racing Project Kickoff | `/racing-project-kickoff` | Kick off a new Racing initiative — creates the full Jira ticket set (FPDISCO, PONY, INITRACING, UXDFLY) wired together with the correct link types |
| Racing Business Case | `/racing-business-case` | Build a structured business case for a Racing feature — interviews you, drafts revenue impact and success metrics, then publishes to Confluence under FDR Transformational Work linked back to the FPDISCO ticket |
| Disco T-Shirt Sizer | `/disco-tshirt-sizer` | Act as a Racing engineering lead to assess t-shirt size (XS/S/M/L/XL/Spike) for a FPDISCO discovery ticket — asks targeted clarifying questions, references comparable shipped tickets, and optionally writes the sizing back to Jira |
| Racing Feature Marketing | `/racing-feature-marketing` | Write email and in-app marketing copy for a Racing feature launch — interviews you, generates 2 variants per channel (baseline + creative), then publishes to Confluence under FDR Transformational Work |

## Adding Skills

1. Create a new directory under `skills/` with the skill name (kebab-case).
2. Add a `SKILL.md` file inside it — see existing skills for the format.
3. Open a PR, get it merged, and teammates pull the latest

## Contributing

Contributions are made via the fork-and-pull-request workflow. You don't need write access to this repo — fork it, make your change on a branch, and open a PR.

### 1. Fork the repository

Fork this repo to your own GitHub account (via the **Fork** button on GitHub, or with the GitHub CLI):

```bash
gh repo fork alexsayles/fanduel-racing-skills --clone=false
```

### 2. Set up your remotes

If you already cloned this repo, point `upstream` at the original and `origin` at your fork:

```bash
git remote rename origin upstream
git remote add origin https://github.com/<your-username>/fanduel-racing-skills.git
git remote -v   # confirm: upstream -> alexsayles, origin -> your fork
```

### 3. Create a branch, edit, commit, and push

```bash
git checkout main
git pull upstream main          # sync with the latest changes

git checkout -b my-change       # create a feature branch

# ...make your edits...

git add path/to/your/file
git commit -m "Describe your change"

git push -u origin my-change    # push to your fork
```

### 4. Open a pull request

```bash
gh pr create --repo alexsayles/fanduel-racing-skills \
  --base main \
  --head <your-username>:my-change \
  --title "Describe your change" \
  --body "Explain what changed and why"
```

Then wait for review. Thanks for contributing!.
