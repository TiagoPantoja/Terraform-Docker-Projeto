FROM python:2.7.8

RUN apt-get update && \
    apt-get install -y nginx supervisor ruby ruby-dev && \
    gem install sass compass && \
    pip install uwsgi

COPY . /project
WORKDIR /project

RUN pip install -r requirements.txt

RUN \
  echo "daemon off;" >> /etc/nginx/nginx.conf \
  && rm /etc/nginx/sites-enabled/default \
  && ln -s /project/docker_config/nginx_app.conf /etc/nginx/sites-enabled/ \
  && ln -s /project/docker_config/supervisor_app.conf /etc/supervisor/conf.d/

EXPOSE 80 443
CMD ["supervisord", "-n"]