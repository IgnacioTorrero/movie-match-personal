FROM node:20-alpine

WORKDIR /app

ENV PRISMA_CLI_QUERY_ENGINE_TYPE="binary"

COPY recommendation-service/package*.json ./
RUN npm install
RUN npm install -g typescript

COPY recommendation-service/. ./
COPY prisma ./prisma
COPY recommendation-service/swagger/swagger.yaml /app/swagger.yaml

RUN rm -rf dist && \
    npx tsc && \
    chmod +x ./node_modules/.bin/prisma && \
    npx prisma generate --schema=./prisma/schema.prisma

EXPOSE 3000

CMD ["sh", "-c", "npx prisma migrate deploy --schema=./prisma/schema.prisma && node dist/server.js"]
