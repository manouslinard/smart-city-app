FROM nodered/node-red

COPY common_functions.json /data/flows.json

# Install the 'clusters' package and save it as a dependency
RUN npm install clusters --save

# Copy the settings.js file
COPY ./settings.js /data/settings.js

ENV PORT 8080
EXPOSE 8080:8080

CMD ["npm", "start", "--", "--userDir", "/data"]


