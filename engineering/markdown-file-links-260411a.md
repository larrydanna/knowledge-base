# How To: Link Another File in Markdown

**Date:** 2026-04-11  
**Category:** engineering  
**Tags:** `markdown`, `github`, `links`, `documentation`  
**Related:** [VSCode — GitHub Flavored Markdown Preview](../environment/vscode-gfm-markdown-260413a.md), [GitHub Markdown Alerts](markdown-github-alerts-260411a.md)

---

## TL;DR

- **Syntax**: `[a relative link](./somefilenamehere.md)`
- **Relative Pathing**: use relative paths 
- **Auto-complete**: Type a dot between the parenthesis to trigger automatic path syntax.
- **Section Links**: Append `#heading-slug` to link to specific sections

---

## Core Syntax

Use the standard Markdown link format: `[Link Text](path/to/file.md)`. [5, 6] 

* Same Folder: `[See more details](details.md)`
* Subfolder: `[View technical specs](docs/technical-specs.md)`
* Parent Folder: `[Back to main](../README.md)`
* Root Level: `[Home](/README.md)` (Starts from the root of the repository) [1, 7, 8, 9, 10, 11] 

---

## Linking to Specific Sections

You can link directly to a heading in another file by appending a lowercase slug after a #. [12, 13] 

* Syntax: `[Link Text](other-file.md#heading-title)`
* Slug Rules: GitHub converts headings to slugs by making them lowercase, replacing spaces with dashes, and removing punctuation.
* Heading: `## Installation & Setup`
* Link: `[Go to setup](docs/setup.md#installation--setup)` [14, 15, 16] 

---

## Best Practices for Compatibility

* Avoid Spaces: Files with spaces in the name can break links. If necessary, use %20 to represent a space (e.g., `file%20name.md`).
* Case Sensitivity: GitHub's file system is case-sensitive. Ensure your path exactly matches the filename, including capitalization.
* Automatic Anchors: Hover over any heading on GitHub to see the chain icon; clicking it will give you the exact URL fragment (the part after #) to use for section linking. [5, 14, 16, 17, 18] 

---

## Why Use Relative Links

To link to another Markdown file on [GitHub](https://github.com/), you should use relative paths instead of full URLs. This ensures your links work whether the repository is viewed on GitHub, GitHub Pages, or a local machine. [1, 2, 3, 4] 

---

## Sources

[1] [https://stackoverflow.com/questions/7653483/github-relative-link-in-markdown-file](https://stackoverflow.com/questions/7653483/github-relative-link-in-markdown-file)
[2] [https://github.blog/news-insights/product-news/relative-links-in-markup-files/](https://github.blog/news-insights/product-news/relative-links-in-markup-files/)
[3] [https://github.blog/news-insights/product-news/relative-links-for-github-pages/](https://github.blog/news-insights/product-news/relative-links-for-github-pages/)
[4] [https://www.geeksforgeeks.org/git/github-relative-link-in-markdown-file/](https://www.geeksforgeeks.org/git/github-relative-link-in-markdown-file/)
[5] [https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
[6] [https://anvilproject.org/guides/content/creating-links](https://anvilproject.org/guides/content/creating-links)
[7] [https://stackoverflow.com/questions/32563078/how-link-to-any-local-file-with-markdown-syntax](https://stackoverflow.com/questions/32563078/how-link-to-any-local-file-with-markdown-syntax)
[8] [https://github.com/github/markup/issues/101](https://github.com/github/markup/issues/101)
[9] [https://stackoverflow.com/questions/70781122/referencing-files-in-a-github-markdown-file](https://stackoverflow.com/questions/70781122/referencing-files-in-a-github-markdown-file)
[10] [https://github.com/orgs/community/discussions/23148](https://github.com/orgs/community/discussions/23148)
[11] [https://github.com/readthedocs/recommonmark/issues/108](https://github.com/readthedocs/recommonmark/issues/108)
[12] [https://stackoverflow.com/questions/77999385/how-to-link-to-a-specific-section-in-another-markdown-file-in-github](https://stackoverflow.com/questions/77999385/how-to-link-to-a-specific-section-in-another-markdown-file-in-github)
[13] [https://www.reddit.com/r/Markdown/comments/1cdcfk2/is_there_a_way_to_link_to_section_in_another/](https://www.reddit.com/r/Markdown/comments/1cdcfk2/is_there_a_way_to_link_to_section_in_another/)
[14] [https://www.youtube.com/watch?v=pblIwWUQzAM](https://www.youtube.com/watch?v=pblIwWUQzAM)
[15] [https://stackoverflow.com/questions/2822089/how-to-link-to-part-of-the-same-document-in-markdown](https://stackoverflow.com/questions/2822089/how-to-link-to-part-of-the-same-document-in-markdown)
[16] [https://stackoverflow.com/questions/27981247/github-markdown-same-page-link](https://stackoverflow.com/questions/27981247/github-markdown-same-page-link)
[17] [https://github.com/BoostIO/BoostNote-Legacy/issues/2539](https://github.com/BoostIO/BoostNote-Legacy/issues/2539)
[18] [https://cghlewis.github.io/mpsi-data-training/training_3.html](https://cghlewis.github.io/mpsi-data-training/training_3.html)
