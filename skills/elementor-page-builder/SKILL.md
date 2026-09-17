---
name: elementor-page-builder
description: Build or rewrite WordPress blog posts on any Elementor site using native, independently editable Elementor widgets, correct SEO-plugin metadata, and public desktop/mobile verification — while respecting a staging-vs-production authorization boundary.
---

# Elementor Page Builder

Build or rewrite an article's body directly in WordPress + Elementor. This skill governs the WordPress/Elementor implementation. Use the companion `elementor-seo-writer` skill for research, fact-checking, search intent, article copy, metadata, links, image planning, and heading decisions — this skill turns that copy into a correctly structured Elementor page.

## SETUP — READ FIRST

This skill is site-agnostic and must never assume any specific site's facts.

1. Look for `SITE-PROFILE.md` in the current project/folder and read it before touching anything. It should tell you: which URL is staging vs. production, the single-post template that supplies the public H1, the default author, current category IDs, which SEO plugin and TOC plugin are active, and whether the site uses a custom completion-tracking meta key.
2. If there is no `SITE-PROFILE.md`, or it's missing a fact you need, ask the user rather than guessing or reusing an example value. Treat any ID, template name, or user ID you're given as a current snapshot, not a permanent fact — WordPress installs change plugins, IDs, and templates over time.
3. Never carry over another site's post IDs, user IDs, category IDs, or meta keys. Confirm the current values on the actual site you're working on before every build.

## Verify the environment first

Before changing a post, inspect the current state on the target environment:

- Confirm which template supplies the public H1, hero, breadcrumb, meta, featured image, author box, related posts, comments, article frame, and TOC styling on this site.
- Confirm the target URL, post ID, status, slug, category, author, template behavior, Elementor version, current `_elementor_data`, `post_content`, SEO-plugin metadata, featured image, and any autosave/revision that Elementor is actually loading.
- Confirm which plugin provides the TOC (if any) so you never add a duplicate.

## Authorization boundary

- Work on staging unless the user explicitly approves production changes. If the site profile or the user hasn't said which environment is staging and which is production, ask before making any change.
- Preserve an established slug unless a strong SEO reason justifies changing it. Explain redirects before changing a ranking URL.
- New posts remain drafts until the user approves publication.
- Do not delete revisions in bulk. Remove a particular stale autosave only after verifying its ID, parent, content, and role in the editor problem.
- Do not invent screenshots, device testing, benchmarks, quotes, statistics, links, or first-hand experience.

## Required workflow

1. Inspect the existing public article, editor data, metadata, images, links, and overlapping site content.
2. Research current technical facts and exact UI labels using primary or authoritative sources. Credit the respective source for factual claims, official screenshots, vendor imagery, or licensed visuals.
3. Plan the article around the reader's task. Choose H2 and H3 headings by useful structure, not a quota.
4. Build the article from native Elementor widgets using the component rules below.
5. Keep `post_content` semantically equivalent to the visible Elementor article so the SEO plugin and non-Elementor consumers read the same copy.
6. Save on the target environment, clear only the relevant Elementor/cache-plugin caches, and verify the editor plus anonymous public view of that environment.
7. If the site uses a custom completion-tracking meta key (per `SITE-PROFILE.md`), set it only after every completion gate below passes.
8. Report staging work separately from production. State clearly whether production is unchanged until the user pushes, or was explicitly authorized and edited live.

## Editorial structure

- Exactly one public H1. The single-post template supplies it; do not add an H1 to the article body.
- Use a short introduction followed by a concise Quick Answer when useful.
- Do not use a fixed H2 count. Each H2 must answer a distinct major question or represent a major stage in the task.
- Use H3 for related methods, brands, versions, error cases, or audience variants that belong under one H2. Use H4 only when an H3 genuinely needs another level.
- Merge shallow or overlapping sections. Never add headings for the SEO plugin, word count, or a predetermined outline length.
- Quick Answer is a visual label, not an H2.
- Do not add a second TOC when the active template/TOC plugin already supplies one. Public verification must find exactly one TOC.
- FAQs are optional. Include only genuine questions that add information, typically 3–7; skip them when they would repeat the article.
- Word count follows search intent. A substantial competitive guide may run long, but a complete shorter answer is better than padding.
- Keep paragraphs short for mobile readability: normally 1–3 sentences. Split a paragraph when the idea, action, condition, warning, or platform changes. Do not fragment closely related sentences merely to make every paragraph one line.

## Native Elementor structure contract

Every important component must be independently editable. Use shallow, top-level native containers in article order.

- Each H2 and H3: its own top-level container with one native Heading widget at the correct semantic level.
- Body copy: native Text Editor widgets in sensible, independently editable blocks. Do not combine unrelated subsections or complete cards in one Text Editor.
- Images and screenshots: each in its own top-level container with a native Image widget and native caption when needed.
- Quick Answer: its own native card container with a Heading widget for the label and a separate Text Editor for the 40–80-word answer.
- Tip, Important, Warning, Compatibility, and Security Note: each its own native card container using independently editable Heading/Icon/Text widgets.
- Related Guide: its own native card container with independently editable label, real linked title, and one short supporting sentence.
- FAQ: its own H2 Heading container followed by a separate native Accordion container/widget. Do not build FAQ `<details>` markup inside a Text Editor.
- Steps: use native text/list widgets, or an approved reusable step component if the site has one, while keeping step content independently editable where practical.
- Tables: use whatever WordPress/Elementor table solution the site already relies on (per `SITE-PROFILE.md`) and verify mobile behavior.
- Code: use a native/reusable code component; escape commands correctly and explain what they do.

