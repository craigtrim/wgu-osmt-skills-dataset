# WGU OSMT Skills

[![License](https://img.shields.io/github/license/craigtrim/wgu-osmt-skills-dataset.svg)](./LICENSE)
[![Version](https://img.shields.io/badge/version-2025.11.01-blue.svg)](https://github.com/craigtrim/wgu-osmt-skills-dataset/releases/tag/v2025.11.01)
[![Downloads](https://img.shields.io/github/downloads/craigtrim/wgu-osmt-skills-dataset/total.svg)](https://github.com/craigtrim/wgu-osmt-skills-dataset/releases)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17516404.svg)](https://doi.org/10.5281/zenodo.17516404)

Canonicalized exports from Western Governors University’s **Open Skills Management Tool (OSMT)**, distributed as **compressed payloads only** (no raw sources in Git). Filenames were normalized prior to archiving; file contents are otherwise verbatim. 📦🗜️

---

## What’s in this repo

- `payloads/collections_v2025.11.01.tar.zst`; all collection CSVs (normalized names).
- `payloads/skills_v2025.11.01.tar.zst`; per-skill JSON (optional set), same normalization policy.
- `manifests/payloads.sha256`; SHA-256 checksums for the payload files above.
- `dataset.yaml`; machine-readable metadata (version, provenance, distribution).
- `LICENSE`; MIT (applies to repo code/docs only).
- `LICENSE-DATA.md`; data attribution; upstream OSMT/WGU terms govern.
- `CITATION.cff`; citation metadata.
- `NOTICE`; attribution notice.

> **Note:** The original raw files (`collections/*.csv`, `skills/**/*.json`) are **not** tracked in Git. This repo intentionally ships only the compressed payloads plus metadata.

---

## Version / Provenance

- Dataset version: **2025.11.01**  
- Acquired: **2025-11-01**  
- Upstream source: https://osmt.wgu.edu/  
- Normalization: filenames only (e.g., `collection-<slug>_vYYYY.MM.DD.csv`); no content edits.

Details are also recorded in `dataset.yaml`. 🧾

---

## Download

Grab the assets from the GitHub Release:  
- **Release page:** https://github.com/craigtrim/wgu-osmt-skills-dataset/releases/tag/v2025.11.01  
- `payloads/collections_v2025.11.01.tar.zst`  
- `payloads/skills_v2025.11.01.tar.zst`  

Or clone the repo and use the payloads directly from `payloads/`. 📥

---

## Verify integrity

### Verify payload checksums
```
# macOS
shasum -a 256 -c manifests/payloads.sha256

# Linux
sha256sum -c manifests/payloads.sha256
```

### Test the zstd stream
```
zstd -t payloads/collections_v2025.11.01.tar.zst
zstd -t payloads/skills_v2025.11.01.tar.zst
```

---

## Extract

```
# collections
zstd -dc payloads/collections_v2025.11.01.tar.zst | tar -xvf -

# skills (if needed)
zstd -dc payloads/skills_v2025.11.01.tar.zst | tar -xvf -
```

---

## Reproduce the archives (deterministic tar + zstd)

> Requires GNU tar. On macOS, install via Homebrew and use `gtar`.

```
# collections payload (example)
gtar --sort=name --owner=0 --group=0 --numeric-owner \
    -cf - collections/*.csv \
| zstd -19 -T0 -f -o payloads/collections_v2025.11.01.tar.zst

# skills payload (example)
gtar --sort=name --owner=0 --group=0 --numeric-owner \
    -cf - skills/**/*.json \
| zstd -19 -T0 -f -o payloads/skills_v2025.11.01.tar.zst
```

---

## Licensing

- **Code & docs:** MIT. See `LICENSE`. ✅  
- **Data:** Subject to OSMT/WGU’s original terms. See `LICENSE-DATA.md`.  
  This repository does **not** grant additional rights to the data beyond upstream terms. 🔐

---

## Citation

Please cite using `CITATION.cff` or this BibTeX (update DOI once minted):

```
@dataset{wgu_osmt_collections_2025_11_01,
  title   = {WGU OSMT Skills ; Collections (payload-only)},
  version = {2025.11.01},
  author  = {Trim, Craig},
  year    = {2025},
  url     = {https://github.com/craigtrim/wgu-osmt-skills-dataset},
  doi     = {10.5281/zenodo.TBD}
}
```

---

## Contact / Takedown

If you are a rights holder requesting changes or removal, open a GitHub issue on this repository or contact the maintainer listed in `dataset.yaml`. 🙏
