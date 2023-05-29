FROM nodered/node-red
#RUN npm install <any needed node-red packaged node for your flows from npm>
#move arbitrary flow from local dir
COPY common_functions.json /data/flows.json
#optional: add a specific settings.js file
#COPY settings.js /data/settings.js
#optional: add a specific flows_cred.js file with credentials. If used then the #credentialSecret option should be set in the settings.js file during credential #creation in the development Node-RED server so that credentials are transferable #to the new image
#COPY flows_cred.json /data/flows_cred.json
ENV PORT 8080
EXPOSE 8080:8080
