from dockerfile/java:oracle-java8
maintainer Diogo Costa, costa.h4evr@gmail.com

RUN echo "deb http://downloads.sourceforge.net/project/sonar-pkg/deb binary/" >> /etc/apt/sources.list

RUN echo "Acquire::http::Proxy \"http://10.11.11.61:3128\";" > /etc/apt/apt.conf.d/10proxy 

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y --force-yes sonar

RUN rm /etc/apt/apt.conf.d/10proxy

RUN sed -i 's|#wrapper.java.additional.8=-server|wrapper.java.additional.8=-server|g' /opt/sonar/conf/wrapper.conf

RUN sed -i 's|#sonar.jdbc.password=sonar|sonar.jdbc.password=123qwe|g' /opt/sonar/conf/sonar.properties
RUN sed -i 's|#sonar.jdbc.user=sonar|sonar.jdbc.user=sonar|g' /opt/sonar/conf/sonar.properties
RUN sed -i 's|sonar.jdbc.url=jdbc:h2|#sonar.jdbc.url=jdbc:h2|g' /opt/sonar/conf/sonar.properties
RUN sed -i 's|#sonar.jdbc.url=jdbc:mysql://localhost|sonar.jdbc.url=jdbc:mysql://${env:DB_PORT_3306_TCP_ADDR}|g' /opt/sonar/conf/sonar.properties 

CMD ["/opt/sonar/bin/linux-x86-64/sonar.sh","console"]
