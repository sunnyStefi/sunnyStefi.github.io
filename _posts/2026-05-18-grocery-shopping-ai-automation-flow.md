---
layout: post
title: "Grocery Shopping AI Automation Flow"
description: "A one-command grocery automation built with Claude Desktop, and why I still keep myself in the loop for the final step."
category: AI Workflow Automations
image: /assets/images/order-buy.jpg
---

<p class="post-tags">
  <span class="tag">Claude Desktop</span>
  <span class="tag">Playwright MCP</span>
  <span class="tag">Human in the loop</span>
</p>

### Why bother automating a recurring trivial task

"It only takes a few minutes" is the most expensive sentence in modern life. Online grocery shopping sounds simple, but it really adds friction to your life. 
What I gain from automating this flow:

1. **Mental overhead**: it frees up attention for work/rest that actually matters.
2. **Health & spending**: fewer impulse buys, more of the things you actually are meant to eat.
3. **Consistency**: a predictable routine show patterns in your own behavior and it's easier to adjust.

Before this, every order meant a weelky review of _multiple lists_ (more than 100 items), manually checking stock, and picking replacements when items were out.
This means double-checking more than 6 thousands items per year. Sit with that for a second.

When Monday afternoon rolls around, my picked grocery shopping time, I genuinely dread every second of it.

Since we have a tool that can lift all that mental clutter, why not use it?

---

### The initial setup

A couple of years ago I reorganized my entire grocery list into four categories: weekly, bi-weekly, monthly, and quarterly. 
Each category has its own pre-configured shopping list on the supermarket's website.

I usually place the order on **Monday** and schedule delivery for **Thursday**, so the cleaning lady can receive everything and put it away while I keep working from home.

---

### The full workflow

Now the whole process runs as a single scheduled job: **Claude Desktop Scheduled Tasks** driving a **Playwright MCP server**. 
No database stock, no external state management. Only one prompt.

The goal was to build a **ready-to-confirm** cart.

The `order-grocery` task fires every **Monday at 10:00** .

**1. Log in (Playwright MCP)**

- Open `https://www.GROCERY_SHOP.com` and fetch credentials from a local config file

> 🎩 **TIP** Claude Desktop runs in a sandbox — it can't read from the system keychain or environment variables, so credentials live in a local file.
> Using Claude Code would solve the issue (adding keychain credentials or encrypted env file) but I did not want to use a separate launchd cjob for this workflow. 

**2. Select the delivery slot**

- Thursday morning, every week. I like to keep it consistent and predictable. 

> 🎩 **NOTE**
> I prefer to space this out from the order day, so the supermarket has time to restock, and you are not left without strawberries.

**3. Add recurring items (rule-based)**

| List       | When it runs                       | URL                                     |
| ---------- | ---------------------------------- | --------------------------------------- |
| Weekly     | Every week                         | `.../lists/WEEKLY_LIST_ID`              |
| Bi-weekly  | Weeks 1 & 3                        | `.../lists/BIWEEKLY_LIST_ID`            |
| Monthly    | Week 1 of the month                | `.../lists/MONTHLY_LIST_ID`             |
| Quarterly  | Week 1 of Jan / Apr / Jul / Oct    | `.../lists/QUARTERLY_LIST_ID`           |

**4. Handle quantities & stock issues**

- Apply quantity multipliers (sparkling water ×2, eggs ×3, mozzarella ×3)
* If something is out of stock, it automatically selects the next best available alternative. This is where AI clearly sparkles and differentiates itself from scripting.

> AI automation can adapt to edge cases like out-of-stock items, unavailable delivery slots, quantity constraints—without needing a predefined rule for every scenario.

**5. AI, wait for your boss to confirm!**

The cart is built, the slot is booked, the substitutions are made. 
Then it stops, and I quickly review and hit **Confirm Order**..

---

### Why I kept a human in the loop

"Confirm Order" is the one step where a mistake has a real cost: a wrong quantity, a duplicate list, a missed substitution. 
Keeping it manual gives me a 30-second sanity check before money leaves the account. That is exactly the kind of friction I want to keep.

![Grocery ordering workflow](/assets/images/order-buy.jpg)
