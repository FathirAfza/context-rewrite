---
name: context-rewrite
description: Clean up "slop" (generic, padded, template-like filler) and fix context mismatches in a draft — esai, KTI/LKTI, laporan, proposal, tugas, in Indonesian or English — by grounding every claim in facts the user actually provides, then running targeted correction passes for any small mistakes that remain. Use this whenever the user says a draft is "terlalu umum", "slop", "ngambang", "nggak nyambung sama konteks", asks to "rapikan", "perbaiki", or "parafrasa ulang biar sesuai konteks", wants to rebuild a text through question-and-answer so it reflects their own understanding, or asks for another pass to fix remaining "mini mistake" after an earlier rewrite. Not for removing watermarks, disguising AI authorship, or beating AI detectors; for checking the user's own writing against detector false positives, use ai-detector-risk-check instead.
---

# Context Rewrite

Slop happens when a text has no real context behind it, so whoever wrote it (often an AI) fills the gap with phrases that sound fine but say nothing. Swapping synonyms doesn't fix that. What fixes it is supplying the missing context and cutting what has no content. This skill does both, with the user as the source of truth, and then checks its own work in small targeted passes.

## Principles

**The user is the source of facts.** Never invent numbers, names, sources, results, dates, or experiences. When something is missing, ask for it or leave a visible marker like `[perlu data: jumlah responden]`. A fabricated specific is worse than an honest generic sentence: it looks credible, and it falls apart the moment a teacher or judge asks about it.

**Edit minimally.** Leave sentences that are accurate and clear alone. Rewriting everything causes meaning drift and tends to introduce new slop, so change only what has a real problem.

**Keep the writer's voice.** Match the register and vocabulary of what the user wrote themselves, or of their answers in interview mode. Don't upgrade their text into polished generic prose; that is its own kind of slop.

**Improve quality, not concealment.** This skill makes text more accurate, specific, and clear. It does not strip watermarks, tune text against detector metrics such as perplexity or burstiness, or make AI-generated text pass as human-written. If the user asks for that, decline that part in a sentence and offer Mode B instead. If the text is headed for a school task or competition, mention once, in one sentence, that they should check the rules on AI assistance and disclosure; don't repeat it in later turns.

## Choose a mode

- **Mode A — Bersihkan & sesuaikan.** The user has a draft plus some context (purpose, audience, data). Clean it and align it to that context.
- **Mode B — Tulis ulang lewat tanya jawab.** The user wants the text rebuilt from their own understanding, or the draft is so generic that cleaning won't help (most sentences have no concrete content to keep).

If unclear, start with Mode A. Suggest Mode B when more than half the problem spots need facts the user hasn't given.

## Mode A process

1. **Collect draft and context.** Context means: tujuan tulisan, pembaca atau juri, data/sumber/fakta asli, and constraints (length, format, competition guidelines). If the draft arrives without context and the problems are about content, ask for these in one short message (at most four questions) before rewriting. If the problems are purely stylistic, proceed without asking.

2. **Scan and classify each problem spot** using the Slop patterns section below. Content problems come first because they matter more:
   - **Kosong** — a generic claim that would fit any topic, padding, or an empty closing sentence.
   - **Meleset konteks** — ignores or contradicts the given context, answers a different question, or targets the wrong scope or audience.
   - **Klaim tanpa dasar** — a number, source, result, or superlative the user's data doesn't support.
   - **Gaya template** — contrast templates, forced triads, stock words, formulaic transitions, uniform rhythm.

   One occurrence of a style pattern is rarely a problem; repetition is. Don't flag every "selain itu".

3. **Fix per spot.**
   - Kosong → reduce it to its core claim. If there is no core, delete it. If there is, fill it with the user's details.
   - Meleset konteks → realign with the context. If the context lacks what's needed, ask.
   - Klaim tanpa dasar → replace with the user's data, scale it down to what's supported, or mark `[perlu data: ...]`.
   - Gaya template → say it directly, keep only the list items that matter, drop the stock words.

4. **Present the result** in the output format below.

## Mode B process

1. **Split the target text into sections** (for example latar belakang, rumusan masalah, solusi, metode, hasil, kesimpulan), or use the user's own outline.
2. **Ask 2–4 concrete questions per section, one section at a time.** Ask what only the writer knows: why this problem, what they actually observed or measured, how their solution works step by step, what is still weak or untested. Don't ask questions whose natural answer is pasting in AI-generated text.
3. **Build the section from the answers.** Keep their phrasing where it's already clear; fix grammar, order, and transitions; add no claims they didn't make.
4. **Show the section and ask for corrections** before moving to the next one.

## Correction pass (putaran koreksi)

Run this after Mode A or B, or whenever the user says "masih ada mini mistake".

1. **Re-read the revised text against the user's context and answers.** Check for leftover slop, open `[perlu data]` markers, claims that can't be traced to the user's input, drift from the original meaning, template patterns introduced by the rewrite itself, and grammar or EYD errors.
2. **Fix only the flagged sentences.** Don't regenerate the whole text; every full rewrite is a new chance for errors and drift.
3. **Show each fix as sebelum → sesudah** with a few words on why.
4. **Stop when nothing substantive remains**, and say so plainly instead of inventing edits. Two passes are usually enough. If the same kinds of issues keep coming back, the cause is almost always missing context, so ask for it rather than polishing again.

