# DASHAN-0079 DSH plugin market

A community plugin index for [DeepSeek Harness](https://github.com/deepseek-ai/dsh) (DSH).
DSH has no official public plugin market that anyone can self-publish to; the supported
community shape is an HTTP(S) **index source** that users add in the Plugins page.

Index URL:

```text
https://raw.githubusercontent.com/DASHAN-0079/dsh-plugin-market/main/index.json
```

## Plugins

| Plugin | Version | Source | What it does |
| --- | --- | --- | --- |
| `dsh-superagent` | 0.1.1 | [DASHAN-0079/dsh-superagent-adapt](https://github.com/DASHAN-0079/dsh-superagent-adapt) | Watches a GitHub repository, turns authorized requests into Tickets, and runs each in its own DSH Session. Adapted to DSH `0.2.2-rc.3`. |
| `dsh-ppt-master` | 6.8.0-dsh.2 | [DASHAN-0079/dsh-ppt-master](https://github.com/DASHAN-0079/dsh-ppt-master) | Bundles the ppt-master skill (Markdown → PowerPoint) and registers it as a DSH skill provider. |

Each entry pins an exact git commit, so installing from this index is reproducible.
Both packages ship their built artifacts, so a git install needs no build step and no
`allowBuilds` permission.

## Add the index in DSH

1. Open **Settings → Plugins** and make sure the experimental plugin manager (which
   contains the Discover page) is enabled.
2. Open the **Plugins** page and switch to the **Discover** tab.
3. Choose **Manage index sources…** (or the empty-state **Add index source** button).
4. Paste the index URL above into **Index URL** and choose **Add**.
5. Superagent and PPT Master appear in Discover; choose **Install** on either card.

Equivalent command line (no market UI needed):

```bash
dsh plugin add "git+https://github.com/DASHAN-0079/dsh-superagent-adapt.git#ca8a271065c4be72489affc835d17dc644721e64"
dsh plugin add "git+https://github.com/DASHAN-0079/dsh-ppt-master.git#dee871bbb0a81d60a1b02e45fd67fa9081eccc50"
```

`dsh plugin add` accepts a registry spec, a `git+https://…#<commit>` spec, or a local
`.tgz`; the commits above are the ones this index lists.

## Compatibility

| Plugin | `engines.dsh` | Notes |
| --- | --- | --- |
| `dsh-superagent` 0.1.1 | `^0.2.2-rc.3` | Built against DSH `0.2.2-rc.3` sources; DSH `0.2.1` and older are rejected. |
| `dsh-ppt-master` 6.8.0-dsh.2 | `>=0.2.0-rc.2 <0.3.0` | Pure skill provider; works across the 0.2.x line. |

## Layout

```text
index.json    Format-1 plugin index (the file DSH fetches)
README.md     This document
```

The index is maintained by hand: each release adds a `versions[]` entry with the new
version, its commit, and a `publishTimestamp`, then moves `dist-tags.latest`. Icons are
absolute `raw.githubusercontent.com` URLs pinned to the same commit as the version, so an
entry keeps rendering even after later commits change the file.

## License

MIT. The listed plugins carry their own licenses; `dsh-ppt-master` vendors the ppt-master
skill (MIT) and notes the AGPL-3.0 status of its optional PyMuPDF dependency in its
README.
