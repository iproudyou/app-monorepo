### STAGE 1: Build ###
FROM node:15.10.0-alpine3.10 as build
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json yarn.lock ./
RUN rm -rf node_modules && yarn install --frozen-lockfile
RUN yarn install --silent
RUN yarn add react-scripts@4.0.1 -g --silent
COPY . ./
RUN yarn build

### STAGE 2: Run ###
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html

COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 3000

CMD [ "nginx", "-g", "daemon off;" ]
