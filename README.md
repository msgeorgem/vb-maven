# vb-maven

A static Maven repository for Voice Bridge dependencies that aren't on Maven Central.
Served over https from `raw.githubusercontent.com`, so builds need no token.

```yaml
repositories:
  - https://raw.githubusercontent.com/msgeorgem/vb-maven/main
```

## Contents

| Artifact | Source | SHA-256 of the binary |
|----------|--------|-----------------------|
| `com.k2fsa.sherpa.onnx:sherpa-onnx:2.0.1` (aar) | [k2-fsa/sherpa-onnx v2.0.1 release](https://github.com/k2-fsa/sherpa-onnx/releases/tag/v2.0.1), asset `sherpa-onnx-2.0.1.aar`, unmodified | `a8d09d1d32f3eb8520482c6d3d43fae674681c5b050385967c70a3c2c9bf0ee7` |

The binaries are byte-identical to the upstream release assets; compare the hash with
the release's asset digest. Only the POM and checksum files are written here.

## Adding a version

1. Download the upstream asset into `<group path>/<artifact>/<version>/`
2. Check its SHA-256 against the upstream release digest
3. Add a minimal POM (`packaging` matching the file) and `.md5` / `.sha1` / `.sha256` / `.sha512` files for the binary and the POM
4. Add a row to the table above

## Licences

- sherpa-onnx: Apache License 2.0, see [`LICENSE-sherpa-onnx`](LICENSE-sherpa-onnx)
- The AAR bundles ONNX Runtime (`libonnxruntime.so`): MIT License, see [`LICENSE-onnxruntime`](LICENSE-onnxruntime)
