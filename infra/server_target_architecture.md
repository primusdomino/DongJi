
# 📌 SERVER TARGET ARCHITECTURE (Goal)
version 1.0.

⚠️ 이 문서는 목표 구조입니다.
현재 구조(server_current_state.md)를 기반으로 점진적으로 이행합니다.
---
## 1. 목표 구조
👉 단일 서버 내 통합 운영 구조
### 핵심 방향
- nginx 단일화
- Docker 기반 통합
- 서비스 분리 유지 (MSA)
---
## 2. 최종 아키텍처

[ Internet ]
↓
NGINX (Reverse Proxy)
↓

|   TOD Backend (Docker)       |
|   DongJi (Docker)            |
|   n8n (Docker)               |

   ↓

DB (Postgres / MySQL)

---
## 3. nginx 전략
### 현재
- docker nginx (80)
- host nginx (미사용)
### 목표
👉 docker nginx 단일화
- 모든 서비스 ingress 통합
- 도메인 기반 라우팅
예:

dongji.ai → landing
api.dongji.ai → TOD backend
admin.dongji.ai → admin
n8n.dongji.ai → n8n

---
## 4. TOD Backend 구조 (목표)
### 현재
- host 실행 (nohup)
### 목표
- Docker 컨테이너화

tod-shop
tod-user
tod-payment
tod-login
tod-media
…

---
## 5. Front 구조
### 현재
- static 파일 (/home/WEB)
### 목표
- nginx container 내부 또는 volume mount

/var/www/tod
/var/www/todshop

---
## 6. 배포 전략
### 현재
- 수동 실행 (start_stable.sh)
### 목표
- docker-compose 기반

docker-compose up -d

---
## 7. 네트워크 구조
- 내부 통신: docker network
- 외부 노출: nginx only
---
## 8. 포트 전략
### 현재
- 여러 포트 직접 노출
### 목표
👉 외부 노출 포트 최소화
| 포트 | 용도 |
|------|------|
| 80 / 443 | nginx only |
---
## 9. 운영 안정성 목표
- 서비스 무중단 배포
- 로그 중앙화
- health check 구성
- 장애 시 롤백 가능
---
## 10. 단계별 이행 계획
### Phase 1 (현재 진행)
- 파일 이관
- backend 기동
### Phase 2
- nginx 테스트 구성 (8088)
- 서비스 연결 확인
### Phase 3
- dockerization
- compose 구성
### Phase 4
- nginx 통합
- 도메인 연결
---
## 11. 추가 필요 정보 (OCI)
향후 최적화를 위해 필요
- Public IP / Private IP
- VCN / Subnet 구조
- Security List / NSG
- Block Volume 구성
- Load Balancer 사용 여부
- DNS 관리 위치 (Cloudflare 여부)
---
## 12. 최종 목표
👉 “단일 nginx + docker 기반 MSA 운영”
- 운영 단순화
- 확장성 확보
- 장애 대응 용이
---
## 13. 운영 원칙
- 기존 서비스 영향 최소화
- 단계적 전환
- 테스트 후 적용

⸻
