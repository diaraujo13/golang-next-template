
ARG NODE_VERSION=20.11.1

FROM node:${NODE_VERSION}-alpine as base

# Update APK repositories and install Yarn
RUN apk update && apk add yarn

WORKDIR /app
EXPOSE 3000

###----------------------------------###
###----------------------------------###
####         /$$                     
####        | $$                     
####    /$$$$$$$  /$$$$$$  /$$    /$$
####   /$$__  $$ /$$__  $$|  $$  /$$/
####  | $$  | $$| $$$$$$$$ \  $$/$$/ 
####  | $$  | $$| $$_____/  \  $$$/  
####  |  $$$$$$$|  $$$$$$$   \  $/   
####   \_______/ \_______/    \_/    
####                                 
####                                 
####                                 
###----------------------------------###

FROM base as dev

COPY package-*.json  ./

RUN apk add --no-cache libc6-compat libstdc++ \
    && yarn add @next/swc-linux-x64-musl --optional || yarn add @next/swc-linux-arm64-musl --optional  \
    && yarn install

COPY . .
CMD yarn dev


###----------------------------------###
###----------------------------------###
### 
### 
###                                      /$$
###                                     | $$
###   /$$$$$$   /$$$$$$   /$$$$$$   /$$$$$$$
###  /$$__  $$ /$$__  $$ /$$__  $$ /$$__  $$
### | $$  \ $$| $$  \__/| $$  \ $$| $$  | $$
### | $$  | $$| $$      | $$  | $$| $$  | $$
### | $$$$$$$/| $$      |  $$$$$$/|  $$$$$$$
### | $$____/ |__/       \______/  \_______/
### | $$                                    
### | $$                                    
### |__/                                    
### 
### 
###----------------------------------###


FROM base as prod

COPY package.json yarn.lock ./

RUN apk add --no-cache libc6-compat libstdc++ \
    && yarn add @next/swc-linux-x64-musl --optional \
    && yarn install
COPY . .
RUN yarn build
CMD yarn start 
