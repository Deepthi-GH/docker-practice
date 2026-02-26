FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY *.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine3.21
WORKDIR /opt/server
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && chown -R roboshop:roboshop /opt/server
LABEL com.project="roboshop" \
       component="cart" \
       created_by="deepu"
ENV REDIS_HOST=redis \
    CATALOGUE_HOST=catalogue \
    CATALOGUE_PORT=8080
COPY --from=build  /opt/server /opt/server   
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"]


# FROM node:20
# EXPOSE 8080
# WORKDIR /opt/server
# COPY *.json .
# COPY *.js .
# RUN npm install
# ENV REDIS_HOST=redis \
#     CATALOGUE_HOST=catalogue \
#     CATALOGUE_PORT=8080
# CMD ["node", "server.js"]