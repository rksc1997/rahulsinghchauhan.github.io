# How to update this site

You never need to install anything. Edit files directly on GitHub in your browser, commit to
`main`, and the site rebuilds and redeploys itself in about two minutes.

**To edit a file on GitHub:** open it in the repository, click the pencil icon (✏️) at the top
right, make your change, then click **Commit changes** at the bottom.

**To upload a file:** go to the folder you want it in, click **Add file → Upload files**, drag the
file in, then **Commit changes**.

If a change doesn't show up, open the **Actions** tab. A green check means it deployed; a red X
means the build failed — click it to see the error. The most common cause is a YAML indentation
mistake, so compare your new entry against the ones already there.

---

## Add a new paper

Edit `data/papers.yaml`. Copy an existing entry and change the fields. Indentation matters: two
spaces, and the `-` marks the start of a new paper.

```yaml
- title: "The Title of Your Paper"
  coauthors: "Jane Doe and John Roe"     # leave out entirely if you are the sole author
  year: 2027
  status: "working paper"
  venue: "NBER Working Paper 99999"      # optional
  pdf: "files/short-name.pdf"            # the file you uploaded to static/files/
  description: >-
    One or two sentences describing the paper.
```

Then upload the PDF to `static/files/` using the same filename you put in `pdf:`.

Papers are grouped on the page by their `status`, in this order: working papers, under review,
work in progress, publications. Within each group they appear in the order they appear in the
file, so put new work wherever you want it to show.

**Valid `status` values** — spelling must match exactly:

| Value | Shows under |
|---|---|
| `working paper` | Working papers |
| `under review` | Under review |
| `revise and resubmit` | Under review |
| `accepted` | Under review |
| `work in progress` | Work in progress |
| `published` | Publications |

**Other fields you can use:**

- `link:` — an external URL (SSRN, NBER, a journal page). Used as the title's link when there is
  no `pdf`.
- `extraLinks:` — additional links shown under the entry, e.g.
  ```yaml
  extraLinks:
    - label: "NBER"
      url: "https://www.nber.org/papers/w31050"
  ```
- `note:` — a short factual note, such as an award attached to the paper.
- `coverage:` — media coverage, rendered as "Coverage: …".
- `abstract:` — only shown for the featured paper (see below).

## Change which paper is highlighted

Exactly one paper should have `featured: true`. That paper gets the highlighted card at the top of
its group and is the only one that shows its full `abstract`. To move the highlight, delete
`featured: true` from the old paper and add it to the new one.

When you go on the job market, this is also how you flag your job market paper — set
`featured: true` on it and add `note: "Job market paper"`.

## Mark a paper as published

In `data/papers.yaml`, change its `status` from `"working paper"` to `"published"` and fill in
`venue:` with the journal name and `year:` with the year. Add `link:` pointing at the published
version.

## Update your bio

Edit `content/_index.md`. Everything below the `---` line is your bio; each blank line starts a
new paragraph. Don't remove the `title:` line at the top.

## Update the tagline, title, or email

These live in `hugo.yaml` under `params:`:

- `tagline` — the sentence under your name
- `yearInProgram` — e.g. change `Fourth-year PhD student` to `Fifth-year PhD student`
- `email`, `institution`, `program`
- `interests` — the "Research interests" line
- `description` — the text search engines and link previews show

## Add a teaching entry

Edit `data/teaching.yaml`:

```yaml
- course: "Corporation Finance (MBA)"
  role: "Teaching Assistant"
  institution: "University of Chicago Booth School of Business"
  instructor: "Professor Name"     # optional
  term: "Winter 2027"              # optional
```

Courses are grouped by `institution`, so spell it identically to the existing entries to keep them
together.

## Add an award or grant

Edit `data/awards.yaml`:

```yaml
- name: "Name of the Award"
  year: "2027"
  note: "short qualifier"     # optional, shown in parentheses
```

## Add a presentation

Edit `data/talks.yaml`. Venues are grouped by paper:

```yaml
- paper: "Title of the Paper"
  venues:
    - "AFA 2027"
    - "Chicago Booth"
```

To add a venue to a paper already listed, just add another `- "…"` line under its `venues:`.

## Update your CV

Upload the new PDF to `static/files/` with the filename `cv.pdf`, replacing the old one. GitHub
will ask you to confirm the overwrite. Keeping the same filename means the CV link in the nav bar
never breaks.

## Change your photo

Replace `static/images/photo.jpg` with a new file using that exact name. It's displayed as a
circle, so a square image cropped close on your face works best — roughly 640×640 pixels.

## Remove the footer credit

In `hugo.yaml`, change `credit: true` to `credit: false` under `params: mysite:`. Set
`discovery: false` to also remove the hidden `generator` tag and the structured-data block in the
page source.

## Add a section that isn't there yet

The homepage sections are built in `layouts/index.html`. Sections with no data disappear
automatically — for example, if you empty `data/talks.yaml`, the Presentations heading goes away
too. Adding a genuinely new kind of section means editing that template, which is worth asking for
help with.

## Point a custom domain at the site

If you buy a domain (say `rahulsinghchauhan.com`):

1. Create a file named `static/CNAME` containing just the domain, with no `http://` and no
   trailing slash.
2. In `hugo.yaml`, change `baseURL` to `https://rahulsinghchauhan.com/`.
3. At your domain registrar, add four `A` records for the apex domain pointing to `185.199.108.153`,
   `185.199.109.153`, `185.199.110.153`, and `185.199.111.153`, plus a `CNAME` record for `www`
   pointing to `rksc1997.github.io`.
4. In the repository, go to **Settings → Pages**, enter the domain under "Custom domain", and tick
   **Enforce HTTPS** once the certificate is issued.

`rksc1997.github.io` keeps working afterwards — it redirects to the new domain.

---

## Optional: preview changes on your own machine

Only needed if you want to see edits before pushing. Install Hugo (extended), then from the
repository folder run:

```bash
hugo server -D
```

and open <http://localhost:1313>. Changes appear as you save.
