# Handoff: maintaining Zihan Zhao's website

Personal academic site for Zihan Zhao (Ph.D. candidate, UC San Diego and CERN; advisor Javier Duarte). The audience is recruiters and researchers at frontier AI labs. The site's message is that he designs efficient transformers: sub-quadratic attention, long context, and fast inference.

- Live: https://javierzhao.github.io/
- Repo: `JavierZhao/JavierZhao.github.io`. It was first named `homebase`, and old remotes still redirect.
- Branch: `zihan/nice-euler-rfzfye` is the only branch, and GitHub Pages serves it from `/ (root)`. Pushes go live in about 40 to 60 seconds.
- The repo is public, and every file in it, this one included, is served by Pages. Never write anything sensitive here.
- `README.md` covers the basic "how to edit" steps for humans. This file holds the context and decisions.

## Stack

- Plain HTML and CSS: no build step, no framework, no dependencies. `.nojekyll` makes Pages serve files as they are.
- `index.html`: all content, plus a small inline script for the click-to-enlarge figure view.
- `assets/css/style.css`: design tokens are in `:root` at the top.
- `assets/fonts/`: self-hosted Inter (sans) and Newsreader (serif). Self-hosting is also why headless screenshots render the real fonts.
- `assets/figs/<id>.png`: one figure per paper.
- `assets/img/photo.jpg`: the headshot. The filename must be lowercase.
- `assets/Zihan_Zhao_CV.pdf`: the linked CV, uploaded by the user.
- SEO files:
  - `robots.txt` and `sitemap.xml`. Bump `<lastmod>` when content changes.
  - Canonical, Open Graph and JSON-LD `Person` tags in `<head>`.
  - `google76e53c55eed5025e.html`: the Google Search Console verification file. **Never delete or edit it.**

## Page structure (section order and ids)

1. **Hero:**
   - The `<h1 class="kicker">` holds the name and affiliation ("Zihan Zhao · Ph.D. Candidate, UC San Diego & CERN"). Keep the name in the `<h1>`, because it matters for name searches.
   - The one-sentence thesis is a `<p class="thesis">`, styled large.
   - Then a short bio, links (Email, CV, GitHub, LinkedIn, InspireHEP) and the photo.
2. **`#research`, "Selected work":** a `grid--2` of large cards, in this order:
   - `lclm`: Structure Before Attention
   - `phatjet`
   - `idm`
   - `pulse`
3. **`#news`:** newest first, dated by month (`<time datetime="YYYY-MM">Mon YYYY</time>`). The user supplied the months in 2026-10 and asked to drop the reviewing item; reviewing stays under Service.
4. **`#more`, "More research":** a `grid--3` of smaller cards, in this order: `moe`, `salt`, `pretrain`, `deeprepro`, `sparse`, `jjepa`, `audit`, `phi4`.
5. **`#experience`:** Futurewei and education in the left column; Toolkit, Mentoring and Service in the right.
6. **`#talks`:** six linked entries, newest first, reading down the left column and then the right.

### Card anatomy

Copy an existing card when adding a paper:

```html
<article class="card" id="short-id">
  <div class="fig"><img src="assets/figs/short-id.png" alt="Describe what the figure shows" loading="lazy"></div>
  <div class="meta"><span class="venue">VENUE</span><span class="role">Co-first author</span></div>
  <h3><a href="PAPER_URL">Title</a></h3>
  <p class="authors">A. Author*, <b>Z. Zhao*</b>, ...</p>
  <p class="sum">One or two sentences: method plus the headline number.</p>
  <div class="plinks"><a href="...">arXiv</a><a href="...">Code</a></div>
</article>
```

- Use `venue venue--review` (grey) while a paper is under review.
- `fig--pending` shows a "Figure coming soon" placeholder.

## Content decisions the user has made (keep them)

- **Selected work** is SBA, PHAT-JeT, IDM and PULSE. The user swapped PULSE in for SAL-T.
- **Structure Before Attention (SBA):**
  - Zihan is the **sole author**, and the card shows "Sole author" with no venue: the user asked to remove "ICLR 2027".
  - The full title is "Structure Before Attention: A Zero-Initialized Convolution Recovers Windowed Language-Model Quality".
  - The numbers come from the paper's abstract (2.1% vs 0.6%, within 0.16%), not from the resume.
- **Author order follows the published version** (arXiv or proceedings), with the user's own name in bold as `Z. Zhao`.
  - `*` marks equal contribution, following the user's CV: Wang, Zhao and Xia on PHAT-JeT; Wang and Zhao on SAL-T; Katel, Li and Zhao on J-JEPA; the first four authors on IDM.
  - Do not reorder authors to match the CV.
  - Roles shown: co-first author (PHAT-JeT, IDM, SAL-T, J-JEPA), first author (PULSE, Pretraining), sole author (SBA), mentored project (MoE, Audit, φ⁴).
- **MoE paper:** public on arXiv (2610.02701) since 2026-10-02, still marked "Under review · ML4PS 2026".
  - Kaushik Pendiyala, the user's mentee, is first author; Zihan is 6th of 11.
  - The card shows the full author list, arXiv and code links (github.com/kpendiyala/MPT), and the role "Mentored project".
