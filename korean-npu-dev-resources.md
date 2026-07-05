# Awesome Korean NPU Developer Resources

FuriosaAI, Rebellions, DEEPX, Mobilint, HyperAccel 등 국내 NPU/AI SoC를 사용하는 개발자를 위한 문서, SDK, 모델 호환성, 설치 이슈, 벤치마크 큐레이션 저장소입니다.

> Status: draft  
> Last updated: 2026-07-06  
> Scope: Korean AI accelerator / NPU / LPU / edge AI SoC developer resources  
> Primary audience: open-source developers, AI inference engineers, edge AI builders, robotics/vision developers, MLOps engineers

## 목적

국내 AI 반도체 생태계는 회사별 SDK, 모델 포맷, 문서, 배포 방식, 지원 모델이 서로 다릅니다. 이 저장소는 개발자가 다음 질문에 빠르게 답할 수 있도록 돕는 것을 목표로 합니다.

- 어떤 하드웨어가 LLM, 비전, 멀티모달, 엣지 추론에 적합한가?
- SDK 설치와 드라이버 확인은 어디서 시작하는가?
- 지원 모델, 모델 변환, 컴파일, 런타임 포맷은 무엇인가?
- Hugging Face, PyTorch, TensorFlow, ONNX, vLLM, Triton과 어느 정도 연결되는가?
- 설치 오류, 버전 충돌, 모델 호환성 문제는 어디서 확인하고 기록할 수 있는가?
- 벤치마크 자료는 공식, 논문, 커뮤니티 재현 사례 중 어디에 속하는가?

## 빠른 비교

| Vendor | Main Hardware / Product | Main Workload | SDK / Runtime | Model Format | Public Docs | Public Model Resources | Access Notes |
|---|---|---|---|---|---|---|---|
| FuriosaAI | Warboy, RNGD | Vision, LLM, multimodal inference | Furiosa SDK, runtime, compiler, vLLM-related stack | ONNX, TFLite, SDK-compiled artifacts | Yes | Furiosa model zoo, Warboy vision examples | Some driver/firmware access may require evaluation program |
| Rebellions / RBLN | ATOM, REBEL family | LLM, vision, diffusion, serving | RBLN SDK, rebel-compiler, optimum-rbln, vllm-rbln, torch-rbln | RBLN compiled artifacts | Yes | RBLN supported models, Optimum RBLN | Compiler/portal access may be required |
| DEEPX | DX-M1, DX-M1 M.2, DX-M1 SoC family | Edge vision, industrial AI, multimedia pipeline | DXNN SDK, DX-AS, DX-COM, DX-RT, DX-Stream | ONNX -> `.dxnn` | Yes | DX Model Zoo | Current public resources are strongest for vision/edge workloads |
| Mobilint | ARIES MLA100, REGULUS SoC/SoM | Edge AI, vision, language, multimodal | SDK qb, qb Runtime, qb Compiler | `.mxq` | Yes | Mobilint Model Zoo, Hugging Face org, PyPI packages | Compiler/download center access may be required |
| HyperAccel | LPU, HyperDex | LLM inference | HyperDex Toolchain, HyperDex transformers, vLLM-oriented stack | HyperDex-compiled LLM artifacts | Yes | Docs mention model zoo/dev page; public access varies | Private PyPI / licensing credentials may be required |
| SAPEON legacy | X220, X330 | Datacenter inference | Legacy/public information limited | 확인 필요 | Limited | 확인 필요 | Rebellions-SAPEON integration status should be tracked separately |

## 저장소 구조 제안

```text
.
├── README.md
├── vendors/
│   ├── furiosaai.md
│   ├── rebellions-rbln.md
│   ├── deepx.md
│   ├── mobilint.md
│   ├── hyperaccel.md
│   └── sapeon-legacy.md
├── compatibility/
│   ├── model-formats.md
│   ├── supported-models.md
│   ├── framework-support.md
│   └── version-matrix.md
├── benchmarks/
│   ├── official.md
│   ├── mlperf.md
│   ├── papers.md
│   └── community-repro.md
├── troubleshooting/
│   ├── driver-runtime.md
│   ├── compiler.md
│   ├── model-conversion.md
│   ├── container-kubernetes.md
│   └── known-issues.md
├── examples/
│   ├── vision.md
│   ├── llm-serving.md
│   ├── multimodal.md
│   └── edge-deployment.md
└── CONTRIBUTING.md
```

