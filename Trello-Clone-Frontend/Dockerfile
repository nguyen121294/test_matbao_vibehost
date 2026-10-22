# Build context = Trello-Clone-Frontend root
FROM node:20-alpine AS build
WORKDIR /app
COPY package.json ./
RUN npm install
COPY packages ./packages
COPY apps ./apps
COPY index.html vite.config.js ./
ARG VITE_API_URL=https://trello-clone-api.n1.tinhgon.xyz
ENV VITE_API_URL=$VITE_API_URL
RUN npm run build

FROM nginx:alpine
COPY apps/user/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
