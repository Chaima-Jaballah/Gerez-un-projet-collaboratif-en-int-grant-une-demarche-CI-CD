FROM node:18.20.2-alpine3.20 AS build

WORKDIR /usr/local/app
COPY ./ /usr/local/app/
RUN yarn && yarn cache clean
RUN npm run build

FROM nginx:1.26.0-alpine3.20 AS production

RUN apk update && apk upgrade --no-cache
RUN adduser -D user
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html
RUN chown -R user:user /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
USER user

EXPOSE 8080
