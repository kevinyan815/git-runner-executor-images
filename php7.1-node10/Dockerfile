# Set the base image for subsequent instructions
FROM php:7.1

MAINTAINER KevinYan

# Update packages
RUN apt-get update

# Install PHP and composer dependencies
RUN apt-get install -qq git curl libmcrypt-dev libjpeg-dev libpng-dev libfreetype6-dev libbz2-dev

# Clear out the local repository of retrieved package files
RUN apt-get clean

# Install needed extensions
# Here you can install any other extension that you need during the test and deployment process
RUN docker-php-ext-install pdo pdo_mysql mcrypt zip gd

# |--------------------------------------------------------------------------
# | Composer
# |--------------------------------------------------------------------------
# |
# | Installs Composer to easily manage your PHP dependencies.
# |
RUN curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer &&\
    composer config -g repo.packagist composer https://packagist.laravel-china.org

# |--------------------------------------------------------------------------
# | NodeJS
# |--------------------------------------------------------------------------
# |
# | Installs NodeJS and npm. The later will allow you to easily manage
# | your frontend dependencies.
# |

RUN apt-get update &&\
    apt-get install -y --no-install-recommends gnupg &&\
    curl -sL https://deb.nodesource.com/setup_10.x | bash - &&\
    apt-get update &&\
    apt-get install -y --no-install-recommends nodejs &&\
    npm config set registry https://registry.npm.taobao.org --global


# |--------------------------------------------------------------------------
# | Ansible
# |--------------------------------------------------------------------------
# |
# | Installs ansible. The later will allow you deploy project to remote server
# | and execute operation on target server remotely from this build enviornment.
# |
RUN apt-get update &&\
    apt-get install -y --no-install-recommends python-setuptools &&\
    apt-get install -y --no-install-recommends python-pip &&\
    pip install ansible
