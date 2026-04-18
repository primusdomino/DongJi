
# 📌 SERVER TRANSITION STRATEGY (핵심 전략 문서)
version 1.0.

⚠️ 본 문서는 단순 이관이 아닌
“TOD → 신규 AI 기반 시스템”으로의 점진적 전환 전략입니다.
---
## 1. 현재 시스템 (Legacy)
### TOD 시스템
- Backend: Java (Spring Boot)
- DB: MySQL
- 구조: MSA (다수 jar 서비스)
- 특징:
  - 안정성 확보된 기존 서비스
  - 빠른 변경 어려움
  - 구조 복잡
---
## 2. 신규 시스템 (Next)
### DongJi / Ranking System
- Language: Python
- DB: PostgreSQL
- 구조:
  - AI 기반 서비스
  - 데이터 중심 설계
  - API 중심 확장 구조
---
## 3. 핵심 전략
👉 **완전 교체가 아니라 "공존 + 점진적 전환"**

[기존 TOD] —–> 유지
\→ [신규 Python 시스템] (확장)

---
## 4. 시스템 역할 분리
### 4.1 TOD (기존 역할 유지)
- 회원/인증
- 결제
- 매장관리
- 기존 API
👉 변경 최소화
---
### 4.2 신규 시스템 (추가 역할)
- 랭킹 엔진
- 리뷰 분석
- AI 추천
- 데이터 집계
👉 TOD 위에 올라가는 구조
---
## 5. 데이터 전략
### 현재
- MySQL (TOD)
### 추가
- PostgreSQL (AI 시스템)
---
### 구조

MySQL (운영 데이터)
↓
Python ETL / API
↓
PostgreSQL (분석/랭킹)

---
## 6. 연결 방식
### 방식 1 (추천)
👉 API 기반 연결

TOD → Python API 호출

예:
- /ranking/top10
- /store/score
- /recommend
---
### 방식 2 (보조)
👉 DB Sync (Batch)

MySQL → PostgreSQL

- n8n / batch 활용 가능
---
## 7. 서비스 구조
### 현재

Java (TOD)
MySQL

---
### 목표 (중간 단계)

Java (TOD) ─────┐
├── API Gateway (nginx)
Python (AI) ────┘

DB:

* MySQL (운영)
* PostgreSQL (분석)

---
## 8. nginx 역할 (중요)
👉 단순 reverse proxy가 아니라
### “라우팅 허브”
예:

/api/* → Java
/ai/* → Python
/n8n → n8n

---
## 9. 단계별 전략
### Phase 1 (현재)
- TOD 이관 완료
- 기존 기능 정상화
---
### Phase 2
- Python 서버 구축
- PostgreSQL 구축
- Ranking API 개발
---
### Phase 3
- TOD에서 Ranking API 호출
- UI 일부 연결
---
### Phase 4
- 기능 점진 이전
- 일부 Java 기능 제거
---
### Phase 5 (최종)
- Python 중심 구조 전환
---
## 10. 기술 스택 분리 전략
| 영역 | 기술 |
|------|------|
| Core 서비스 | Java |
| AI / 분석 | Python |
| 운영 DB | MySQL |
| 분석 DB | PostgreSQL |
---
## 11. 리스크 관리
- 기존 서비스 영향 금지
- DB 직접 변경 금지
- API 기반 연결 유지
---
## 12. 핵심 원칙
### 절대 금지
- TOD 구조 직접 변경
- MySQL 구조 변경
---
### 권장
- 신규 기능은 Python에서만 개발
- TOD는 호출만
---
## 13. 최종 방향
👉 “Java는 점점 얇아지고  
👉 Python이 중심이 되는 구조”
---
## 14. 한 줄 전략
👉 “Replace가 아니라 Expand 후 Replace”
---
## 15. 운영 철학
- 안정성 > 속도
- 분리 > 통합
- 점진적 전환

⸻
