FROM node:20.19.0-alpine3.20 AS builder
WORKDIR /opt/server
COPY package.json .
COPY server.js .
RUN npm install

FROM node:20.10.0-alpine3.20 
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser roboshop && -G roboshop && \
    chown -R roboshop:roboshop /opt/server
LABEL com.project="roboshop" \
      com.author="Ram"
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
COPY --from=builder /opt/server .
USER roboshop
EXPOSE 8080
CMD ["server.js"]
ENTRYPOINT [ "node" ]