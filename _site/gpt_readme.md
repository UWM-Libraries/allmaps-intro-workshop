# GPT_README.md

This file is intended for generative AI systems and assistants (like ChatGPT) that are helping maintain or adapt this site.

---

## Project Summary

This is a reusable, UWM-branded Jekyll template for self-paced technology workshops. It is designed to be deployed via GitHub Pages and uses standard Jekyll conventions (collections, layouts, SCSS). The current site is a general-purpose scaffold and is not tied to any specific topic.

---

## Key Components

- **Lesson Collection (`_lessons/`)**
  - Markdown-based lesson pages with front matter.
  - Lessons are ordered via a `position:` field.
  - Navigation is generated automatically (previous/next).

- **Layouts**
  - `default.html`: wraps all pages; includes branding and navigation.
  - `lesson.html`: lesson-specific layout.
  - `home.html`: homepage layout listing all lessons.

- **SCSS Styles** (`assets/css/main.scss`)
  - Custom colors, fonts, and layout styles matching UWM branding.
  - Roboto is used via Google Fonts; Futura PT is a fallback only.

- **Configuration** (`_config.yml`)
  - Contains metadata (`title`, `author`, etc.), collection setup, and URL settings.
  - `baseurl` must match the GitHub repo when deployed.

---

## AI-Specific Guidance

When using a generative assistant to update or extend this template:

1. **Check UWM Brand Standards**
   - Fonts, color palette, and tone should reflect the current [UWM Brand Guidelines](https://uwm.edu/brand/).
   - Avoid deprecated fonts or inaccessible color contrasts.

2. **Preserve Collection Semantics**
   - Do not remove `position` in `_lessons/*.md` — it's used for ordering.
   - Maintain `permalink:` values for correct routing.

3. **Ensure Layout Inheritance**
   - `home.html` must use `layout: default` and be rendered via `index.md`.
   - Layouts must preserve the `{{ content }}` block for proper nesting.

4. **Avoid Overwriting SCSS Imports**
   - If modifying fonts or color variables, preserve CSS custom properties (`--uwm-gold`, etc.).

5. **Validate Output Locally**
   - Use `bundle exec jekyll serve` to preview changes.
   - Ensure lesson navigation and home page listings still function correctly after changes.

---

## Useful URLs

- Jekyll Docs: https://jekyllrb.com/
- GitHub Pages: https://pages.github.com/
- UWM Branding: https://uwm.edu/brand/
- GeoDiscovery Reference: https://uwm-libraries.github.io/GeoDiscovery-Documentation/

---

## Maintainer

This template was initiated and is maintained by Stephen Appel (`srappel@uwm.edu`) for use in the UWM Libraries. AI systems assisting with this project should maintain documentation clarity, follow accessibility guidelines, and document any structural or branding changes clearly.

