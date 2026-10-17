# ==============================================================================
# Practical 11: Containerization with Docker & Docker Compose
# Student: Aayush Malhotra (24CS051)
# Multi-stage Dockerfile for React (Vite) Frontend
# ==============================================================================

# Stage 1: Build the React Application (Node 20+ required for Vite 8 / Rolldown)
FROM node:20-alpine AS build

WORKDIR /app

# Copy dependency manifests and install packages
COPY package*.json ./
RUN npm install

# Copy application source code and build production bundle
COPY . .
RUN npm run build

# Stage 2: Lightweight Production Runtime Stage (Supplementary Problem: Multi-stage build)
FROM node:20-alpine AS production

WORKDIR /app

# Install minimal production preview runner
COPY package*.json ./
RUN npm install --omit=dev

# Copy compiled dist from build stage
COPY --from=build /app/dist ./dist

# Expose Vite preview port
EXPOSE 5173

# Serve production build using Vite preview accessible across Docker bridge network
CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "5173"]
