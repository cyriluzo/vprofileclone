FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN export GIT_TRACE_PACKET=1
RUN export GIT_TRACE=1
RUN export GIT_CURL_VERBOSE=1
RUN git config --global core.compression 0
RUN git clone --depth 1 https://github.com/cyriluzo/vprofileclone.git
RUN cd vprofile-project
RUN git fetch --unshallow 
RUN git pull --all
RUN git checkout docker && mvn install
FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
