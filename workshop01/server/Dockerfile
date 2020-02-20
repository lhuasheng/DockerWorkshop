## BUILD PHASE ###

# FROM node:13.8
FROM node:latest


# or ENV APP_PORT=3000 APP_ROOT=/app   MESSAGE='Something something'
ENV DB_PORT=3306
ENV DB_HOST=localhost
ENV DB_USER=root
ENV DB_PASSWORD=changeit
ENV APP_ROOT=/app
ENV APP_PORT=3000

# create APP_ROOT directory and cd inside
WORKDIR ${APP_ROOT}


#Copy files from local into${APP_DIR}
#ADD works for folders and HTTPS
#COPY only local, add does remote references
 ADD ./main.js .
 ADD ./package-lock.json .
 ADD ./package.json .
 # directories must give the name
 ADD public public
 ADD views views
 ADD config config

# if npm install successful run next command [ie echo in this case]
 RUN npm install && echo "all done"

 # RUN pip install -r requirements.txt

 # what port is the application using
 # udp need to EXPOSE ${APP_PORT}/tcp

### EXECUTE PHASE ##
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1 

 EXPOSE ${APP_PORT}

 # Entry point
 ENTRYPOINT ["node","main.js"]
 #CMD ['8080']   #this adds arguments
 # CMD ["${APP_PORT}"]