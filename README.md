# exsited-docs-kb

Paste-ready HubSpot knowledge base articles for the Exsited API and SDKs, and a page that
lets you copy each one. The full reference lives on the Mintlify site; every article links to it.

## Using the copy page

Open the published page (GitHub Pages) and pick an article. Then, in HubSpot:

1. Create the article in the right category and paste its **title** and **subtitle** from the page.
2. Click **Copy article** on the page, click into the article body in HubSpot and press Ctrl+V
   (Cmd+V on a Mac). The article arrives as formatted text: headings, lists, tables, links, bold and
   code keep their formatting.
3. Save, then preview before you publish.

**Copy HTML** copies the raw markup instead, for an editor that has a Source code view.

## Layout

| Path | What it is |
| --- | --- |
| `src/articles/*.html` | Article sources. Links to the docs are written `{{MINTLIFY}}/<page>`. |
| `src/articles.json` | Title, category and summary for each article. |
| `src/index.template.html` | The copy page. |
| `config.json` | `mintlify_base`, the live docs address, and `docs_dir`, the Mintlify project. |
| `build.py` | Builds `articles/` and `index.html`. |
| `articles/`, `index.html` | Build output. Commit it: GitHub Pages serves it. |

## Building

```bash
python build.py
```

The build needs the Mintlify project checked out at `docs_dir` (by default `../mintlify-docs`). It fails if:

- a `{{MINTLIFY}}/<page>` link names a page that is not in the Mintlify navigation,
- an article contains an `<h1>`, a `class` attribute, or a `<style>`, `<script>` or `<link>` tag
  (HubSpot keeps inline styles only and renders the title as the heading),
- an article contains a development host, an API version other than v4, a dash character or a credential.

While `mintlify_base` is still the placeholder, the copy page shows a warning. Set it to the live
docs address and rebuild before anyone pastes.

## Changing an article

Work on a branch, edit `src/`, run `python build.py`, commit the source and the output together,
and open a pull request.
