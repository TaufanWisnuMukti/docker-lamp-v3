FROM php:8.0-apache

RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod ssl
RUN usermod -u 33 www-data
RUN usermod -G staff www-data
