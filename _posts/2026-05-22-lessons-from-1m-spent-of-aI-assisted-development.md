---
layout: post
title: "Lessons Learned from $1M spent of AI-Assisted Development"
description: "I explored Steinberger's recent agentic engineering projects and what it emerges it's a clear shift from implementaion to design agentic environments."
category: AI Workflow Automations
image: /assets/images/ste-coding-01.jpg
---

<p class="post-tags">
  <span class="tag">Inspiration</span>
  <span class="tag">Agentic engineering</span>
  <span class="tag">Human in the loop</span>
</p>

A few days ago, I came across [this tweet about Peter Steinberger's work at OpenAI](https://x.com/steipete/status/2055346265869721905/photo/1) and found myself asking an uncomfortable question:

> Why does my developer experience feel so different, and what value am I actually delivering now that machines handle a large part of the work?

I spent some time reasoning with Opus and Grok, and I reverse engineered [Peter Steinberger's](https://github.com/steipete) 2025-26 projects (not OpenClaw related) to understand the mindset behind his output.

---
### Mindset

Peter focuses on **agentic engineering**, **tight human–AI feedback loops**, and systematically **eliminating friction** in high-speed development workflows. His tools are clearly designed for power users who operate inside agent environments all day.

The tradeoff is that this strong bias for speed and autonomy often comes at the expense of robust security boundaries.

> The speed of shipping is the speed of learning.  🍃

Another clear preference is **CLI-first design over GUI or MCP-heavy interfaces**, mainly to reduce token overhead and improve composability. Looking across the repos, a few pattern emerge:

---
### Agent Perception

One important thing I realized is that agents are no longer primarily constrained by model intelligence, but by what they can **perceive** and reliably **act on** in real environments.

- **[Peekaboo MCP](https://github.com/steipete/Peekaboo)**: the agents can capture screenshots of the environment
- **[AXorcist](https://github.com/steipete/AXorcist)**: exposes macOS accessibility APIs so agents can click UI elements, fill forms, and traverse apps via accessibility trees.
- **[oracle](https://github.com/steipete/oracle)**: routes complex decisions to stronger models with full context, reducing human intervention.
- **[fluegel](https://github.com/steipete/fluegel)**: a privilege broker that grants temporary elevated permissions
- **[sweetlink](https://github.com/steipete/sweetlink)**: uses existing authenticated browser sessions instead of headless automation
- **[canvas](https://github.com/steipete/canvas)**: a controlled browser environment owned by the agent

--- 

### Monitoring

I hadn’t considered that dashboards are essentially another attention sink. Once agents are running continuously in the background, traditional dashboards become just another stream of noise competing for your focus. These menu bar tools replace them with always-on, **glanceable signals** that answer cost, failure, and execution state without a context switch.

- **[CodexBar](https://github.com/steipete/CodexBar)**: a macOS menu bar tool that surfaces real-time usage stats, limits, resets, credits, and costs across multiple AI coding providers.
- **[RepoBar](https://github.com/steipete/RepoBar)**: shows GitHub repo state directly in the menu bar, reducing context switching.
- **[ReleaseBar](https://github.com/steipete/ReleaseBar)**: tracks dependency freshness across OSS projects.
- **[BlackBar](https://github.com/steipete/BlackBar)**: displays CI status in real time.
- **[Trimmy](https://github.com/steipete/Trimmy)**: converts multiline shell snippets into single-line, paste-ready commands.

---

### CLI Utilities

For Peter, CLI it's the primary interface that makes his tools *composable* by machines. It can be scheduled via cron, composed through pipes, and executed by agents directly. A GUI cannot.

- [`gogcli`](https://github.com/steipete/gogcli), [`wacli`](https://github.com/steipete/wacli), [`remondctl`](https://github.com/steipete/remondctl), [`metcli`](https://github.com/steipete/metcli) : terminal-first access to Google services, WhatsApp, Apple Reminders, and Messages
- Home automation tools: [`blucli`](https://github.com/steipete/blucli), [`camsnap`](https://github.com/steipete/camsnap), [`sonoscli`](https://github.com/steipete/sonoscli), [`spogo`](https://github.com/steipete/spogo), [`ordercli`](https://github.com/steipete/ordercli), [`eightctl`](https://github.com/steipete/eightctl)
- Distribution: [`homebrew-tap`](https://github.com/steipete/homebrew-tap), a personal Homebrew repo for CLIs fast installation

---

### Local Archives

Personal data that lives inside apps is invisible to agents, and most of our data lives inside apps. The intent behind these tools is to make personal data _queryable by agents by default_, by reframing applications as continuously harvested data sources, normalized and made locally accessible.

- [`birdclaw`](https://github.com/steipete/birdclaw), [`wacrawl`](https://github.com/steipete/wacrawl), [`slacrawl`](https://github.com/steipete/slacrawl), [`telecrawl`](https://github.com/steipete/telecrawl): archive X, WhatsApp, Slack, Telegram, Notion data into SQLite/Markdown
- [`sweet-cookie`](https://github.com/steipete/sweet-cookie): browser cookie extraction for agent to authenticate without extensions

---
### Reimplement the 10% That Matters

When an official tool is slow, web-bound, login-gated, or missing a key capability, the solution he founds is to *extract the essential 10%* and reimplement it as a lightweight native tool.

- [`summarize`](https://github.com/steipete/summarize): extracts content from URLs, PDFs, podcasts, videos.
- [`VibeTunnel`](https://github.com/steipete/VibeTunnel): browser-based access to a local terminal.
- [`Poltergeist`](https://github.com/steipete/poltergeist): hot reload + file watching.
- [`sag`](https://github.com/steipete/sag): voice synthesis CLI.
- [`tmuxwatch`](https://github.com/steipete/tmuxwatch): TUI for tmux sessions.
- [`osc-progress`](https://github.com/steipete/osc-progress), [`Swiftdansi`](https://github.com/steipete/Swiftdansi): terminal UX improvements.

The workflow itself is also a deliverable: **[`agent-scripts`](https://github.com/steipete/agent-scripts)** is a living archive of the rules he gives agents, the scripts he chains, and the editor setup.

---
### Takeaway: Build Environments for Agents

From this categorization, we can clearly see that these systems compose an *agent-centric environment* where they are able to see the screen, authenticate to services, query personal data, route decisions, and report status without ever forcing the user to switch context.

The value is no longer in implementation. It’s in the *design* of the places agents can act on and eliminating everything that slows the human-machine feedback loop down. 🌟


![ste-coding-01.jpg](/assets/images/ste-coding-01.jpg)
