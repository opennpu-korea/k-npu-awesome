# Awesome Korean NPU Developer Resources

FuriosaAI, Rebellions/RBLN, DEEPX, Mobilint, HyperAccel 등 국내 NPU, LPU, AI SoC 기반 개발을 위한 문서, SDK, 모델 호환성, 설치 이슈, 추론 예제, 벤치마크 자료를 모으는 큐레이션 저장소입니다.

> Status: draft  
> Last updated: 2026-07-06  
> Scope: Korean AI accelerator / NPU / LPU / Edge AI SoC developer resources  
> Audience: open-source developers, AI inference engineers, edge AI builders, robotics/vision developers, MLOps engineers

## 저장소 목적

국내 AI 반도체 생태계는 제조사별 SDK, 모델 포맷, 컴파일러, 런타임, 지원 모델, 배포 방식이 서로 다릅니다. 이 저장소는 개발자가 다음 질문에 빠르게 답할 수 있도록 구성합니다.

- 어떤 제조사의 어떤 칩이 LLM, Vision, Multimodal, Edge AI, Serving에 적합한가?
- SDK, 드라이버, 런타임, 컴파일러 설치는 어디서 시작하는가?
- ONNX, PyTorch, TensorFlow, Hugging Face 모델을 어떤 포맷으로 변환해야 하는가?
- vLLM, Triton, TorchServe, Kubernetes, GStreamer와 어느 정도 연결되는가?
- 설치 오류, 모델 변환 실패, CPU fallback, 성능 저하 문제는 어떻게 기록하고 재현하는가?
- 벤치마크 자료는 공식 자료, 논문, 커뮤니티 재현 사례 중 어디에 속하는가?

## 문서 구성

| File | Description |
|---|---|
| [vendors.md](./vendors.md) | FuriosaAI, Rebellions/RBLN, DEEPX, Mobilint, HyperAccel, SAPEON legacy 등 제조사별 문서·SDK·모델·체크리스트 |
| [applications.md](./applications.md) | 설치, 모델 변환, LLM Serving, Vision, Multimodal, Edge, Kubernetes, 벤치마크, 트러블슈팅 등 응용 분야별 정리 |

## 빠른 비교

| Vendor | Main Hardware / Product | Main Workload | SDK / Runtime | Model Format | Public Docs | Access Notes |
|---|---|---|---|---|---|---|
| FuriosaAI | Warboy, RNGD | Vision, LLM, multimodal inference | Furiosa SDK, runtime, compiler | ONNX, TFLite, SDK artifact | Yes | 일부 driver/firmware는 evaluation program 필요 |
| Rebellions/RBLN | ATOM, REBEL family | LLM, vision, diffusion, serving | RBLN SDK, rebel-compiler, optimum-rbln, vllm-rbln, torch-rbln | `.rbln` artifact | Yes | compiler/portal access 필요 가능 |
| DEEPX | DX-M1, DX-M1 M.2, DX-M1 SoC family | Edge vision, industrial AI, multimedia pipeline | DXNN SDK, DX-AS, DX-COM, DX-RT, DX-Stream | `.dxnn` | Yes | 공개 자료는 vision/edge 중심 |
| Mobilint | ARIES MLA100, REGULUS SoC/SoM | Edge AI, vision, language, multimodal | SDK qb, qb Runtime, qb Compiler | `.mxq` | Yes | compiler/download center access 필요 가능 |
| HyperAccel | LPU, HyperDex | LLM inference | HyperDex Toolchain, HyperDex transformers | HyperDex artifact | Yes | private PyPI/licensing credentials 필요 가능 |
| SAPEON legacy | X220, X330 | Datacenter inference | 확인 필요 | 확인 필요 | Limited | Rebellions 통합 이후 상태 추적 필요 |

## 추천 탐색 순서

1. 처음 시작하는 개발자: [vendors.md](./vendors.md)에서 제조사별 공식 문서와 SDK 진입점을 확인합니다.
2. 특정 기능을 구현하려는 개발자: [applications.md](./applications.md)에서 LLM Serving, Vision, Edge Deployment, Model Conversion 섹션을 확인합니다.
3. 설치 오류를 겪는 개발자: [applications.md](./applications.md)의 Troubleshooting 섹션 템플릿으로 환경과 로그를 정리합니다.
4. 성능 비교가 필요한 개발자: [applications.md](./applications.md)의 Benchmark 섹션 기준에 맞춰 측정 조건을 기록합니다.

## 링크 추가 기준

- 공식 문서, 공식 GitHub, 공식 모델 주를 우선합니다.
- 커뮤니티 자료는 재현 환경과 한계를 함께 기록합니다.
- 성능 수치는 SDK 버전, 드라이버 버전, 모델명, 정밀도, 입력 크기, 배치 크기, 측정 도구가 없으면 벤치마크로 인정하지 않습니다.
- NDA 자료, 비공개 문서, 라이선스 위반 가능 자료는 올리지 않습니다.

## Issue/PR 라벨 제안

| Label | Meaning |
|---|---|
| `vendor/furiosaai` | FuriosaAI 관련 문서, SDK, 모델, 이슈 |
| `vendor/rbln` | Rebellions/RBLN 관련 항목 |
| `vendor/deepx` | DEEPX 관련 항목 |
| `vendor/mobilint` | Mobilint 관련 항목 |
| `vendor/hyperaccel` | HyperAccel 관련 항목 |
| `topic/install` | 드라이버, 런타임, SDK 설치 |
| `topic/model-zoo` | 모델 주, 지원 모델, 사전 컴파일 모델 |
| `topic/compiler` | 모델 변환, 컴파일러, 양자화 |
| `topic/runtime` | Python/C++ 런타임, inference API |
| `topic/serving` | vLLM, Triton, TorchServe, Ray Serve, API server |
| `topic/kubernetes` | Kubernetes, device plugin, operator, feature discovery |
| `topic/benchmark` | 성능 측정, MLPerf, 논문, 재현 벤치마크 |
| `topic/troubleshooting` | 설치 실패, 드라이버 인식, segmentation fault, 버전 충돌 |
| `status/verified` | 실제 실행 검증 완료 |
| `status/needs-check` | 최신성 또는 실행 검증 필요 |

## License

Recommended license: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) for documentation and [MIT](https://opensource.org/license/mit/) for scripts.

## Disclaimer

이 저장소는 공개 문서와 커뮤니티 자료를 큐레이션하는 비공식 개발자 자료입니다. 각 회사의 SDK, 드라이버, 모델, 벤치마크, 라이선스 조건은 변경될 수 있으므로 실제 프로젝트 적용 전 공식 문서를 다시 확인해야 합니다.
