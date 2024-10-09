FROM php:8.2-fpm

# تنظیم دایرکتوری کاری
WORKDIR /var/www/html

# نصب وابستگی‌ها
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev

# پاک‌سازی کش
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# نصب افزونه‌ها
RUN docker-php-ext-install pdo_mysql zip exif pcntl gd
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# نصب کامپوزر
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# اضافه کردن کاربر برای اپلیکیشن لاراول
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# کپی کردن محتویات اپلیکیشن
ADD . /var/www/html
RUN chown -R www:www /var/www/html

# تغییر کاربر فعلی به www
USER www

# باز کردن پورت 9000 و شروع سرور php-fpm
EXPOSE 9000
CMD ["php-fpm"]
