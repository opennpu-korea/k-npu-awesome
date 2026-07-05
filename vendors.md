# Vendor Resources

국내 NPU, LPU, AI SoC 제조사별 개발자 문서, SDK, GitHub, 모델 주, 런타임, 컴파일러, 설치 체크리스트를 정리합니다.

## FuriosaAI

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
| Furiosa Models | [furiosa-models](https://github.com/furiosa-ai/furiosa-models) | Public pre-trained and pre-quantized models |
| Warboy Vision Models | [warboy-vision-models](https://github.com/furiosa-ai/warboy-vision-models) | Object detection, pose estimation, instance segmentation |
| YOLOv5s example | [yolov5s](https://github.com/furiosa-ai/yolov5s) | YOLOv5s compile/eval example |

### 체크리스트

- [ ] SDK 버전과 대상 하드웨어가 일치하는지 확인
- [ ] Kernel driver, firmware, runtime 설치 경로 확인
- [ ] `furiosa` CLI 또는 런타임 헬스체크 명령 확인
- [ ] ONNX/TFLite 입력 모델의 opset과 지원 연산 확인
- [ ] 양자화 후 정확도 저하 여부 측정
- [ ] Docker/컨테이너 환경에서 디바이스 패스스루 확인

## Rebellions / RBLN

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

- [vLLM RBLN](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html)
- [NVIDIA Triton Inference Server Support](https://docs.rbln.ai/latest/software/model_serving/triton_support/)
- [TorchServe Support](https://docs.rbln.ai/latest/software/model_serving/torchserve_support/)
- [Ray Serve Support](https://docs.rbln.ai/latest/software/model_serving/ray_serve_support/)
- [RBLN Kubernetes NPU Feature Discovery](https://docs.rbln.ai/latest/software/system_management/kubernetes/npu_feature_discovery.html)

### 모델 및 호환성

| Resource | Link | Notes |
|---|---|---|
| Supported Models | [RBLN SDK User Guide](https://docs.rbln.ai/latest/index.html) | Optimum, PyTorch, TensorFlow model support entry point |
| Optimum RBLN | [optimum-rbln](https://github.com/RBLN-SW/optimum-rbln) | Hugging Face Transformers/Diffusers integration |
| vLLM RBLN | [vLLM RBLN docs](https://docs.rbln.ai/v0.9.4/software/model_serving/vllm_support/vllm-rbln.html) | LLM serving plugin |
| PyTorch RBLN | [torch-rbln docs](https://docs.rbln.ai/v0.10.0/software/rbln_pytorch/overview.html) | PyTorch extension, beta status should be checked |

### 체크리스트

- [ ] `rbln-smi`로 드라이버와 NPU 인식 여부 확인
- [ ] `rebel-compiler`, `optimum-rbln`, `vllm-rbln`, `torch-rbln` 버전 매칭
- [ ] RBLN Portal 계정 또는 PyPI access 필요 여부 확인
- [ ] vLLM 버전과 `vllm-rbln` 버전 호환성 확인
- [ ] OpenAI-compatible server 테스트
- [ ] Kubernetes 환경에서는 device plugin, feature discovery, operator 확인

## DEEPX

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
| DX Model Zoo | [developer.deepx.ai/modelzoo](https://developer.deepx.ai/modelzoo/) | Precompiled/benchmark-oriented model resources |
| DX-Runtime | [dx-runtime](https://github.com/DEEPX-AI/dx-runtime) | Runtime, firmware, driver, DX-APP, DX-Stream |
| DX-Stream | [dx-runtime submodule](https://github.com/DEEPX-AI/dx-runtime) | GStreamer-based multimedia pipeline |
| Community Raspberry Pi 5 port | [zlorenzini/pi-m1](https://github.com/zlorenzini/pi-m1) | Community reproduction; verify before production use |

### 체크리스트

- [ ] DX-M1 M.2 / module / carrier board form factor 확인
- [ ] PCIe lane, host architecture, Ubuntu version 확인
- [ ] DX-Runtime, driver, firmware, DX-APP, DX-Stream 버전 확인
- [ ] ONNX -> DX-COM -> `.dxnn` 변환 경로 확인
- [ ] 모델 주의 `.dxnn` 파일과 런타임 버전 호환성 확인
- [ ] GStreamer pipeline에서 카메라/비디오 입력 지연 시간 측정
- [ ] LLM/decoder 모델 지원 여부는 최신 공식 문서 기준 재확인

## Mobilint

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

| Resource | Link | Notes |
|---|---|---|
| SDK qb Docs | [docs.mobilint.com](https://docs.mobilint.com/v1.2/en/introduction.html) | Driver, runtime, compiler overview |
| Model Zoo | [Mobilint Model Zoo](https://docs.mobilint.com/v0.28/en/model_zoo.html) | Vision, language, multimodal model catalog |
| Runtime PyPI | [mobilint-qb-runtime](https://pypi.org/project/mobilint-qb-runtime/) | Python runtime package |
| Model Zoo PyPI | [mblt-model-zoo](https://pypi.org/project/mblt-model-zoo/) | Pre-quantized model package |
| HF Models | [huggingface.co/mobilint](https://huggingface.co/mobilint) | Transformer model resources |

### 체크리스트

- [ ] ARIES / REGULUS / MLA100 / SoM별 설치 절차 확인
- [ ] Driver, Runtime, Firmware compatibility matrix 확인
- [ ] `.mxq` 파일의 format version과 runtime 호환성 확인
- [ ] `mobilint-qb-runtime` Python 버전 지원 범위 확인
- [ ] 직접 학습 모델은 ONNX/TensorFlow/PyTorch -> qb Compiler -> `.mxq` 변환 경로 검증
- [ ] Windows/Ubuntu 지원 여부와 배포 대상 OS 확인

## HyperAccel

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

### 체크리스트

- [ ] LPU hardware / AMD Alveo FPGA card / XRT requirement 확인
- [ ] Ubuntu/RHEL/Rocky Linux 버전 확인
- [ ] HyperDex private PyPI credentials 필요 여부 확인
- [ ] PyTorch, CUDA, CPU-only wheel 조합 확인
- [ ] Hugging Face model compatibility and max sequence length 확인
- [ ] LPU-only vs LPU+GPU hybrid serving 구조 확인

## SAPEON Legacy

SAPEON 관련 공개 SDK/개발자 문서는 제한적으로 확인됩니다. Rebellions와 SAPEON의 통합 이후 SDK와 제품 라인업이 RBLN 문서 체계로 흡수되는지 지속 추적이 필요합니다.

### 참고 링크

- [Reuters - Rebellions and Sapeon to merge](https://www.reuters.com/technology/artificial-intelligence/south-korean-ai-chip-developers-rebellions-sapeon-merge-2024-06-12/)
- [Reuters - Rebellions and Sapeon agree to merge](https://www.reuters.com/technology/artificial-intelligence/south-korean-ai-chip-makers-rebellions-sapeon-agree-merge-2024-08-18/)
- [Rebellions Developers](https://rebellions.ai/developers/)

### 확인 필요

- [ ] SAPEON X220/X330 대상 공개 SDK 존재 여부
- [ ] 기존 SAPEON 고객용 문서의 공개 전환 여부
- [ ] Rebellions 통합 이후 제품명/SDK명/지원 모델 변경 사항
