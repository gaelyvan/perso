# CLAUDE.md

This file provides guidance to Claude Code when working in this Obsidian vault.

## Overview

This is Gael's personal vault for managing ideas, personal projects, notes, articles, and tasks.

## About Gael

Sound engineer and software developer with over 30 years of experience, primarily coding in **C++** and **Python**. Works on real-time multimedia projects and cross-platform frameworks (macOS, Linux, Windows). Favors **simplicity over complexity** and **quality over quantity**.

## The 10 Commandments

Philosophy summed up in the phrase **"Legal Beautiful KISS"**:

### 1. Legal
Crime doesn't pay! Do things right from the start. Don't be lazy, don't procrastinate. When you think "this isn't great, but I'll do better later" — make the effort and do it better right now. Otherwise, problems come back like a boomerang. Never sweep anything under the rug.

### 2. Beautiful
Make it beautiful! Beauty is a guarantee of quality. Paying attention to aesthetics forces you to refine and focus on the essentials. Ugly, poorly written code is likely buggy — and there's no reason to be proud of it. So be proud and make it beautiful.

### 3. KISS
Keep It Super Simple. Simplicity should always be the first choice. If not for yourself, do it for others who will read or maintain your work. That person could be you in a few years, and you'll be glad you kept it simple. Complexity is never a sign of intelligence.

### 4. Test everything
If it's not tested, it doesn't work!

### 5. Be explicit
Write code clearly and explicitly. Code should require little or no documentation.

### 6. But also document
Document what needs to be documented. Always favor a good diagram over a long speech. Integrate diagrams into source code (ASCII format when possible).

### 7. Use debugger
Debug rather than trace with printf.

### 8. KEEP learning
Take time to train yourself and learn new things.

### 9. Use your own products
Spend time using the products you create. Make at least one production per year to understand the issues, problems, and qualities firsthand.

### 10. Enjoy what you do

## The Zen of Python (Complementary Philosophy)

```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

## Vault Structure

```
Perso/
├── Daily/                    # Daily task files, archived monthly
│   └── YYYY-MM/              # Monthly archive folders
│       └── YYYY-MM-DD.md
├── Tasks/                    # Task management (hybrid structure)
│   ├── backlog.md            # INDEX: one-liner tasks by priority
│   └── [task-name].md        # DETAIL: breakdown for #L tasks
├── Notes/                    # Individual note files
│   └── YYYY-MM-DD_topic.md
├── Ideas/                    # Ideas for later exploration
│   └── YYYY-MM-DD_idea-title.md
├── Articles/                 # Articles in progress
└── todos.md                  # Quick todos catch-all
```

---

## Task Management System

### Quick Commands

| Command | Action |
|---------|--------|
| `daily` | Create today's daily file with calendar, tasks by priority, pending items |
| `wrap the day` | Archive completed tasks, summarize day, calculate time stats, carry forward incomplete |
| `take a note: [text]` | Create `Notes/YYYY-MM-DD_topic.md` with formatted content |
| `new task: [text]` | Add to backlog index; create detail file for #L tasks |
| `task today: [text]` | Add task directly to today's daily file (prompt for Q1/Q2/Q3) |
| `new idea: [text]` | Create `Ideas/YYYY-MM-DD_idea-title.md` |
| `todo: [text]` | Quick add to `todos.md` |
| `start: [task]` | Start working on a task, log start time |
| `pause` | Pause current task, log time spent |
| `stop` | Stop current task, log time spent, mark complete |
| `monthly stats` | Generate time and task statistics for current month |
| `update guides` | Should we update any CLAUDE.md files based on what you learned in this session? |

### Eisenhower Matrix (Priority System)

| Priority | Tag | Description | Action |
|----------|-----|-------------|--------|
| **Q1** | `#Q1` | Urgent + Important | Do immediately |
| **Q2** | `#Q2` | Important, Not Urgent | **Target 20%+ of time** |
| **Q3** | `#Q3` | Urgent, Not Important | Batch or delegate |
| **Q4** | `#Q4` | Not Urgent, Not Important | Should be deleted |
| **Q5** | `#Q5` | "If God Exists" | Weekly review only |

**Note:** Q5 items do not appear in daily view, only during weekly review.

### Effort Estimation

| Size | Tag | Typical Duration |
|------|-----|------------------|
| Small | `#S` | < 1 hour |
| Medium | `#M` | 1-4 hours |
| Large | `#L` | > 4 hours (consider breaking down) |

### Obsidian Tasks Compatibility

