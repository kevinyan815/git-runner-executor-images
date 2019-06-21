FROM php:7.1.22-fpm

# Update packages
RUN apt-get update

# Install PHP and composer dependencies
RUN apt-get install -qq git curl libmcrypt-dev libjpeg-dev libpng-dev libfreetype6-dev libbz2-dev

# Clear out the local repository of retrieved package files
RUN apt-get clean

# Install needed extensions
# Here you can install any other extension that you need during the test and deployment process
# |--------------------------------------------------------------------------
# | Install php extensions from docker hub php source
# |--------------------------------------------------------------------------
# |
# | Installs PHP extension
# |
RUN docker-php-ext-install pdo pdo_mysql mcrypt zip gd pcntl opcache bcmath


# |--------------------------------------------------------------------------
# | Install php extensions using pecl
# |--------------------------------------------------------------------------
# |
# | Installs PHP redis gRPC extension
# |
RUN pecl install grpc \
     && docker-php-ext-enable grpc \
     && pecl install -o -f redis \
     && docker-php-ext-enable redis \
     && rm -rf /tmp/pear


# |--------------------------------------------------------------------------
# | PHP phalcon extension from source code
# |--------------------------------------------------------------------------
# |
# | Installs PHP phalcon extension
# |
ENV PHALCON_VERSION=3.4.2
ENV PTOOLSPATH=/usr/local/phalcon-devtools
RUN curl -sSL "https://codeload.github.com/phalcon/cphalcon/tar.gz/v${PHALCON_VERSION}" | tar -xz \
    && cd cphalcon-${PHALCON_VERSION}/build \
    && ./install \
    && cp ../tests/_ci/phalcon.ini $(php-config --configure-options | grep -o "with-config-file-scan-dir=\([^ ]*\)" | awk -F'=' '{print $2}') \
    && cd ../../ \
    && rm -r cphalcon-${PHALCON_VERSION} \
    # install phalcon develop tools
    && cd /usr/local \
    && git clone git://github.com/phalcon/phalcon-devtools.git \
    && . ./phalcon-devtools/phalcon.sh \
    && ln -s /usr/local/phalcon-devtools/phalcon.php /usr/local/bin/phalcon



# |--------------------------------------------------------------------------
# | Composer
# |--------------------------------------------------------------------------
# |
# | Installs Composer to easily manage your PHP dependencies.
# |
RUN curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer &&\
    composer config -g repo.packagist composer https://packagist.laravel-china.org
