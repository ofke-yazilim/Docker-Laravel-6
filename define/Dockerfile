ARG PHP_VERSION=7.2
ARG COMPOSER_VERSION=1.8

FROM composer:${COMPOSER_VERSION} => Docker Composer image alınıyor.
FROM php:${PHP_VERSION}-cli => Docker php image alınıyor. Cli Ngnix ya da Apache olmadan çalışabilir.

RUN apt-get update && \
    apt-get install -y autoconf pkg-config libssl-dev git libzip-dev zlib1g-dev && \
    pecl install mongodb && docker-php-ext-enable mongodb && \   => Projemizde mongo db kullanıyoruz mongo için gerekli uzantılar indiriliyor.
    pecl install xdebug && docker-php-ext-enable xdebug && \
    docker-php-ext-install -j$(nproc) pdo_mysql zip

COPY --from=composer /usr/bin/composer /usr/local/bin/composer => Docker projemiz içerisine composer ekliyoruz. Php kullanıyorsanız composer elzemdir.

RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install bcmath pdo pdo_pgsql pgsql => Projemizde Postgresql, Pdo kullanacağız.

RUN docker-php-ext-install mbstring => Php üzerinde tüm dillerin kullanılmasını sağlar.

RUN apt-get update -y && apt-get install -y sendmail libpng-dev

RUN apt-get -y update \
&& apt-get install -y libicu-dev \
&& docker-php-ext-configure intl \
&& docker-php-ext-install intl   => Bu kütüphane projemizde NumberFormatter classın çalışması için gereklidir.

RUN docker-php-ext-install gd => Image işlmelerinde kullanılmak için gereklidir.

RUN apt-get update -y \
  && apt-get install -y \
     libxml2-dev \
  && apt-get clean -y \
  && docker-php-ext-install soap => Soap işlemleri için gerekli.

WORKDIR /app  => Docker projemniz için app adı altında bir çalışma ortamı oluşturuyoruz.
COPY . /app   => Laravel projemizi oluşturduğumuz app ortamına kopyalıyoruz.

CMD php artisan serve --host=0.0.0.0 --port=8000  => Projemizi 0.0.0.0:8000 adresinden ayağı kaldırıyoruz.
EXPOSE 8000   => 8000 portunu container kullansın diye yaralıyoruz.
