---
layout: post
title: "Hour Registration AI Automation Flow"
description: "How I automade my entire billing cycle with a Claude Code plugin that reads my calendar, submits hours, downloads timesheets, and emails work slips."
category: AI Workflow Automations
image: /assets/images/tiger-clock.jpg
---

<p class="post-tags">
    <span class="tag">Claude Code</span>
    <span class="tag">Claude Marketplace</span>  
    <span class="tag">Google Calendar</span>
    <span class="tag">Human in the loop</span>
</p>

Logging working hours feels trivial — until you notice how often it interrupts your flow, breaks concentration, and quietly eats away at your attention. And a couple of hours every year, too.

> The real cost of manual hour logging isn't the 5 minutes it takes. It's the context switch at the end of every week, the moment you have to mentally reconstruct what you did and when.

So I built a **Claude Code Hour Registration Plugin** that automates the entire billing cycle. Two scheduled commands handle everything.

---

### What it does

**Weekly command** — runs every Monday morning:
- Reads my Google Calendar for the previous week 📅
- Submits hours to both the client portal and employer portal automatically

**Monthly command** — runs on the first of each month:
- Downloads timesheets from the portals
- Fetches my NS (Dutch rail) travel history
- Emails compiled work slips to the administration ✉️

> No spreadsheets. No portal logins. No reconstructing your week from memory on a Friday afternoon.

The whole thing is open source and fully customizable — swap in your own clients and portals through a single config file.

---

### What I learned building it entirely with Claude agents

#### 1. Rules are your context layer

Claude rules let you define your context once and reuse it across commands and skills. Including a **personality file** — so generated drafts and summaries actually sound like you, not like a generic assistant writing on your behalf. 💁🏻‍♀️

#### 2. Worktrees make experimentation fearless

Worktrees let you iterate freely on a separate branch, refine until it feels right, and merge when ready — without any risk of breaking your main setup. For plugin development where you're testing against real APIs and real data, this is invaluable.

#### 3. Agents shift the nature of the work

> The challenge stops being "how do I implement this?" and starts being "what exactly do I want to build?"

That's a meaningful shift. When the implementation friction disappears, you spend your energy on product thinking — on defining the right behavior — rather than on wiring up code. 🔨

#### 4. The gap between local and hosted

I'd happily run this entirely in Claude's hosted environment. But connector support for the specific portals I use isn't there yet ☁️ — so a local **launchd** job fills the gap for now. When the ecosystem catches up, migrating will be a config change, not a rewrite.

---

### Try it

The plugin is open source and fully customizable. One config file controls your clients, portals, and schedules. [Check it out →](https://github.com/sunnyStefi/stefania-marketplace/blob/main/hour-registration/README.md) ⚡

![Tiger eating a clock](/assets/images/tiger-clock.jpg)
