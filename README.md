# HTML Resume

Professional, print resume of Nathan J Klingensmith written completely in HTML and CSS.

## Setup

The page loads its templates with `fetch`, so it must be served over HTTP rather than opened as a file.

- **VSCode:** install the `Live Server` extension and open `resume.html` with it.
- **Terminal:** run `python3 -m http.server` in the repo root and visit `http://localhost:8000/resume.html`.

## Printing

Open `resume.html` in Chrome and print with these settings:

- `Destination` Save as PDF
- `Background graphics` _Checked_, otherwise the header and sidebar colors are dropped

Page size, margins, and the single-page layout are set in the stylesheet, so the remaining settings can stay at their defaults.

## Editing content

All content lives in `data/` and is rendered by the Mustache templates in `templates/`.

| File                          | Section                |
| ----------------------------- | ---------------------- |
| `data/work_experience.js`     | Work History           |
| `data/academic_experience.js` | Education              |
| `data/details.js`             | Info (contact details) |
| `data/skills.js`              | Skills                 |
| `data/awards.js`              | Awards                 |

### Experience entries

```js
{
    title: 'Co-Founder & CTO',
    subtitle: 'Pallyt Technologies',
    logo: './images/pallyt.jpg',      // optional; a placeholder is shown without one
    tag: 'Mar 2021 — Jun 2022',
    content: `<ul><li>...</li></ul>`
}
```

To show several roles under one company, replace `content` with a `roles` list. The company becomes the heading and each role gets its own title, dates, and content:

```js
{
    title: 'Jellyfish',
    subtitle: 'Boston, MA',
    logo: './images/jellyfish.jpg',
    tag: 'Jun 2022 — present',
    roles: [
        { title: 'Senior Software Engineer', tag: 'Jul 2024 — present', content: `<ul>...</ul>` },
        ...
    ]
}
```

### Sidebar items

Info, Skills, and Awards items share these optional fields; any that are left out take no space:

- `title` bold label
- `subtitle` plain line
- `href` / `link` link URL and its text
- `subtitleItalic` italic line

## Assets

- `images/` company and school logos (square, around 100–200px)
- `icons/` section icons from [Font Awesome Free](https://fontawesome.com/search?ic=free) (Solid style)

## Machine readability

Resume parsers often read PDF text in the order it is drawn, not where it sits on the page. Elements with `position` or `z-index` are drawn in a later pass and land out of order in the PDF, so the layout uses flexbox and grid only. Keep it that way when making changes.
