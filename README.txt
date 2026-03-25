
Read-only filesystem write failure
----------------------------------
Making .tmp/ro-kustomize read-only
Running flux build kustomization against read-only directory...
---
✗ failed to generate kustomization.yaml: failed to save original kustomization.yaml: open .tmp/ro-kustomize/kustomization.yaml.original: permission denied <nil> <nil>
---
Exit code: 1

Concurrent flux build file contention
-------------------------------------
Spawning 30 concurrent 'flux build kustomization' against ./kustomize
---
Succeeded: 26/30
Failed:    4/30

process 4 stderr:
✗ failed to cleanup repository: rename kustomize/kustomization.yaml.original kustomize/kustomization.yaml: no such file or directory

process 8 stderr:
✗ kustomize build failed: kustomization.yaml is empty

process 24 stderr:
✗ failed to cleanup repository: rename kustomize/kustomization.yaml.original kustomize/kustomization.yaml: no such file or directory

process 25 stderr:
✗ failed to cleanup repository: rename kustomize/kustomization.yaml.original kustomize/kustomization.yaml: no such file or directory

Orphaned artifacts from killed builds
-------------------------------------
Launching 50 concurrent flux builds, then killing all via SIGKILL
---
Leftover .original files: 0
Orphaned TMPDIR entries:  0
kustomization.yaml corrupted: YES
