<!-- markdownlint-disable -->

# Hardening Report: ComunidadAylas--PackSquash-action/v4.0.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ComunidadAylas--PackSquash-action/v4.0.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

None of the 13 workflow files under .github/workflows/ define a top-level permissions: key, and no job within any of these files defines its own permissions: key. Without explicit permissions, workflows inherit the default repository permissions, violating the principle of least privilege.

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
- build.yml: `contents: write` (needed for the EndBug/add-and-commit step that commits and pushes the built action bundle)
- static_analysis.yml: `contents: read` (read-only linting workflow)
- test_all_inputs_override.yml: `contents: read`
- test_custom_options_file.yml: `contents: read`
- test_double_checkout.yml: `contents: read`
- test_empty_pack_with_latest_build.yml: `contents: read`
- test_empty_resource_pack.yml: `contents: read`
- test_pack_in_submodule.yml: `contents: read`
- test_pack_submodule.yml: `contents: read`
- test_run_in_multiple_steps.yml: `contents: read`
- test_system_id.yml: `contents: read`
- test_unusual_action_cache_revision_characters.yml: `contents: read`
- test_windows_runner.yml: `contents: read`

All permissions follow the principle of least privilege — only the minimum required permissions are granted.