Never place custom card wrappers, Heading markup, Related Guide cards, callout boxes, FAQ markup, images, or a whole article inside a Text Editor or HTML widget.

Avoid nested containers unless a real layout requires them, such as an icon-and-copy row or desktop columns that stack on mobile. Do not use empty containers or Spacer widgets for ordinary spacing. Use container padding, margin, and gap. Keep roughly 24px separation after cards unless the site's approved design specifies otherwise.

### Spacing contract for every container

Every top-level article container must have intentional, explicit responsive spacing settings; do not leave spacing to accidental widget defaults.

- Heading container: 0 padding and 12px bottom margin before its related body block.
- Body text, list, steps, code, table, image, and FAQ container: 0 padding and 24px bottom margin by default.
- Quick Answer, callout, and Related Guide card: appropriate internal card padding plus 24px bottom margin. Use about 20–24px internal padding on desktop and 16–20px on mobile unless an approved reusable component already defines it.
- End of a major H2 section: use 32px separation on desktop and 24px on mobile before the next H2 heading. Apply this by adjusting the final component's bottom margin, not by adding another container.
- Nested layout containers, when genuinely required: use an explicit gap, normally 12–16px, and verify the mobile stack.
- Avoid double spacing. If adjacent containers both contribute to the same visual gap, keep the spacing on the preceding container and set the following container's top margin to 0.
- Use zero horizontal padding on ordinary article-content containers when the article template already supplies page padding. Card containers may use their approved internal padding.
- Verify the resulting rhythm publicly on desktop and mobile. Reduce spacing only when necessary to prevent excessive empty space; do not remove separation entirely.

## Content and trust requirements

- Use one primary focus keyword naturally. Do not stuff exact matches.
- Verify every internal URL exists and fits the context.
- Prefer official documentation and primary sources for technical claims. Attribute vendor claims and licensed visual sources clearly.
- Use original screenshots only when actually captured from an available device/account. If the required device is unavailable, recommend the shot and defer it; never fabricate it.
- Use short sentences, plain English, numbered actions, exact verified labels, and low-risk fixes first.
- Warn before destructive steps, explain restart/admin/data-loss implications, and recommend backups where appropriate.
- Keep images purposeful, compressed, correctly sized, and descriptive. Do not duplicate existing inline images.

## SEO-plugin metadata

- Use one focus keyword.
- Write a natural SEO title that matches intent; do not force a power word, number, sentiment term, or year.
- Write a useful 120–160 character meta description.
- Keep an established slug unless a change is justified and redirected.
- Use the keyword naturally in the title, description, introduction, body, and a relevant heading where appropriate.
- Use real internal links and authoritative external sources only where useful; no fixed link quota.
- Recommend only schema that matches visible page content.
- Do not sacrifice accuracy, clarity, or trust for a plugin score.

## Safe data handling

- Read and decode current `_elementor_data` before modifying it. Preserve unrelated user content and settings.
- Elementor metadata read through WordPress is unslashed. Encode valid JSON and apply the required WordPress slashing once before saving.
- Keep `post_content` and Elementor content synchronized without duplicating the template-owned H1 or TOC.
- Do not rely on a saved database value, cache notice, enabled Publish button, or HTTP 200 as proof that the requested result is publicly visible.
- Treat autosaves and revisions carefully: `update_post_meta()` may remap revision metadata to the parent. Verify which record Elementor reads before any targeted repair.

## Completion gates

Do not mark the post complete (or set any completion-tracking meta key) until all applicable checks pass:

- Correct staging/production URL, post ID, status, title, slug, author, category, and featured image.
- Exactly one public H1, supplied by the template.
- Heading count and hierarchy match the content rather than a quota.
- Every H2/H3 is a native Heading widget in its own container.
- Every image is a native Image widget in its own container.
- Every callout and Related Guide is an independent native card container.
- FAQ uses native independently editable components when present.
- No heading, card wrapper, FAQ component, or image is embedded in a Text Editor.
- No unnecessary nested or empty containers.
- Every top-level article container has explicit responsive margin, padding, and gap values appropriate to its component type; no accidental default or double spacing.
- Exactly one public TOC.
- `post_content` and visible Elementor copy are semantically synchronized.
- No visible escape artifacts such as literal `u2014` or `\\u2014`.
- Real internal/external links resolve as intended.
- Desktop and mobile have no horizontal overflow; images, tables, cards, headings, and controls remain readable.
- Anonymous public view reflects the saved article after relevant cache clearing.
- SEO-plugin metadata is present and the post remains in the user-approved publication state.

## Handoff

After each completed step, give the user a short update that separates:

- **Staging:** exactly what changed and how it was verified.
- **Production:** unchanged, user-pushed, or explicitly modified and verified.
- **Sources/credits:** official documentation, image creator/library, vendor media, or original screenshot ownership as applicable.

After the complete build, report the post ID, title, URL, publication state, H2/H3 structure, approximate word count, native container/widget audit, link/image/FAQ status, SEO-plugin metadata status, desktop/mobile result, completion-tracking status (if used), and whether staging and production are currently synchronized.
