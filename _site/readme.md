# allmaps-intro-workshop
Workshop for Georerferencing IIIF Maps in Allmaps


# UWM Workshop Template

A reusable Jekyll template for building technology-focused workshop sites with University of Wisconsin–Milwaukee (UWM) branding standards.

---

## Features

- UWM-branded styling using official colors and fonts (with accessible fallbacks)
- Organized lesson structure using a Jekyll **collection**
- Automatically generated **Previous / Next** navigation for lesson pages
- Simple **home page layout** listing lessons in order
- Template-ready setup with example `_config.yml`

---

## Getting Started

### Prerequisites

- Ruby and Bundler installed (e.g., `ruby -v`, `bundle -v`)
- Basic familiarity with Jekyll: themes, layouts, and front matter

### Local Setup

1. **Clone the template repository**:

   ```bash
   git clone https://github.com/uwm-libraries/workshop-template.git
   cd workshop-template
   ```

2. **Install dependencies**:

   ```bash
   bundle install
   ```

3. **Run locally**:

   ```bash
   bundle exec jekyll serve
   ```

   Visit `http://localhost:4000` to preview.

---

## Deployment via GitHub Pages

1. Commit all changes to your repository.
2. Enable GitHub Pages in **Settings → Pages**.
3. Make sure the build source is set to your branch (e.g., `main`) and the correct path (root or `/docs`).
4. Wait a moment — your site should go live at:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```
