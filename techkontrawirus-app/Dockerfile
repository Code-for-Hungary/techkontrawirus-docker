FROM webdevops/php-nginx:7.2
ENV DEBIAN_FRONTEND=noninteractive
ENV HOME /home/techkontrawirus

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x  | bash -
RUN apt-get -y install nodejs

RUN apt-get update && apt-get upgrade -y && \
      apt-get install -yq \
      nodejs \
      git

# Clone Github repo.
RUN git clone https://github.com/k-monitor/techkontrawirus.git $HOME

# Make sure laravel.log is writable to both root and www-data (e.g. cron jobs).
RUN touch ${HOME}/storage/logs/laravel.log \
    && chown root:application ${HOME}/storage/logs/laravel.log \
    && chmod 664 ${HOME}/storage/logs/laravel.log

# Run composer
ADD https://getcomposer.org/installer /tmp
RUN php /tmp/installer --install-dir=/usr/local/bin --filename=composer --version=1.10.16 && \
    cd $HOME && composer install && npm install && npm run production

RUN chown -R application:application $HOME/storage/ && \
    chown -R application:application $HOME/bootstrap/cache

WORKDIR $HOME
