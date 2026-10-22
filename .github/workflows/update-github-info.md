---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
engine:
  id: copilot
  copilot-sdk: true
permissions:
  contents: read
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
network:
  allowed:
    - defaults
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    reviewers: [mona]
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub info

Keep `site/content/github-info.md` current and propose the change as a pull request for Mona to review.

1. Use the GitHub repository API tools (not terminal, CLI, or shell commands) to read `notes/mona-notes.md` and any other repository guidance or reference files you need.
2. Use web fetch to read these public pages:
   - https://github.blog/latest/
   - https://github.blog/changelog/
3. Update only `site/content/github-info.md` with accurate, concise information supported by those sources and guided by Mona's notes.
4. If nothing meaningful has changed, call `noop` with a short reason.
5. Otherwise open one pull request via the `create-pull-request` safe output, describing what changed and why, for Mona to review. Never write directly to `main`.
