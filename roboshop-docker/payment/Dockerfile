FROM python:3.9.25-alpine3.21 AS build
WORKDIR /opt/server
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev
COPY payment.ini *.py requirements.txt  .
RUN pip3 install -r requirements.txt

FROM python:3.9.25-alpine3.21
EXPOSE 8080
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
ENV CART_HOST=cart \
    CART_PORT=8080 \
    USER_HOST=user \
    USER_PORT=8080 \
    AMQP_HOST=rabbitmq \
    AMQP_USER=roboshop \
    AMQP_PASS=roboshop123 
COPY --from=build /opt/server requirements.txt
USER roboshop
CMD [ "--ini", "payment.ini"]
ENTRYPOINT ["uwsgi"]


# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST=cart \
#     CART_PORT=8080 \
#     USER_HOST=user \
#     USER_PORT=8080 \
#     AMQP_HOST=rabbitmq \
#     AMQP_USER=roboshop \
#     AMQP_PASS=roboshop123 
# CMD ["uwsgi", "--ini", "payment.ini"]