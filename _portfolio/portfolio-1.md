---
title: "SPEED-JOBS — AI 기반 채용 인텔리전스 대시보드"
excerpt: "경쟁사 채용 공고 데이터를 기반으로 채용 현황·트렌드 분석, 스킬 키워드, 공고 품질 평가까지 제공하는 AI 채용 인텔리전스 서비스<br/>Period: 2025.07 - 2025.12"
collection: portfolio
---

## 개요

대규모 채용 공고 데이터를 기반으로 경쟁사 채용 현황·트렌드 분석·스킬 키워드·공고 품질 평가까지 제공하는 AI 채용 인텔리전스 서비스입니다. 경험 중심의 채용 판단(AS-IS)을 AI로 설명 가능한 채용 전략(TO-BE)으로 바꾸는 것을 목표로 했습니다.

* **Period** : 2025.07 - 2025.12
* **Point** : 경험 중심의 채용 전략을 AI 기반 채용 의사결정으로 지원하는 서비스

## 주요 기능

1. **대시보드** — 경쟁사 채용 추이, AI 인사이트, 경쟁사 스킬 변화 비교, 그래프 모델 기반 유사 스킬 분석
2. **채용 운영** — 직군 비중 변화 분석, 직무 인재 수급 난이도 지수, 공고 품질 평가 및 AI 추천 수정 사항, 채용 일정 시뮬레이션
3. **CHATBOT** — RDB 통계, Vector DB 유사 공고 검색, 웹 검색을 결합한 채용 특화 챗봇

## 데이터 파이프라인

1. **크롤러 실행** — 경쟁사 사이트에서 공고 전문 수집, LLM Few-shot 프롬프트로 제목/회사/경력 등 핵심 정보를 JSON으로 추출
2. **스킬셋 추출** — LLM 기반 자동 스킬 매핑, 요구 스킬 딕셔너리 컨텍스트 주입으로 정확도 강화
3. **직무 매칭** — Personalized PageRank로 후보 1차 선별 → Jaccard 유사도 → Sentence-BERT 의미 유사도 → 최종 결합
4. 3일 간격 스케줄링으로 경쟁사 및 IT 기업 공고를 상시 수집

## 서비스 아키텍처

* **Frontend** : React, Next.js
* **Backend** : Spring(인증/권한/DB 조회), FastAPI(데이터 처리, Agent 관리, 크롤링)
* **AI/Agent** : 공고 품질 평가 Agent(가독성/구체성/매력도 세부 Agent + 품질 보고서 생성 Agent), AI 챗봇 Agent(DB 통계 / Vector 검색 / 웹 검색 Tool)
* **Model Layer** : PageRank, Jaccard Similarity, Node2Vector, Sentence-BERT
* **Data** : MySQL(RDB), Qdrant(Vector DB), Amazon S3(원본 이미지)
* **CI/CD** : GitHub → GitHub Actions → Docker → HARBOR → Kubernetes

## What I did

* **프론트엔드 개발** : React + TypeScript 기반 대시보드 전체 설계 및 구현, Recoil 기반 전역 상태 관리 및 API 연동 구조 설계, 직무 수급 난이도·트렌드 분석·직무 매칭 결과 UI 구현, Chart.js 기반 데이터 시각화 및 비동기 로딩 최적화
* **데이터·AI 설계** : 공고 품질 평가 기준 정의 및 LLM 기반 점수화 모델 설계, Jaccard + SBERT + PageRank 결합 Hybrid 직무 매칭 알고리즘 설계, LangGraph 기반 Multi-Agent 파이프라인 구조 설계
* **공고 수집·데이터 구조 설계** : 3일 주기 경쟁사 공고 자동 수집 및 JSON 구조화, jobs-skills N:M ERD 설계 및 복합 인덱스 전략 적용, Vector DB 분리 및 집계 테이블 기반 읽기 최적화 구조 설계

## Troubleshooting & Lesson Learned

* **비정형 채용 공고 데이터 구조화 문제** — 기업마다 공고 형식이 달라 정규식 기반 파싱이 불안정했음. LLM 기반 Few-shot 프롬프트 설계, JSON 구조 강제 출력, 후처리 Validation Layer를 추가해 해결. *LLM은 만능이 아니라 프롬프트 설계와 후처리 로직이 핵심이며, 비정형 데이터는 AI + Rule 기반 Hybrid 접근이 가장 안정적이다.*
* **직무 매칭 정확도 개선** — 초기 Jaccard Similarity만으로는 표현 차이로 인한 매칭 실패가 발생. Jaccard(정확 키워드) + SBERT(의미 유사도) + Personalized PageRank(스킬 네트워크 중요도)를 결합한 Hybrid 설계로 개선. *단일 알고리즘은 한계가 있으므로 정확성·의미성·구조성을 결합한 Hybrid 설계가 실제 서비스에서 효과적이다.*
* **직무 인재 수급 난이도 지표의 객관성 확보** — 단순 채용공고 수 기반 산정은 왜곡 가능성이 컸음. 전년 대비 채용공고 증가율(YoY)과 HHI(시장 집중도 지수)를 결합해 설명 가능한 난이도 지표를 설계. *복잡한 모델보다 신뢰 가능한 지표 설계가 더 중요하다.*
* **ERD 기반 구조의 확장성 문제** — jobs-skills-job_skills N:M 구조에서 공고 증가 시 중간 테이블이 기하급수적으로 증가해 Join 비용이 상승. 복합 인덱스 설계, 집계 전용 summary 테이블, 읽기 최적화 구조로 해결. *정규화는 중요하지만 실서비스에서는 읽기 최적화 설계가 필요하며 논리 모델과 물리 모델은 다를 수 있다.*
* **데이터 증가에 따른 시스템 확장 전략** — 데이터 누적 시 통계 쿼리 지연, 임베딩 검색 속도 저하, 운영 DB 부하가 증가. OLTP/OLAP 분리, 날짜 기반 파티셔닝, Vector DB 분리, Redis 캐싱, 배치 기반 집계 구조로 대응. *AI 서비스는 모델 성능보다 확장 가능한 아키텍처가 더 중요하다.*
