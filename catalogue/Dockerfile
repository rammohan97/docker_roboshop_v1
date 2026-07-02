FROM node:20.19.5-alpine3.21 AS builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine3.21
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
LABEL com.project="roboshop" \
      com.author="Ram" 
COPY --from=builder /opt/server .
USER roboshop
EXPOSE 8080
CMD ["server.js"]
ENTRYPOINT [ "node" ]
