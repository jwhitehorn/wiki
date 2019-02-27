FROM mono:5.18.0.225


RUN  apt-get update && apt-get install -y nginx mono-fastcgi-server4 \
  && apt-get autoremove -y && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/*

RUN update-rc.d nginx defaults

RUN mkdir /app
COPY nginx.conf /etc/nginx/nginx.conf
COPY . /app

EXPOSE 80

STOPSIGNAL SIGTERM

# CMD ["nginx", "-g", "daemon off;"]
CMD ["fastcgi-mono-server4", "/applications=/:/app", "/socket=tcp:127.0.0.1:9000"]
