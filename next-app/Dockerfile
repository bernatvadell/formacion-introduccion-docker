FROM node:16 as deps

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

FROM node:16 as build-env

WORKDIR /app

COPY --from=deps /app/node_modules /app/node_modules

COPY . .

RUN npm run build

FROM node:16-alpine as runtime

WORKDIR /app

COPY --from=build-env /app /app/

ENTRYPOINT [ "sh", "-c" ]

CMD ["npm", "run", "start"]

