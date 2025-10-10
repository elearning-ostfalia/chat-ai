FROM php:8.4-apache



RUN echo "Europe/Berlin" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

ENV APACHE_DOCUMENT_ROOT /var/www/html


# install for debugging (remove when running)
RUN apt-get update && apt-get upgrade -y && apt-get install -y net-tools libapache2-mod-auth-openidc

#RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
#RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Enable SSL module, configure Apache for PHP support, and enable our SSL site configuration
#RUN a2enmod rewrite && \
#    a2enmod headers && \
#    a2enmod expires && \
#    a2enmod ssl && \
#    a2enmod proxy && \
#    a2enmod proxy_http && \
#    a2enmod proxy_wstunnel

RUN a2enmod rewrite && \
    a2enmod proxy && \
    a2enmod proxy_http && \
    a2enmod ssl

#RUN docker-php-ext-install pcntl
#RUN docker-php-ext-configure pcntl --enable-pcntl


#RUN apt-get update && apt-get install -y libzip-dev zip libicu-dev libpq-dev && docker-php-ext-install zip


# Copy SSL certificate and key
COPY chat-ai-dev.crt /etc/ssl/certs/chat-ai-dev.crt
COPY chat-ai-dev.key /etc/ssl/private/chat-ai-dev.key

# Copy the custom Apache virtual host config
COPY ./httpd-vhosts.conf /etc/apache2/sites-available/apache-ssl.conf

RUN a2dissite 000-default default-ssl && a2ensite apache-ssl


# run entrypoint.sh with installation script
# ENTRYPOINT ["/var/www/html/tests/docker-simulation/install.sh"]

