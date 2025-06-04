---
layout: base 
title: Documentation
search_exclude: true
permalink: /documents/
nav: true
---

# Internal Documentation Overview

This page provides links and descriptions for internal documentation about the Open Coding Society repository structure and theme/navigation system.

Each document is crucial for understanding the technical setup and best practices students should follow while working with the repository.

---

## `_includes` Consolidation Documentation

The `_includes` directory was historically a flat, disorganized collection of layout fragments. We performed a large-scale refactor to clean up, consolidate, and modularize these includes.

- Common layout files such as `toc.html`, and `utterances.html` have been consolidated into a single `post_meta_block.html`.
- Notebook badges for GitHub, Binder, Colab, and Deepnote have been unified into `badge_block.html`.
- Navigation and post listing files are organized into logical subfolders (`head/`, `layout/`, `nav/`, `notebooks/`, `posts/`).
- File deletions were performed to remove obsolete, duplicated, or unused includes.

This reorganization leads to:
- Cleaner `_includes/` structure
- Reduced duplication
- Simpler, reusable layout logic
- Easier future maintenance

[View `_includes` Consolidation Documentation Here]({{ site.baseurl }}/includes_docs)

---

## Theme Switching and Navigation Logic Documentation

Our repository supports dynamic theme switching between **Minimal** and **Minima**.

- Theme selection is controlled via `remote_theme` in `_config.yml`.
- Pages should use `layout: base`, and `base.html` handles theme detection dynamically:
  - If `remote_theme` contains `minimal@v0.2.0`, it includes `minimal_default.html`.
  - If `remote_theme` contains `minima`, it includes `minima_default.html`.
- **Minimal** theme:
  - Uses TailwindCSS for responsive layout
  - Navigation is controlled by `nav: true` front matter on each page
- **Minima** theme:
  - Uses Jekyll's standard SASS-based styling
  - Navigation is controlled globally via `header_pages` in `_config.yml`
- No Tailwind Typography plugin is used to preserve clean Markdown styling.

This ensures:
- Dynamic layout selection
- Proper navigation logic per theme
- Clean, maintainable theme and style management

[View Theme and Navigation Logic Documentation Here]({{ site.baseurl }}/theme_and_nav_docs)

---

# End of Documentation

For best practices, refer to these documents whenever you are modifying layouts, navigation, or includes within the Open Coding Society repositories.

