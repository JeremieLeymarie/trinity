FROM node:22.11.0-alpine3.20 as builder 


WORKDIR /app
COPY ./package.json .

# Install dependencies
RUN npm i

COPY . .

# Build application
RUN npm run build


FROM node:22.11.0-alpine3.20 

WORKDIR /app

COPY --from=builder /app/public ./public

COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static

EXPOSE 3000
ENV HOSTNAME="0.0.0.0"

CMD node server.js