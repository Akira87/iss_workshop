# 1. Set the dependencies or software required for the program
FROM node:latest

# 2. Set environment variables
ENV APP_ROOT="db"
ENV DB_HOST="localhost"
ENV DB_PORT=3306
ENV DB_USER="root"
ENV DB_PASSWORD="changeit"
#ENV INSTANCE_IP_ADDRESS="172.17.0.2"
ENV APP_RETRIES=3
ENV APP_RETRY_INTERVAL=30
ENV APP_PORT=3000

# 3. Create the directory and cd into it
WORKDIR ${APP_ROOT}

# 4. Copy files in the image
# Files will be copied into /app
ADD main.js .
ADD package.json .
ADD config config
ADD public public
ADD views views

# 5. Run some commands
RUN npm install

# 6. Set what port our container will be exposing
# Default is TCP
EXPOSE ${APP_PORT}

# 7. Add health check to the application
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
    CMD curl -f http://localhost:${APP_PORT}/health > /dev/null || exit 1
    
# 8. Set the entry point or the command to run
ENTRYPOINT [ "node", "main.js" ]