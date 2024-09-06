FROM alpine:3.20.2 AS base
WORKDIR /app

FROM base AS install_dependencies
RUN apk add --update npm
ADD ./src ./src
ADD ./package.json ./tsconfig.json .
RUN npm install

# ⬇️ Adding new stage to build the project
FROM install_dependencies AS build

# ⬇️ Execute the build command for this project
RUN npm run build
