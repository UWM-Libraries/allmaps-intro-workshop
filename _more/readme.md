---
layout: home
title: "Template Instructions"
position: 0
permalink: /more/readme/
published: true
---

## How to use this Template

1. [Fork this repo](#fork-this-repository)
1. [Modify \_config.yml](#modify-_configyml)
1. [Modify index.md](#modify-indexmd)
1. [Create lessons pages in markdown](#create-lessons-pages-in-markdown)
1. [Add setup instructions, instructor notes, or other auxiliary pages](#add-setup-instructions-instructor-notes-or-other-auxiliary-pages)
1. [Clean up template pages](#clean-up)
1. [Problems? Suggestions? Need Help](#problems-suggestions-need-help)

### Fork this repository

1. Sign in to GitHub
2. Navigate to this [repository’s main page](https://github.com/UWM-Libraries/uwm-workshop-theme).
3. In the top-right corner, click the **Fork** button.
4. Choose your GitHub account (or an organization you belong to) as the destination.
5. (Optional) Rename your forked repository and update the description.
6. Click **Create fork**.

Now you can clone the repository to your local machine and [build using Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)
(recommended!)
or
modify the files directly in GitHub.

### Modify \_config.yml

Edit the site-wide settings in `_config.yml` to match your workshop:

These values control the core identity and deployment details of your workshop site:

```yaml
title: UWM Workshop Template # The main title displayed in the header and metadata
email: srappel@uwm.edu # The primary contact email shown on the site
author: Stephen Appel # The author or maintainer of the workshop
github_username: uwm-libraries # The GitHub username or organization for the workshop repo
website: https://uwm.edu/libraries/ # The website for the author or hosting institution
description: >-
  A reusable template for building self-paced technology workshops at the University of Wisconsin–Milwaukee.
baseurl: "/workshop-template" # Path to the site when hosted (usually the repo name)
url: "https://uwm-libraries.github.io" # The base domain for the hosted site
...
```

- **`title`**<sup>(required)</sup>,
**`email`**<sup>(recommended)</sup>,
**`author`**<sup>(recommended)</sup>,
**`github_username`**<sup>(optional)</sup>,
and **`website`**<sup>(optional)</sup>
personalize your workshop.
- **`description`**<sup>(recommended)</sup>
appears in metadata for search engines and social sharing.
- **`baseurl`**<sup>(required)</sup> must match your repository name when hosting on GitHub Pages (e.g., `/workshop-template`).
- **`url`**<sup>(required)</sup> should be your GitHub Pages domain or custom domain.

### Modify index.md

Update the home page (`index.md`) with your workshop introduction, goals, and links.
You can use Liquid syntax like {% raw %}`{{ site.title }}`{% endraw %} to insert site-wide values defined in `_config.yml`.

Include any special instructions or expectations for participants.

### Create lessons pages in markdown

Add markdown files to the `_lessons` folder. Use YAML front matter to set:

```yaml
---
layout: home
title: "Lesson 1: Introduction"
position: 1
permalink: /lessons/intro/
---
```

The `position` value controls the order in lesson lists.

Modify the "title" object to reflect the lesson title.

Use the permalink to set a "pretty" url. Keep `/lessons/` in place!

### Add setup instructions, instructor notes, or other auxiliary pages

Add markdown files to the `_more` folder or modify the existing ones. 

Use YAML front matter to set:

```yaml
---
layout: home
title: "Instructor Notes"
position: 2
permalink: /more/notes/
---
```

The `position` value controls the order in "more resources" lists.

Modify the "title" object to reflect the page title.

Use the permalink to set a "pretty" url. Keep `/more/` in place!

### Clean Up

Remove any template pages from `/_lessons` and `/_more` that you aren't using.

Remove this page from navigation by setting
```yaml
published: false
```
in thie page's front matter.

Update favicon.svg and logos in `assets/images` if desired.

Update colors and styles in `assets/css/main.scss` if desired.

### Problems? Suggestions? Need Help

If you run into issues or have ideas to improve this template:

- Open an issue or pull request on the [repository](https://github.com/UWM-Libraries/uwm-workshop-theme)
- Share suggestions with your workshop’s maintainers
- Check the documentation for Jekyll and Liquid for troubleshooting
