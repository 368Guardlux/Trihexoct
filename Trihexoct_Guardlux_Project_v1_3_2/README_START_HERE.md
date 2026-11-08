# Start here — Trihexoct Guardlux v1.3.2

1. Extract the **complete** project ZIP and back up the existing `README.md` and `Trihexoct.txt` in `368Guardlux/Trihexoct`.
2. Upload/commit all project files to branch `main`, preserving `.github/workflows/`, `config/`, `src/`, `tools/`, `tests/`, `docs/`, `reports/`, `requirements-ci.txt`, and `VERSION`. Uploading `main.yml` alone is not sufficient.
3. The main workflow is `.github/workflows/main.yml`. It contains YAML only. The Python code lives in `tools/build_filter.py`, `tools/validate_filter.py`, `tools/validate_workflows.py`, and `tools/write_summary.py`.
4. Allow GitHub Actions to read/write repository contents at Settings → Actions → General → Workflow permissions. Write permission is scoped to the publishing job and only commits after all validation steps pass.
5. Open Actions → **Build and validate Trihexoct** → **Run workflow**. Review the build report artifact. If a source-count anomaly or more-than-40% rule-set delta is reported, review the report before enabling the corresponding manual-approval input.
6. Keep using `https://raw.githubusercontent.com/368Guardlux/Trihexoct/main/Trihexoct.txt` in Brave after the first successful live run. The URL does not change.

**Current package status:** the bundled `Trihexoct.txt` was regenerated from a successful live reference-feed reconciliation. The project is now in the `ONLINE RECONCILIATION` state, and the report confirms that all configured feeds passed validation.

CI-only YAML validation uses the pinned PyYAML dependency in `requirements-ci.txt`; the filter builder itself uses only the Python standard library. See `docs/OPERATIONS_RUNBOOK.md` for failure handling and recovery.
