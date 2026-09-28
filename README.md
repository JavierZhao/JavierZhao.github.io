# Zihan Zhao · personal website

A static one-page site in plain HTML and CSS. It has no build step and no dependencies.

```
index.html              all content
assets/css/style.css    styles (colors and fonts are set in :root at the top)
assets/fonts/           self-hosted Inter + Newsreader (SIL Open Font License)
assets/figs/            one representative figure per paper
assets/img/photo.jpg    headshot (the "ZZ" placeholder shows until this file exists)
assets/Zihan_Zhao_CV.pdf
```

## Preview locally

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Update content

- **New paper:** copy an `<article class="card">` block in `index.html`, then add its figure to `assets/figs/`. Use a PNG about 1400px wide with the white margins trimmed.
  - Use `grid--2` for the large cards under "Selected work" and `grid--3` for the smaller ones under "More research".
  - Use `venue--review` on the venue label while the paper is under review.
- **CV:** replace `assets/Zihan_Zhao_CV.pdf`, keeping the same filename.
- **Photo:** save the headshot as `assets/img/photo.jpg`. It is cropped to 4:5, so a square photo works.
- **News:** edit the `<ul class="news">` list.

## Deploy (GitHub Pages)

This repository is `JavierZhao.github.io`, so the site is served at `https://javierzhao.github.io/`.

1. Open Settings → Pages. Under Source, choose "Deploy from a branch".
2. Select the branch that holds the site and `/ (root)`.
3. Pushes to that branch redeploy automatically within a minute or two.
