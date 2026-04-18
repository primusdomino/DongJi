# SERVER CURRENT STATE

## 1. Server Info

- OS: Canonical Ubuntu 22.04

- Image Build: 2025.10.31-0

- Instance Type: VM.Standard.A1.Flex

- CPU: 4 OCPU

- Memory: 24 GB

- Network: 4 Gbps

- Architecture: ARM64

- Public IP: 168.107.46.230

## 2. DNS / Domain

- Primary domain: dongji.ai

- DNS management: Cloudflare

- Current direction:

  - dongji.ai -> landing page

  - user.dongji.ai -> TOD user web

  - shop.dongji.ai -> TOD shop web

## 3. Runtime

- Java 11: installed

- Java 17: installed

- Legacy startup scripts:

  - updated from amd64 paths to arm64 paths

## 4. Existing Containers / Services

### Docker

- dongji-nginx

- n8n

- postgres

### Host-based TOD services

- tod_login: running (8112)

- tod_user: running (8082)

- tod_shop: running (8081)

- tod_money: running (8111)

- tod_payment: running (8086)

- tod_media: running (8085)

- tod_user_advert: running (8182)

- tod_shop_advert: running (8183)

- tod_franchise: running (18118)

- tod_batch: running

## 5. Web Verification

- TOD user web frontend: browser access verified

- TOD shop web frontend: browser access verified

- Interpretation:

  - legacy TOD was app-oriented in operation

  - browser/web access is technically possible

  - migration can proceed toward web + app accessible structure

## 6. Frontend Paths

- Landing source path: /home/ubuntu/dongji

- Landing backup path: /home/ubuntu/dongji_landing_bak

- TOD user web dist: /home/WEB/tod/m1/dist

- TOD shop web dist: /home/WEB/todshop/m1/dist

## 7. Backend Paths

- TOD backend base path: /home/WAS/apps

## 8. Nginx / Proxy

- Current public 80 port is handled by docker nginx

- docker nginx can proxy to host TOD backends through 172.17.0.1

- Verified proxy connectivity:

  - 8112

  - 8082

  - 8081

## 9. Migration Direction

- Keep legacy TOD (Java/MySQL) running

- Add new services incrementally (Python/PostgreSQL)

- Final target:

  - dongji.ai -> landing

  - user.dongji.ai -> user web

  - shop.dongji.ai -> shop web

- New AI/ranking services should be added without breaking legacy TOD

## 10. Immediate Next Step

- Step 1: add DNS records in Cloudflare

- Step 2: prepare separated web directories for landing / user / shop

- Step 3: formalize nginx routing