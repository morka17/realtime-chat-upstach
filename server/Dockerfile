# Step 1 - Build the base 
FROM node:lts-alpine AS base 
WORKDIR /app
COPY src ./src 
COPY package*.json ./
COPY tsconfig*.json ./
RUN npm install 


# Step 2 - Build the app
FROM base AS build 
WORKDIR /app 
RUN npm run build 


# Step 2 - Production 
FROM node:lts-alpine
WORKDIR /app 
COPY package*.json ./
RUN npm install --only-production
COPY --from=build /app/build ./ 

CMD [ "node" "main.js" ]