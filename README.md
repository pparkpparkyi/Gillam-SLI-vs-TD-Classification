# Gillam-SLI-vs-TD-Classification

# 🧠 Gillam SLI vs TD Classification

아동 자연 발화 데이터를 활용한 **특정 언어 장애(SLI)** 자동 분류 프로젝트

[![Test Accuracy](https://img.shields.io/badge/Test%20Accuracy-80.9%25-brightgreen)](https://github.com/) [![SLI Recall](https://img.shields.io/badge/SLI%20Recall-63.2%25-orange)](https://github.com/)

## 🎯 프로젝트 개요

**목표**: 5-11세 아동의 자연스러운 발화 데이터를 분석하여 SLI(특정 언어 장애)와 TD(정상 발달)를 자동 분류하는 머신러닝 모델 개발

**문제 해결**: 
- SLI 조기 발견을 위한 **1차 스크리닝 도구**
- 클래스 불균형(TD:SLI = 2.8:1) 해결
- **NumPy로 Logistic Regression 완전 구현**

### 최종 성능 (Test Set)
```
Accuracy: 80.9%
SLI Recall: 63.2% (19명 중 12명 정확 탐지)
TD Recall: 87.8% (49명 중 43명 정확 분류)
```

## 📊 데이터셋

**Gillam Database (CHILDES TalkBank)**

| Dataset | 총 샘플 | TD | SLI | 비율 |
|---------|---------|----|-----|------|
| Train | 540 | 398 | 142 | 26.3% |
| Dev | 68 | 50 | 18 | 26.5% |
| **Test** | **68** | **49** | **19** | **27.9%** |

- **형식**: CHAT 전사 파일 (.cha)
- **특징**: 아동 발화(CHI)만 추출
- **전처리**: Bag-of-Words (2000 어휘)

## 🛠️ 기술 스택

```
NumPy (모델 구현)
Pandas (데이터 처리)
Matplotlib/Seaborn (시각화)
Google Colab (실행 환경)
```

## 🚀 빠른 시작

### Google Colab (권장)

1. **Google Drive 마운트**
```python
from google.colab import drive
drive.mount('/content/drive')
```

2. **작업 디렉토리 이동**
```python
import os
os.chdir('/content/drive/MyDrive/DL_project2')
```

3. **메인 노트북 실행**
```bash
# DL_Project2-4.ipynb (최종 최적화 버전) 순서대로 실행
Runtime → Run all
```

**예상 소요시간**: 10-15분

### 로컬 환경

```bash
# 요구사항
Python 3.8+
pip install numpy pandas matplotlib seaborn

# 실행
python split_gillam.py  # 데이터 분할 (최초 1회)
jupyter notebook DL_Project2-4.ipynb
```

## 📈 주요 결과

### 최적 모델 (Version 3)
```
LR=0.1, λ=0.01, Balanced Weight, Threshold=0.5

Test Set 성능:
Accuracy: 80.9%
TD F1: 0.869, SLI F1: 0.649
SLI Recall: 63.2% ← 3배 개선 (21% → 63%)
```

### Test Confusion Matrix
```
              Predicted
           TD    SLI
Actual TD  43     6
       SLI   7    12
```

### 하이퍼파라미터 비교
| 버전 | LR | λ | Weight | Test Acc | SLI Recall |
|------|----|---|--------|----------|------------|
| Ver.1 | 0.01 | 0.1 | None | 77.9% | **21.1%** |
| **Ver.3** | **0.1** | **0.01** | **Balanced** | **80.9%** | **63.2%** |
| Ver.4 | 0.1 | 0.5 | Balanced | 75.0% | 47.4% |
| Ver.5 | 0.1 | 1.0 | Balanced | 79.4% | 57.1% |

## 📁 파일 구조

```
DL_project2/
├── DL_Project2-[1-5].ipynb      # 5가지 실험 버전
├── README.md                     # 이 파일
├── utils.py                      # CHAT 파싱
├── split_gillam.py              # 데이터 분할
├── gillam_[train/dev/test].csv  # 메타데이터
├── results_*.png                # 시각화 결과
└── Gillam/                      # 원본 CHAT 파일
    ├── SLI/
    └── TD/
```

## 💡 핵심 발견

### 1. **Balanced Class Weight**가 핵심
```
미적용: SLI Recall 21.1% (4/19명)
적용:   SLI Recall 63.2% (12/19명)
─────── 3배 개선 ───────
```

### 2. 최적 하이퍼파라미터
```
Learning Rate: 0.1 (빠른 수렴)
Lambda: 0.01 (성능 우선)
Class Weight: 'balanced' (필수!)
Threshold: 0.5 (기본값 유지)
```
## 🔮 향후 개선 방향

1. **데이터 증강** (목표: 5000+ 샘플)
2. **고급 특징** (TF-IDF, N-gram, MLU)
3. **딥러닝** (LSTM → 85%, BERT → 90% 예상)
4. **실시간 시스템** (음성→전사→예측 파이프라인)

## 📚 참고 문헌

- CHILDES TalkBank (MacWhinney, 2000)
- Bishop (2014): SLI 정의 및 임상 기준
- Leonard (2014): *Children with SLI*



**👨‍💻 작성자**: SEOJIN PARK
**📅 최종 업데이트**: 2025.12.12  


***
