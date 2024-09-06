FROM alpine:3.20.2 AS base
WORKDIR /app

FROM base AS install_dependencies
RUN apk add --update npm
ADD ./src ./src
ADD ./package.json ./tsconfig.json .
RUN npm install

FROM install_dependencies AS build
RUN npm run build

# ⬇️ Install production dependencies only
FROM install_dependencies AS prod_dependencies
RUN mkdir /app/prod_node_modules
ADD package.json /app/prod_node_modules
RUN npm install --omit=dev --prefix /app/prod_node_modules

# ⬇️ Add a clean new stage without without any reference to previous stages
FROM node:21

# ⬇️ Copy required files from previous stages to run the application
COPY --from=build /app/dist /app/dist
COPY --from=prod_dependencies /app/prod_node_modules/node_modules /app/dist/node_modules

# ⬇️ Run the application
CMD ["node", "/app/dist/index.js"]