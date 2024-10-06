# Deployment Stage
FROM node:18-alpine
LABEL maintainer="Mohamed Belkacem mohamed.belkacem4004@gmail.com"
LABEL version="1.0.0"
LABEL description="A Docker image for Express-gateway."
LABEL source="https://github.com/belkacem-mohamed-404/Garage-management-system.git"
RUN apk add --no-cach curl
RUN addgroup -S pitstop && adduser -S pitstop -G pitstop
WORKDIR /app
COPY package*.json .
RUN npm install --force
COPY . .
ENV PORT 8080
EXPOSE ${PORT}
RUN chown -R pitstop:pitstop /app 
USER pitstop
ENTRYPOINT ["node"]
CMD ["server.js"]
