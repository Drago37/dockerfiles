FROM mariadb:11.3

ENV TZ="Europe/Paris"

RUN apt-get update && apt-get install -y tzdata
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && dpkg-reconfigure --frontend noninteractive tzdata

RUN chmod o-w -R /etc/mysql/conf.d/
