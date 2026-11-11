# Portfolio Creator

A free, no-code tool that helps students build a personal portfolio website and publish it with GitHub Pages.

Students fill in their information in the browser, preview the result on a laptop and phone, and export one file, `index.html`. They upload that file to a GitHub repository to get a link like `https://username.github.io/my-portfolio/`.

Plain HTML, CSS and JavaScript. No backend, accounts, database, frameworks, tracking or external services.

---

## Pages

| Page | Purpose |
|---|---|
| `index.html` | Homepage: how it works, the three designs, FAQ |
| `creator.html` | The editor (works with `creator.js`) |
| `example.html` | A finished sample portfolio shown in all three designs |
| `guide.html` | Step-by-step guide for publishing with GitHub Pages |
| `Portfolio_Creator_Student_Instructions.pdf` / `.docx` | Printable detailed instructions (linked from `guide.html`) |

## Features

- **Three designs:** Professional Light, Editorial Minimal, Modern Dark. Students can switch at any time and their content is kept.
- **Content:** name, title, extra title lines, photo, About me, links, projects with images, and Experience, Education, Skills and Certifications sections, plus custom sections.
- **Preview** shows the exact file that will be exported, on desktop and mobile.
- **Export** creates one self-contained `index.html`. Images are embedded, and the file has no scripts and makes no external requests.
- **Autosave:** drafts are saved in the student's own browser. **Download backup** and **Restore backup** let students move a draft to another computer.
- **Accessibility:** keyboard support, labelled forms and dialogs, and it works on phone screens down to 320 px.

## Publish this site (GitHub Pages)

1. Create a new **public** repository on GitHub.
2. Upload all files and folders from this package to the repository **root**, not inside a sub-folder.
3. Go to **Settings → Pages**. Under **Source**, choose **Deploy from a branch**, then select the **main** branch and the **/ (root)** folder. Click **Save**.
4. After 1–2 minutes the site is live at `https://<username>.github.io/<repository-name>/`.

All links are relative, so the site works under any username or repository name.

## File structure

```
index.html         Homepage
creator.html       Editor page
creator.js         Editor logic, the three portfolio designs, preview and export
example.html       Sample portfolio in three designs
guide.html         Publishing guide
style.css          Styles for the homepage, editor, example and guide pages
profile.jpg        Photo used on the Example page
example-assets/    Project images used on the Example page
home-assets/       Design screenshots shown on the homepage
Portfolio_Creator_Student_Instructions.pdf / .docx
```

## How it works (for developers)

- All portfolio content lives in one `state` object in `creator.js`.
- `renderPortfolio(state, "edit")` draws the editor view, and `renderPortfolio(state, "export")` draws the published view. Both use the same portfolio CSS (`PORTFOLIO_CSS` in `creator.js`), so the editor, Preview and the exported file always match.
- The exported file includes a strict Content Security Policy. User text is HTML-escaped, links are limited to `http`/`https`/`mailto`, and only image data URLs are accepted.
- Drafts are stored in `localStorage` under `portfolioCreatorData.v2`.
- `example.html` contains portfolio markup exported from the editor. If you change the portfolio designs in `creator.js`, re-export the example so it stays in sync. The homepage screenshots in `home-assets/` are images and have to be retaken too.
- **Cache busting:** pages load `style.css?v=10` and `creator.js?v=10`. After changing either file, raise the number in the HTML pages so browsers load the new version.

## Privacy

- Nothing a student types leaves their computer until they upload their own `index.html` to GitHub.
- A published GitHub Pages site is public. Students should not include private details such as a home address or phone number.

## Known limitations

- Drafts are stored per browser and device. Clearing browser data removes them, so students should use **Download backup**.
- Browser storage is about 5 MB. Many very large images can fill it. Export still works when this happens.
- Drag-and-drop reordering does not work on touch devices. The ↑ / ↓ buttons work everywhere.
