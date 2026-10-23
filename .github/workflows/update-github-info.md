---
name: update-github-info
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
tools:
  github:
    toolsets: [repos]
  web-fetch:
  edit: true
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    title-prefix: "Update GitHub info: "
---

# Update GitHub Info

Keep the GitHub Info section of Mona's website current with concise, practical updates from official GitHub sources.

1. Read `notes/mona-notes.md` and `site/content/github-info.md`.
2. Use the web-fetch tool to fetch `https://github.blog/latest/` and `https://github.blog/changelog/`.
3. Read external public guidance with web-fetch when needed to understand the fetched source content, and use GitHub repository API tools for repository guidance or reference files rather than terminal, CLI, or sandboxed commands.
4. Select only useful recent items for developers. Keep summaries short and practical, match the existing editorial angle, and identify whether each update came from the GitHub Blog or GitHub Changelog.
5. Use the edit tool to update `site/content/github-info.md`. Preserve its existing structure and avoid unrelated changes.
6. Propose the changes with the `create-pull-request` safe output for Mona to review. Do not write directly to the default branch.