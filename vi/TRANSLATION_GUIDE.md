# EN → VI Translation Guide

Conventions for translating a section folder from `eng/` to `vi/` in this repo.
Paste this into a new session together with: "Translate `eng/<folder>` into `vi/<folder>`
following this guide. Refer to already-translated files in `vi/` for tone."

---

## 1. Scope & workflow

- **Source:** `eng/<N>. <Section Name>/` — one `.md` per question + `00. Section Navigator.md`.
- **Target:** `vi/<n>.<kebab-section-name>/` — filenames usually already exist (they start
  as untranslated copies of the English). Translate **in place**, keeping the exact filename.
- **If the `vi/` folder was NOT renamed yet** (still `vi/<N>. <Section Name>/` with
  `NN. Title.md` files, as section 5 arrived): rename first, matching the sibling sections.
  - Folder → `vi/<n>.<kebab-section-name>/` (number, dot, no space; kebab of the English
    section name: `5. Spring Spring Boot` → `5.spring-spring-boot`).
  - Files → `<n>.<short-topic-kebab>.md` — number **without** leading zero, name is a
    concise kebab of the question's topic (drop "What is / How to / Difference between"
    where it reads fine; keep it where it doesn't — cf. `4.when-use-arraylist-vs-linkedlist.md`).
    `00. Section Navigator.md` → `0.section-navigator.md`.
  - These copies are **untracked in git** — use plain `mv`, not `git mv`.
  - Then update the navigator's table links to the new filenames.
- Work **one file at a time**. For each: read the English source, overwrite the VI file
  with the translation.
- A VI file whose byte size still equals the English source is an untranslated copy —
  those are the ones left to do.
- **Never omit content.** Every section, paragraph, list item, table row, code block,
  diagram, and note in the source must appear in the translation.
- Preserve all structure: `---` separators, heading levels, table columns, list nesting,
  blank lines, emoji (✅ ❌ ⚠️).

## 2. Title (first line)

Keep the English H1, append the Vietnamese translation in parentheses:

```
# What is stored in Heap? (Những gì được lưu trữ trong Heap?)
```

Keep the `?` in both. If the English title has a parenthetical already
(e.g. `What is Old Generation (Tenured)?`), keep it and still append the VI gloss:
`# What is Old Generation (Tenured)? (Old Generation (Tenured) là gì?)`

## 3. Headings

- **Keep the level markers verbatim in English, emoji and all** — copy exactly what the
  source uses. Some sections write `## Junior Level` / `## Middle Level` / `## Senior Level`
  / `## Interview Cheat Sheet`; others write `## 🟢 Junior Level` / `## 🟡 Middle Level` /
  `## 🔴 Senior Level` / `## 🎯 Interview Cheat Sheet`. Match the source file's style.
  Emoji-prefixed subsection markers elsewhere (`## 📋 …`, `## 🗺️ …`) keep the emoji and
  translate the text after it.
- **Keep verbatim in English:** `### Best Practices`, and any heading that is just a
  technical term (`### SATB (Snapshot-At-The-Beginning)`, `### Load Reference Barriers`,
  `### JIT Deoptimization`, `### ExplicitGCInvokedConcurrent`).
- `### Senior Summary` **or** `### Summary for Senior` (sections vary) → `### Tóm tắt cho Senior`.
- **Translate:** descriptive headings — `### Common mistakes` → `### Các lỗi thường gặp`,
  `### Why not Reference Counting?` → `### Tại sao không dùng Reference Counting?`.
  You may keep the English term inside a translated heading
  (`### Cơ chế Safepoint Polling`, `### Sự nguy hiểm của Dump`).
- `## Interview Cheat Sheet` → `## Tóm tắt phỏng vấn (Interview Cheat Sheet)`
- `### Senior Summary` → `### Tóm tắt cho Senior`

## 4. Technical terms — DO NOT translate

Leave in English: Heap, Stack, GC, Garbage Collection, Young/Old Generation, Eden,
Survivor, Metaspace, PermGen, TLAB, PLAB, Escape Analysis, Scalar Replacement,
Compressed OOPs, Virtual Threads, Stop-The-World / STW, Safepoint, Card Table,
Write/Load Barrier, SATB, G1, ZGC, Shenandoah, Minor/Major/Full GC, Mixed GC,
Humongous, RSet, CSet, IHOP, Allocation Stall, Evacuation, `OutOfMemoryError`,
`StackOverflowError`, heap dump, thread dump, GC roots, reachability, Strong/Soft/Weak/
Phantom reference, Cleaner, finalize, JIT, JNI, NMT, JFR, throughput, latency, footprint,
Reachability Analysis, Reference Counting, Dominator Tree, class loader, deadlock,
anti-pattern, benchmark, container, etc. Also: JVM flags (`-Xmx`, `-XX:+UseZGC`, …),
class/method/API names, code identifiers, log strings, tool names (jcmd, jmap, MAT, Arthas).

**On first use in a file**, add a short Vietnamese gloss in parentheses:

```
Memory Leak (rò rỉ bộ nhớ) — …
throughput (thông lượng)
latency (độ trễ)
reachability (khả năng tiếp cận)
Premature Promotion (thăng cấp sớm)
dangling pointer (con trỏ treo)
```

After the first gloss, use the bare English term for the rest of the file.
Don't force a gloss where it adds nothing (Heap, Stack, GC, cache, buffer are fine bare).

## 5. Code blocks

