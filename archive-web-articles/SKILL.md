---
name: archive-web-articles
description: Archive user-supplied news, magazine, and blog article URLs as clean Obsidian-compatible Markdown with local article images and optional inline-playable audio. Use when the user asks to crawl, save, download, organize, batch, number, or repair web articles and their media. Use the signed-in browser for pages that require the user's existing access. Do not use for converting EPUB, PDF, DOCX, or book-length source files.
---

# Archive Web Articles

Archive only content the user can access. Prefer the user's signed-in Chrome session when requested or when a page requires authentication. Preserve article meaning and reading order; do not invent missing text, metadata, rubrics, images, or audio.

## Resolve the output layout

Apply the newest explicit user instruction over older defaults.

Default output root:

`/Users/echo/Downloads/输出/文章`

For an ordinary link, create one folder per article:

```text
文章/
└── Article Title/
    ├── Article Title.md
    └── asset/
        ├── cover.jpg
        ├── image-02.jpg
        └── audio.mp3
```

When the user asks for multiple articles in one named project folder, put the Markdown files in that folder and share one `asset/` directory. Number files in the exact order supplied, using zero-padded prefixes:

```text
Project/
├── 01 Article Title.md
├── 02 Article Title.md
└── asset/
    ├── 01-cover.jpg
    ├── 01-audio.mp3
    └── 02-cover.jpg
```

Prefix every image and audio filename with the same article number in a shared batch. Sanitize filesystem-forbidden characters while keeping human-readable titles. Keep only one cover-image format and make the extension match the actual file type.

## Capture the article

1. Open each URL in Chrome in the order supplied and wait for the article to finish loading.
2. Capture the exact title, subtitle or deck, publication, first-level section, secondary rubric or column, publication date, article body, body subheadings, captions, blockquotes, footnotes, corrections, and editorial notes that belong to the article.
3. Determine the secondary rubric from the article header or page metadata, not from a print-edition teaser or a guessed topic. Verify named columns such as `Schumpeter`, `Lexington`, `Charlemagne`, `Bello`, `Bagehot`, `Bartleby`, `Back Story`, and `Free exchange` when present.
4. Remove navigation, footer material, advertisements, subscription prompts, newsletters, share controls, recommendations, related stories, teaser cards, and reading-time labels such as “5 min read”.
5. Repair extraction artifacts such as detached drop caps, broken paragraph joins, duplicated lines, and obvious casing damage to acronyms or proper names. Do not rewrite the author's prose.
6. Preserve meaningful inline links when practical. Always include a link to the original article.

## Write the Markdown

Use the source site's spelling and capitalization. For Economist articles, format the primary section name in red; leave other publications' section styling at the default unless the user asks otherwise.

```markdown
# Article Title

> Subtitle or deck

**The Economist · <span style="color:#E3120B">Leaders</span> · Masters of the universe**  
*October 3, 2019* · [Original article](https://example.com/article)

![Cover](asset/01-cover.jpg)

<audio controls preload="metadata" src="asset/01-audio.mp3">
Your browser does not support the audio element.
</audio>

First paragraph of the article…
```

Omit the subtitle line, secondary rubric, cover, or audio player when the source lacks that item. Place `[Original article](URL)` immediately after the date. Do not add an `Audio` heading. Do not add a horizontal rule between the media and the article body. Preserve an article-end divider only when it separates an original print note, correction, or comparable source note.

## Save images and audio

- Download only images that belong to the article: the lead image and meaningful body illustrations or photographs. Exclude logos, icons, ads, trackers, avatars, and recommendation thumbnails.
- Store all media in `asset/` and insert each image near its original position in the article. Use concise alt text based on its caption or subject.
- If a downloadable article narration or podcast MP3 exists, save it in `asset/` and embed it with the HTML `<audio controls>` element so it plays directly from the Markdown preview.
- Do not Base64-embed audio inside the Markdown. It makes the file very large, slows editors and sync, and reduces compatibility.
- If local audio download is unavailable but the source provides a stable direct media URL that plays inline, preserve an inline player only when it works in the target preview. Otherwise omit audio and report the limitation.
- Never create an empty audio section or pretend that an audio file was downloaded.

## Validate before finishing

Check every article, not just the first:

- Markdown filenames and asset prefixes match the supplied link order.
- The title, date, primary section, and true secondary rubric match the source.
- The body is complete and in source order, without promotional residue or reading-time text.
- Every relative image and audio reference resolves to an existing file.
- Each image opens successfully and its extension matches its content.
- Each saved MP3 is non-empty and decodable.
- No unwanted `Audio` heading or media/body divider remains.
- Existing unrelated output is untouched.

Report the final output directory, the article count, and any unavailable image or audio assets. If access to an article is blocked, identify that article instead of silently producing an incomplete archive.
