# Arbores Restore

![Arbores Restore logo](assets/branding/arbores-restore-logo.png)

The project logo is included in `assets/branding/` as a square PNG and a multi-resolution ICO. The ICO is configured for the Python executable and the Visual Basic Windows application.

**Reconstruct the structure. Not the data.**

This utility reconstructs a file/folder tree and zero-byte placeholder files from a CSV inventory. It does not recover original file contents.


## Why it exists

After losing more than a terabyte of data, I realized that I had lost more than files: I had also lost their organization, names, paths and the way projects were arranged. I wanted to rebuild that architecture, even when the actual data was no longer recoverable.

The tool uses a WizTree CSV inventory as a record of a previous disk. It reconstructs that structure on another storage location so it can be browsed and used as a reference for further recovery efforts.

## What it does

- Recreates directories from inventory paths.
- Creates zero-byte files with recorded names.
- Previews the operation before writing.
- Filters hidden/system entries where metadata supports it.
- Includes extension filters and folder exclusions.
- Reports path validation issues, collisions and skipped entries.
- Includes Python CLI, PowerShell and Visual Basic GUI source.

## What it does not do

- Recover original file contents.
- Guarantee a complete reconstruction from incomplete or incompatible inventories.
- Recreate metadata not present in the source CSV.
- Intentionally overwrite existing files.

Size-aware filters and original-size reporting are planned for a later release.

## Status

Early development, `0.1.0`. Compatibility is currently tested with the provided fixtures, not every WizTree CSV export/version. Validate your own sanitized export before a real reconstruction.

## Quick start

Requires Python 3.10+.

```powershell
cd src/python
python -m pip install .
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --preview
```

Review the preview, then run again with `--apply`. The Python CLI does not ask for an interactive confirmation, so preview first and use a new destination directory.

```powershell
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --apply
```

## Tests

```powershell
cd src/python
python -m pip install -e . pytest
python -m pytest ../../tests -v
```

See [docs](docs/), [contributing](CONTRIBUTING.md), and [security](SECURITY.md).

## Roadmap and repository insights

See [the roadmap](docs/roadmap.md). GitHub popularity and growth metrics (stars, forks, downloads, traffic and trends) will be tracked using actual repository data after publication and kept separate from the reconstruction engine.
