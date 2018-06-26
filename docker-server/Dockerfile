FROM anapsix/alpine-java:8_server-jre
ADD bakery-app.war .

ARG dbip
ARG dbname=flow_bakery
ARG dbuser=flow_bakery_user
ARG dbpw=flow_bakery_user_pw

ENV dbip=$dbip
ENV dbname=$dbname
ENV dbuser=$dbuser
ENV dbpw=$dbpw

ENTRYPOINT java -jar \
                -Xmx8g -Xms8g \
                -Dvaadin.productionMode \
                -Dspring.datasource.url=jdbc:postgresql://$dbip:5432/$dbname \
                -Dspring.datasource.username=$dbuser \
                -Dspring.datasource.password=$dbpw \
                bakery-app.war