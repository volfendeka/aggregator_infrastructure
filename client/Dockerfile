FROM ubuntu:16.04
MAINTAINER Volodymyr Deka <volfendeka@gmail.com>

ARG environment=prod
# Update distribution
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y git wget

# Copy nodejs install script and run it
ADD ./npm-install.sh /root/npm-install.sh
RUN chmod +x /root/npm-install.sh
RUN /root/npm-install.sh

# remove chache and temporary files
RUN apt-get clean && rm -rf /tmp/*

# Copy application files
RUN git clone https://github.com/volfendeka/aggregator_admin_front.git /www

ADD ./config-$environment.js /www/src/configs/config.js

#Run project
RUN cd /www && npm install

# Copy startup script
ADD ./entrypoint.sh /root/entrypoint.sh
RUN chmod +x /root/entrypoint.sh

EXPOSE 80

# Run startup script
ENTRYPOINT ["/root/entrypoint.sh"]
