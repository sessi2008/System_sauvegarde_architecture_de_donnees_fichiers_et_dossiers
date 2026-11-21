# Contributing

Contributions are welcome, especially sanitized WizTree CSV compatibility samples, bug reports, and tests for Windows path edge cases.


## Before submitting

- Open an issue describing the expected and actual behavior.
- Remove personal names, usernames, sensitive directory names, drive labels, and file contents from CSV examples.
- Add regression tests for parser/filter/safety changes.
- Run `python -m pytest ../../tests -v` from `src/python`.
- Clearly label any Windows-only tests you cannot run locally.
- Do not claim support for a WizTree schema without a real, sanitized fixture.


## Development principles

- Preserve existing files and never overwrite silently.
- Preview/diagnostics must not write reconstructed files.
- Use explicit errors and skip reasons instead of swallowing exceptions.
- Keep features focused on inventory-based structure reconstruction; size analytics are deferred.