- **Information-Loss Audit paper:** still an anonymized ML4PS 2026 submission. Show the title, figure, summary and an "Under review" label only. Host no PDF, and show no author list until the user provides one or it appears on arXiv.
- **PULSE venue** is written "CVPR 2026 Sense of Space Workshop · Oral", in the card, in Experience and in Talks.
- **Contact:** email only. Never add the phone number.
- **Figures:** one representative figure per paper. The user asked for this.
- **Writing style:**
  - Never use dashes (em dashes or `--`) to set off a clause; use ":" or "," instead. This is the user's stated preference.
  - Keep claims factual, with numbers taken from the papers, and avoid hype.

## Where content comes from

- **The CV PDF in the repo** is the source of truth for talks, roles and awards.
  - Its embedded hyperlinks hold the talk links. Extract them with `pymupdf`: `page.get_links()`, reading the `uri` field.
  - The CV may lag the site: the CVPR oral is on the site but not under Talks in the CV.
- **arXiv IDs:**
  - PHAT-JeT 2605.21789
  - SAL-T 2510.23641
  - PULSE 2510.24058
  - J-JEPA 2412.05333
  - Pretraining 2408.09343
  - φ⁴ 2605.01145
  - Sparse attention 2512.00210
  - MoE 2610.02701
  - Metadata: `https://export.arxiv.org/api/query?id_list=...`
  - LaTeX source with the original figures: `https://arxiv.org/e-print/<id>`
- **Not on arXiv:** SBA, IDM (COLM 2026, [OpenReview](https://openreview.net/forum?id=qgZtkgTwrJ), project page idmath.github.io), Deep-Reproducer (DL4C @ NeurIPS 2025, OpenReview) and Audit.
  - OpenReview blocks automated PDF downloads, so ask the user to upload any PDF you need.
- **Code links** are copied from the papers themselves or the IDM project page.

### Figure processing recipe

1. Install tools if needed: `apt-get install -y poppler-utils` and `pip install pymupdf pillow`.
2. Get the figure:
   - Raster figure inside a PDF: `doc.extract_image(xref)`.
   - Vector figure inside a PDF: `page.get_pixmap(clip=Rect(...), dpi=400)`.
   - PDF graphic from an arXiv source tarball: `pdftocairo -png -r 200`.
3. Flatten any transparency onto white, and trim the white margins (pixel threshold of about 12, keep about 8px padding).
4. Resize to at most 1400px wide and save with `PNG optimize=True`.
5. Most figures are wide (2:1 to 3.5:1). Figure frames use `aspect-ratio: 2 / 1`.

## Workflow for any change

1. **Pull first:** `git fetch origin && git merge --ff-only origin/zihan/nice-euler-rfzfye`. The user also edits and pushes from a Mac.
2. **Edit, then preview locally:**
   - Start a server: `python3 -m http.server 8765 --bind 127.0.0.1 &`.
   - Screenshot it with Playwright from Node, loaded with `require('/opt/node22/lib/node_modules/playwright')`. Chromium is preinstalled.
   - Run Node with `NO_PROXY=127.0.0.1` so it can reach the local server.
   - Check the desktop width (1280px) and the phone width (390px).
3. **Stop the server** with `kill $(pgrep -f "^python3 -m http.server 8765")`. Do **not** use `pkill -f "http.server..."`: that pattern matches the shell running the command and kills it.
4. **Check links** with `curl`.
   - From the sandbox, github.com returns 403 and LinkedIn returns 999. Both come from the proxy or LinkedIn's bot blocking, so they don't mean the link is dead.
5. **Commit, push, and confirm the live site** with `curl https://javierzhao.github.io/...` after about a minute.
6. **Tell the user to `git pull`** before they edit locally again.

## Known gotchas

- macOS treats filenames as case-insensitive and GitHub Pages does not. A file committed as `photo.JPG` once broke the photo. Keep all asset filenames lowercase. To fix a case-only rename on a Mac, use two `git mv` steps.
- The user's Mac keychain holds a GitHub login for a different account (`IDMath`), which caused a push to fail with 403. The fix is a remote URL that names the account: `https://JavierZhao@github.com/JavierZhao/JavierZhao.github.io.git`, used with a personal access token.

## Open items

- **Search ranking:**
  - The site is indexed: searching "javierzhao" finds it, as of 2026-10.
  - It does not yet reach page 1 for "Zihan Zhao UCSD". Pages ahead of it include LinkedIn, OpenReview, Scholar, GitHub and the UCSD physics directory.
  - On-page work is done: the title, description, `<h1>` and bio all contain "Zihan Zhao" and "UC San Diego (UCSD)".
  - What is left is backlinks:
    - GitHub profile website field (empty as of 2026-10)
    - LinkedIn website field
    - a link from the Duarte group people page (it currently has no personal links for anyone)
    - the UCSD directory, OpenReview, InspireHEP and the CV
  - The Search Console sitemap shows "Couldn't fetch". The file is valid; this is a known pending state on github.io sites.
- **Google Scholar:** the profile `scholar.google.com/citations?user=tXQZ5MwAAAAJ` is the user's. It is verified with a ucsd.edu email, and its homepage field already links here. It is listed in the JSON-LD `sameAs` only, not as a visible link, until the user decides; its top entries are large CMS collaboration papers.
- **MoE and Audit:** update the venue once ML4PS 2026 decisions are out. Audit also still needs its author list.
- **SAL-T:** update the venue after the PRX Intelligence decision.
- **SBA:** add a paper link if it becomes public.
- **PHAT-JeT:** swap in the NeurIPS 2026 proceedings link when it exists.
- **PULSE author order:** the workshop's accepted-paper list has Zhao, Pendiyala, Yan, Mortazavi. The site follows arXiv: Zhao, Pendiyala, Mortazavi, Yan. Change it only if the user asks.
