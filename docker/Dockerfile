FROM nginx:stable

RUN apt-get update && apt-get upgrade -y && apt-get install goaccess cron -y

# Configuraciones Nginx
COPY ./resources/conf/nginx.conf /etc/nginx/nginx.conf
COPY ./resources/conf/buffer.conf /etc/nginx/conf.d/buffer.conf
COPY ./resources/conf/my_test_api.conf /etc/nginx/conf.d/my_test_api.conf
COPY ./resources/certs/ /etc/ssl/certs/nginx/

#Configuraciones goaccess
RUN mkdir /usr/share/nginx/html/goaccess
COPY ./resources/conf/goaccess.conf /etc/goaccess/goaccess.conf

RUN printf "#!/bin/bash \
\n# update report  \
\n rm /usr/share/nginx/html/goaccess/report.html\n \
\n goaccess /var/log/nginx/mytestapi.com.access.log -o /usr/share/nginx/html/goaccess/report.html\n" > /usr/bin/update_report.sh
RUN chmod +x /usr/bin/update_report.sh

COPY cronjob /etc/cron.d/cronjob
RUN chmod 0644 /etc/cron.d/cronjob && crontab /etc/cron.d/cronjob

CMD cron && nginx -g "daemon off;"