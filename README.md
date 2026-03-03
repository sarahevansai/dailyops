# Daily Ops Digest Kit for Claude Cowork

**Turn scattered Slack threads, emails, and Monday.com updates into a single, beautiful status email — twice a day.**

Claude Cowork cross-references your Slack channel, Gmail inbox, and Monday.com boards, then produces a formatted HTML digest with color-coded name badges, urgency-sorted sections, and action tables with deadlines. It delivers as a Gmail draft you send to your Slack channel's email address.

![License](https://img.shields.io/badge/license-MIT-blue)
![Platform](https://img.shields.io/badge/platform-Claude%20Cowork-blueviolet)

---

## What It Looks Like

### TL;DR Dashboard
A summary table at the top, sorted by urgency, with tinted rows so you can scan the whole project in seconds:

```
⚠️  Globex Corp     Draft in client review (Thu 3/6); client flagged tone concerns
🟡  Initech         Outline approved; waiting on SME interview scheduling
🟢  Umbrella Inc    All approvals in; writing underway
⏸️  Stark Ltd       On hold — contract renewal pending
```

### Color-Coded Name Badges
Every action item is tagged with a colored badge so team members instantly spot their tasks:

```
[ALEX]  Review Casey's tone revision before resending       Wed EOD
[JORDAN]  Follow up with client on full draft review        Thu 3/6
[CASEY]  Revise draft intro to soften technical language     Today
```

### Per-Client Sections
Each client gets its own section with a colored left border indicating urgency (orange = needs attention, yellow = in progress, green = on track, red = critical, gray = on hold), a status summary, completed items, and an action table.

> Open `example-output.html` in a browser to see the full rendered format.

---

## What's in the Kit

```
daily-ops-digest-kit/
├── README.md                    # This file
├── config.md                    # ⬅️ START HERE — your project settings
├── morning-update-prompt.md     # Full daily snapshot prompt
├── afternoon-update-prompt.md   # Changes-only midday prompt
└── example-output.html          # Sample output — open in browser to preview
```

---

## Quick Start

### 1. Fill in `config.md`

This is your single source of truth. Replace the placeholders with:

- Your Slack channel name, ID, and email address
- Your client/project list with key links
- Your team members, roles, and badge colors
- Your workflow dependency gates
- Your reference links (boards, docs, drives)

### 2. Connect Your Tools

In Claude Cowork, make sure these connectors are enabled:

- **Gmail** — reads inbox/sent, creates drafts
- **Slack** — reads your ops channel and threads

### 3. Get Your Slack Channel Email

Your Slack channel has an email address that lets you post formatted HTML emails directly into it:

1. Open your Slack channel
2. Click the channel name → **Integrations**
3. Copy the address under **Send emails to this channel**
4. Paste it into `config.md`

### 4. Run It

Start a new Claude Cowork session and paste:

> The contents of `morning-update-prompt.md` + your filled-in `config.md`

Claude will scan your sources, cross-reference everything, and create a Gmail draft. You hit send.

For the afternoon update, paste `afternoon-update-prompt.md` + `config.md` instead.

---

## How It Works

```
┌─────────────┐   ┌──────────────┐   ┌──────────────────┐
│  Slack       │   │  Gmail       │   │  Monday.com      │
│  Channel     │   │  Inbox/Sent  │   │  Notifications   │
└──────┬───────┘   └──────┬───────┘   └────────┬─────────┘
       │                  │                     │
       └──────────┬───────┴─────────────────────┘
                  │
         ┌────────▼────────┐
         │  Claude Cowork  │
         │  Cross-Reference│
         │  + Format       │
         └────────┬────────┘
                  │
         ┌────────▼────────┐
         │  Gmail Draft    │
         │  (HTML email)   │
         └────────┬────────┘
                  │
         ┌────────▼────────┐
         │  Slack Channel  │
         │  (via email)    │
         └─────────────────┘
```

**Morning update** (full snapshot): Every client, every status, every action item. Start-of-day alignment for the whole team.

**Afternoon update** (changes only): What moved since morning. Escalates missed deadlines and flags unanswered client emails.

---

## Customization

### Team Members

Edit the `TEAM` section in `config.md`. Each person gets a name, role, and hex color.

Available badge colors (high contrast on white backgrounds):

| Color | Hex | Preview |
|-------|-----|---------|
| Purple | `#7c3aed` | Owner / Lead |
| Blue | `#2563eb` | PM / Coordinator |
| Teal | `#0d9488` | SEO / Analytics |
| Orange | `#ea580c` | Editorial / Creative |
| Sky | `#0284c7` | Operations |
| Pink | `#db2777` | Editorial |
| Gray | `#737373` | Support / Writer |
| Red | `#dc2626` | Urgent / Executive |
| Gold | `#ca8a04` | Finance / Strategy |
| Emerald | `#059669` | Success / Growth |

### Clients / Projects

Add or remove rows in the `CLIENTS` section. Each client needs a name and key links.

### Workflow Gates

The `WORKFLOW_GATES` section defines your dependency chain. Claude will never assign a downstream task if the upstream step isn't done. Customize this to match your actual process.

### Urgency Levels

| Emoji | Color | Border | Row Background | When to Use |
|-------|-------|--------|----------------|-------------|
| ⚠️ | Orange | `#f59e0b` | `#fff4e5` | Deadline within 48 hrs, unanswered email, blocker |
| 🔴 | Red | `#dc2626` | `#fee2e2` | Terminated, contract at risk, major blocker |
| 🟡 | Yellow | `#eab308` | `#fef9c3` | Waiting on client, work underway |
| 🟢 | Green | `#16a34a` | `#dcfce7` | Approvals received, moving forward |
| ⏸️ | Gray | `#9ca3af` | `#f3f4f6` | Paused, not active |

### Delivery Method

Default: Gmail draft → Slack channel email. You can also:
- Post directly to Slack (if channel is not externally shared / Slack Connect)
- Email to a distribution list
- Adjust subject line format in `config.md`

---

## Use Cases

This kit was built for client services ops, but it works for any team that needs daily cross-source status updates:

- **Agency client management** — track deliverables across multiple clients
- **Product launches** — monitor workstreams across engineering, design, marketing
- **Event planning** — coordinate vendors, venues, timelines across teams
- **Consulting engagements** — keep multiple project teams aligned
- **Editorial operations** — track articles, reviews, and publication pipelines

---

## Requirements

- [Claude Cowork](https://claude.ai) (desktop app) with Gmail and Slack connectors
- A Slack channel with an email address enabled
- Gmail account with access to the relevant inbox

---

## Tips

- **Slack is king.** In most teams, Slack messages are more current than project boards. The prompts prioritize Slack data when sources conflict.
- **Client emails matter.** Claude flags emails unanswered for 48+ hours. This catches things before they escalate.
- **The color badges are the secret weapon.** People instantly spot their name and know what's theirs without reading the whole update.
- **Urgency ordering works.** Critical items first means the team sees what matters immediately.
- **Start with morning only.** Get comfortable with the full snapshot before adding the afternoon changes-only update.

---

## License

MIT — use it however you want.

---

## Credits

Built by [Sarah Evans](https://twitter.com/PRsarahevans) / [Zen Media](https://zenmedia.com). Powered by [Claude Cowork](https://claude.ai).
