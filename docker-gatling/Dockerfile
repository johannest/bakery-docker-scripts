# HOWTO
# cp ../src/test/scala/BaristaFlow.scala .
# cp -r ../src/test/resources/bodies .
# scp -i your-ssh-keypair.pem -r * ec2-user@ipaddress:.
# ssh -i your-ssh-keypair.pem ec2-user@ipaddress
# docker build . --rm -t bakery-gatling --build-arg users=1 --build-arg ramp=1 --build-arg repeats=5 --build-arg baseUrl=http://appserver-node.ip.address:8080
# docker run -it --ulimit nofile=90000:90000 bakery-gatling && docker cp $(docker ps -alq):/opt/gatling/results . && docker rm $(docker ps -alq)
# scp -i your-ssh-keypair.pem -r ec2-user@ipaddress:results .
FROM denvazh/gatling:latest

ADD BaristaFlow.scala /opt/gatling/user-files/simulations/BaristaFlow.scala
ADD bodies /opt/gatling/user-files/bodies
VOLUME /opt/gatling/results

ARG users=1
ARG ramp=1
ARG repeats=1
ARG baseUrl

ENV JAVA_OPTS="-Dgatling.baseUrl=$baseUrl \
               -Dgatling.sessionCount=$users \
               -Dgatling.sessionRepeats=$repeats \
               -Dgatling.sessionStartInterval=$ramp"

ENTRYPOINT /opt/gatling/bin/./gatling.sh -s BaristaFlow