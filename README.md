# Needlessly Verbose JLPT N1

普段の文章や会話を、JLPT N1 レベルの言い回しに変換して学べるアプリ。

The app helps learners turn plain Japanese sentences, casual conversations, and selected article excerpts into more advanced N1-style Japanese, then study what changed and why.

## Product Direction

This is a small learning app built with Nuxt 4 and Nuxt UI. The first target audience is Taiwanese learners of Japanese, but the product should stay flexible enough to support English-speaking learners and other language backgrounds later.

The tone is intentionally playful: a stereotyped Japanese-style website layout for fun, while keeping the actual learning interface practical and easy to scan.

## Core Learning Flow

1. The learner enters an everyday Japanese sentence, conversation snippet, or chooses a supported reading source.
2. The app transforms the text into JLPT N1-style Japanese while preserving the original meaning.
3. The learner compares:
   - original sentence
   - transformed N1-style sentence
   - changed grammar, vocabulary, tone, and register
4. The explanation panel teaches the N1 grammar and vocabulary used in the transformation.
5. The learner practices with generated questions based on the same source text.
6. Useful sentences, grammar points, and mistakes can be bookmarked and reviewed later.

## Learning Features

- Sentence-by-sentence comparison between original and transformed text.
- Highlighted differences for grammar, vocabulary, idioms, and sentence structure.
- Explanation corner based on curated JLPT N1 grammar and vocabulary references.
- Bookmarks for useful expressions and difficult grammar.
- Review queue for saved items and past mistakes.
- Active reminders or notifications asking learners to revise.
- Practice questions generated from the source:
  - JLPT-style 4-option grammar questions
  - vocabulary replacement questions
  - sentence ordering questions
  - "choose the closest meaning" questions

## Reference Data

The app should keep two first-class reference collections:

- JLPT N1 grammar patterns
- JLPT N1 vocabulary and expressions

Each transformed sentence should link back to these references whenever possible, so the explanation is not just "AI says so". The reference entries should be structured enough to support:

- Japanese grammar point
- reading
- Traditional Chinese explanation
- optional English explanation
- example sentences
- nuance and usage notes
- common mistakes
- source or license metadata

## Default Reading Sources

Default source options should be treated as learner shortcuts, not as permission to copy whole articles. Before implementing ingestion for any source, check robots.txt, terms of service, copyright rules, and whether excerpts are allowed.

Candidate default sources:

- NHK NEWS WEB
- NHK NEWS WEB EASY
- Yahoo!ニュース
- 朝日新聞デジタル
- 毎日新聞
- 読売新聞オンライン
- 日本経済新聞
- ITmedia
- 5ちゃんねる-style forums or public thread sources
- common SNS posts, when provided by the learner or available through allowed APIs

Safer first version:

- Let learners paste text or a URL.
- Fetch only when allowed.
- Store source URL, title, author/publisher when available, timestamp, and a content hash.
- Avoid republishing full copyrighted articles.
- Prefer short excerpts for study.
- Cache transformations by content hash so multiple learners can reuse the same learning result when legally safe.

## LLM Transformation Strategy

The transformation should be lazy and cost-aware.

- Do not transform every source article in advance.
- Transform only when a learner requests a sentence, paragraph, or article excerpt.
- Split long content into small chunks.
- Show estimated token cost before paid transformations.
- Cache successful transformations by:
  - source content hash
  - source URL
  - learner explanation language
  - reference data version
  - model and prompt version
- Reuse cached transformations across learners when the source policy allows it.
- Keep the free tier focused on short sentence conversion and limited daily reading.

Transformation quality rules:

- Preserve the original meaning.
- Mark when the transformed sentence becomes more formal, literary, indirect, or news-like.
- Avoid pretending that every advanced phrase is always better.
- Explain why the N1 expression fits the context.
- Keep the original sentence available at all times.

## Cost And Payment Model

The app should support a small free tier plus token-based paid usage for enthusiastic learners.

Possible model:

- Free users get limited daily transformations.
- Registered users get bookmarks, review history, and cached article access.
- Paid users can transform longer articles or custom sources.
- Paid transformation price is calculated from estimated input and output tokens.
- The UI should show:
  - estimated token usage
  - estimated price
  - whether a cached transformation already exists

Important implementation note: never expose provider API keys to the browser. LLM calls should go through server routes.

## UI Direction

Use a stereotyped Japanese-style layout, but keep it usable.

Ideas:

- red and white base palette with restrained dark ink text
- simple header inspired by 暖簾
- stamp-like logo mark
- subtle 和紙 texture or paper-like background
- section labels that feel like 駅名標 or お品書き
- vertical accent text for decorative headings where it does not hurt readability
- compact study dashboard instead of a marketing-heavy landing page

Primary screens:

- Home / transform workspace
- Source selection
- Sentence comparison
- Grammar and vocabulary explanation
- Practice questions
- Bookmarks
- Review queue
- Settings for explanation language
- Payment / token balance

## Tech Stack

- Nuxt 4
- Nuxt UI
- TypeScript
- ESLint
- Tailwind CSS
- pnpm

## Setup

Install dependencies:

```bash
pnpm install
```

Start the development server:

```bash
pnpm dev
```

Run lint:

```bash
pnpm lint
```

Run typecheck:

```bash
pnpm typecheck
```

Build for production:

```bash
pnpm build
```

Preview the production build:

```bash
pnpm preview
```

## Planning

Implementation milestones and TODOs live in [docs/IMPLEMENTATION_PLAN.md](docs/IMPLEMENTATION_PLAN.md).

## Working Name Ideas

- Needlessly Verbose JLPT N1
- やたらN1
- N1っぽくして
- 文豪化ドリル
- N1言い換え道場
