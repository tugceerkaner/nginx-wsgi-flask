FROM nginx:latest
RUN apt-get update && apt-get install -y gettext
#WORKDIR /app
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /tmp/default.conf
RUN mkdir -p /app
COPY start.sh /app/start.sh
RUN chmod +x /app/start.sh
#RUN chown -R nginx:nginx /app/start.sh
#ENV FLASK_SERVER_ADDR=flask-app:8000
ENV FLASK_SERVER_ADDR=flask-app.app.svc.cluster.local:80
#CMD ["bash", "/app/start.sh"]
#CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT ["bin/bash", "/app/start.sh"]