- **Code itself:** unchanged (identifiers, keywords, flags, string literals stay as-is).
- **Comments** (`//`, `#`) and **prose inside ``` fenced diagrams**: translate to Vietnamese.
  ```java
  int a = 5;         // Stack
  methodB();         // Frame mới trên stack
  ```
- **ASCII box diagrams:** translate the descriptive labels, keep the structure name.
  `│ Local Variable Table │` stays; `│ For computations: push, pop │` →
  `│ Cho các phép tính: push, pop │`.
- `# Output:` / `# Đầu ra:` — either is fine; match nearby translated files.
- Keep language hints (` ```java `, ` ```bash `, ` ```sql `).

## 6. Wiki-links (`[[...]]`)

Keep the link target **exactly** as the English (they point to English note names),
then append a Vietnamese gloss in parentheses after the closing `]]`:

```
- [[4. What is Garbage Collection]] (Garbage Collection là gì)
- [[16. What is stop-the-world]] (Stop-the-world là gì)
```

Some sections' links have no number prefix (`[[What is Deque]]`) — keep whatever form the
source uses, still append the gloss: `[[What is Deque]] (Deque là gì)`.
This matches the Section Navigator. Do not renumber or rename targets.

## 7. Standard label translations (Cheat Sheet & body)

| English | Vietnamese |
|---|---|
| **Must know:** | **Cần phải biết:** |
| **Common follow-up questions:** | **Các câu hỏi phụ thường gặp:** |
| **Red flags (DO NOT say):** | **Dấu hiệu cảnh báo (Red flags — KHÔNG nên nói):** |
| **Related topics:** | **Các chủ đề liên quan:** |
| **Simple analogy:** | **Ví dụ minh họa đơn giản:** |
| **Example:** | **Ví dụ:** |
| **Why it's needed:** | **Tại sao cần đến nó:** |
| **Symptoms:** | **Triệu chứng:** |
| **Solution:** / **Solutions:** | **Giải pháp:** |
| **Cause:** / **Causes:** | **Nguyên nhân:** |
| Production Experience | Kinh nghiệm Production |
| Real scenario | Tình huống thực tế |
| When NOT to use … | Khi nào KHÔNG nên dùng … |
| Diagnostics | Chẩn đoán |
| Terms: | Các thuật ngữ: |

## 8. Recurring phrase choices (house style)

- "next collection / next cycle" → **"lần thu gom tiếp theo" / "chu kỳ tiếp theo"**
  (use *tiếp theo*, not *kế tiếp*).
- "reference" (the OOP sense) → **tham chiếu**; "normal/plain reference" →
  **"tham chiếu thông thường"**.
- "unreachable" → **"không thể tiếp cận (được)"**.
- "live objects" → **"các đối tượng còn sống"**; "dead" → **"đã chết"**.
- "leak" (short) → **"rò rỉ"**; first mention **"rò rỉ bộ nhớ"**.
- "overhead" → keep **overhead** or use **"chi phí"** — match surrounding file.
- "pause(s)" → **"khoảng dừng"**; "pauses < 1 ms" → **"khoảng dừng < 1 ms"**.
- "thread" → **"luồng"**; "thread pool" stays **thread pool**.
- "static field/collection" → **"trường/collection tĩnh"** (keep *collection*).
- "by value / by reference" → **"theo giá trị / theo tham chiếu"**.
- Bullet imperatives keep an encouraging **"hãy"** where the English is directive
  ("Avoid deep recursion" → "Tránh đệ quy sâu" / "hãy dùng vòng lặp").
- Keep numbers/units exactly (`~2 KB`, `32 GB`, `1-2 ns`, `5-15%`).

## 9. Section Navigator file

`00. Section Navigator.md` → `0.section-navigator.md`. Special cases:

- The table of questions: translate the question text, keep the relative `.md` links
  and the numbering (repoint links to the new kebab filenames if you renamed the files);
  the difficulty column header ("Difficulty Level" / "Difficulty" → "Độ khó"). Keep `⭐`
  values as-is; if the source spells them as words ("One star" / "Two stars" / "Three
  stars", as section 5 did) normalise to `⭐` / `⭐⭐` / `⭐⭐⭐` to match the sibling
  sections; leave the cell blank if the source is blank.
- The English navigator may itself be an untranslated copy even when its file timestamp
  is newer than the sibling question files (a rename bumps the mtime). Check the content,
  not the date.
- ASCII dependency map: translate the category labels and short descriptions,
  keep the `Q1`, `Q13` shorthands and the box drawing.
- Learning-path tables: translate headers ("Bước", "Chủ đề", "Mục tiêu") and cell prose;
  keep `Q#` refs and technical keyword lists (Region, RSet, CSet, …).
- "File format" / structure description at the bottom: translate fully.

## 10. Don't

- Don't translate identifiers, flags, API names, log strings, tool names.
- Don't drop the "9 hours", edge-case notes, ⚠️ warnings, or "Real scenario" stories.
- Don't renumber or re-target `[[wiki-links]]`.
- Don't change the English `## Junior/Middle/Senior Level` headings.
- Don't add commentary that isn't in the source.

---

## Quick checklist per file

- [ ] H1 = `English? (Tiếng Việt?)`
- [ ] `## Junior/Middle/Senior Level` untouched
- [ ] All prose in Vietnamese; technical terms English + first-use gloss
- [ ] Code unchanged; comments & diagram text translated
- [ ] Cheat-sheet labels use the standard translations (§7)
- [ ] `## Tóm tắt phỏng vấn (Interview Cheat Sheet)` present
- [ ] `[[links]]` unchanged + `(gloss)` appended
- [ ] Nothing omitted; `---`, tables, emoji preserved
