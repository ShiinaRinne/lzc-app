FROM openjdk:21-slim

RUN apt-get update
RUN apt-get install -y curl && \
    curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get install -y nodejs 

RUN npm install -g serve && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app
RUN mkdir -p /app/data

COPY statics/resources /app/statics/resources
COPY server /app/server

COPY statics/assets /app/statics/assets
COPY statics/index.html /app/statics/index.html

EXPOSE 25565 3000

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["mkdir -p /app/data && \
      if [ ! -f /app/data/run.sh ]; then \
        cp -r /app/server/* /app/data/; \
      fi && \
      cd /app/data && \
      chmod +x run.sh && \
      (serve -s /app/statics -l 3000 &) && \
      bash run.sh"]