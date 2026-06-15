# ═══ Stage 1: Build Vue App ══════════════════════════════════════
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build
# ผลลัพธ์จาก npm run build อยู่ที่ /app/dist/

# ═══ Stage 2: Serve with Nginx ═══════════════════════════════════
FROM nginx:alpine
# copy เฉพาะ /app/dist จาก stage 1 — ไม่มี Node.js ใน image สุดท้าย
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]