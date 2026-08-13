<!-- markdownlint-disable -->

# Hardening Report: ComunidadAylas--PackSquash-action/v4.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ComunidadAylas--PackSquash-action/v4.0.3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

None of the 13 workflow files under .github/workflows/ declare a top-level permissions: block, and no job within any of these files declares its own permissions: block. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege. All workflow files are affected: build.yml, static_analysis.yml, test_all_inputs_override.yml, test_custom_options_file.yml, test_double_checkout.yml, test_empty_pack_with_latest_build.yml, test_empty_resource_pack.yml, test_pack_in_submodule.yml, test_pack_submodule.yml, test_run_in_multiple_steps.yml, test_system_id.yml, test_unusual_action_cache_revision_characters.yml, test_windows_runner.yml.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/static_analysis.yml:1`
- `.github/workflows/test_all_inputs_override.yml:1`
- `.github/workflows/test_custom_options_file.yml:1`
- `.github/workflows/test_double_checkout.yml:1`
- `.github/workflows/test_empty_pack_with_latest_build.yml:1`
- `.github/workflows/test_empty_resource_pack.yml:1`
- `.github/workflows/test_pack_in_submodule.yml:1`
- `.github/workflows/test_pack_submodule.yml:1`
- `.github/workflows/test_run_in_multiple_steps.yml:1`
- `.github/workflows/test_system_id.yml:1`
- `.github/workflows/test_unusual_action_cache_revision_characters.yml:1`
- `.github/workflows/test_windows_runner.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added top-level `permissions:` blocks to all 13 workflow files under .github/workflows/:
- build.yml: `contents: write` (needs to commit and push built bundle via EndBug/add-and-commit)
- static_analysis.yml: `contents: read` (only needs to check out code for format/lint checks)
- All 11 test_*.yml files: `contents: read` + `actions: write` (checkout + artifact upload and cache operations used by the PackSquash action)

All permissions are scoped to the minimum required for each workflow's operations.

