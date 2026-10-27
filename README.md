# DQUEST

# Few tips to add a project on the page

Each file in `_posts/` is a **project** (an experiment). Projects are listed as cards on the Projects page (`projects.md`) and each one has its own page rendered with `_layouts/post.html`.

## Table of Contents
- [Fast launch](#fast-launch)
- [More details](#more-details)
  - [0. Ask permission for pull and push](#0-ask-permission-for-pull-and-push)
  - [1. Create the project file](#1-create-the-project-file)
  - [2. Front matter reference](#2-front-matter-reference)
  - [3. Body sections](#3-body-sections)
  - [4. Images](#4-images)
  - [5. Markdown Cheatsheet](#5-markdown-cheatsheet)
- [Acknowledgments](#acknowledgements)
- [TODO](#todo)


## Fast launch
If you want to run the server locally clone the repo and install jekyll:

https://jekyllrb.com/

Then run:
```
bundle install
bundle exec jekyll serve
```

If `bundle install` fails because of the versions pinned in `Gemfile.lock`, you can delete it locally, but do not push the modifications to the `Gemfile` or `Gemfile.lock` on the repo when you add your project.

When pushing, only add the files you modified '.md', '.scss', images etc..

Every push to `main` is checked by the "Jekyll site CI" workflow (`.github/workflows/jekyll-docker.yml`), which builds the site. The site itself is published by GitHub Pages directly from the `main` branch.

***
## More details
### 0. Ask permission for pull and push

Contact any admin; for instance, julien.rosenberger@inria.fr.

---

### 1. Create the project file

All projects live in `_posts/`. The easiest way is to copy one of the templates:

- `templates/ongoing_experiment.md`: sections for a running study (Purpose, What Happens, Who Can Participate, Duration, Compensation, How To Participate).
- `templates/completed_experiment.md`: sections for a finished study (Purpose, Method, Key Findings, Future Work, Publications).

Then change at least the `title`, `date`, `summary` and `permalink` in the copied front matter.

Name the new file:

```
_posts/YYYY-MM-DD-your-project-slug.md
```

The date prefix controls the sort order on the Projects page (newest first). The URL is set by `permalink`.

---

### 2. Front matter reference

Every project starts with a YAML front matter block between `---` delimiters, for instance:

```yaml
---
layout: post
title: "Your Project Title" (to change)
date: 2026-05-11 (to change)
summary: "One or two sentences describing the project (shown on the project card)." (to change)
permalink: your_project_slug (will be in the URL) (to change)
status: "Ongoing" (or "Completed" or "Under Development") (to change)
people:
  - "First Collaborator" (to change)
  - "Second Collaborator" (to change)
location: "INRIA Bordeaux (France)" (to change)
contact:
  name: "First Collaborator" (to change)
  email: "first.collaborator@inria.fr" (to change)
thumbnail: "/images/posts/YYYY-MM-DD-your-project-slug/thumbnail.png" (to change)
participate_type: "On-site" (or "Remote") (to change)
---
```

#### Field descriptions

| Field | Required | Description |
|---|---|---|
| `layout` | Yes | Always `post`. |
| `title` | Yes | Project title shown on the card and the page header. Use double quotes if it contains colons or special characters. |
| `date` | Yes | Date in `YYYY-MM-DD` format. Should match the filename date. |
| `summary` | Yes | Short description shown on the project card. |
| `permalink` | Yes | Slug for the project URL (e.g. `permalink: question-asking` → `developmentalsystems.org/DQUEST/question-asking/`). Omit the leading slash. |
| `status` | Yes | Badge shown on the card and the page. Only `"Ongoing"` (yellow) and `"Completed"` (blue, card greyed out) are styled; other values (e.g. `"Under Development"`) are displayed without colour. A precision can be added in parentheses (e.g. `"Ongoing (Analyzing)"`): the colour follows the part before the parentheses, and the precision is shown in lighter text. |
| `people` | Optional | List of collaborator names, displayed comma-separated on the card and the page. |
| `location` | Optional | Where the study takes place, shown on the card and the page. |
| `contact` | Optional | Contact person shown at the top of the project page, with `name` and `email` (the email becomes a `mailto:` link). |
| `thumbnail` | Optional | Path to the image shown on the project card. Shared stock images are in `images/` (e.g. `/images/pexels-cottonbro-9290021.jpg`). |
| `participate_type` | Optional | `"On-site"` or `"Remote"`. Currently not displayed anywhere. |

Collaborators shown on the Contact page (`contact.md`: name, photo, role, institution...) are defined separately, one file per person, in `_collaborators/` (photos in `images/collaborators/`). The names in `people` are plain text and are not linked to those files.

---

### 3. Body sections

After the front matter, write the content in Markdown using `##` headings. The current projects use:

- `## Purpose`
- `## What Happens`
- `## Who Can Participate`
- `## Duration`
- `## Compensation`
- `## How To Participate`

MathJax is enabled: use `$...$` for inline and `$$...$$` for display math.

---

### 4. Images

Store project images in a dedicated subdirectory (a folder, without `.md` in its name):

```
images/posts/YYYY-MM-DD-your-project-slug/
```

The site is served under `/DQUEST`, so in the body of the project, reference images with `relative_url` (a plain `/images/...` path would miss the `/DQUEST` prefix):

```markdown
![Alt text]({{ '/images/posts/YYYY-MM-DD-your-project-slug/my-figure.png' | relative_url }})
*Figure caption goes here.*
```

The `thumbnail` field does not need this: the Projects page adds the prefix itself.

---

### 5. Markdown Cheatsheet

See https://www.markdown-cheatsheet.com/

---


## Acknowledgements

The design of this blog is inspired by [Anatole](https://github.com/lxndrblz/anatole) (Hugo theme by Alexander Bilz), developed with [Claude Code](https://claude.com/fr/product/claude-code) (Anthropic) and built with [Jekyll](https://jekyllrb.com).


## TODO

- [ ] have another branch for development and where others could see other test versions.
