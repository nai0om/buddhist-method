# Buddhist Method — a skill for Claude

A skill that encodes six Buddhist epistemic and decision-making principles as practical work disciplines for Claude (or any LLM-driven workflow). Each principle targets a specific failure mode that LLMs routinely exhibit: pattern-matching instead of verifying, patching symptoms instead of removing causes, capitulating under social pressure instead of holding to evidence.

> 🇹🇭 อ่าน [README.th.md](README.th.md) สำหรับเวอร์ชันภาษาไทย

## What's in here

A Claude skill (`SKILL.md` plus `references/`) that gives Claude a checklist for:

| Principle | What it catches |
|-----------|-----------------|
| **Kalāma** (กาลามสูตร) | Stating facts from pattern memory without verifying |
| **Yoniso Manasikāra** (โยนิโสมนสิการ) | Treating symptoms instead of finding root causes |
| **Sati-Sampajañña** (สติ-สัมปชัญญะ) | Acting on stale or remembered state |
| **Anatta** (อนัตตา) | Patching a fundamentally wrong draft instead of rewriting |
| **Pahāna** (ปหานะ) | Workarounds that hide bugs instead of removing them |
| **Upekkhā** (อุเบกขา) | Capitulating under user pressure or thrashing under tool failures |

Plus deeper references for harder situations:
- The **Four Noble Truths** as a debugging frame (`references/ariyasacca-debug.md`)
- **Apāyakosalla** — recognizing decline / anti sunk-cost
- **Appamāda** — heedfulness across long tasks
- **Sappurisadhamma (3 of 7)** — knowing self / time / audience
- **Atthatraya** — short-term vs long-term benefit trade-offs
- **Majjhimā Paṭipadā** — the middle way for solution sizing

## Why keep the Pali / Thai names

The Pali names are kept on purpose. They are mnemonic keys — each name retrieves a complete, well-developed pattern that a paragraph of plain English does not retrieve as cleanly. *Yoniso manasikāra* pulls in the whole discipline of attention to causes; "root cause analysis" loses the framing of attention itself.

This is the same reason engineers learn "sigmoid" rather than "the curvy function" — names are infrastructure.

The skill is **not** a religious framework. It does not require belief, ritual, or commitment to any tradition. It is a checklist with cultural roots, presented honestly. For the principles in their full traditional depth, read the suttas — this skill makes no claim to teach them.

## How to use

### With Claude Code (plugin, recommended)

Run these two commands inside Claude Code:

```
/plugin marketplace add nai0om/buddhist-method
/plugin install buddhist-method@buddhist-method
```

Third-party plugins do not update on their own. To get new versions, run `/plugin`, open **Marketplaces**, pick `buddhist-method`, and choose **Enable auto-update**. Or update by hand with `claude plugin marketplace update buddhist-method` and then `claude plugin update buddhist-method@buddhist-method`.

If you installed the skill earlier with `git clone`, delete `~/.claude/skills/buddhist-method` so it does not load twice. A plugin install has no `~/.claude/skills/buddhist-method/SKILL.md`, so wherever a `CLAUDE.md` points at that path (the manual install below adds one to `~/.claude/CLAUDE.md`, and "Make it always active" shows another), use this pointer instead:

```markdown
## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill
before responding.
```

### With other agents (Codex, Cursor, Gemini CLI, Windsurf, …)

Install with the [Skills CLI](https://github.com/vercel-labs/skills):

```
npx skills add nai0om/buddhist-method
```

Add `-g` to install it for your user instead of the current project, or `-a <agent>` to target one agent.

### Manual install for Claude Code

Paste this prompt into Claude Code — it clones the skill and wires up `~/.claude/CLAUDE.md` in one step:

```
Install the buddhist-method skill:
1. Run: git clone https://github.com/nai0om/buddhist-method ~/.claude/skills/buddhist-method
2. Open ~/.claude/CLAUDE.md (create it if it does not exist) and append:

## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill at
~/.claude/skills/buddhist-method/SKILL.md before responding.
```

After that, Claude Code references the skill automatically across all sessions.

### With other Claude products

Anywhere skills are supported, drop the directory in. The structure is standard (a `SKILL.md` with YAML frontmatter, plus `references/`).

### As a reference for yourself

The `SKILL.md` and `references/` files are readable on their own. Each principle has a **trigger** (when it fires) and an **action** (what to do). You can use them as a personal checklist without involving an LLM.

### Make it always active (optional)

By default, Claude loads the skill on demand — it sees the description and decides whether to read the full `SKILL.md` based on the task at hand. That is fine for most uses, and it keeps your context budget free for everything else.

If you want the skill to be a persistent reminder regardless of task, add a small pointer to your `CLAUDE.md`:

```markdown
## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill at
~/.claude/skills/buddhist-method/SKILL.md before responding.
```

Two places you can put this:

- **Project root `CLAUDE.md`** — applies only when working in that project.
- **`~/.claude/CLAUDE.md`** — applies globally across all your Claude Code sessions.

The pointer is only a few lines, so it doesn't bloat your context. Claude still loads the body of the skill progressively when triggers fire — you are just guaranteeing that the skill stays on Claude's radar.

## Structure

```
buddhist-method/
├── .claude-plugin/
│   ├── plugin.json                       # Claude Code plugin manifest
│   └── marketplace.json                  # lets /plugin marketplace add find it
├── SKILL.md                              # six core principles + dispatch
├── README.md                             # this file
├── README.th.md                          # Thai version
├── LICENSE                               # MIT
└── references/
    ├── ariyasacca-debug.md               # Four Noble Truths as debug frame
    └── extended-principles.md            # five secondary principles
```

## License

MIT. Use, modify, and redistribute freely. See [LICENSE](LICENSE).

## Contributing

Issues and pull requests welcome. Particularly interested in:
- Failure modes the current principles don't catch.
- Better triggers (more specific situations that should fire each principle).
- Translations into other languages where the source tradition is alive.

If proposing a new principle, please show:
1. The specific failure mode it catches.
2. A concrete trigger and action.
3. Why an existing principle doesn't already cover it.

The bar is keeping the skill tight. New principles are easy to add; what's hard is keeping the set small enough to actually be used.
