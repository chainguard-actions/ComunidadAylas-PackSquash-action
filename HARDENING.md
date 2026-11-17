<!-- markdownlint-disable -->

# Hardening Report: ComunidadAylas--PackSquash-action/v4.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ComunidadAylas--PackSquash-action/v4.0.3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed src/manifests/binary_manifest.json without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/src/manifests/binary_manifest.json b/src/manifests/binary_manifest.json
deleted file mode 120000
index 91adf1f..0000000
--- a/src/manifests/binary_manifest.json
+++ /dev/null
@@ -1 +0,0 @@
-../../data/packsquash_binary_manifests/v1.json
\ No newline at end of file
diff --git a/src/manifests/binary_manifest.json b/src/manifests/binary_manifest.json
new file mode 100644
index 0000000..4b31d65
--- /dev/null
+++ b/src/manifests/binary_manifest.json
@@ -0,0 +1,87 @@
+{
+  "latestManifestVersion": 1,
+
+  "repoOwner": "ComunidadAylas",
+  "repoName": "PackSquash",
+
+  "latestRelease": "v0.4.0",
+
+  "v0.4.0": {
+    "type": "staticBinary",
+    "fetch": {
+      "strategy": "httpGetRequest",
+      "url": {
+        "linux": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.0/PackSquash.CLI.executable.x86_64-unknown-linux-musl.zip",
+          "arm64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.0/PackSquash.CLI.executable.aarch64-unknown-linux-musl.zip"
+        },
+        "windows": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.0/PackSquash.CLI.executable.x86_64-pc-windows-gnu.zip"
+        },
+        "macos": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.0/PackSquash.CLI.executable.universal-apple-darwin.zip",
+          "arm64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.4.0/PackSquash.CLI.executable.universal-apple-darwin.zip"
+        }
+      }
+    }
+  },
+
+  "v0.3.1": {
+    "type": "appImage",
+    "fetch": {
+      "strategy": "httpGetRequest",
+      "url": {
+        "linux": {
+          "x64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.3.1/PackSquash-v0.3.1-x86_64.AppImage",
+          "arm64": "https://github.com/ComunidadAylas/PackSquash/releases/download/v0.3.1/PackSquash-v0.3.1-aarch64.AppImage"
+        }
+      }
+    }
+  },
+
+  "unstable": [
+    {
+      "applicabilityPeriod": {
+        "from": 1685981019,
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
+    },
+    {
+      "applicabilityPeriod": {
+        "from": 0,
+        "to": 1685981018
+      },
+      "type": "appImage",
+      "fetch": {
+        "strategy": "actionsWorkflowArtifact",
+        "workflowId": 32465409,
+        "branch": "master",
+        "name": {
+          "linux": {
+            "x64": "PackSquash CLI AppImage (x86_64)",
+            "arm64": "PackSquash CLI AppImage (aarch64)"
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

**Notes:**

prior-fix is NOT fixed. The previous harden replaced the symlink src/manifests/binary_manifest.json (which points to ../../data/packsquash_binary_manifests/v1.json) with a regular file holding the same 87-line manifest. I wrote that exact content (2679 bytes, the same as v1.json) to the path. Listing the directory afterwards still shows a symlink with the same target, so write_file seems to have written through the link instead of replacing it. I have no tool that can delete a symlink, so I couldn't turn it into a regular file. The file's content is correct, but someone needs to remove the symlink by hand and commit the regular file, as the previous patch did.

