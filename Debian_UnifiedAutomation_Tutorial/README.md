//Get the Unified Automation CPP Debian SDK and store it in the same folder as the Dockerfile with the name "uasdkcppbundle-bin-EVAL-debian7.tar.gz"
// https://www.unified-automation.com/products/server-sdk/c-ua-server-sdk.html

//Build it
docker build -t mydock . 

//The server is now running on port 4000
// Note the server allows anonymous login and supports only secure channel NONE!!! All your data are public available
docker run -p 4000:4841 --name myname -t mydock

//Get a public client, e.g., 
//https://www.unified-automation.com/de/downloads/opc-ua-clients.html
//Add Server within the advanced tab
//Endpoint Url: opc.tcp://XXXXXXXXXXXXXXXXXXXXXXXXXXXX:4000
//The server refuses the connection with securitymode sign or sign and encrypt. 
//After the failed connection try you have to copy the rejected certificate from the folder bin/PKI/rejected to the folder bin/PKI/signed


docker ps // here you get the id of the running job

//IMPORTANT: YOU HAVE TO STOP THE JOB BECAUSE IT IS PUBLIC AVAILABLE
docker stop [id]
