# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A content repository — 500+ Java backend interview questions with layered answers, written as Markdown. There is no application to build; the only executable code is two Python site generators. Work here is almost entirely **writing and translating Markdown**.

## Layout

- `eng/` — canonical English source. One folder per topic: `N. Section Name/`, containing `00. Section Navigator.md` plus one `NN. Question Title.md` per question.
- `ru/`, `ua/` — Russian / Ukrainian translations, mirroring `eng/`'s folder and file names (only the prose differs).
- `vi/` — Vietnamese translation, **in progress**. Uses a different naming scheme (see below). Governed by `vi/TRANSLATION_GUIDE.md`.
- `docs/` — Jekyll site source. `docs/questions/`, `docs/ru/questions/`, `docs/uk/questions/` are **generated** (git-ignored) — never edit them by hand.
- `scripts/` — `generate_site_pages.py` (builds the per-question site pages from `eng/`, `ru/`, `ua/`), `generate_social_preview.py` (OG images).
- `.github/workflows/pages.yml` — CI: runs `generate_site_pages.py`, then Jekyll build + deploy on push to `master`.

`vi/` is **not** wired into the site generator (`LANGUAGES` in `generate_site_pages.py` covers only `eng`/`ru`/`ua`); it currently lives only in the repo.

## Commands

```bash
python scripts/generate_site_pages.py       # regenerate docs/**/questions/ from source Markdown (same as CI)
python scripts/generate_social_preview.py   # regenerate social-preview images
```

No build, lint, or test step for content. `generate_site_pages.py` takes no arguments and writes into `docs/`.

## Answer file structure (all languages)

Every question file follows the same shape, and translations must preserve it exactly:

- H1 title ending in `?`
- Three level sections — `## Junior Level`, `## Middle Level`, `## Senior Level` (some sections prefix them with `🟢`/`🟡`/`🔴`; match the source file)
- `## Interview Cheat Sheet` (or `## 🎯 Interview Cheat Sheet`) with fixed sub-labels: Must know / Common follow-up questions / Red flags (DO NOT say) / Related topics
- `---` separators, tables, code blocks, ASCII diagrams, emoji, and `[[wiki-links]]` that point to other questions by their English note name

The Section Navigator (`00. Section Navigator.md` / `0.section-navigator.md`) additionally has a questions table with per-file links, an ASCII topic-dependency map, learning-path tables, and a "what to know per level" cheat sheet.

## Vietnamese translation workflow

`vi/TRANSLATION_GUIDE.md` is the authority — read it before translating. Key points:

- **Folder/file renaming**: `vi/` uses kebab-case, not the English `N. Section Name/` scheme. `eng/5. Spring Spring Boot/` → `vi/5.spring-spring-boot/`; `07. What is the equals() and hashCode() Contract.md` → `7.equals-hashcode-contract.md` (number without leading zero, concise kebab topic); `00. Section Navigator.md` → `0.section-navigator.md`. Sections 1–10 are already renamed + translated; **11–20 are still untranslated English copies under the old `vi/N. Section Name/` naming**.
- These `vi/` copies are **untracked in git** until a section is committed — rename with plain `mv`, never `git mv`.
- Translate **one file at a time**; overwrite the VI file with the full translation. A VI file whose byte size equals its English source is still an untranslated copy.
- **Never omit content** — every paragraph, list item, table row, code block, and diagram from the source must appear.
- **Technical terms stay in English** (Heap, GC, HashMap, `synchronized`, CAS, Stream, ForkJoinPool, flags, API names, …) with a short `(gloss tiếng Việt)` on **first use** in each file, bare English thereafter.
- **Code is unchanged**; only comments and diagram prose get translated.
- **`## Junior/Middle/Senior Level` headings are kept verbatim English**; `## Interview Cheat Sheet` → `## Tóm tắt phỏng vấn (Interview Cheat Sheet)`.
- **Wiki-links**: keep the `[[English target]]` exactly (form and numbering as in the source), append `(gloss)` after `]]`.
- Standard cheat-sheet labels have fixed Vietnamese forms (guide §7): `Cần phải biết:`, `Các câu hỏi phụ thường gặp:`, `Dấu hiệu cảnh báo (Red flags — KHÔNG nên nói):`, `Các chủ đề liên quan:`.
- After renaming files, repoint the navigator table links to the new kebab filenames.
- Per-section commit message style (see `git log`): `Add section N VI translated`.

### Post-section verification

After finishing a section, sanity-check: file count = navigator + question files; every navigator link resolves; no residual English cheat-sheet labels/headings; each question file has exactly the 3 level headings + 1 cheat-sheet heading; `---` / H2 counts match the English source on a few spot-checked files.
