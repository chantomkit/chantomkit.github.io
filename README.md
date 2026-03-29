# chantomkit.github.io

Personal profile page — pure HTML/CSS/JS, no build step, no framework dependencies.

## File structure

```
.
├── index.html                       # The entire site — edit this to update content
├── .nojekyll                        # Tells GitHub Pages to skip Jekyll entirely
├── assets/
│   ├── img/
│   │   ├── avatar.png               # Profile photo
│   │   ├── favicon.png              # Browser tab icon (light mode)
│   │   └── favicon-dark.png         # Browser tab icon (dark mode)
│   └── files/
│       └── resume_baseline.pdf      # Resume — linked from the hero and footer
└── README.md
```

---

## Deploying to GitHub Pages

### 1. Create the repository

Create a new GitHub repository named exactly **`chantomkit.github.io`**.

### 2. Push this folder as the repo root

```bash
# Run these commands inside this folder (migration/), or wherever you've copied its contents
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/chantomkit/chantomkit.github.io.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to the repository on GitHub → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / Folder: `/ (root)`
4. Click **Save**

Live at `https://chantomkit.github.io` within ~60 seconds.

> `.nojekyll` tells GitHub Pages to serve files directly — no Ruby, no gem installs, no build step.

---

## Updating content

Everything lives in `index.html`. Edit it directly and push — it goes live immediately.

### Hero section

```html
<!-- Status badge text -->
Open to new opportunities · Right to work in UK

<!-- Name -->
<h1 class="hero-name">Tom <span class="grad">Chan</span></h1>

<!-- Current role pills -->
<span class="role-pill tesco"> ... Data Scientist · Tesco</span>
<span class="role-pill apart"> ... Research Fellow · Apart Research</span>

<!-- One-liner tagline -->
<p class="hero-tagline"> ... </p>
```

To change the role pill colours, edit the CSS variables for `.role-pill.tesco` and `.role-pill.apart`.

### Resume link

The resume is linked in two places. To swap the file:
1. Replace `assets/files/resume_baseline.pdf` with your new file
2. Update both `href` references in `index.html` if the filename changes:
   ```html
   href="./assets/files/resume_baseline.pdf"
   ```

### About section

Find `<!-- ABOUT -->`. Edit the three `<p>` tags inside `.about-copy`.
Wrap highlighted phrases in `<span class="kw">text</span>`.

### Experience section

Find `<!-- EXPERIENCE -->`. Each role is a `.t-card` block:

```html
<div class="t-card reveal reveal-d1">
  <div class="t-header">
    <div>
      <div class="t-title">Role — Company</div>
      <div class="t-sub">Location</div>
    </div>
    <div class="t-period">Month Year – Month Year</div>
  </div>

  <!-- Optional sub-group label -->
  <div class="t-group">Sub-team or Project Name</div>

  <ul class="t-bullets">
    <li>Achievement. Wrap key numbers in <span class="metric">X</span>.</li>
  </ul>

  <div class="tags">
    <span class="tag">Tool</span>
  </div>
</div>
```

Use `reveal-d1` through `reveal-d4` to stagger the scroll-in animation.

### Research section

Find `<!-- RESEARCH -->`. Each project is an `.r-card` block.

To show a hackathon badge:
```html
<span class="r-badge">🏆 Top 4 — Hackathon 2025</span>
```

To show stats (accuracy, AUC, etc.):
```html
<div class="r-stats">
  <div class="stat">
    <span class="stat-val">85%</span>
    <span class="stat-lbl">Accuracy</span>
  </div>
</div>
```

### Education section

Find `<!-- EDUCATION -->`. Same `.t-card` structure as Experience.
Use `.t-note` for the grade and thesis title:
```html
<div class="t-note">Distinction · 82.3% · Thesis: <em>"..."</em></div>
```

### Skills section

Find `<!-- SKILLS -->`. Each category is a `.skill-row`:
```html
<div class="skill-row reveal reveal-d1">
  <div class="skill-cat">Category Name</div>
  <div class="chips">
    <span class="chip">Skill</span>
  </div>
</div>
```

### Accent colour

All colours are CSS custom properties in `:root` near the top of `index.html`:

```css
--accent:   #6e6bff;  /* indigo — primary */
--accent-2: #9d9bff;  /* lighter indigo */
--accent-3: #c4b5fd;  /* lavender */
```

Replace all three to change the colour theme.

---

## Optional: Custom domain

1. Add a `CNAME` file at the repo root with your domain:
   ```
   tomchan.dev
   ```
2. Add a DNS `CNAME` record pointing to `chantomkit.github.io`
3. In GitHub → Settings → Pages → Custom domain, enter your domain

---

## Stack

| Concern | Approach |
|---|---|
| Markup | Semantic HTML5 |
| Styling | Pure CSS — custom properties, Grid, `backdrop-filter`, `@keyframes` |
| Interactivity | ~25 lines vanilla JS — `IntersectionObserver` for scroll animations |
| Fonts | Inter via Google Fonts CDN |
| Icons | Font Awesome 6 via CDN |
| Hosting | GitHub Pages — static, free, no build pipeline |
