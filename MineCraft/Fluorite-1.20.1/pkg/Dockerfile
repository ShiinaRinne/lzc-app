FROM openjdk:21-slim

RUN apt-get update && apt-get install -y curl && \
    curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g serve && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY statics/assets /app/statics/assets
COPY server /app/server

RUN mkdir -p /app/data

COPY statics/index.html /app/statics/index.html

EXPOSE 25565 3000

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["mkdir -p /app/data && \
      if [ ! -f /app/data/Fluorite-1.20.1-225413d-server.jar ]; then \
        cp -r /app/server/* /app/data/; \
      fi && \
      cd /app/data && \
      (java -jar Fluorite-1.20.1-225413d-server.jar &) && \
      serve -s /app/statics -l 3000"]