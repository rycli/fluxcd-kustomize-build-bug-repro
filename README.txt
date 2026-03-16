
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

WriteFile/CleanDirectory race simulation
----------------------------------------
Simulating WriteFile/CleanDirectory race with 20 processes x 50 iterations
Original checksum: a4709e6861f59978ace6364984c70a7bbed8023d8d7f085219a02366c7045b1b
---
Total I/O errors across all processes: 296

Expected checksum: a4709e6861f59978ace6364984c70a7bbed8023d8d7f085219a02366c7045b1b
Final checksum:    01ba4719c80b6fe911b091a7c05124b64eeece964e09c058ef8f9805daca546b
Checksums match:   no

Final content:

Orphaned artifacts from killed builds
-------------------------------------
Launching 50 concurrent flux builds, then killing all via SIGKILL
---
Leftover .original files: 0
Orphaned TMPDIR entries:  0
kustomization.yaml corrupted: YES
