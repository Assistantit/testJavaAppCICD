FROM tomcat:latest

LABEL maintainer="Griml"

ADD ./target/helloworld.war /usr/local/tomcat/webapps/

EXPOSE 8080

CMD ["catalina.sh", "run"]
