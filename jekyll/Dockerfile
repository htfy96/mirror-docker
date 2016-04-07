############################################################
# Dockerfile to build Nginx Installed Containers
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu:xenial

# File Author / Maintainer
MAINTAINER VicLuo

# Add USTC Repo
RUN rm /etc/apt/sources.list
ADD apt_sources.list /etc/apt/sources.list

# Update the repository
RUN apt-get update

# Install zlib(required by jekyll)
RUN apt-get install -y zlib1g-dev jekyll bundler

# Install python
#RUN apt-get install -y python
#RUN apt-get install -y python-toml python-sh python-setproctitle

#Set up the web page
ADD mirror-web /home/mirror-web

WORKDIR /home/mirror-web

RUN bundle install

# WTF
# This is a terrible workaround for
#   Conversion error: Jekyll::Converters::Babel encountered an error while converting 'static/js/index.es6':
#   "\xEF" on US-ASCII
# It seems that encoding.rb mishandles babel.js's leading <EF>, which is a utf-8 zero-width whitespace
RUN sed -i "s/^[ \t]*string.encode('UTF-8')/return string/g" /usr/lib/ruby/vendor_ruby/execjs/encoding.rb

