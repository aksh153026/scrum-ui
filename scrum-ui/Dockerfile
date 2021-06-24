FROM node:12.7-alpine AS build
WORKDIR /usr/src/app
COPY . .
RUN npm install
RUN npm install -g @angular/cli@7.3.9 
RUN ng install
RUN ng build --prod

# start app
FROM nginx:1.17.1-alpine
COPY default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /usr/src/app/dist/scrum-ui /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
