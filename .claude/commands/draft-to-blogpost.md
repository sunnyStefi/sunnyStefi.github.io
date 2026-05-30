---
name: draft-to-blogpost
model: sonnet
description: Create a blog post from a draft.
---

You are writing a technical blog post for Stefania's blog at https://sunnystefi.github.io/.

**Input draft:** $1

## Task

Turn the draft into a finished post that matches the voice, structure, and content pillars defined in the social rules (already in context). Expand where the draft is thin, cut padding, and keep every claim concrete.

## Blog-specific requirements

- **Length**: 600-1000 words — long enough to develop the idea, short enough to stay tight. A blog post earns more room than a LinkedIn post, so include the why and the how, not just the takeaway.
- **Front matter**: start the file with this exact Jekyll front matter block, filled in:
  ```yaml
  ---
  layout: post
  title: "..."           # clickable, specific — name the result or the pain, not a vague topic
  description: "..."     # one sentence summarizing the post's core insight
  category: ...          # a single thematic category, e.g. "Agentic Engineering"
  image: /assets/images/...   # check in assets/images if there is an image that references this blogpost explicitly
  ---
  ```
- **Structure**: open with a hook that names the problem, develop the story in themed sections using `###` (H3) headings — the title is the only H1, supplied by the front matter. Start each major section with a short italicized statement for emphasis. Separate sections with a `---` horizontal rule. End with a `### Takeaway` section holding one concrete insight.
- **Formatting**: Markdown. Short paragraphs (2-4 sentences). Use bulleted lists for tools/resources and link tool names to their GitHub repos. Use a blockquote for the single sharpest insight. Use fenced code blocks and inline `code` only when the draft involves actual commands or file names.
- **Footer**: close with a brief footer line (author name, LinkedIn link, location) if the draft provides those details.
- Do not use the "—" character.
- 0-2 emojis max, only if they add meaning.

## Reference posts

Existing posts in `_posts/` show the exact voice, structure, and front matter to match. Read one or two before writing:

- `_posts/2026-05-22-lessons-from-1m-spent-of-aI-assisted-development.md`
- `_posts/2026-05-18-grocery-shopping-ai-automation-flow.md`
- `_posts/2026-05-15-hour-registration-AI-automation.md`

## Output

Write the finished post as a new file under `_posts/`, named `YYYY-MM-DD-title-slug.md` (today's date prefix, kebab-case slug from the title) — this is the directory Jekyll publishes from. The file content is only the finished blog post in Markdown, ready to commit — no preamble, no "here's a draft", no meta-commentary.

