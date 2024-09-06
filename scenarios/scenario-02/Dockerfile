FROM alpine:3.20.2 AS base
# ⬆️ Adding the alias "base" with the keyword "AS". This can be used for later references

WORKDIR /app

# ⬇️ Adding new stage and use the "base" alias as the base image
FROM base AS install_dependencies

# ⬇️ installing the npm package inside of this stage
RUN apk add --update npm

# ⬇️ Copy all files in src, package.json and tsconfig.json to the /app directory
ADD ./src ./src
ADD ./package.json ./tsconfig.json .

# ⬇️ Execute npm install to install all packages defined in package.json
RUN npm install
