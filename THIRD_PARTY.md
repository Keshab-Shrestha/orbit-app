# Third-party models

## Parakeet TDT 0.6B v3 (default speech-to-text model)

- Model: Parakeet TDT 0.6B v3, made by NVIDIA.
- Licence: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).
- GGUF conversion (Q8_0): handy-computer.
- Source: https://huggingface.co/handy-computer/parakeet-tdt-0.6b-v3-gguf
- Revision: `85ac09ea12fc4b1112fa76810059364bc6adc9de`
- File: `parakeet-tdt-0.6b-v3-Q8_0.gguf`, 739508576 bytes.
- SHA-256: `5859f77944efcd8eafa23a6350731960b2b55b2203df51f319665c807d802cc7`

Orbit does not ship the file. The sidecar downloads it on first use and checks the SHA-256.
Orbit made no change to the model weights.

## Kokoro-82M (text-to-speech voice, "Read aloud")

- Model: Kokoro-82M v1.0, made by hexgrad.
- Licence: Apache-2.0 (https://www.apache.org/licenses/LICENSE-2.0).
- ONNX conversion: onnx-community.
- Source: https://huggingface.co/onnx-community/Kokoro-82M-v1.0-ONNX
- Revision: `1939ad2a8e416c0acfeecc08a694d14ef25f2231`
- Files: the 8-bit model `onnx/model_quantized.onnx` (92361116 bytes, SHA-256 `fbae9257e1e05ffc727e951ef9b9c98418e6d79f1c9b6b13bd59f5c9028a1478`), `tokenizer.json`, `config.json` and 55 voice files in `voices/` (121089905 bytes in total).
- The SHA-256 of every file is in `sidecar/src/speech/tts/kokoro-manifest.json`. The sidecar refuses a file that does not match.

Orbit does not ship these files. The sidecar downloads them when the user presses Download in Settings, Voice, Read aloud.
Orbit made no change to the model weights.

## Libraries that run Kokoro

| Package | Version | Licence | Notes |
| --- | --- | --- | --- |
| kokoro-js | 1.2.1 | Apache-2.0 | By hexgrad. Text rules and the Kokoro model wrapper. |
| @huggingface/transformers | 3.8.1 | Apache-2.0 | ONNX model loader. Orbit sets it to read local files only. |
| @huggingface/jinja | 0.5.12 | MIT | Dependency of transformers.js. |
| onnxruntime-node | 1.21.0 | MIT | Microsoft ONNX Runtime with a Node binding. Orbit stages the Mac arm64 binary only. |
| onnxruntime-common | 1.21.0 | MIT | Dependency of onnxruntime-node. |
| phonemizer | 1.2.1 | Apache-2.0 (wrapper) | Contains eSpeak NG compiled to WebAssembly. See the warning below. |
| sharp | 0.34.5 | Apache-2.0 | Image library that transformers.js loads. Not used for speech. |
| @img/sharp-libvips-darwin-arm64 | 1.2.4 | LGPL-3.0-or-later | Native image code that sharp loads. |

Warning for the owner. The phonemizer package holds eSpeak NG, which has the licence GPL-3.0-or-later.
The wrapper package says Apache-2.0, but the WebAssembly inside it is eSpeak NG code.
Orbit is MIT. Shipping the eSpeak NG code in the app may need a GPL notice and an offer of its source.
The sidecar loads phonemizer only through kokoro-js, in a child process.
This is an open decision. See ADR-008.
The libvips code is LGPL. It needs a notice and must stay replaceable.
