---
title: 安装部署
category: QSphere
order: 15
---

### 安装/升级

```bash
docker-compose -f docker-compose.yaml pull
docker-compose -f docker-compose.yaml up -d
```

#### docker-compose.yaml
```yaml
version: "3"
services:
  qsphere-db:
    container_name: qsphere-db
    image: postgres:10
    restart: always
    environment:
      POSTGRES_DB: 'qsphere'
      POSTGRES_PASSWORD: 'password'
    volumes:
      - ./qsphere-pgdata:/var/lib/postgresql/data
    command: ["-c", "max_connections=2000"]

  qsphere-svc:
    container_name: qsphere-svc
    image: bxwill/qsphere:svc-latest
    restart: always
    ports:
      - 6001:6001
    environment:
      PG_DB: 'qsphere'
      PG_SERVER: qsphere-db
      PG_USER: 'postgres'
      PG_PASSWORD: 'password'
    depends_on:
      - qsphere-db

  qsphere-dashboard:
    container_name: qsphere-dashboard
    image: bxwill/qsphere:dashboard-latest
    restart: always
    ports:
      - 3000:3000
    environment:
      PG_DB: 'qsphere'
      PG_SERVER: qsphere-db
      PG_PORT: '5432'
      PG_USER: 'postgres'
      PG_PASSWORD: 'password'
    depends_on:
      - qsphere-db
      - qsphere-svc

  qsphere-ui:
    container_name: qsphere-ui
    image: bxwill/qsphere:ui-latest
    restart: always
    ports:
      - 8080:80
    depends_on:
      - qsphere-svc
      - qsphere-dashboard
```
