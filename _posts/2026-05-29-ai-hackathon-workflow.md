---
layout: post
title: "AI Hackathon Aftermath: My 6h hackathon agentic Workflow"
description: "With 6 hours and my Claude subscription I had to ship a retro game from scratch. Here is exactly what I learned and my AI workflow."
category: Agentic Engineering
image: /assets/images/ultracode.png
---

### The Nostalgic Specs

Once a month, our team at [Sourcelabs](https://sourcelabs.nl/) sets aside a full day to learn something new.

This time we needed to draw a game from big classics like Simon the Sorcerer, Command and Conquer, Doom, Jazz Jackrabbit, and Duke Nukem. 
Retro-styled, stylish, with music and sound effects, fun, educational, and with a personal touch.

The tech constraints were minimal: host it in a browser, no backend, local storage only. It sounded like the recipe for a fun day!

[See what I built](https://sunnystefi.github.io/grand-hotel/) — then read on for the adventure I lived behind it.

--- 

### Step 1: Ultracode Planning

I decided to dedicate the first full hour to the **system planning** and to give Opus 4.8's ultracode mode a try. 
It combines high reasoning effort with automatic agentic workflow orchestration.

I did so because I'm convinced that nailing the planning is half of the work and fixing a bad plan always costs more than investing time in building a solid one upfront.

This is what I gave it:
- the requirements
- my preferences, style, and observations
- the core principles that make those retro games immortal
- my time constraint - I had 2 hours to develop it

Ultracode burned through more than 10% of my daily token budget in a single session — around 10 minutes.

A lot of time, but the output was a [proper design document](https://github.com/sunnyStefi/grand-hotel/blob/main/docs/grand-hotel-math-maze.md)
with a clear creative direction, core mechanics, and a personality for the game.

I reviewed it by going back and forth with Claude in plan mode — using `openspec explore` to ask questions and refine the document.

Then I drafted the remaining specs with [openspec new and continue](https://github.com/Fission-AI/OpenSpec/blob/main/docs/commands.md) and kicked off a full implementation run.

---

### Step 2: Linear vs Parallel Agent Loops - The honest answer

For the implementation I decided to downgrade from Opus to Sonnet to save tokens, during a phase that is mostly about translating a clear spec into code. 

Sonnet took roughly **27 minutes** to implement the `task.md` file and produce the initial game.

> That was me realizing that spawning a team of agents could have saved me tokens, time, and improved the quality of the output.

One big challenge with **agent parallelization** is that you typically want to _stay in the loop_ so you can steer the agents based on the outputs they produce.

As I saw the game taking shape, I kept a running list of _follow-up prompts_. Each one was ready to send the moment the previous change was confirmed working. 
This meant I was never sitting idle — always checking results or drafting the next prompt.

For code changes I kept the workflow very simple:
- `git push` if the result was good enough to keep
- `git stash` if the change did not work and I needed to reset fast

Clearing the context between every change and sticking to this stash-push rhythm was the single biggest thing that kept me moving fast. 

That said, I was still just using two Claude instances in a staggered pipeline, not true parallelization.

![Staggered agent loop: the human steers two Claude instances between each iteration](/assets/images/agent-loop.png)

I applied the same principle (human in the loop for anything that requires taste) to the main background music 🎶. I trimmed the design document down to 3k characters, fed it to [Suno](https://suno.com) as a style prompt, and refined from there.
Five minutes of prompting produced a custom chiptune track that actually fits the game's mood.

No agent could have made that call for me. Knowing *when* to hand creative decisions back to yourself is part of the workflow too.

Parallelization works best when _you are the bottleneck_: you don’t want to sit idle, but instead continuously steer agents between interactions 🌼.

> "Technically correct" and "actually fun" are two different things, and a machine can't tell them apart — it never lives through the product it's building.

### Takeaways

What I learned from this experience: 

- **Parallelize** when tasks are clearly independent and there is nothing yet to break
- **Stay sequential** when each result shapes the next prompt: anything where you have to experience the output before choosing your next move.

For me, it was a genuinely fun adventure 🏝. Treating Claude as an integrated part of my workflow, not just an efficient machine is what kept me fully engaged the whole way through.

![sourcelabs-hackathon.jpeg](/assets/images/sourcelabs-hackathon.jpeg)
