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
| `com.example.mypaiab.models:silero-vad:1` (aar) | packaged here: the unmodified `silero_vad.onnx` from the [sherpa-onnx `asr-models` release](https://github.com/k2-fsa/sherpa-onnx/releases/tag/asr-models) as `assets/silero_vad.onnx` | aar `97693b32bbbc3a8367b7431569c775ef130fd4862a57d543777f2c6138a753cb`, model inside `9e2449e1087496d8d4caba907f23e0bd3f78d91fa552479bb9c23ac09cbb1fd6` |

The upstream binaries are byte-identical to the upstream release assets; compare the hash with
the release's asset digest. Only the POM and checksum files are written here.

`silero-vad` is the one artifact built in this repository rather than mirrored: it is a plain
asset-only AAR (`AndroidManifest.xml`, an empty `classes.jar`, empty `R.txt`,
`assets/silero_vad.onnx`) so the app can ship the VAD model without committing a model file to
the app repository. The model itself is unmodified; verify it by unzipping the aar and hashing
`assets/silero_vad.onnx`.

## Releases (large model files)

Files too big for a Maven artifact live as release assets, pinned by tag:

| Tag | Contents |
|-----|----------|
| [`models-whisper-turbo-v1`](https://github.com/msgeorgem/vb-maven/releases/tag/models-whisper-turbo-v1) | Whisper large-v3-turbo int8 (encoder, decoder, tokens), byte-identical to [csukuangfj/sherpa-onnx-whisper-turbo](https://huggingface.co/csukuangfj/sherpa-onnx-whisper-turbo) at commit `2ca6ff69fc878651b770880507669577ac41c2ff`. Per-file SHA-256 in the release notes |

The app downloads these on first launch and verifies every file against the SHA-256 in its own
manifest before installing anything.

## Adding a version

1. Download the upstream asset into `<group path>/<artifact>/<version>/`
2. Check its SHA-256 against the upstream release digest
3. Add a minimal POM (`packaging` matching the file) and `.md5` / `.sha1` / `.sha256` / `.sha512` files for the binary and the POM
4. Add a row to the table above

## Licences

- sherpa-onnx: Apache License 2.0, see [`LICENSE-sherpa-onnx`](LICENSE-sherpa-onnx)
- The AAR bundles ONNX Runtime (`libonnxruntime.so`): MIT License, see [`LICENSE-onnxruntime`](LICENSE-onnxruntime)
- Silero VAD model: MIT License, see [`LICENSE-silero-vad`](LICENSE-silero-vad)
- Whisper model weights (release assets): MIT License (OpenAI)
