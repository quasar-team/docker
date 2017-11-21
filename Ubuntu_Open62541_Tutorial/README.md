NOTE: CURRENTLY Open62541 does not supports the opc ua security features! 

//Build it
docker build -t mydock . 

//The server is now running on port 4000
// Note the server allows anonymous login and supports only secure channel NONE!!! All your data are public available
docker run -p 4000:4841 --name dock5 -t mydock

//Get a public client, e.g., 
//https://www.unified-automation.com/de/downloads/opc-ua-clients.html
//Add Server within the advanced tab
//Endpoint Url: opc.tcp://virtual-factory-iem-fraunhofer.cs.upb.de:4000

docker ps // here you get the id of the running job

//IMPORTANT: YOU HAVE TO STOP THE JOB BECAUSE IT IS PUBLIC AVAILABLE
docker stop [id]
