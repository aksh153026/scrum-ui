FROM node:12.2.0

# install chrome for protractor tests

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /app/package.json
RUN npm install
COPY . /app
RUN npm install -g @angular/cli@7.3.9 --unsafe

# start app
CMD ["ng" ,"serve"]
