# 프로젝트명

📢 2025년 2학기 [AIKU](https://github.com/AIKU-Official) 활동으로 진행한 프로젝트입니다

🎉 2025년 2학기 AIKU - 열심히상 수상!

## 소개

영화, 드라마, 뮤직비디오 제작을 위한 AI 기반 스토리보드 스케치 자동 생성 시스템

Scene 정보(장면 설명, 대사)와 Shot 정보(Close-up shot, Medium shot, Full shot)를 입력받아 깨끗한 스케치 형태의 스토리보드 이미지를 자동으로 생성하는 파이프라인을 구축하였습니다. 

## 방법론
**[모델링 전략] Textual Embedding 기반의 정교한 샷(Shot) 제어**

- **Base Model & Fine-tuning Strategy**
    - **Backbone:** Stable Diffusion v1.5
    - **Optimization:** LoRA (Low-Rank Adaptation)를 적용하여 적은 연산량으로 목표 스토리보드 작화 스타일을 효율적으로 학습.

**Model Architecture**

<img width="1280" height="720" alt="pipeline" src="https://github.com/user-attachments/assets/54334050-e7e1-4f64-8c91-e3844c6a9b2e" />


- **핵심 방법론: Textual Embedding**

특히 본 프로젝트에서는 원하는 구도를 정확하게 생성해내기 위해 **Textual Embedding** 기법을 중점적으로 도입했습니다. 이 기법은 기존 DreamBooth 연구 등에서 제안된 '희귀 토큰(Rare Token)을 활용한 주체(Subject) 학습' 방식을 응용한 것입니다.

일반적인 텍스트 프롬프트만으로는 '클로즈업', '풀샷' 등의 카메라 워킹을 일관성 있게 제어하기 어렵습니다. 이를 해결하기 위해 우리는 **CLIP Text Encoder의 임베딩 레이어**에 샷(Shot) 정보를 담은 새로운 토큰을 추가하여 학습시켰습니다.

- **Custom Tokens:**
    - `<cu_trg>`: 얼굴 표정과 감정을 강조하는 **Close Up** 정보 학습
    - `<ms_trg>`: 인물의 동작과 상반신을 표현하는 **Medium Shot** 정보 학습
    - `<fs_trg>`: 인물의 전신과 공간감을 나타내는 **Full Shot** 정보 학습

이를 통해 모델은 사용자가 입력한 토큰에 맞춰 화풍(Style)은 유지하되, 스토리보드 연출에 필수적인 **구도(Composition) 정보**를 명확하게 분리하여 생성할 수 있게 되었습니다.

> ReferenceRuiz, N., et al. "DreamBooth: Fine Tuning Text-to-Image Diffusion Models for Subject-Driven Generation." CVPR 2023.
>
## 환경 설정

(Requirements, Anaconda, Docker 등 프로젝트를 사용하는데에 필요한 요구 사항을 나열해주세요)

## 사용 방법

(프로젝트 실행 방법 (명령어 등)을 적어주세요.)

## 예시 결과
Input text = " Eye level, female, youth, happy, slim body, white shirt, black pants, no background, day time "
<img width="1769" height="593" alt="image" src="https://github.com/user-attachments/assets/29988724-fc99-440b-b878-6677a67d3144" />

동일 Prompt에 대해 Shot 별로 Trigger Word를 설정하여 Inference한 결과물입니다.
Text를 잘 반영한 Consistent한 그림체로, Shot 별 차이가 확연히 드러나는 것을 확인할 수 있습니다. 

## 팀원

- [신명경] : Lead, Model Architecture, Data Augmentation
- [김태관] : Experiment, Pipeline Construction, Data Clustering
- [정성윤] : Image Preprocessing
- [박서연] : Text Data Preprocessing
- [장서현] : Data Preprocessing, Evaluation Metrics

