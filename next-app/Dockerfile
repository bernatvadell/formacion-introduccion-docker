FROM node:16 as deps

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

FROM node:16 as builder

WORKDIR /app

COPY --from=deps /app/node_modules /app/node_modules
COPY . .
RUN npm run build

FROM node:16-alpine as runtime

ENV NODE_ENV production

WORKDIR /app

COPY --from=builder /app/next.config.js ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./package.json
COPY --from=builder /app/styles ./styles

CMD npm run start