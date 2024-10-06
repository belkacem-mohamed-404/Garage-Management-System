
# Build stage
FROM node:lts-alpine as build

## Metadata of this container
LABEL maintainer="Mohamed Belkacem mohamed.belkacem4004@gmail.com"
LABEL version="1.0.0"
LABEL description="A Docker image for a Vue.js app using http-server."
LABEL source="https://github.com/belkacem-mohamed-404/Garage-management-system.git"

WORKDIR /app
COPY package*.json ./
RUN npm install --force
COPY . .
RUN npm run build

# Deployment stage
FROM node:lts-alpine as deployment
RUN apk add --no-cach curl
RUN addgroup -S pitstop && adduser -S pitstop -G pitstop
RUN npm install -g http-server
WORKDIR /app
COPY --from=build /app/dist ./dist
RUN chown -R pitstop:pitstop /app
USER pitstop
ENV PORT 8080
EXPOSE ${PORT}
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
 CMD curl -f http://localhost:${PORT} || exit 1
CMD ["http-server", "dist"]

