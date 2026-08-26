---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* 2025 — SKALA | SK AI Leader Academy

Certification
======
* 2024.12 — SQL 개발자 (SQLD)
* 2025.06 — 데이터 분석 준전문가 (ADsP)

Awards
======
* 2024.07 — OO 대학교 해커톤 우수상

Projects
======
* **SPEED-JOBS — AI 기반 채용 인텔리전스 대시보드** (2025.07 - 2025.12)
  * 경쟁사 채용 공고 데이터를 기반으로 채용 현황·트렌드 분석, 스킬 키워드, 공고 품질 평가까지 제공하는 AI 채용 인텔리전스 서비스
  * React + TypeScript 기반 대시보드 전체 설계 및 구현, Recoil 기반 전역 상태 관리
  * LLM 기반 Few-shot 프롬프트로 비정형 채용 공고 데이터 구조화, Jaccard + SBERT + Personalized PageRank 결합 Hybrid 직무 매칭 알고리즘 설계
  * LangGraph 기반 Multi-Agent 파이프라인으로 공고 품질(가독성/구체성/매력도) 평가

* **CultureLens — 딥러닝 기반 생성형 AI의 문화적 인식 향상**
  * AI가 생성한 이미지-설명의 문화적 적절성을 정량 평가하고, Human-in-the-loop 학습을 통해 편향을 완화하는 예측 모델 설계
  * React 기반 설문 플랫폼 전체 구조 설계, CLIP 이미지-텍스트 임베딩 추출 및 회귀 모델 학습
  * Human Feedback 기반 회귀 모델 도입으로 Zero-shot 대비 예측 오차(MAE) 70% 감소 (2.87 → 0.86)

* **TeachING — 흩어진 정보를 연결해 나만의 지식으로 만드는 AI 학습 서비스**
  * 수집한 자료를 분석해 하나뿐인 맞춤형 학습 로드맵을 설계하는 서비스
  * Qdrant 벡터DB 연동 RAG 챗봇 파이프라인 설계/구현, 검색 정확도 개선(top-k 튜닝, Multiquery, citation 표기)
  * URL/Notion 등 원문 수집 → AI 자료 분석(요약, 시맨틱 태그 생성) 파이프라인 공동 개발

Skills
======
* **Frontend** : React, TypeScript, Recoil, Chart.js, Next.js
* **Backend** : Spring, FastAPI, Node.js/Express
* **Data & AI** : LLM 프롬프트 엔지니어링, LangGraph Multi-Agent, CLIP, Sentence-BERT, PageRank/Jaccard 기반 유사도 매칭, 회귀 모델
* **Infra & DB** : MySQL, MongoDB, Qdrant, AWS (EC2/S3), Docker, Kubernetes, GitHub Actions, Nginx

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>

Teaching
======
  <ul>{% for post in site.teaching reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
