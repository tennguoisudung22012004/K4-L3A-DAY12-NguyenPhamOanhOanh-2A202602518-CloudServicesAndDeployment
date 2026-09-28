# Thong Tin Deploy - Checkpoint 5

## Thong Tin Hoc Vien

| Muc | Noi dung |
|-----|----------|
| Ho va ten | Nguyen Pham Oanh Oanh |
| mã học viên | 2A202602518 |
| Repo | https://github.com/tennguoisudung22012004/K4-L3A-DAY12-NguyenPhamOanhOanh-2A202602518-CloudServicesAndDeployment |

## Service

| Muc | Noi dung |
|-----|----------|
| Public URL | https://k4-l3a-day12-nguyenphamoanhoanh-2a202602518-clou-production.up.railway.app |
| Platform | Railway |
| Ngay deploy | 2026-09-28 |

## Bien Moi Truong Da Set Tren Cloud

Chi ghi ten bien, khong ghi gia tri secret that.

| Bien | Da set | Ghi chu |
|------|--------|---------|
| `PORT` | co | Railway tu gan |
| `AGENT_API_KEY` | can kiem tra tren Railway | dat trong Railway Variables, khong nam trong repo |
| `REDIS_URL` | can kiem tra tren Railway | Redis add-on cua Railway |
| `RATE_LIMIT_PER_MINUTE` | co | 10 |
| `MONTHLY_BUDGET_USD` | co | 10.0 |
| `LOG_LEVEL` | co | INFO |

## Lenh Kiem Tra

Thay URL bang Public URL o tren:

```bash
curl -i https://k4-l3a-day12-nguyenphamoanhoanh-2a202602518-clou-production.up.railway.app/health

curl -i https://k4-l3a-day12-nguyenphamoanhoanh-2a202602518-clou-production.up.railway.app/ready

curl -i -X POST https://k4-l3a-day12-nguyenphamoanhoanh-2a202602518-clou-production.up.railway.app/ask \
  -H "Content-Type: application/json" \
  -d '{"question":"Hello"}'

curl -i -X POST https://k4-l3a-day12-nguyenphamoanhoanh-2a202602518-clou-production.up.railway.app/ask \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $AGENT_API_KEY" \
  -H "X-User-Id: sv-test" \
  -d '{"question":"Deploy la gi?"}'
```

## Ket Qua Chay That

Lan kiem tra gan nhat:

```text
GET /health
HTTP/1.1 200 OK
{"status":"ok","service":"day12-agent","version":"1.0.0"}

GET /ready
HTTP/1.1 500 Internal Server Error
Internal Server Error

POST /ask khong co API key
HTTP/1.1 500 Internal Server Error
Internal Server Error
```

Ghi chu: `/health` da hoat dong. `/ready` va `/ask` dang can kiem tra lai Railway Variables, dac biet la `AGENT_API_KEY` va `REDIS_URL`, sau do redeploy/restart service.

## Anh Chup Man Hinh

Dat anh minh chung trong thu muc `screenshots/`:

- `screenshots/dashboard.png`: dashboard Railway co service dang online.
- `screenshots/health.png`: ket qua goi `/health`, `/ready`, `/ask`.

## Neu Dung Phuong An Du Phong

Khong dung phuong an du phong. Bai deploy tren Railway.
