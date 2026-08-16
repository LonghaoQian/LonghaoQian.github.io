# Setting Up Your Portfolio Site with GitHub Pages (VS Code Workflow)

This guide covers two paths:
- **Path A: al-folio** — pre-built academic/researcher portfolio theme (fastest, good fit for publications + projects)
- **Path B: Custom static site** — plain HTML/CSS, full control

Pick one. Both deploy free on GitHub Pages.

---

## Prerequisites

- Git installed (`git --version` to check)
- VS Code with the **GitHub Pull Requests and Issues** or just the built-in Source Control panel (Git is built into VS Code)
- A GitHub account
- Node.js only needed if you go with a JS-based theme (not required for either path below)

---

## Path A: al-folio (recommended — fastest, built for researchers)

al-folio is a Jekyll theme designed for academics: sections for projects, publications, CV, news/blog.

### 1. Fork the repo
- Go to https://github.com/alshedivat/al-folio
- Click **Fork** (top right) → creates a copy under your GitHub account
- Rename the fork to `yourusername.github.io` (Settings → repository name) — this exact naming makes GitHub auto-host it at `https://yourusername.github.io`

### 2. Clone it locally in VS Code
```bash
git clone https://github.com/yourusername/yourusername.github.io.git
cd yourusername.github.io
code .
```

### 3. Install Ruby + Jekyll (needed to preview locally)
- Mac: `brew install ruby` then `gem install bundler jekyll`
- Windows: use [RubyInstaller](https://rubyinstaller.org/) (includes DevKit), then `gem install bundler jekyll`
- Linux: `sudo apt install ruby-full build-essential` then `gem install bundler jekyll`

Then in the project folder:
```bash
bundle install
bundle exec jekyll serve
```
Open `http://localhost:4000` to preview.

### 4. Edit your content (all in VS Code)
Key files to edit:
- `_config.yml` — your name, title, bio, social links, email
- `_pages/about.md` — homepage bio text
- `_projects/` — one markdown file per project (this is where VACTS, slung-load winch, vision pipeline, etc. go)
- `_bibliography/papers.bib` — your publications in BibTeX format (Science China Technological Sciences paper, etc.)
- `_pages/cv.md` — CV/timeline (or just link a PDF)
- `assets/img/` — drop project photos/GIFs/diagrams here

### 5. Enable GitHub Pages
- On GitHub, go to your repo → **Settings** → **Pages**
- Source: **Deploy from a branch** → branch `main` (or check repo docs — al-folio sometimes uses a GitHub Action, check the repo's own README for the current recommended deploy method)
- Wait 1-2 minutes, then visit `https://yourusername.github.io`

### 6. Commit and push from VS Code
- Use the **Source Control** panel (left sidebar, branch icon)
- Stage changes → write a commit message → Commit → Sync/Push
- Or via terminal:
```bash
git add .
git commit -m "Add VACTS project and publications"
git push
```

---

## Path B: Custom static site (plain HTML/CSS)

### 1. Create the repo
- On GitHub, create a new repo named exactly `yourusername.github.io`
- Do NOT initialize with a README if you plan to push local files immediately (or do, and merge later)

### 2. Clone and open in VS Code
```bash
git clone https://github.com/yourusername/yourusername.github.io.git
cd yourusername.github.io
code .
```

### 3. Recommended file structure
```
/
├── index.html          # home page
├── projects.html       # or projects/ folder with one page per project
├── publications.html
├── cv.pdf              # downloadable resume
├── style.css
├── /assets
│   ├── /images
│   └── /videos
```

### 4. Build your pages
- Start with `index.html`: hero section (name, one-liner, photo), then sections for Projects / Publications / Contact
- Use semantic HTML (`<section>`, `<article>`) so it's easy to style and maintain
- Keep CSS in one `style.css`, mobile-responsive (use a simple flexbox/grid layout, add a `<meta name="viewport">` tag)
- Embed project videos/GIFs directly (drone footage will make a strong impression)

### 5. Preview locally
- Install the **Live Server** extension in VS Code
- Right-click `index.html` → "Open with Live Server" → auto-refreshing local preview

### 6. Enable GitHub Pages
- Repo → **Settings** → **Pages** → Source: `main` branch, root folder
- Site goes live at `https://yourusername.github.io` within a minute or two

### 7. Push from VS Code
- Source Control panel → stage → commit → push (same as Path A step 6)

---

## After it's live

- **Custom domain (optional, ~$10-15/year)**: buy on Namecheap/Google Domains, add a `CNAME` file in your repo root with your domain, then configure DNS records per GitHub's custom domain docs
- **Add a `robots.txt` / sitemap** if you want it indexed well by Google
- **Update regularly**: every time you finish a project or get a paper accepted, add it — recruiters do check for recent activity via your commit history too

---

## Content checklist for job hunting (fill these in first)

- [ ] One-line positioning statement (postdoc → industry robotics R&D framing)
- [ ] 4-6 project write-ups: problem → your role → approach → result (with visuals)
  - VACTS multi-drone slung-load
  - Slung-load winch (AK40-10)
  - Vision/YOLO localization pipeline
  - PX4/ELRS drone hardware builds
  - RL-based UAV control (PPO)
- [ ] Publications list (BibTeX or simple list with links)
- [ ] Downloadable CV/resume PDF
- [ ] Contact info / LinkedIn / GitHub links