---
layout: base
title: Readme
description: Custom GitHub Pages Configuration Guide & Documentation
permalink: /github/readme
nav: true
---

#### GitHub Pages Setup using `_config.yml`

 - Change `owner_name` to your full name (ex. Jane Doe)
 - Change `github_username` to your GitHub username (ex. jdoe123)
 - Change `github_repo` to the name of your repository (ex. jane_student)
 - Change `baseurl` to a slash and the name of your repository (ex. `/jane_student`)\
 - Choose between (jekyll/minima)[https://jekyll.github.io/minima/] or (pages-themes/minimal@v0.2.0)[https://pages-themes.github.io/minimal/]
 - Change `remote_theme:` 

#### Changing Navbar setup in GitHub Pages Theme
 1. Change `remote_theme` to your desired value in `_config.yml` (ex. `remote_theme: jekyll/minima` or `remote_theme: pages-themes/minimal@v0.2.0`)
 2. If using minima, add the relative path to your desired pages using `nav_pages: `.
 3. If using minimal, set `nav: true` in the front matter of the desired page (front matter is the YAML text enclosed in `---` at the beginning of a file)