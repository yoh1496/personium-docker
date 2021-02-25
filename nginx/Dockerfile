FROM nginx:1.14

ENV MDNS_HOSTNAME=personium.local

RUN apt-get update && apt-get install -y \
  vim \
  curl \
  jq

RUN apt-get update -y && apt-get install -y \
  dbus avahi-daemon avahi-utils supervisor

COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY avahi.sh /usr/local/bin/avahi.sh

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY entrypoint.sh /

EXPOSE 443
EXPOSE 80

# ENTRYPOINT [ "/entrypoint.sh" ]

ENTRYPOINT ["/usr/bin/supervisord","-nc","/etc/supervisor/supervisord.conf"]