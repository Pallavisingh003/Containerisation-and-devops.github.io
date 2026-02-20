
# Docker Lab: NGINX Base Image Comparison

## Objective

Deploy NGINX using:

- Official nginx image
- Ubuntu-based custom image
- Alpine-based custom image

Compare:
- Image size
- Image layers
- Startup time
- Security surface
- Real-world use cases

---

# Part 1: Official NGINX Image

## Pull Image

docker pull nginx:latest

## Run Container

docker run -d --name nginx-official -p 8080:80 nginx

## Verify

curl http://localhost:8080

---

# Part 2: Ubuntu-Based NGINX

Go inside ubuntu folder:

cd ubuntu

## Build Image

docker build -t nginx-ubuntu .

## Run

docker run -d --name nginx-ubuntu -p 8081:80 nginx-ubuntu

---

# Part 3: Alpine-Based NGINX

cd alpine

## Build

docker build -t nginx-alpine .

## Run

docker run -d --name nginx-alpine -p 8082:80 nginx-alpine

---

# Compare Image Sizes

docker images | grep nginx

Approximate Results:

| Image | Size |
|--------|------|
| nginx:latest | ~140MB |
| nginx-ubuntu | ~220MB+ |
| nginx-alpine | ~25–30MB |

---

# Inspect Image Layers

docker history nginx
docker history nginx-ubuntu
docker history nginx-alpine

---

# Serve Custom HTML

cd custom-html

docker run -d \
  -p 8083:80 \
  -v $(pwd):/usr/share/nginx/html \
  nginx

---

# Comparison Summary

| Feature | Official | Ubuntu | Alpine |
|----------|----------|----------|----------|
| Image Size | Medium | Large | Very Small |
| Startup Time | Fast | Slow | Very Fast |
| Debugging Tools | Limited | Excellent | Minimal |
| Production Ready | Yes | Rarely | Yes |

---
<img width="1320" height="88" alt="Screenshot 2026-02-20 at 10 13 25 AM" src="https://github.com/user-attachments/assets/cd6e326d-ddf4-4381-83d3-258615a375df" />
<img width="1438" height="779" alt="Screenshot 2026-02-20 at 10 13 55 AM" src="https://github.com/user-attachments/assets/fd8ed4b5-9b72-4a3c-a211-e5408e5b23e1" />
<img width="1440" height="720" alt="Screenshot 2026-02-20 at 10 14 18 AM" src="https://github.com/user-attachments/assets/a072acbe-23b9-4c55-90cc-b078b78c1f05" />
<img width="1399" height="621" alt="Screenshot 2026-02-20 at 10 14 37 AM" src="https://github.com/user-attachments/assets/2ec4cbb5-bced-4030-b021-f5209bdb726c" />
<img width="1309" height="662" alt="Screenshot 2026-02-20 at 10 14 49 AM" src="https://github.com/user-attachments/assets/c92fa78c-a0f0-42d4-87c8-a5812793a869" />
<img width="1440" height="673" alt="Screenshot 2026-02-20 at 10 15 01 AM" src="https://github.com/user-attachments/assets/1eef1fef-5d38-41a0-9b17-2cbb545eceb0" />
<img width="1195" height="91" alt="Screenshot 2026-02-20 at 10 15 08 AM" src="https://github.com/user-attachments/assets/e185d118-9f88-49d3-b3bf-f547861114c2" />
<img width="939" height="41" alt="Screenshot 2026-02-20 at 10 20 11 AM" src="https://github.com/user-attachments/assets/ef50bc28-8f2c-4fad-bb8d-a3d6b816a643" />
<img width="1127" height="372" alt="Screenshot 2026-02-20 at 10 20 45 AM" src="https://github.com/user-attachments/assets/9c424a00-6e8a-479a-9b3e-e608b0970791" />



