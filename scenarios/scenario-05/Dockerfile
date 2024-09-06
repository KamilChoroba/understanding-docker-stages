FROM alpine:3.20.2 AS base
WORKDIR /app

FROM base AS install_dependencies
RUN apk add --update npm
ADD ./src ./src
ADD ./package.json ./tsconfig.json .
RUN npm install

# ⬇️ Adding new stage for dev in between
FROM install_dependencies AS dev
CMD ["npm", "run", "dev"]

FROM install_dependencies AS build
RUN npm run build

FROM install_dependencies AS prod_dependencies
RUN mkdir /app/prod_node_modules
ADD package.json /app/prod_node_modules
RUN npm install --omit=dev --prefix /app/prod_node_modules

FROM node:21
COPY --from=build /app/dist /app/dist
COPY --from=prod_dependencies /app/prod_node_modules/node_modules /app/dist/node_modules
CMD ["node", "/app/dist/index.js"]