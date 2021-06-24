FROM node:12.7-alpine

# install chrome for protractor tests

# set working directory
WORKDIR /usr/src/app


# install and cache app dependencies
COPY package.json /app/package.json
RUN npm install
COPY . .
RUN npm install -g @angular/cli@7.3.9 --unsafe

# start app
CMD ["ng" ,"serve"]
