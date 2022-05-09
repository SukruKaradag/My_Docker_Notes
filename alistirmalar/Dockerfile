FROM ubuntu:18.04
RUN apt-get update -y
RUN apt-get install -y default-jre
WORKDIR /merhaba
COPY /myapp .
CMD ["java",  "merhaba"]