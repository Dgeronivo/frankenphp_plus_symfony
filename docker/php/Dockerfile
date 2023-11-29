FROM dunglas/frankenphp


ARG HOST_UID=1000
ARG HOST_GID=1000

RUN apt-get update && apt-get -y install git

COPY --from=composer:2.2 /usr/bin/composer /usr/local/bin/composer

WORKDIR /app

COPY . /app

RUN userdel -f www-data &&\
    if getent group www-data ; then groupdel www-data; fi &&\
    groupadd -g ${HOST_GID} www-data &&\
    useradd -l -u ${HOST_UID} -g www-data www-data &&\
    install -d -m 0755 -o www-data -g www-data /home/www-data &&\
    chown --changes --silent --no-dereference --recursive \
          --from=33:33 ${HOST_UID}:${HOST_GID} \
        /app

USER www-data

#ENTRYPOINT ["php", "simpleStart.php"]
