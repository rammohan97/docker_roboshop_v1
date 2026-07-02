FROM python:3.9.25-alpine3.21 AS builder
WORKDIR /opt/server
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev \
COPY requirements.txt .
RUN pip3 install --prefix=/install -r requirements.txt


FROM python:3.9.25-alpine3.21
WORKDIR /opt/server
RUN apk add --no-cache pcre
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /install /usr/local
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt ./
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
USER roboshop
EXPOSE 8080
CMD ["uwsgi", "--ini", "payment.ini"]