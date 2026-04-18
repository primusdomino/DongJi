
# 📌 SERVER CURRENT STATE (Baseline)
version 1.0.

⚠️ 이 문서는 현재 서버의 실제 상태 기준 문서입니다.
모든 작업은 이 구조를 유지하면서 진행합니다.
---
## 1. 서버 정보
- OS: Canonical Ubuntu 22.04 / 2025.10.31-0
- Instance: VM.Standard.A1.Flex
- CPU: 4 OCPU
- Memory: 24 GB
- Network: 4 Gbps
---
## 2. 운영 구조 개요
현재 서버는 **Docker + Native(Java) 혼합 구조**입니다.
- Docker: DongJi, n8n, DB
- Host: TOD (Spring Boot)
---
## 3. Docker 서비스
```bash
docker ps

서비스	포트
dongji-nginx	80
n8n	5678
postgres	5432

⸻

4. 포트 사용 현황

ss -tulnp

사용 중 포트

포트	서비스
80	docker nginx
5678	n8n
5432	postgres
3306	mysql
22	ssh

⸻

5. TOD Backend 구조

경로

/home/WAS/apps

서비스 목록

* tod_login (8112)
* tod_media (8085 추정)
* tod_money (8111)
* tod_payment (8086)
* tod_shop (8081)
* tod_user (8082)
* tod_user_advert (8182)
* tod_shop_advert (8183)
* tod_franchise (18118)
* tod_batch (internal)

⸻

실행 방식

nohup java -jar -Dserver.port=XXXX app.jar --spring.profiles.active=prod &

⸻

6. TOD Front 구조

경로

/home/WEB

주요 경로

경로	설명
/home/WEB/tod/m1/dist	사용자 프론트
/home/WEB/todshop/m1/dist	쇼핑 프론트
/home/WEB/public	공용
/home/WEB/term	약관
/home/WEB/tod_content	리소스
/home/WEB/todnotice	공지

⸻

7. nginx 구조

Docker nginx (운영 중)

* 포트: 80
* root: /usr/share/nginx/html
* 현재: dongji.ai 커밍순 페이지

Host nginx

* 경로: /etc/nginx
* 상태: TOD 설정 미적용

⸻

8. 현재 상태 요약

항목	상태
Backend 파일	완료
Front 파일	완료
포트 충돌	없음
nginx (TOD)	미구성
Java 런타임	확인 필요

## Java Runtime

- Java 11: installed

- Java 17: installed

- Architecture: ARM64 (OCI A1)

⸻

9. 리스크

* media 포트 불명확
* nginx 이중 구조 (docker vs host)
* Java 11 / 17 혼용

⸻

10. 운영 원칙

* 기존 docker 서비스 영향 금지
* 포트 충돌 금지
* 테스트 후 운영 전환

⸻

11. 업데이트 규칙

* 구조 변경 시 반드시 본 문서 수정
* nginx 변경 시 기록
* 포트 변경 시 기록

