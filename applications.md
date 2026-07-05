# Application-Oriented Resources

국내 NPU, LPU, AI SoC 개발 자료를 응용 분야별로 정리합니다. 제조사별 공식 링크는 [vendors.md](./vendors.md)를 함께 참고하십시오.

## 1. 설치와 드라이버 확인

| Vendor | Start Here | Health Check / First Command |
|---|---|---|
| FuriosaAI | [Driver, Firmware, and Runtime Installation](https://developer.furiosa.ai/docs/latest/en/software/installation.html) | SDK CLI / runtime tool 확인 필요 |
| Rebellions/RBLN | [RBLN Installation Guide](https://docs.rbln.ai/latest/getting_started/installation_guide.html) | `rbln-smi` |
| DEEPX | [DX-Runtime](https://github.com/DEEPX-AI/dx-runtime) | driver/firmware/runtime install logs |
| Mobilint | [Getting Started](https://docs.mobilint.com/v1.0/en/getting_started.html) | device path, runtime import, sample inference |
| HyperAccel | [HyperDex Installation](https://docs.hyperaccel.ai/1.5.2/install_hyperdex/) | `xbutil examine`, package list |

### 설치 전 공통 체크리스트

- [ ] OS 버전, Linux kernel, Python 버전 확인
- [ ] NPU/PCIe 장치가 host에서 인식되는지 확인
- [ ] driver, firmware, runtime, compiler 버전 매트릭스 확인
- [ ] Docker 또는 Kubernetes 사용 시 device mount, privilege, cgroup 설정 확인
- [ ] 공식 sample model로 최소 추론 성공 여부 확인

## 2. 모델 포맷과 변환 경로

| Vendor | Input Model | Compiler / Converter | Runtime Artifact |
|---|---|---|---|
| FuriosaAI | ONNX, TFLite, selected model zoo artifacts | Furiosa compiler / quantization tools | Furiosa executable/runtime artifact |
| Rebellions/RBLN | PyTorch, TensorFlow, Hugging Face models | `rebel-compiler`, Optimum RBLN | `.rbln` compiled model |
| DEEPX | ONNX | DX-COM | `.dxnn` |
| Mobilint | PyTorch, TensorFlow, TFLite, ONNX, Keras | qb Compiler / qubee | `.mxq` |
| HyperAccel | Hugging Face Transformers models | HyperDex AutoCompiler | HyperDex-compatible artifact |

### 모델 변환 체크리스트

- [ ] 원본 모델 라이선스 확인
- [ ] 입력 shape 정적화 가능 여부 확인
- [ ] ONNX opset 및 unsupported op 확인
- [ ] 전처리/후처리 layout 확인: NCHW, NHWC, HWC
- [ ] 정밀도 확인: FP16, FP8, INT8, INT4
- [ ] 양자화 calibration dataset 준비
- [ ] CPU fallback 발생 여부 확인

## 3. LLM 추론 및 OpenAI 호환 서버

| Vendor | Main Stack | Notes |
|---|---|---|
| FuriosaAI | RNGD, Furiosa SDK, vLLM-related materials | 최신 RNGD SDK와 공개 예제 확인 필요 |
| Rebellions/RBLN | `optimum-rbln`, `vllm-rbln`, RBLN SDK | Llama, Qwen, VL 모델 튜토리얼 중심으로 확인 |
| Mobilint | SDK qb, Mobilint Model Zoo, Hugging Face org | batch LLM 지원 범위는 최신 문서 확인 필요 |
| HyperAccel | HyperDex Toolchain, HyperDex Transformers | LPU 기반 LLM inference 특화 |
| DEEPX | DXNN SDK | 공개 자료 기준 vision/edge 중심, LLM decoder 지원은 확인 필요 |

### 관련 링크

- [RBLN vLLM](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html)
- [RBLN Optimum](https://docs.rbln.ai/latest/software/optimum/)
- [HyperDex Hugging Face API](https://docs.hyperaccel.ai/1.5.2/huggingface_api/)
- [HyperDex Quick Start](https://docs.hyperaccel.ai/1.5.3/quick_start/)
- [Mobilint Hugging Face Organization](https://huggingface.co/mobilint)
- [Furiosa RNGD Product Page](https://furiosa.ai/rngd)

### LLM Serving 체크리스트

- [ ] 모델 크기와 NPU 메모리 또는 HBM 용량 확인
- [ ] prefill/decode 분리 또는 hybrid serving 구조 확인
- [ ] max sequence length, batch size, concurrent users 조건 명시
- [ ] OpenAI-compatible API server 지원 여부 확인
- [ ] streaming response, tokenizer, chat template 처리 확인
- [ ] cold start compile 시간과 warm inference 성능 분리 측정

## 4. Vision / Edge AI 추론

| Vendor | Main Stack | Suitable Workloads |
|---|---|---|
| FuriosaAI | Furiosa SDK, Furiosa Models, Warboy Vision Models | Classification, detection, pose, segmentation |
| DEEPX | DXNN SDK, DX-Runtime, DX-Stream, DX Model Zoo | Edge vision, camera pipeline, industrial AI |
| Mobilint | SDK qb, Model Zoo, `.mxq` runtime | Detection, segmentation, classification, super resolution |
| Rebellions/RBLN | RBLN SDK, TensorFlow/PyTorch model path | Vision model compile and serving |
| HyperAccel | Not primary | LLM 중심 |

### 관련 링크

- [Furiosa Models](https://github.com/furiosa-ai/furiosa-models)
- [Furiosa Warboy Vision Models](https://github.com/furiosa-ai/warboy-vision-models)
- [Furiosa YOLOv5s](https://github.com/furiosa-ai/yolov5s)
- [DEEPX DX Model Zoo](https://developer.deepx.ai/modelzoo/)
- [DEEPX DX-Runtime](https://github.com/DEEPX-AI/dx-runtime)
- [Mobilint Model Zoo](https://docs.mobilint.com/v0.28/en/model_zoo.html)

### Vision 체크리스트

- [ ] 입력 해상도와 FPS 목표 정의
- [ ] RGB/BGR, NCHW/NHWC, normalization 일치 여부 확인
- [ ] camera input, video file, RTSP, GStreamer pipeline 구분
- [ ] post-processing이 NPU 외부에서 CPU 병목이 되는지 확인
- [ ] end-to-end latency와 model-only latency를 분리 측정

## 5. Multimodal / Vision-Language

| Vendor | Resource | Notes |
|---|---|---|
| Rebellions/RBLN | [RBLN SDK User Guide](https://docs.rbln.ai/latest/index.html) | Qwen VL 계열 튜토리얼 존재 여부 확인 |
| FuriosaAI | [Furiosa SDK 2026.3 Blog](https://furiosa.ai/blog/furiosa-sdk-2026-3-a-new-kernel-framework-and-the-models-it-unlocks) | Qwen3-VL 등 최신 모델 지원 범위 확인 필요 |
| Mobilint | [Mobilint Hugging Face](https://huggingface.co/mobilint) | multimodal model resources 확인 필요 |
| DEEPX | [DX Model Zoo](https://developer.deepx.ai/modelzoo/) | vision 중심, VLM은 최신 공식 자료 확인 필요 |
| HyperAccel | [HyperDex Toolchain](https://docs.hyperaccel.ai/1.5.3/hyperdex_toolchain/) | transformer LLM 중심 |

### Multimodal 체크리스트

- [ ] image encoder와 text decoder가 같은 런타임에서 처리되는지 확인
- [ ] vision encoder만 NPU 가속하고 decoder는 CPU/GPU 처리하는 hybrid 구조인지 확인
- [ ] tokenizer, image processor, chat template 호환성 확인
- [ ] image resolution, number of images, context length 조건 명시

## 6. Model Serving / MLOps

| Serving Layer | FuriosaAI | Rebellions/RBLN | DEEPX | Mobilint | HyperAccel |
|---|---|---|---|---|---|
| OpenAI-compatible server | 확인 필요 | `vllm-rbln` | 확인 필요 | 확인 필요 | HyperDex/vLLM-oriented support 확인 |
| vLLM | RNGD materials 확인 | Documented | 확인 필요 | 확인 필요 | Mentioned |
| Triton | 확인 필요 | Documented | 확인 필요 | 확인 필요 | 확인 필요 |
| TorchServe | 확인 필요 | Documented | 확인 필요 | 확인 필요 | 확인 필요 |
| Ray Serve | 확인 필요 | Documented | 확인 필요 | 확인 필요 | 확인 필요 |
| GStreamer | 확인 필요 | 확인 필요 | DX-Stream | 확인 필요 | Not primary |

### 관련 링크

- [RBLN vLLM](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html)
- [RBLN Triton Support](https://docs.rbln.ai/latest/software/model_serving/triton_support/)
- [RBLN TorchServe Support](https://docs.rbln.ai/latest/software/model_serving/torchserve_support/)
- [RBLN Ray Serve Support](https://docs.rbln.ai/latest/software/model_serving/ray_serve_support/)
- [DEEPX DX-Runtime](https://github.com/DEEPX-AI/dx-runtime)

## 7. Kubernetes / Cloud Native

| Vendor | Resource | Notes |
|---|---|---|
| Rebellions/RBLN | [RBLN Kubernetes NPU Feature Discovery](https://docs.rbln.ai/latest/software/system_management/kubernetes/npu_feature_discovery.html) | Node labels, device discovery |
| Rebellions/RBLN | [rbln-npu-feature-discovery](https://github.com/rebellions-sw/rbln-npu-feature-discovery) | Kubernetes node feature discovery |
| FuriosaAI | [furiosa-sdk GitHub](https://github.com/furiosa-ai/furiosa-sdk) | Device plugin 자료 확인 필요 |
| DEEPX | [DX-Runtime](https://github.com/DEEPX-AI/dx-runtime) | Container support 확인 필요 |
| Mobilint | [SDK qb Docs](https://docs.mobilint.com/v1.2/en/introduction.html) | Container/K8s 공개 자료 확인 필요 |
| HyperAccel | [HyperDex Installation](https://docs.hyperaccel.ai/1.5.2/install_hyperdex/) | XRT/FPGA device pass-through 확인 필요 |

### Kubernetes 체크리스트

- [ ] node에 NPU driver 설치
- [ ] device plugin 또는 feature discovery 구성
- [ ] pod에서 `/dev/*`, sysfs, runtime library 접근 가능 여부 확인
- [ ] node label, taint/toleration, resource request 설정
- [ ] multi-NPU scheduling과 isolation 정책 확인

## 8. Benchmark / 성능 측정

### 공식 자료

- [Furiosa RNGD Product Page](https://furiosa.ai/rngd)
- [Furiosa SDK 2026.3 Blog](https://furiosa.ai/blog/furiosa-sdk-2026-3-a-new-kernel-framework-and-the-models-it-unlocks)
- [Rebellions Developers](https://rebellions.ai/developers/)
- [DEEPX DX Model Zoo](https://developer.deepx.ai/modelzoo/)
- [Mobilint SDK qb](https://www.mobilint.com/sdk-qb)
- [HyperAccel Software](https://hyperaccel.ai/ha_product/software/)

### 논문 / 학술 자료

- [LPU: A Latency-Optimized and Highly Scalable Processor for Large Language Model Inference](https://arxiv.org/abs/2408.07326)

### 커뮤니티 재현 사례

- [DEEPX DX-M1 on Raspberry Pi 5 - GitHub](https://github.com/zlorenzini/pi-m1)
- [DEEPX DX-M1 on Raspberry Pi 5 - Reddit discussion](https://www.reddit.com/r/rasberrypi/comments/1rl9sse/i_got_the_deepx_dxm1_pcie_npu_fully_working_on/)

### Benchmark Report Template

````markdown
## Benchmark Report

| Field | Value |
|---|---|
| Vendor |  |
| Hardware |  |
| Host CPU/RAM |  |
| OS/Kernel |  |
| SDK/driver/runtime |  |
| Model |  |
| Dataset / prompt |  |
| Precision |  |
| Batch size |  |
| Input length |  |
| Output length |  |
| Metric | latency / throughput / tokens/sec / FPS / power / accuracy |
| Result |  |
| Measurement command |  |
| Measurement tool |  |
| Power measurement method | board / chip / system / estimated |
| Reproducibility | single run / repeated / independently reproduced |

## Command

```bash

```

## Raw Output

```text

```
````

## 9. Troubleshooting

| Problem | Likely Cause | First Check |
|---|---|---|
| Device not detected | Driver/firmware mismatch, PCIe issue, permission issue | Vendor health-check command, `lspci`, `dmesg` |
| Compiler fails | Unsupported op, dynamic shape, opset mismatch | Supported ops list, static input shape |
| Model output is wrong | Pre/post-processing mismatch, quantization issue | Calibration dataset, normalization, layout NCHW/NHWC |
| Runtime segmentation fault | Version mismatch, invalid compiled artifact | Driver-runtime-compiler compatibility matrix |
| Poor performance | CPU fallback, wrong batch, unoptimized precision | Runtime logs, profiler, device utilization |
| vLLM server fails | Plugin/version mismatch | vLLM, PyTorch, plugin version matrix |
| Docker cannot see NPU | Device mount/cgroup/privilege issue | Container runtime, `/dev/*`, Kubernetes device plugin |

### Installation Issue Template

````markdown
## Environment

- Vendor:
- Hardware:
- Host:
- OS:
- Kernel:
- Python:
- SDK version:
- Driver version:
- Runtime version:
- Compiler version:
- Container/Docker:

## Goal

What are you trying to run?

## Steps to Reproduce

1.
2.
3.

## Expected Result

## Actual Result

```bash
paste error log here
```

## What I Tried

- [ ] Reinstalled driver
- [ ] Checked device with vendor health-check command
- [ ] Checked version matrix
- [ ] Tried official sample
- [ ] Tried precompiled model
- [ ] Tried clean virtual environment

## Related Links

- Docs:
- Model:
- Issue/PR:
````

## 10. 확인 필요 목록

- [ ] Furiosa RNGD 최신 SDK 문서 버전과 공개 개발자 문서 URL 정리
- [ ] Furiosa vLLM / Hugging Face / gpt-oss / Qwen3-VL 공개 예제 확인
- [ ] Rebellions 최신 `docs.rbln.ai/latest` 세부 경로 안정성 확인
- [ ] Rebellions-SAPEON 통합 이후 제품명/SDK명 변화 확인
- [ ] DEEPX LLM/Transformer decoder 지원 범위 공식 확인
- [ ] DEEPX DX-COM 공개 설치 경로와 Docker workflow 정리
- [ ] Mobilint SDK qb v1.2 이후 batch LLM 지원 범위 검증
- [ ] Mobilint Model Zoo GitHub repository URL 확인
- [ ] HyperAccel HyperDex public model zoo / GitHub 공개 여부 확인
- [ ] 각 회사별 MLPerf 결과와 공식 제출 링크 정리