## Output format (Mode A)

1. **Temuan** — each problem spot: quoted original, category, one-line reason. Group repeated patterns instead of listing every instance.
2. **Data yang dibutuhkan** — questions for missing facts (skip if none).
3. **Revisi** — for short texts (about three paragraphs or less), the full revised text. For longer texts, per-spot sebelum → sesudah, then offer the full version.
4. **Catatan** — open `[perlu data]` markers and anything the user should verify against sources.

Respond in the user's language (default Indonesian). Keep the write-up short; the response itself shouldn't contain the patterns it removes.

## Example

Context from the user: esai tentang bank sampah sekolah; 120 siswa ikut; sekitar 45 kg sampah plastik terkumpul per bulan.

**Sebelum:** "Di era modern ini, bank sampah tidak hanya menjadi solusi pengelolaan sampah, tetapi juga sarana edukasi, pemberdayaan, dan inovasi yang sangat krusial bagi generasi muda."

**Temuan:** Kosong + gaya template — pembuka klise, kontras "tidak hanya… tetapi juga", triad, "sangat krusial"; tidak ada satu fakta pun tentang bank sampah yang dibahas.

**Sesudah:** "Sejak dibuka, bank sampah sekolah kami diikuti 120 siswa dan mengumpulkan sekitar 45 kg sampah plastik setiap bulan."

Without those numbers from the user, the honest version would be: "Bank sampah sekolah kami mengajak siswa memilah sampah plastik sejak [perlu data: kapan dimulai]."

## Slop patterns

Use this as a checklist, not a blacklist: one occurrence is usually fine; density and repetition are the problem.

### A. Content-level patterns (check these first)

- **A1. Generic claims** — a sentence that would fit any topic unchanged. ID: "Teknologi memiliki peran penting dalam berbagai aspek kehidupan." EN: "This plays a vital role in many aspects of society." Fix: ask "peran apa, untuk siapa, buktinya apa?" and fill from the user's facts, or delete.
- **A2. Inflated significance** — ID: "sangat revolusioner", "mengubah segalanya", "solusi paling efektif". EN: "groundbreaking", "game-changing", "transformative". Fix: replace with a measurable claim, or scale down to what the data supports.
- **A3. Vague attribution** — ID: "Banyak ahli berpendapat…", "Penelitian menunjukkan…" (tanpa sumber). EN: "Experts agree…", "Studies show…". Fix: name the source the user actually used, or mark `[perlu data: sumber]`.
- **A4. Fake precision** — numbers, percentages, or years with no source in the user's material. Fix: never keep an unsourced number; ask, or remove it.
- **A5. Empty closers** — ID: "Dengan demikian, dapat disimpulkan bahwa hal ini sangat penting." EN: "In conclusion, this highlights the importance of…". Fix: replace with the actual finding or next step, or delete if the paragraph already made the point.
- **A6. Context drift** — answers a broader or different question than the one the text is about, targets the wrong audience (e.g., explaining basics to expert judges), or wanders into unrelated benefits. Fix: cut back to the stated purpose and audience.

### B. Style-level patterns

- **B1. Cliché openers** — ID: "Di era digital saat ini…", "Seiring perkembangan zaman…", "Dalam dunia yang terus berkembang…". EN: "In today's fast-paced world…", "In an era of…". Fix: start with the specific subject or problem.
- **B2. Contrast templates** — ID: "tidak hanya X, tetapi juga Y", "bukan sekadar X, melainkan Y". EN: "not just X, but Y", "isn't merely A — it's B". Fix: state both points plainly, or keep only the one that matters.
- **B3. Forced triads** — ID: "cepat, efisien, dan andal"; "edukasi, pemberdayaan, dan inovasi". EN: "fast, reliable, and scalable". Fix: keep the items that are actually supported; two or four is fine.
- **B4. Stock vocabulary** — ID: krusial, signifikan, komprehensif, holistik, optimal, "memainkan peran penting", "menjadi kunci", "lanskap" (metaforis), "menavigasi" (metaforis). EN: delve, landscape, pivotal, robust, seamless, leverage, foster, underscore, tapestry, realm. Fix: use the plain word, or the concrete thing it stands for.
- **B5. Formulaic transitions** — ID: "Selain itu,", "Lebih lanjut,", "Di sisi lain,", "Oleh karena itu," opening most paragraphs. EN: "Moreover,", "Furthermore,", "Additionally,". Fix: drop most of them; order the ideas so the link is obvious.
- **B6. Hedging reflexes** — ID: "Penting untuk dicatat bahwa…", "Perlu diingat bahwa…". EN: "It's important to note that…", "It's worth mentioning…". Fix: delete the hedge and state the point.
- **B7. Uniform rhythm and structure** — every paragraph the same length, every sentence roughly the same length, every section following the same mini-template (claim, explanation, restatement). Fix: combine or split sentences where it helps meaning; let paragraphs be as long as their content needs.
- **B8. Over-formatting** — bold labels on every point, bullet lists for what should be prose, heavy dash use. Fix: use the format the document type calls for (a KTI or essay is mostly paragraphs).
