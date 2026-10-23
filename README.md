# Dev Mentor

A Claude Skill that acts like a mentor pairing with you, not a tool you dump your tickets into. It works tickets with you — hints before answers on the parts worth struggling through, straight talk the moment something's actually wrong, and a memory of what you're still working on so it gets more useful the longer you use it.

## What is this Skill?

Dev Mentor changes how Claude behaves when you bring it a ticket. Instead of reading the ticket and handing back a finished diff, it calibrates: asks what type of ticket this is and how much pressure you're under, then decides how much to hold back versus hand over. Bug fixes get a hint ladder instead of an instant answer. Pattern-copy features get out of the way. Spikes get a nudge to write down what was learned before it's forgotten. Every ticket ends with a PR review that's direct about real defects and Socratic about judgment calls, closing with the one or two things most worth remembering — which is also what the skill quietly learns about you over time.

There's always an escape hatch. Say the word and it drops straight into "just solve it" mode, no questions asked.

## The Problem

In ["The Slow and Quiet Cognitive Atrophy of a Modern Software Engineer"](https://dev.to/codingwithjiro/the-slow-and-quiet-cognitive-atrophy-of-a-modern-software-engineer-3lbh), Elmar Chavez names a workflow a lot of developers will recognize: prompt, accept, repeat — with no review step in between. Each individual shortcut feels harmless. Taken together, over months, they quietly erode the ability to work without the tool.

A few things from that piece (and the discussion under it) shaped this skill directly:

- The habit worth protecting isn't typing syntax — it's **forming and revising a mental model of the system**: hypothesizing why something's broken, predicting what a change might affect, before you see the AI's answer.
- Skipped review doesn't stay contained. One commenter described it as a **domino effect** — a junior trusts the AI, a senior trusts the junior, and unreviewed code reaches production with nobody who can actually explain it.
- The fix isn't abandoning AI. It's using it as a **complement, not a substitute** — delegating the mechanical and mundane while staying the one who can own, explain, and fix what gets shipped.

This tracks with the (still young, still mixed) research on "cognitive offloading" more broadly: effects seem to depend heavily on *how* AI gets used — passive accept-and-move-on looks the riskiest, while deliberate, structured use looks protective — and the clearest evidence so far comes from domains like medicine, where skills visibly dull within months of leaning on an assistant.

## The Solution

Dev Mentor tries to keep the parts of engineering that AI makes easy to skip in the loop, without turning every ticket into homework:

- **Type-calibrated friction** — a hint ladder for bug fixes, hands-off help for pattern-copy features, predict-before-reveal for genuinely new features, findings-capture for spikes. The friction goes where the skill actually lives, not everywhere evenly.
- **Pressure-aware, not pressure-blind** — you set Light / Medium / Hard at the start of each ticket, and a kill-switch phrase overrides it instantly if a "medium" ticket turns into a crunch.
- **PR review with teaching** — direct about actual defects, Socratic about design decisions, and closing with explicit learning points instead of a generic "LGTM."
- **A memory that's actually yours** — a plain, human-readable profile file (`~/.claude/mentor-profile.md`) that tracks your stable goals once and your active growth areas as they're observed, decaying entries that you've since gotten clean on rather than holding them against you forever.
- **Quiz me** — a knowledge check pulled from your own recent growth areas, not generic trivia.
- **Documentation-grounded learnings** — when a learning point is actually about framework or library behavior, the skill links the specific official doc section (short quote, clearly marked, full explanation in its own words) instead of asking you to take its word for it.

## Installation

Dev Mentor is a single skill: one `SKILL.md` file.

### Personal (available in every project)

```bash
mkdir -p ~/.claude/skills/dev-mentor
cp SKILL.md ~/.claude/skills/dev-mentor/SKILL.md
```

### Project only (commit it so your team gets it too)

```bash
mkdir -p .claude/skills/dev-mentor
cp SKILL.md .claude/skills/dev-mentor/SKILL.md
```

Restart Claude Code (or start a new session) afterward — skills are picked up at session start. Since the mentor profile lives at `~/.claude/mentor-profile.md` regardless of install scope, your growth areas and goals follow you across every project either way.

### Uninstall

```bash
rm -rf ~/.claude/skills/dev-mentor
# optionally, to also forget what it's learned about you:
rm ~/.claude/mentor-profile.md
```

## Usage

Once installed, just bring it a ticket:

```
"Starting TICKET-482, it's a bug fix. Here's the description: [paste]"
→ Asks your pressure level, then works the hint ladder with you instead of
  handing over a fix outright.

"PR's up for TICKET-482, can you review it?"
→ Reviews directly for real issues, asks about the judgment calls, and closes
  with the learning points from this ticket.

"Quiz me"
→ Pulls a question from something you've actually struggled with recently,
  not a random trivia question.

"Just solve it, I don't have time for this right now"
→ Drops all friction immediately and helps directly, no hint ladder, no
  follow-up questions.
```

## Why This Matters

This skill doesn't ship with invented success metrics — it's a v1, and the honest answer is that whether it works is something you'll find out by using it. What it's built around is a fairly simple bet: the parts of engineering that make you better at engineering are also the parts AI makes easiest to skip, and a mentor who notices that — without getting in the way of the work that doesn't need it — is worth more over a career than a tool that just finishes tickets faster.

## Contributing

This is a personal skill, still being shaped through use. If you fork it and land on an improvement — a better hint-ladder pattern, a cleaner profile format, a mode this version is missing — issues and PRs are welcome.

## License

MIT License — use this however you want.

---

*Built after reading too many articles about AI and cognitive atrophy, and deciding to do something about it instead of just worrying.*
