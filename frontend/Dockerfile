# -------- Stage 1: Minimal builder --------
FROM alpine:3.20 AS builder

WORKDIR /app

# Copy only required file (optimized layering)
COPY Devops_Intern.html .

# -------- Stage 2: Production --------
FROM nginx:alpine

# Remove default files
RUN rm -rf /usr/share/nginx/html/*

# Copy and rename to index.html (so no custom config needed)
COPY --from=builder /app/Devops_Intern.html /usr/share/nginx/html/index.html

# Expose port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
