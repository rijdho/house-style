# house-style

The shared "violet" look of rijdho's public tools: one stylesheet, `house.css`, plus the self-hosted
Inter fonts it needs. It is the original; every project keeps an **exact copy**, and a test in each
project fails if that copy is edited or falls behind.

Used by: [chilean-altoutputs](https://github.com/rijdho/chilean-altoutputs).
To migrate: fair-repo-audit, coara-action-planner, orcid-finder (they carry the same tokens, copied by
hand, and have started to drift in their interface names).

## What it gives a project

| Layer | Contents |
|---|---|
| Fonts | Inter Variable, latin + latin-ext, served from the project's own origin |
| Tokens | the palette, light and dark, and the OS preference before any script runs |
| Interface | stable names to read in components and charts: `--bg`, `--text`, `--muted`, `--accent`, `--border`, `--surface-alt`, `--track`, `--sans`, `--mono` |
| Shell | `.app` > `.rail` (brand, nav, foot) + `.main-col` > `.cmdbar` + `.content` > `.content-inner`, and a drawer below 880 px (`.app.rail-open`, `.menu-btn`, `.rail-backdrop`) |
| Components | `.eyebrow`, `.lede`, `.card`, `.muted`, `.btn`, `.ghost-btn`, `.icon-btn`, `.chip`, `.langs`, `.site-foot` |
| Data palette | `--f-F --f-A --f-I --f-R` (FAIR), `--lvl-hi --lvl-mid --lvl-lo` (levels), kept apart from the chrome |

The brand glyph takes its letters from the project: `<span class="brand-glyph" style="--glyph: 'CA'">`.

## The house footer

Every tool ends with the same line, in its interface language:

> By Ricardo Hartley Belmar (ORCID 0000-0001-5058-9309) · Code under Apache-2.0, data under CC BY 4.0 · Source on GitHub · DOI 10.5281/zenodo.NNN

- **Author** links to https://rijdho.github.io; the ORCID links to https://orcid.org/0000-0001-5058-9309.
- **Licences** say what the project actually uses (code, and data if it publishes any).
- **Source on GitHub** links to the repository.
- **DOI** appears only once the project is archived on Zenodo, and is always the **concept DOI**
  (it resolves to the latest version), linked through https://doi.org/.

Markup: `<footer class="site-foot">`, items separated by `<span class="sep">·</span>`.

The same credits also stand at the foot of the left rail (`<div class="rail-foot">`), one item
per line because the rail is narrow (the licences split at the comma, one per line), and without the ORCID, which the page footer carries:

```
By Ricardo Hartley Belmar
Code under Apache-2.0
data under CC BY 4.0
Source on GitHub
Part of Metaudits               (tools in that family)
Data from DataCite and ANID     (where the tool shows data; name the sources)
DOI 10.5281/zenodo.NNN          (once archived: the concept DOI)
```

A tool whose page has no rail (pollen) carries the page footer only.

The family is called **Metaudits** in every signature, in every language, and links to
https://rijdho.github.io/metaudits-home/. Not "Metadata Audits", which describes it.

The rail is hidden in a drawer on a phone, so it never replaces the page footer: both are shown.

| | English | Español | Deutsch |
|---|---|---|---|
| by | By | Por | Von |
| licences | Code under Apache-2.0, data under CC BY 4.0 | Código bajo Apache-2.0, datos bajo CC BY 4.0 | Code unter Apache-2.0, Daten unter CC BY 4.0 |
| source | Source on GitHub | Código en GitHub | Quellcode auf GitHub |
| family | Part of Metaudits | Parte de Metaudits | Teil von Metaudits |

## Using it in a project

The project copies `house.css` and `fonts/` into its own tree and records what it copied:

```
src/house/house.css
src/house/fonts/*.woff2
src/house/house.lock.json      {"version": "1.0.0", "sha256": "..."}
```

- `sync-house` copies from a sibling checkout (`../house-style`) and rewrites the lock.
- A test hashes the copy against the lock (always runs, so a hand edit fails in CI), and, when the
  original is present next to the project, the lock against the original (so a stale copy fails locally).
- Project-specific styles go in the project's own stylesheet, after `house.css`, never inside the copy.

## Changing the style

Edit `house.css` here, bump the version in its first line, then in each project: sync, run its tests,
look at it, deploy. A change reaches a site when that site is redeployed, never all at once.

## License

MIT. Inter is under the SIL Open Font License 1.1.
