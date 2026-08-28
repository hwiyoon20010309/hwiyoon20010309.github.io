---
title: "CultureLens — 딥러닝 기반 생성형 AI의 문화적 인식 향상"
excerpt: "AI가 생성한 이미지-설명의 문화적 적절성을 정량 평가하고, Human-in-the-loop 학습을 통해 편향을 완화하는 예측 모델 설계"
collection: portfolio
---

## 개요

AI가 생성한 이미지-설명의 문화적 적절성을 정량 평가하고, Human-in-the-loop 학습을 통해 편향을 완화하는 예측 모델을 설계한 프로젝트입니다. CLIP 등 대규모 비전-언어 모델은 서구 중심 데이터로 학습되어 비서구권 문화(한복, 한옥 등) 요소를 "의상", "집"처럼 모호하게 일반화해 문화적 맥락과 정체성을 제대로 반영하지 못한다는 문제의식에서 출발했습니다.

## 문제 · 해결 · 성과

* **문제** : CLIP 등 대규모 비전-언어 모델은 서구 중심 데이터로 학습되어 비서구권 문화 요소를 모호하게 일반화하고, 이미지-설명의 문화적 적절성을 판단할 정량적 기준이 없어 주관적 판단에 의존해야 했습니다. 특정 문화 데이터로 학습한 모델은 다른 문화권에서 성능이 떨어졌고, 사람의 문화적 판단 피드백이 모델 개선에 반영되지 않는 구조였습니다.
* **해결** : React 기반 설문 플랫폼을 직접 구축해 이미지-설명 쌍의 문화적 적절성을 5점 척도로 평가하고 응답 데이터를 수집했습니다. CLIP 이미지-텍스트 임베딩과 회귀 모델을 결합한 HITL(Human-in-the-loop) Regression 모델을 설계하고, 한국 데이터 기반 모델을 한중일로 확장하는 Fine-tuning 및 통합 학습 구조를 적용했습니다.
* **성과** : HITL 회귀 모델 도입으로 예측 오차(MAE)가 Zero-shot 대비 **2.87 → 0.86 (약 70% 감소)**로 크게 개선됐습니다. 인간 피드백을 AI 모델에 직접 결합해 생성형 AI의 문화적 포용성(Cultural Inclusivity)을 높일 수 있음을 정량적으로 입증했고, 이 연구 결과를 논문으로 정리했습니다.

## AS-IS → TO-BE

* **문화적 맥락 반영 부족** → 5점 척도 기반 문화적 적절성 정량화 체계 도입
* **설명 적절성 정량 평가 불가** → CLIP + 회귀 모델 기반 적절성 예측 모델 구축
* **일반화 성능 불안정** (한국 → 중국/일본 성능 저하) → 한중일 확장 Fine-tuning 및 통합 학습 구조 설계
* **Human Feedback 미반영 구조** → Human-in-the-loop 학습 구조 적용 (Zero-shot 대비 성능 향상 검증: MAE, R², Pearson r)

## 주요 기능

1. **문화적 적절성 설문 플랫폼 구축** — 이미지-설명 쌍에 대한 문화적 적절성 평가 시스템, 사용자 응답 데이터 수집/저장, 관리자 승인 및 통계 대시보드
2. **문화별 데이터 기반 예측 모델 구축** — CLIP 이미지-텍스트 임베딩 추출, 회귀 모델 기반 적절성 점수 예측, 문화권별 모델 vs 통합 모델 비교
3. **Human-in-the-loop 학습 구조 설계** — 사람 평가 데이터 기반 Fine-tuning 실험, Zero-shot 모델과 성능 비교, MAE/R²/Pearson r 기반 정량 평가

## 서비스 아키텍처

![CultureLens 서비스 아키텍처](/images/portfolio/culturelens-architecture.png)

* **Frontend** : React
* **Backend** : Node.js + Express, MongoDB Atlas
* **AI Inference** : FastAPI + CLIP + Regression Model (Amazon EC2)
* **Storage** : Amazon S3, Cloudflare

## What I did

* **프론트엔드 개발** : React 기반 설문 플랫폼 전체 구조 설계, 설문 진행 상태 유지 로직 구현, 관리자 통계 대시보드 UI 구현
* **데이터 구조 설계** : 설문 응답 스키마 정의, 문화권별 데이터 구조 설계, 학습 데이터셋 변환 파이프라인 설계
* **모델 실험** : CLIP embedding 추출 및 데이터 전처리, 회귀 모델 학습 및 성능 비교, Zero-shot vs Fine-tuning 실험 분석 정리

## 논문

**From Zero-shot to Human-in-the-loop: Human Feedback Framework for Reducing Cultural Bias in CLIP-based Generative AI**

* **핵심 기여** : HITL 웹 설문 플랫폼(React + Express.js + MongoDB) 직접 구축, 인간 피드백 기반 선형 회귀(HITL Regression) 모델로 Zero-shot 스코어 보정
* **주요 성과** : HITL 회귀 모델 도입 결과 평균 절대 오차(MAE)가 CLIP Zero-shot의 2.87에서 0.86으로 약 **70% 감소**, 인간의 문화적 판단 피드백을 AI 모델에 결합해 생성형 AI의 문화적 포용성(Cultural Inclusivity) 제고 가능성 입증
* [논문 원본 보기](https://drive.google.com/file/d/1vi9dApaAEtt3F5BjGlTdg-1Ej1vfiJj8/view?usp=sharing)

## Troubleshooting & Lesson Learned

* **Zero-shot 일반화 한계** — 한국 데이터 기반 학습 모델이 중국·일본 데이터에서 성능이 저하됨. Fine-tuning과 다문화 통합 학습 모델 설계로 해결. *Zero-shot 모델은 문화적 맥락 일반화에 한계가 있으며, Human feedback 기반 학습이 편향 완화에 효과적임을 확인.*
* **문화적 적절성의 정량화 어려움** — 문화적 적절성은 주관적 개념이라 레이블링이 불안정했음. 5점 척도 기반 정량 점수화와 가중 평균 기반 단일 점수 생성으로 해결. *추상적 개념도 명확한 기준을 정의하면 정량 예측 문제로 변환할 수 있다.*
* **설문 데이터 신뢰성 확보 문제** — 응답 편차 및 이상치 존재. 응답 분포 분석, 이상치 제거 기준 설정, 문화권별 표본 균형 조정으로 해결. *AI 성능은 모델보다 데이터 품질에 더 크게 좌우된다.*
* **배열 인덱스 처리 오류** — 이전에 응답한 데이터가 새 응답으로 덮어쓰기되는 문제 발생. push 방식이 아닌 조건 기반 업데이트 로직으로 재설계. *데이터 저장 로직은 단순 CRUD가 아니라 기존 데이터 흐름을 이해한 설계가 필요하다.*
* **CORS & 쿠키 정책 이슈 해결** — 프론트엔드(Vercel)와 백엔드(EC2)가 서로 다른 도메인으로 분리되어 Cross-Origin 환경에서 세션 쿠키 인증 실패 발생. Express CORS에서 origin 명시 및 credentials: true 설정, 쿠키를 SameSite=None/Secure=true로 변경, fetch 요청에 credentials: "include" 추가, Nginx와 Express의 CORS 헤더 중복 문제를 Express 단일 관리로 정리해 해결.
