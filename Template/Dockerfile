FROM majiajue/jdk1.8

COPY src/ezgadget.jar /var/www/html/
COPY _files/flag /flag
COPY _files/flag.sh /flag.sh
COPY _files/start.sh /start.sh

EXPOSE 8888

RUN sh -c "chown -R www-data:www-data /var/www/html"
RUN sh -c "chmod 777 -R /var/www/html/"

ENTRYPOINT ["/start.sh"]