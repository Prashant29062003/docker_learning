# --- Stage-1 --- BUILD STAGE
FROM node:24-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

# --- Stage-2 --- PRODUCTION STAGE
FROM node:24-alpine
WORKDIR /myapp
COPY --from=builder /app /myapp
EXPOSE 3000
ENV PORT=3000
CMD ["node", "index.js"]
