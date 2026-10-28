# Course Notes Pattern — Anthropic Claude Certified Architect (Foundations)

This repo holds exam-prep notes for the **Anthropic Academy / Claude Certified Architect – Foundations** path. Each course is conspected from the Anthropic course videos/pages into a consistent, exam-focused format.

When adding or editing a course, follow the pattern below. The three completed courses are the canonical template — read `claude-code-101/README.md` as the reference example before writing a new one.

## Goal of these notes

Material that is **correct, consistent, simple, and easy to remember** for the certification exam. Optimize for: fast pre-exam scanning, no redundancy, no over-complication. Two completed courses scored 10/10 and one scored 100% on the real quizzes — match that bar.

## Repo structure

- Each course = its own folder: `course-slug/README.md` + `course-slug/assets/`
- Screenshots live under `course-slug/assets/LN-topic/` (one subfolder per lesson/chapter)
- The root `README.md` is the course index — update its progress table and the course row (status + "Certified" note) when a course is finished

## Per-file structure (top to bottom)

1. `[⬅ Back to course index](../README.md)` link
2. `# 📚 <Course Name> — Course Notes` title, plus a one-line "builds on…" note if it depends on an earlier course
3. 🗺️ **Course Map** table — Units → Chapters (with anchor links) → status column
4. **Annotation guide** blockquote (see below) — so markers are never mistaken for exam content
5. Chapters in order

## Per-chapter structure

- `## Chapter N: <Title>` and a `> 🗂️ Unit …` / `> 🎬 Video …` lead-in
- 🎯 **Learning Objectives** (when the lesson lists them)
- 🧠 **Key Takeaways** (bulleted, bold the key terms)
- Body: use **tables** heavily (comparisons, before/after, option lists), embed screenshots with descriptive alt text
- 🔁 **Recap** where the lesson has one
- 📝 **Quick Reference: <topic> (for exam prep)** table
- 🎓 **Memory tip** — a short mnemonic
- **Key features for exam:** bullet list of the most testable facts

## Annotation markers (keep testable content clean)

- 📌 = my own reading from a screenshot or my inference — **not stated in the lesson**. Not exam material.
- 🔗 = my cross-reference/mapping between chapters or courses — **my mapping, not the lesson's wording**.
- Every new course README must include this annotation-guide blockquote near the top:

  > **Annotation guide for these notes:** 📌 = my own reading from screenshots/context — **not stated in the lesson text itself**. 🔗 = my cross-reference between chapters — **my mapping, not the lesson's wording**. For exam prep, focus on the **📝 Quick Reference** tables and **Key features for exam** bullet lists at the end of each chapter.

## Accuracy rules

- **Be faithful to the course, not the live product.** The exam tests what the course teaches. If the live Anthropic docs have since diverged (e.g. more permission modes than the course covers), do NOT replace the course content. Add a clearly-labeled 📌 footnote marked "Beyond the course (not on the exam)" instead.
- Cross-check factual claims (numbers, names, plan availability, definitions) against Anthropic's live sources — anthropic.com, support.claude.com, and the Claude Academy course pages — where it matters. Prefer official sources over blogs.
- Keep terminology ordering consistent across courses (e.g. Claude's principles are **Helpful, Honest, Harmless** — Anthropic's own wording).
- The agent cannot watch the videos. The user supplies each chapter's content (transcript text, page text, or screenshots); conspect from what they provide.

## Style

- Plain, concise prose. Tables and bullets over long paragraphs. Bold the exam-relevant terms.
- Use the same emoji vocabulary as existing courses for section headers (🧠 🎯 📝 🎓 🔁 🗺️ ⚠️ 💡 🔗 📌) so the courses feel uniform.
- Write/edit notes in the user's provided language.

## Git

- This repo is scoped to a **local** git identity: Avet Badalyan <avetbadalyan@gmail.com> (personal). The global identity is the work client — do not change it.
- Only commit/push when the user explicitly asks.
