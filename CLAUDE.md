# CLAUDE.md — Anthony_Notes

## Project Overview
Anthony_Notes is a personal content-intelligence and self-analysis project covering three of Anthony's public/professional profiles. It is governed by the **AnthonyVA** skill (installable, built via skill-creator) and executes work through three dedicated subagents, one per profile. This project is separate from Portfolio_Project — there is no BI dashboard, DAX, or 4-report structure here.

Primary user: Anthony Chilaka. See `D:\AI Tools\Claude Cowork\About Me\about-me.md` for full profile — read it before every session, per Anthony's universal instructions.

---

## The Three Profiles & Their Subagents

| Profile | Subagent | Method | Purpose |
|---|---|---|---|
| LinkedIn (linkedin.com/in/anthonychilaka) | **LinkedInVA** | Claude in Chrome, human-paced browsing | Analyze top-engagement posts and top-impression comments; build a post calendar from niche/keyword signals; recommend 5 profiles to follow |
| YouTube (@go2stjoseph) | **YoutubeVA** | Claude in Chrome (style review) + YouTube Data connector (stats) | Find best day/time to post from real engagement data; study competitor description/caption style; ask clarifying questions before framing new topics; self-learn Anthony's content style over time |
| Church Instructor | **SpiritualDirectorVA** | Local file research (bookshelf/) + web search as needed | Research topics Anthony assigns, grounded in literature he saves to `profiles/church/bookshelf/` |

Each subagent is a real, isolated Agent tool call — not a persona played in the main session. It reads its brief from `subagent-briefs/`, does its work, and reports back. The AnthonyVA skill (the orchestrator) is the only thing that reads/writes the shared logs — subagents report their findings back to the orchestrator, which then logs them.

---

## Session Start Protocol (run by the AnthonyVA skill)

1. Read `subagent-logs/context-log.md` for the last known state across all three profiles.
2. Ask via AskUserQuestion: **"Which profile do you want to load — LinkedIn, YouTube, Church Instructor, or refresh all?"**
3. Route to the matching brief in `subagent-briefs/` and spawn that subagent via the Agent tool.
4. On return: write findings into the relevant `profiles/` files, append a dated entry to that subagent's log in `subagent-logs/`, and update `context-log.md` + `project-notes.md`.

This project is **recurring and self-updating** — each run appends to the logs rather than overwriting, so patterns can be confirmed/escalated over multiple runs (same pattern as the Freelance Profile project's `niche-patterns.md`).

**Do not schedule LinkedIn/YouTube browsing on an unattended cron job.** Manually trigger each run ("run AnthonyVA") — unattended overnight browsing is more likely to look bot-like, not less.

---

## Folder Map

```
Anthony_Notes/
├── CLAUDE.md                    # this file
├── project-notes.md             # status tracker
├── subagent-briefs/             # one prompt file per subagent (read by AnthonyVA, passed to Agent tool)
├── subagent-logs/                # append-only logs, one per subagent + a master context-log.md
└── profiles/
    ├── linkedin/                 # post-performance.md, comment-performance.md, post-calendar.md, recommended-profiles.md
    ├── youtube/                  # engagement-timing.md, competitor-channel-review.md, content-style-notes.md
    └── church/
        ├── bookshelf/            # Anthony drops literature files here
        └── research-outputs/     # topic write-ups land here
```

---

## Cross-References (read-only, do not copy)
- `D:\AI Tools\Claude Cowork\OUTPUTS\Freelance Profile\knowledge-base\niche-patterns.md`
- `D:\AI Tools\Claude Cowork\OUTPUTS\Freelance Profile\knowledge-base\keyword-tracker.md`

LinkedInVA reads these two files to ground the post calendar in confirmed market signals — it does not duplicate them into this project.

---

## Working Rules
- Never read `OUTPUTS\`, `TEMPLATES\`, or any folder outside this project unless explicitly pointed to a file (per Anthony's universal CLAUDE.md).
- If a brief is unclear, stop and ask via AskUserQuestion — do not fill gaps with invented detail.
- Save all deliverables under this project folder.
- LinkedInVA and YoutubeVA must browse at human pace (read, pause, scroll) — no rapid-fire tool calls — to avoid bot detection.
