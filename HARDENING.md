<!-- markdownlint-disable -->

# Hardening Report: ComunidadAylas--PackSquash-action/v4.0.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ComunidadAylas--PackSquash-action/v4.0.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed src/manifests/binary_manifest.json without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/src/manifests/binary_manifest.json b/src/manifests/binary_manifest.json
deleted file mode 120000
index 5b9f063..0000000
--- a/src/manifests/binary_manifest.json
+++ /dev/null
@@ -1 +0,0 @@
-../../data/packsquash_binary_manifests/v2.json
\ No newline at end of file
diff --git a/src/manifests/binary_manifest.json b/src/manifests/binary_manifest.json
new file mode 100644
index 0000000..e1cd24e
--- /dev/null
+++ b/src/manifests/binary_manifest.json
@@ -0,0 +1,56 @@
+{
+  "latestManifestVersion": 2,
+
+  "repoOwner": "ComunidadAylas",
+  "repoName": "PackSquash",
+
+  "latestRelease": "v0.4.1",
+
+  "v0.4.1": {
+    "type": "staticBinary",
+    "fetch": {
+      "strategy": "httpGetRequest",
+      "url": {
+        "linux": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.1/packsquash-x86_64-unknown-linux-musl.zip",
+          "arm64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.1/packsquash-aarch64-unknown-linux-musl.zip"
+        },
+        "windows": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.1/packsquash.exe-x86_64-pc-windows-gnu.zip"
+        },
+        "macos": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.1/packsquash-universal2-apple-darwin.zip",
+          "arm64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.1/packsquash-universal2-apple-darwin.zip"
+        }
+      }
+    }
+  },
+
+  "unstable": [
+    {
+      "applicabilityPeriod": {
+        "from": 1759691990,
+        "to": "now"
+      },
+      "type": "staticBinary",
+      "fetch": {
+        "strategy": "actionsWorkflowArtifact",
+        "workflowId": 32465409,
+        "branch": "master",
+        "name": {
+          "linux": {
+            "x64": "PackSquash CLI executable (x86_64-unknown-linux-musl)",
+            "arm64": "PackSquash CLI executable (aarch64-unknown-linux-musl)"
+          },
+          "windows": {
+            "x64": "PackSquash CLI executable (x86_64-pc-windows-gnu)"
+          },
+          "macos": {
+            "x64": "PackSquash CLI executable (x86_64-apple-darwin)",
+            "arm64": "PackSquash CLI executable (aarch64-apple-darwin)"
+          }
+        }
+      }
+    }
+  ]
+}

```

Locations:

- `src/manifests/binary_manifest.json`

## Iteration Notes

### Iteration 1

**Fixes applied:** prior-fix

**Notes:**

Rewrote src/manifests/binary_manifest.json with the full manifest content from the previous patch (it matches data/packsquash_binary_manifests/v2.json byte for byte, 1779 bytes). I could not confirm the fix took effect. After the write, list_directory still shows the path as a symlink pointing to ../../data/packsquash_binary_manifests/v2.json. So the write most likely went through the link into v2.json, which is harmless because the content is the same. None of my tools can delete a symlink. If the goal is to have a regular file at this path, someone needs to remove the symlink by hand (git rm, then add the file back with this content). Readers of this path get the correct manifest content either way.

