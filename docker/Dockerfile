FROM openjdk:8u151-jdk-alpine3.7
RUN apk update && apk upgrade && apk add ca-certificates && update-ca-certificates \
    && apk add --update tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && rm -rf /var/cache/apk/* 
ENV TZ=Asia/Shanghai

EXPOSE 8070

ENV APP_HOME /usr/src/app

COPY docker/Shanghai /etc/localtime

COPY target/shopping-cart-0.0.1-SNAPSHOT.jar $APP_HOME/app.jar

WORKDIR $APP_HOME

#ENTRYPOINT exec java -jar -Duser.timezone=Asia/Shanghai app.jar
ENTRYPOINT exec java -jar -Duser.timezone=Asia/Shanghai app.jar