## 태그 체계

GitHub Issue/PR 라벨로 다음 태그를 권장합니다.

| Label | Meaning |
|---|---|
| `vendor/furiosaai` | FuriosaAI 관련 문서, SDK, 모델, 이슈 |
| `vendor/rbln` | Rebellions / RBLN 관련 항목 |
| `vendor/deepx` | DEEPX 관련 항목 |
| `vendor/mobilint` | Mobilint 관련 항목 |
| `vendor/hyperaccel` | HyperAccel 관련 항목 |
| `topic/install` | 드라이버, 런타임, SDK 설치 |
| `topic/model-zoo` | 모델 주, 지원 모델, 사전 컴파일 모델 |
| `topic/compiler` | 모델 변환, 컴파일러, 양자화 |
| `topic/runtime` | Python/C++ 런타임, inference API |
| `topic/serving` | vLLM, Triton, TorchServe, Ray Serve, API server |
| `topic/kubernetes` | K8s, device plugin, operator, feature discovery |
| `topic/benchmark` | 성능 측정, MLPerf, 논문, 재현 벤치마크 |
| `topic/troubleshooting` | 설치 실패, 드라이버 인식, segmentation fault, 버전 충돌 |
| `status/verified` | 실제 실행 검증 완료 |
| `status/needs-check` | 최신성 또는 실행 검증 필요 |

## 1. FuriosaAI

### 공식 사이트 및 제품

