# Repository Guidelines

## Project Structure & Module Organization

This repository is a Docsify-powered collection of Markdown notes. Most top-level directories group notes by book or subject, such as `CodeComplete/`, `CleanCode/`, `WORK/`, and `share/`. Numbered book chapters follow the pattern `CodeComplete/1.欢迎来到软件构建的世界.md`. Monthly notes live in `monthly_work_exp/` and use `YYYYMM.md` names. Store images beside their related content in an `assets/` subdirectory (for example, `share/assets/`).

`README.md` is the site homepage, while `SUMMARY.md` defines the Docsify sidebar. Site configuration is in `index.html`; vendored scripts and styles are under `guide/`.

## Build, Test, and Development Commands

The site has no build step or committed dependency manifest. Preview it from the repository root:

- `docsify serve .` — starts the Docsify development server (also used by `startServe.bat`).
- `python3 -m http.server 3000` — provides a simple static preview when Docsify CLI is unavailable.
- `git diff --check` — catches whitespace errors before committing.
- `git status --short` — confirms that only intended notes and assets changed.

Open the reported local URL and navigate through each changed sidebar entry and relative link.

## Writing Style & Naming Conventions

Write Markdown in UTF-8 with LF line endings. Preserve the language and terminology of the surrounding note. Use descriptive headings, fenced code blocks with language tags, and repository-relative links such as `[标题](CodeComplete/1.欢迎来到软件构建的世界.md)`. Paths are case-sensitive after deployment.

Follow `.editorconfig`: JSON and YAML use two spaces; Markdown may retain intentional trailing spaces and need not end with a final newline. Keep HTML and JavaScript formatting consistent with the existing four-space style. Add new sidebar-visible notes to `SUMMARY.md` in the appropriate section.

## Testing Guidelines

There is no automated test framework or coverage requirement. Validate documentation changes by previewing the site, checking headings and code rendering, opening new links and images, and testing search/sidebar navigation when relevant. For `index.html`, `pwa.js`, or `guide/` changes, check the browser console at desktop and narrow viewport sizes.

## Commit & Pull Request Guidelines

Recent commits use short, topic-first summaries in Chinese or English, for example `代码大全更新` and `update Fraxure`. Keep each commit focused and name the affected subject or month. Pull requests should summarize changed sections, explain structural or navigation updates, list manual checks performed, and link an issue when one exists. Include screenshots only for visible theme, layout, or image changes.
