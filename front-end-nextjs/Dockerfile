FROM node:18 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:18 AS production
WORKDIR /app
COPY package*.json ./
RUN npm install --only=production
COPY --from=build /app/.next ./.next
COPY --from=build /app/public ./public
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/next.config.js ./next.config.js
EXPOSE 3000
CMD ["npm", "start"]