Tasks use [Obsidian Tasks plugin](https://publish.obsidian.md/tasks) emoji format:

| Field | Emoji | Example |
|-------|-------|---------|
| Due date | 📅 | `📅 2025-01-15` |
| Scheduled | ⏳ | `⏳ 2025-01-10` |
| Start date | 🛫 | `🛫 2025-01-05` |
| High priority | ⏫ | (Q1 tasks) |
| Medium priority | 🔼 | (Q2 tasks) |
| Low priority | 🔽 | (Q3, Q4, Q5 tasks) |
| Done date | ✅ | `✅ 2025-01-15` |
| Recurrence | 🔁 | `🔁 every week` |

**Task format:** `- [ ] Task description #M 📅 2025-01-15 ⏫`

### GitHub Integration

Development tasks are tracked using **GitHub Issues** and **GitHub Projects**.

**Configuration:**
- **Source paths:**
  - `/Users/gael/Sources/pactole` - Personal finance management tool
- **GitHub username:** gaelyvan

#### Source Code Scanning

**Exclude folders:**
- 3rdParts, build, Build, Archives
- .git, cmake-, cmake_*, venv*, node_modules

**Filter:** Only TODOs assigned to @gael or unassigned

### External Sources

When configured, `daily` pulls tasks from:

| Source | Method | Status |
|--------|--------|--------|
| Source Code | Grep `TODO`, `FIXME` assigned to @gael or unassigned | Pending config |
| GitHub Issues | GitHub CLI (`gh`) integration | Pending config |
| Calendar | macOS Calendar | Pending config |

### Daily File Template

```markdown
# Daily - YYYY-MM-DD (Weekday)

## Calendar
- 09:00 - Event

## Tasks

### Q1 - Urgent & Important ⏫
- [ ] Task description #S 📅 2025-01-15 ⏫

### Q2 - Important, Not Urgent (20%+ target) 🔼
- [ ] Task description #M 🔼

### Q3 - Not Urgent, Not Important 🔽
- [ ] Task description #S 🔽

## Currently Working On
> **Task:** None
> **Started:** --:--

## Time Log
| Task | Start | End | Duration |
|------|-------|-----|----------|

## Quick Notes
-

## End of Day
### Completed
-

### Carry Forward
-

### Time Stats
- **Total tracked:** 0h
- **Q1:** 0h | **Q2:** 0h | **Q3:** 0h
- **Q2 ratio:** 0%

### Summary
_Brief reflection_
```

### Note Template

```markdown
# [Title]

**Date:** YYYY-MM-DD
**Tags:** #note #topic

## Content

[Formatted content]

## Related
- [[links]]
```

### Backlog Structure (Hybrid Approach)

The backlog uses a **hybrid structure** to stay scannable while supporting detailed task breakdowns:

| Location | Content | When to Use |
|----------|---------|-------------|
| `backlog.md` | One-liner index with priority, size, due date, link | All tasks |
| `Tasks/[task-name].md` | Full breakdown: phases, subtasks, notes, references | #L (Large) tasks |

**Backlog entry format:**
```markdown
- [ ] Task Title #L 📅 2025-01-15 ⏫ → [[task-file-name]]
```

**Task detail file template** (`Tasks/[task-name].md`):
```markdown
# [Task Title]

**Priority:** Q1/Q2/Q3/Q4/Q5
**Size:** #S / #M / #L
**Due:** YYYY-MM-DD
**Project:** [name]
**Source:** GitHub/Code/Manual

---

## Phase 1: [Name]
- [ ] Step 1
- [ ] Step 2

## Phase 2: [Name]
- [ ] Step 3

## Notes
_Document decisions and progress here_
```

**Rules:**
- Small tasks (#S) stay inline in backlog.md
- Large tasks (#L) get their own file with detailed breakdown
- Medium tasks (#M) use judgment - complex ones get a file
- Moving tasks between priorities only requires editing backlog.md

### Idea Template

```markdown
# [Idea Title]

**Date:** YYYY-MM-DD
**Tags:** #idea #domain
**Status:** raw / exploring / validated / archived

## The Idea
[2-3 sentences]

## Why It Matters
[Problem/value]

## First Steps
1.
2.
```

### todos.md Structure

```markdown
# Quick Todos

Uncategorized items. Review weekly.

## Inbox
- [ ] YYYY-MM-DD: Item description

## Done (clear monthly)
- [x] YYYY-MM-DD: Completed item
```

### Weekly Review Checklist

1. Review `todos.md` inbox - categorize or delete
2. Review Q4 and Q5 items - still relevant?
3. Check backlog - any items ready to schedule?
4. Verify 20% Q2 time was achieved
5. Archive previous month's daily files if new month

---

## Working with This Vault

- Files are Markdown formatted for Obsidian
- Links use Obsidian's `[[wikilink]]` syntax
- Prefer straightforward, simple solutions
- When in doubt, refer to the 10 Commandments above
