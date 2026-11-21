# System_sauvegarde_architecture_de_donnees_fichiers_et_dossiers

**Reconstruct the structure. Not the data.**

![Arbores Restore logo](assets/branding/arbores-restore-logo.png)

The project logo is included as a square PNG and a multi-resolution Windows ICO. The ICO is configured for the Python standalone build and the Visual Basic Windows application.

A Windows-oriented utility that rebuilds a file/folder hierarchy and creates zero-byte files from a CSV inventory. It does **not** recover original file contents.


## Project

- [French documentation](README.fr.md)
- [English documentation](README.en.md)
- [Origin story](docs/origin-story.md)
- [How it works](docs/how-it-works.md)
- [Limitations](docs/limitations.md)
- [Safety model](docs/safety.md)
- [WizTree inventory guide](docs/guides/wiztree/README.md)

**Status:** early development (`0.1.0`). CSV compatibility has only been verified against the included sample fixtures, not against every WizTree export/version. Validate a copy of your actual export before trusting a reconstruction.


## Available implementations

| Implementation | Location | Status |
|---|---|---|
| Python CLI / engine | `src/python` | Implemented; automated tests included |
| PowerShell | `src/powershell/ArboresRestore.ps1` | Initial implementation; not yet runtime-verified on Windows |
| Visual Basic WinForms | `src/visual-basic/ArboresRestore` | UI source; requires packaged Python engine and Windows build validation |

The Python standalone executable and VB GUI packaging are build outputs, not committed binaries. See `scripts/`.


## Quick start (Python)

Requires Python 3.10+.

```powershell
cd src/python
python -m pip install .
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --preview
```

When the preview looks right, run with `--apply` after reviewing the preview:

```powershell
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --apply
```

Python CLI defaults to preview; `--apply` is required to write. The PowerShell version asks for explicit confirmation. Review the preview first. The Python engine never overwrites existing files; files are created exclusively and collisions are skipped. Use a new destination folder on a healthy disk.


## Safety defaults

- Inventory paths are validated and traversal entries such as `..` are rejected.
- Existing files are never overwritten.
- Preview mode does not write to the destination.
- Diagnostics mode reports the planned operation without reconstructing.
- Names invalid on Windows and reserved device names are skipped with a warning.
- No source file contents are read or copied.


## Current feature scope

- Directory reconstruction and zero-byte file creation.
- CSV parsing with common path/name/type/extension/attribute column names.
- UTF-8/BOM and Windows-1252 decoding fallback.
- Hidden/system filters, extension inclusion/exclusion, folder exclusion.
- Preview counts, collisions and skipped-entry reasons.
- Python CLI; Windows GUI and PowerShell source included.

Size-based filtering and size reporting are intentionally deferred to a later version. Date filtering, robust resumable runs, broad WizTree-version compatibility, and large-scale performance tuning are not claimed yet.


## Development and tests

```powershell
cd src/python
python -m pip install -e . pytest
python -m pytest ../../tests -v
```

The included CSV is synthetic and is not a real drive inventory.


## Contributing / security

Read [CONTRIBUTING.md](CONTRIBUTING.md) and [SECURITY.md](SECURITY.md) before submitting changes. Please open an issue with a sanitized CSV header and a few representative rows if an export format is not recognized. Never post personal filenames or paths from an actual drive without reviewing and redacting them.


## License

MIT. See `LICENSE`.

## Roadmap and repository insights

See [docs/roadmap.md](docs/roadmap.md). GitHub stars and repository metrics will be tracked only from real repository data after publication; that analytics work is separate from the reconstruction engine.

### Filters and reports

```powershell
# Exclude hidden items and Windows system entries
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --preview --exclude-hidden-files --exclude-hidden-folders --exclude-system

# Include only selected file extensions
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --preview --include-ext pdf docx zip

# Exclude file types or named folders
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --preview --exclude-ext tmp bak --exclude-folder Temp Cache

# Save a JSON report to a new file; report files are never overwritten
arbores-restore "C:\Inventory\wiztree.csv" "E:\Reconstructed" --preview --report "C:\Reports\inventory-report.json"
```

Use `--config path-to-settings.json` to save/load CLI filter settings. Size filters are not part of this initial release.