- [FuriosaAI Homepage](https://furiosa.ai/)
- [Furiosa RNGD Product Page](https://furiosa.ai/rngd)
- [Furiosa SDK 2026.3 Release Blog](https://furiosa.ai/blog/furiosa-sdk-2026-3-a-new-kernel-framework-and-the-models-it-unlocks)
- [Furiosa Access Program](https://furiosa.ai/rngd)

### 문서

- [FuriosaAI SDK Documentation](https://developer.furiosa.ai/docs/v0.5.0/en/)
- [FuriosaAI Driver, Firmware, and Runtime Installation](https://developer.furiosa.ai/docs/latest/en/software/installation.html)
- [FuriosaAI Command Line Tools Quickstart](https://developer.furiosa.ai/docs/v0.5.0/en/quickstart/cli.html)
- [FuriosaAI SW Stack Introduction](https://developer.furiosa.ai/docs/v0.6.0/en/software/intro.html)
- [FuriosaAI NPU Acceleration Operators List](https://developer.furiosa.ai/docs/v0.5.0/en/advanced/supported_operators.html)

### GitHub

- [furiosa-ai GitHub Organization](https://github.com/furiosa-ai)
- [furiosa-ai/furiosa-sdk](https://github.com/furiosa-ai/furiosa-sdk)
- [furiosa-ai/furiosa-models](https://github.com/furiosa-ai/furiosa-models)
- [furiosa-ai/warboy-vision-models](https://github.com/furiosa-ai/warboy-vision-models)
- [furiosa-ai/yolov5s](https://github.com/furiosa-ai/yolov5s)
- [furiosa-ai/furiosa-rngd-validator](https://github.com/furiosa-ai/furiosa-rngd-validator)
- [furiosa-ai/inference-compression releases](https://github.com/furiosa-ai/inference-compression/releases)

### 모델 및 호환성

| Resource | Link | Notes |
|---|---|---|
| Furiosa Models | [furiosa-models](https://github.com/furiosa-ai/furiosa-models) | Public pre-trained and pre-quantized models for FuriosaAI NPU |
| Warboy Vision Models | [warboy-vision-models](https://github.com/furiosa-ai/warboy-vision-models) | Object detection, pose estimation, instance segmentation examples |
| YOLOv5s example | [yolov5s](https://github.com/furiosa-ai/yolov5s) | YOLOv5s compile/eval example using Furiosa SDK |

### 벤치마크 및 검증 자료

- [Furiosa RNGD Product Page - performance overview](https://furiosa.ai/rngd)
- [Furiosa SDK 2026.3 Blog](https://furiosa.ai/blog/furiosa-sdk-2026-3-a-new-kernel-framework-and-the-models-it-unlocks)
- [furiosa-ai/inference-compression releases](https://github.com/furiosa-ai/inference-compression/releases)

### 설치/운영 체크리스트

- [ ] SDK 버전과 대상 하드웨어가 일치하는지 확인
- [ ] Kernel driver, firmware, runtime 설치 경로 확인
- [ ] `furiosa` CLI 또는 런타임 헬스체크 명령 확인
- [ ] ONNX/TFLite 입력 모델의 opset과 지원 연산 확인
- [ ] 양자화 후 정확도 저하 여부 측정
- [ ] Docker/컨테이너 환경에서 디바이스 패스스루 확인

## 2. Rebellions / RBLN

### 공식 사이트 및 개발자 페이지

- [Rebellions Homepage](https://rebellions.ai/)
- [Rebellions Developers](https://rebellions.ai/developers/)
- [RBLN SDK User Guide](https://docs.rbln.ai/latest/index.html)
- [RBLN Installation Guide](https://docs.rbln.ai/latest/getting_started/installation_guide.html)
- [RBLN Quick Start](https://docs.rbln.ai/v0.10.4/getting_started/quick_start.html)

### 핵심 SDK 문서

- [RBLN Compiler API Overview](https://docs.rbln.ai/latest/software/api/)
- [RBLN C/C++ Runtime API Tutorials](https://docs.rbln.ai/latest/getting_started/tutorials.html)
- [RBLN Optimum - Hugging Face Model Support](https://docs.rbln.ai/latest/software/optimum/)
- [RBLN Optimum Installation](https://docs.rbln.ai/v0.10.0/software/optimum/installation.html)
- [PyTorch RBLN](https://docs.rbln.ai/v0.10.0/software/rbln_pytorch/overview.html)
- [vLLM RBLN](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html)
- [RBLN Profiler](https://docs.rbln.ai/latest/software/profiler/index.html)

### GitHub

- [RBLN-SW GitHub Organization](https://github.com/RBLN-SW)
- [RBLN-SW/optimum-rbln](https://github.com/RBLN-SW/optimum-rbln)
- [RBLN-SW/torch-rbln](https://github.com/RBLN-SW/torch-rbln)
- [RBLN-SW/rbln-npu-feature-discovery](https://github.com/rebellions-sw/rbln-npu-feature-discovery)

### Serving / MLOps / Cloud Native

- [vLLM RBLN - OpenAI Compatible Server and tutorials](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html)
- [NVIDIA Triton Inference Server Support](https://docs.rbln.ai/latest/software/model_serving/triton_support/)
- [TorchServe Support](https://docs.rbln.ai/latest/software/model_serving/torchserve_support/)
- [Ray Serve Support](https://docs.rbln.ai/latest/software/model_serving/ray_serve_support/)
- [RBLN Kubernetes NPU Feature Discovery](https://docs.rbln.ai/latest/software/system_management/kubernetes/npu_feature_discovery.html)
- [rbln-npu-feature-discovery GitHub](https://github.com/rebellions-sw/rbln-npu-feature-discovery)

### 모델 및 호환성

| Resource | Link | Notes |
|---|---|---|
| Supported Models | [RBLN SDK User Guide](https://docs.rbln.ai/latest/index.html) | Optimum, PyTorch, TensorFlow model support entry point |
| Optimum RBLN | [optimum-rbln](https://github.com/RBLN-SW/optimum-rbln) | Hugging Face Transformers/Diffusers integration |
| vLLM RBLN | [vLLM RBLN docs](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html) | LLM serving plugin |
| PyTorch RBLN | [torch-rbln docs](https://docs.rbln.ai/v0.10.0/software/rbln_pytorch/overview.html) | PyTorch extension, beta status should be checked |

### 설치/운영 체크리스트

- [ ] `rbln-smi`로 드라이버와 NPU 인식 여부 확인
- [ ] `rebel-compiler`, `optimum-rbln`, `vllm-rbln`, `torch-rbln` 버전 매칭
- [ ] RBLN Portal 계정 또는 PyPI access 필요 여부 확인
- [ ] vLLM 버전과 `vllm-rbln` 버전 호환성 확인
- [ ] OpenAI-compatible server 테스트
- [ ] Kubernetes 환경에서는 device plugin / feature discovery / operator 확인

## 3. DEEPX

### 공식 사이트 및 제품

- [DEEPX Homepage](https://deepx.ai/)
- [DX-M1 Product Page](https://deepx.ai/products/dx-m1/)
- [DXNN SDK Product Page](https://deepx.ai/products/dxnn-sdk/)
- [DEEPX Developer Portal](https://developer.deepx.ai/)
- [DX Model Zoo](https://developer.deepx.ai/modelzoo/)

### GitHub

- [DEEPX-AI GitHub Organization](https://github.com/DEEPX-AI)
- [DEEPX-AI/dx-runtime](https://github.com/DEEPX-AI/dx-runtime)
- [DEEPX DX-M1 Raspberry Pi 5 community port](https://github.com/zlorenzini/pi-m1)

### 핵심 SDK / 런타임

- [DXNN SDK](https://deepx.ai/products/dxnn-sdk/)
- [DX-Runtime GitHub](https://github.com/DEEPX-AI/dx-runtime)
- [DX Model Zoo](https://developer.deepx.ai/modelzoo/)
- [Radxa DX-M1 SDK Docs](https://docs.radxa.com/en/aicore/dx-m1/dx-sdk/dx-model-zoo)
- [Sixfab DEEPX Model Zoo](https://docs.sixfab.com/docs/ai-model-deployment-sixfab-model-zoo)

### 모델 및 호환성

| Resource | Link | Notes |
|---|---|---|
| DX Model Zoo | [developer.deepx.ai/modelzoo](https://developer.deepx.ai/modelzoo/) | Precompiled/benchmark-oriented DX model resources |
| DX-Runtime | [dx-runtime](https://github.com/DEEPX-AI/dx-runtime) | Runtime, firmware, driver, DX-APP, DX-Stream |
| DX-Stream | [dx-runtime submodule](https://github.com/DEEPX-AI/dx-runtime) | GStreamer-based multimedia pipeline |
| Community Raspberry Pi 5 port | [zlorenzini/pi-m1](https://github.com/zlorenzini/pi-m1) | Community reproduction; verify before production use |

### 벤치마크 및 검증 자료

- [DX Model Zoo benchmark metadata](https://developer.deepx.ai/modelzoo/)
- [DX-M1 Product Page](https://deepx.ai/products/dx-m1/)
- [Sixfab Model Zoo](https://docs.sixfab.com/docs/ai-model-deployment-sixfab-model-zoo)

### 설치/운영 체크리스트

- [ ] DX-M1 M.2 / module / carrier board form factor 확인
- [ ] PCIe lane, host architecture, Ubuntu version 확인
- [ ] DX-Runtime, driver, firmware, DX-APP, DX-Stream 버전 확인
- [ ] ONNX -> DX-COM -> `.dxnn` 변환 경로 확인
- [ ] 모델 주의 `.dxnn` 파일과 런타임 버전 호환성 확인
- [ ] GStreamer pipeline에서 카메라/비디오 입력 지연 시간 측정
- [ ] LLM/decoder 모델 지원 여부는 최신 공식 문서 기준 재확인

## 4. Mobilint

### 공식 사이트 및 제품

- [Mobilint Homepage](https://www.mobilint.com/)
- [Mobilint SDK qb](https://www.mobilint.com/sdk-qb)
- [Mobilint SDK qb Documentation](https://docs.mobilint.com/v1.2/en/introduction.html)
- [Mobilint Getting Started](https://docs.mobilint.com/v1.0/en/getting_started.html)
- [Mobilint Discuss](https://discuss.mobilint.com/)

### SDK / 런타임 / 컴파일러

- [SDK qb Introduction](https://docs.mobilint.com/v1.2/en/introduction.html)
- [Compiler Installation](https://docs.mobilint.com/v1.1/en/installing_compiler.html)
- [Programming Guide](https://docs.mobilint.com/v0.28/en/programming_guide.html)
- [Checking Compatibility](https://docs.mobilint.com/v1.1/en/compatibility.html)
- [mobilint-qb-runtime PyPI](https://pypi.org/project/mobilint-qb-runtime/)
- [mblt-model-zoo PyPI](https://pypi.org/project/mblt-model-zoo/)

### 모델 및 호환성

- [Mobilint Model Zoo Docs](https://docs.mobilint.com/v0.28/en/model_zoo.html)
- [Mobilint Hugging Face Organization](https://huggingface.co/mobilint)
- [mblt-model-zoo PyPI](https://pypi.org/project/mblt-model-zoo/)
- [mobilint-qb-runtime PyPI](https://pypi.org/project/mobilint-qb-runtime/)

| Resource | Link | Notes |
|---|---|---|
| SDK qb Docs | [docs.mobilint.com](https://docs.mobilint.com/v1.2/en/introduction.html) | Driver, runtime, compiler overview |
| Model Zoo | [Mobilint Model Zoo](https://docs.mobilint.com/v0.28/en/model_zoo.html) | Vision, language, multimodal model catalog |
| Runtime PyPI | [mobilint-qb-runtime](https://pypi.org/project/mobilint-qb-runtime/) | Python runtime package |
| Model Zoo PyPI | [mblt-model-zoo](https://pypi.org/project/mblt-model-zoo/) | Pre-quantized model package |
| HF Models | [huggingface.co/mobilint](https://huggingface.co/mobilint) | Transformer model resources |

### 설치/운영 체크리스트

- [ ] ARIES / REGULUS / MLA100 / SoM별 설치 절차 확인
- [ ] Driver, Runtime, Firmware compatibility matrix 확인
- [ ] `.mxq` 파일의 format version과 runtime 호환성 확인
- [ ] `mobilint-qb-runtime` Python 버전 지원 범위 확인
- [ ] 직접 학습 모델은 ONNX/TensorFlow/PyTorch -> qb Compiler -> `.mxq` 변환 경로 검증
- [ ] Windows/Ubuntu 지원 여부와 배포 대상 OS 확인

## 5. HyperAccel

### 공식 사이트 및 문서

- [HyperAccel Homepage](https://hyperaccel.ai/)
- [HyperAccel Software](https://hyperaccel.ai/ha_product/software/)
- [HyperDex Documentation](https://docs.hyperaccel.ai/)
- [HyperDex Installation Guide](https://docs.hyperaccel.ai/1.5.2/install_hyperdex/)
- [HyperDex Toolchain](https://docs.hyperaccel.ai/1.5.3/hyperdex_toolchain/)
- [HyperDex Quick Start](https://docs.hyperaccel.ai/1.5.3/quick_start/)
- [HyperDex Hugging Face API](https://docs.hyperaccel.ai/1.5.2/huggingface_api/)

### 연구/벤치마크

- [LPU: A Latency-Optimized and Highly Scalable Processor for Large Language Model Inference - arXiv](https://arxiv.org/abs/2408.07326)
- [HyperAccel LPU Hot Chips Page](https://hyperaccel.ai/hyperaccel-latency-processing-unit-lputmaccelerating-hyperscale-models-for-generative-ai/)
- [HyperAccel Software Demos](https://hyperaccel.ai/ha_product/software/)

### 모델 및 호환성

| Resource | Link | Notes |
|---|---|---|
| HyperDex Toolchain | [docs.hyperaccel.ai](https://docs.hyperaccel.ai/1.5.3/hyperdex_toolchain/) | Compiler/runtime stack for LLM inference |
| Hugging Face API | [HyperDex HF API](https://docs.hyperaccel.ai/1.5.2/huggingface_api/) | Similar interface to Hugging Face Transformers |
| Quick Start | [Quick Start](https://docs.hyperaccel.ai/1.5.3/quick_start/) | First LLM inference guide |
| LPU Paper | [arXiv 2408.07326](https://arxiv.org/abs/2408.07326) | Architecture and performance claims should be read as paper benchmark context |

### 설치/운영 체크리스트

- [ ] LPU hardware / AMD Alveo FPGA card / XRT requirement 확인
- [ ] Ubuntu/RHEL/Rocky Linux 버전 확인
- [ ] HyperDex private PyPI credentials 필요 여부 확인
- [ ] PyTorch, CUDA, CPU-only wheel 조합 확인
- [ ] Hugging Face model compatibility and max sequence length 확인
- [ ] LPU-only vs LPU+GPU hybrid serving 구조 확인

## 6. SAPEON Legacy

SAPEON 관련 공개 SDK/개발자 문서는 제한적으로 확인됩니다. Rebellions와 SAPEON의 통합 이후 SDK와 제품 라인업이 RBLN 문서 체계로 흡수되는지 지속 추적이 필요합니다.

### 참고 링크

- [Reuters - Rebellions and Sapeon to merge](https://www.reuters.com/technology/artificial-intelligence/south-korean-ai-chip-developers-rebellions-sapeon-merge-2024-06-12/)
- [Reuters - Rebellions and Sapeon agree to merge](https://www.reuters.com/technology/artificial-intelligence/south-korean-ai-chip-makers-rebellions-sapeon-agree-merge-2024-08-18/)
- [Rebellions Developers](https://rebellions.ai/developers/)

### 확인 필요

- [ ] SAPEON X220/X330 대상 공개 SDK 존재 여부
- [ ] 기존 SAPEON 고객용 문서의 공개 전환 여부
- [ ] Rebellions 통합 이후 제품명/SDK명/지원 모델 변경 사항

## 주제별 큐레이션

## A. 설치와 드라이버 확인

| Vendor | Start Here | Health Check |
|---|---|---|
| FuriosaAI | [Driver, Firmware, and Runtime Installation](https://developer.furiosa.ai/docs/latest/en/software/installation.html) | SDK CLI / runtime tool 확인 필요 |
| Rebellions | [RBLN Installation Guide](https://docs.rbln.ai/latest/getting_started/installation_guide.html) | `rbln-smi` |
| DEEPX | [DX-Runtime](https://github.com/DEEPX-AI/dx-runtime) | driver/firmware/runtime install logs |
| Mobilint | [Getting Started](https://docs.mobilint.com/v1.0/en/getting_started.html) | device path, runtime import, sample inference |
| HyperAccel | [HyperDex Installation](https://docs.hyperaccel.ai/1.5.2/install_hyperdex/) | `xbutil examine`, package list |

## B. 모델 포맷과 변환 경로

| Vendor | Input Model | Compiler / Converter | Runtime Artifact |
|---|---|---|---|
| FuriosaAI | ONNX, TFLite, selected model zoo artifacts | Furiosa compiler / quantization tools | Furiosa executable/runtime artifact |
| Rebellions | PyTorch, TensorFlow, Hugging Face models | `rebel-compiler`, Optimum RBLN | RBLN compiled model |
| DEEPX | ONNX | DX-COM | `.dxnn` |
| Mobilint | PyTorch, TensorFlow, TFLite, ONNX, Keras | qb Compiler / qubee | `.mxq` |
| HyperAccel | Hugging Face Transformers models | HyperDex AutoCompiler | HyperDex-compatible model artifact |

## C. 프레임워크 지원

| Framework / Serving | FuriosaAI | Rebellions / RBLN | DEEPX | Mobilint | HyperAccel |
|---|---|---|---|---|---|
| PyTorch | SDK path 확인 | `torch-rbln`, compiler path | ONNX export path 중심 | Supported via SDK qb/compiler path | HyperDex transformers path |
| TensorFlow | SDK path 확인 | Supported by RBLN SDK | ONNX conversion path 중심 | Supported via SDK qb/compiler path | Not primary |
| ONNX | Strong | Supported path 확인 | Primary input path | Supported path | Not primary |
| Hugging Face Transformers | RNGD/vLLM-related materials 확인 | Optimum RBLN, vLLM RBLN | LLM support 확인 필요 | Hugging Face org/model zoo available | Primary-style API |
| vLLM | RNGD materials 확인 | `vllm-rbln` | 확인 필요 | 확인 필요 | vLLM-oriented support mentioned |
| Triton | 확인 필요 | Documented | 확인 필요 | 확인 필요 | 확인 필요 |
| GStreamer | 확인 필요 | 확인 필요 | DX-Stream | 확인 필요 | Not primary |
| Kubernetes | 확인 필요 | Operator, device plugin, feature discovery | 확인 필요 | 확인 필요 | 확인 필요 |

## D. 벤치마크 자료

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

## E. 설치 이슈 템플릿

새로운 이슈를 등록할 때 아래 형식을 권장합니다.

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

## F. 모델 호환성 등록 템플릿

````markdown
## Model Compatibility Report

| Field | Value |
|---|---|
| Vendor |  |
| Hardware |  |
| SDK version |  |
| Runtime version |  |
| Model name |  |
| Model source |  |
| Task |  |
| Input format | ONNX / PyTorch / TensorFlow / Hugging Face / TFLite |
| Compiled format | `.dxnn` / `.mxq` / RBLN artifact / Furiosa artifact / HyperDex artifact |
| Quantization | FP16 / FP8 / INT8 / INT4 / other |
| Batch size |  |
| Sequence length / image size |  |
| Status | Works / Partially works / Fails |
| Accuracy delta |  |
| Latency |  |
| Throughput |  |
| Power |  |
| Reproducibility | Verified / Needs independent reproduction |

## Notes

## Logs

## Links
````

## G. 벤치마크 등록 템플릿

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

## H. 기여 가이드 초안

### 링크 추가 기준

- 공식 문서, 공식 GitHub, 공식 모델 주를 우선합니다.
- 커뮤니티 자료는 `community-repro`로 분류하고 실행 환경과 재현 가능성을 함께 기록합니다.
- 성능 수치는 출처, SDK 버전, 모델, 정밀도, 배치, 입력 크기, 측정 도구가 없으면 벤치마크로 인정하지 않습니다.
- 사내/비공개 문서, NDA 자료, 라이선스 위반 가능 자료는 올리지 않습니다.
- 링크가 깨졌거나 버전이 오래된 경우 `status/needs-check` 라벨을 붙입니다.

### PR 체크리스트

- [ ] 공식 출처 또는 재현 가능한 커뮤니티 출처인가?
- [ ] Vendor, topic, status 라벨을 붙였는가?
- [ ] SDK/드라이버/런타임 버전을 명시했는가?
- [ ] 모델 라이선스를 확인했는가?
- [ ] 성능 수치에 측정 조건을 포함했는가?
- [ ] 동일 링크가 이미 등록되어 있지 않은가?

## 확인 필요 목록

아래 항목은 후속 리서치 또는 실제 장비 검증이 필요합니다.

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

## 참고: 개발자가 자주 겪는 문제

| Problem | Likely Cause | First Check |
|---|---|---|
| Device not detected | Driver/firmware mismatch, PCIe issue, permission issue | Vendor health-check command, `lspci`, `dmesg` |
| Compiler fails | Unsupported op, dynamic shape, opset mismatch | Supported ops list, static input shape |
| Model output is wrong | Pre/post-processing mismatch, quantization issue | Calibration dataset, normalization, layout NCHW/NHWC |
| Runtime segmentation fault | Version mismatch, invalid compiled artifact | Driver-runtime-compiler compatibility matrix |
| Poor performance | CPU fallback, wrong batch, unoptimized precision | Runtime logs, profiler, device utilization |
| vLLM server fails | Plugin/version mismatch | vLLM, PyTorch, plugin version matrix |
| Docker cannot see NPU | Device mount/cgroup/privilege issue | Container runtime, `/dev/*`, Kubernetes device plugin |

## License

Recommended license for this curation repository: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) for documentation and [MIT](https://opensource.org/license/mit/) for scripts.

## Disclaimer

이 저장소는 공개 문서와 커뮤니티 자료를 큐레이션하는 비공식 개발자 자료입니다. 각 회사의 SDK, 드라이버, 모델, 벤치마크, 라이선스 조건은 수시로 변경될 수 있으므로 실제 프로젝트 적용 전 공식 문서를 다시 확인해야 합니다.
