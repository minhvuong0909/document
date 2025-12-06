# ☁️ BACKEND & CLOUD FULL GUIDE

- giải thích và hướng dẫn

## 1. Kiến thức nền tảng Backend

### Kiến trúc Backend gồm:

```
API layer (REST hoặc GraphQL)

Business logic layer

Database layer

Authentication / Authorization

File storage

Caching

Background jobs

Monitoring & Logging


```

### Các giao thức:

HTTP / HTTPS

WebSocket (real-time)

gRPC (microservices)

### Database:

SQL: MySQL, PostgreSQL
NoSQL: MongoDB, Redis, DynamoDB

### Mô hình thiết kế backend:

Monolithic

Microservices

Event-driven

Serverless

## 2. Cloud là gì?

`Cloud = dùng tài nguyên máy chủ của AWS / GCP / Azure.`

### Cloud cung cấp 4 nhóm dịch vụ chính:

| Loại           | Giải thích                                     |
| -------------- | ---------------------------------------------- |
| **Compute**    | Nơi chạy code backend (EC2, Cloud Run, Lambda) |
| **Storage**    | Lưu file (S3, Cloud Storage)                   |
| **Database**   | RDS, Cloud SQL, DynamoDB                       |
| **Networking** | Load balancer, VPC, Firewall                   |

## 3. Serverless là `Chỉ viết hàm → cloud tự chạy, tự scale.`

### ✔ Ưu điểm:

Không quản lý server

Tự scale vô hạn

Rẻ (trả theo request)

### ✔ Nhược:

Không phù hợp API real-time

Cold start

### Dịch vụ:

```
AWS Lambda

Google Cloud Functions

Cloudflare Workers
```

## 4. Load Balancing

### Mục đích:

```
Chia đều traffic vào nhiều server → tránh quá tải.

Load balancer làm được:

Chia tải

Health-check

Tự chuyển hướng khi server chết

Triển khai blue-green hoặc canary

LB phổ biến:

AWS Application Load Balancer

Google Cloud Load Balancer

NGINX
```

## 5. Docker

### Docker dùng để gì?

Đóng gói app vào container với:

Code

Runtime

Dependencies

Chạy ở đâu cũng giống nhau.

### ✔ Lệnh cơ bản:

```
docker build -t myapp .
docker run -p 3000:3000 myapp
docker ps
docker stop <id>
```

### Dockerfile mẫu:

```
FROM node:18
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

## 6. Kubernetes (K8s)

### ✔ Dùng để:

Quản lý hàng trăm container

Tự động scale

Tự healing (restart nếu crash)

Quản lý rolling update

### Tài nguyên quan trọng:

Pod

Deployment

Service

Ingress

ConfigMap

Secret

## 7. CI/CD (DevOps)

### ✔ CI = Continuous Integration

Tự build, test mỗi lần push code.

### ✔ CD = Continuous Deployment

Tự deploy lên cloud khi merge main.

Tools:

GitHub Actions

GitLab CI

Jenkins

- Ví dụ CI/CD YAML:

```
name: Deploy

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install deps
        run: npm install
      - name: Run tests
        run: npm test
```

## 8. Cách deploy backend lên Cloud (thực tế)

### 🚀 Cách 1 — Deploy bằng Docker lên AWS EC2

```bash
- Bước 1: Tạo EC2
  Chọn Ubuntu
  Mở port (80/443/3000)

- Bước 2: SSH vào EC2
    ssh -i your-key.pem ubuntu@<ip>

- Bước 3: Cài Docker
    sudo apt update
    sudo apt install docker.io -y

- Bước 4: Upload code (hoặc pull GitHub)
    git clone <repo>
    cd project

- Bước 5: Build Docker image
    docker build -t backend .

- Bước 6: Chạy container
    docker run -d -p 3000:3000 backend
```
