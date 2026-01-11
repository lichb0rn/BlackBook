Source: [https://rutracker.org/forum/viewtopic.php?t=6234967](https://rutracker.org/forum/viewtopic.php?t=6234967)
  
  
###  **✅ **1. Introduction:   
    - [x] 	8. ~~Mistakes. We all make them..mp4~~  
    - [x] 	7. ~~Asking for help.mp4~~  
    - [x] 	6. ~~Installing Docker.mp4~~  
    - [x] 	5. ~~Installing Make.mp4~~  
    - [x] 	4. ~~Installing Visual Studio Code.mp4~~  
    - [x] 	3. ~~Installing Go.mp4~~  
    - [x] 	2. ~~About me.mp4~~  
    - [x] 	1. ~~Introduction.mp4~~  
  
###  **✅ **2. Building a simple front end and one Microservice:  
	1. ~~What we'll cover in this section.mp4~~  
	2. ~~Setting up the front end.mp4~~  
	3. ~~Reviewing the front end code.mp4~~  
	4. ~~Our first service the Broker.mp4~~  
	5. ~~Building a docker image for the Broker service.mp4~~  
	6. ~~Adding a button and JavaScript to the front end.mp4~~  
	7. ~~Creating some helper functions to deal with JSON and such.mp4~~  
	8. ~~Simplifying things with a Makefile (Mac & Linux).mp4~~  
	9. ~~Simplifying things with a Makefile (Windows).mp4~~  
  
  
###  **✅ **3. Building an Authentication Service:  
	1. ~~What we'll cover in this section.mp4~~  
	2. ~~Setting up a stub Authentication service.mp4~~  
	3. ~~Creating and connecting to Postgres from the Authentication service.mp4~~  
	5. ~~Updating our docker-compose.yml for Postgres and the Authentication service.mp4~~  
	6. ~~Populating the Postgres database.mp4~~  
	7. ~~Adding a route and handler to accept JSON.mp4~~  
	8. ~~Update the Broker for a standard JSON format, and conect to our Auth service.mp4~~  
	9. ~~Updating the front end to authenticate thorough the Broker and trying things out.mp4~~  
  
###   
  
###  **✅ **4. Building a Logger Service:  
- [x] 	11. Trying things out.mp4  
- [x] 	9. Update the front end to post to the logger, via the broker.mp4  
- [x] 	8. Adding a route and handler on the Broker to communicate with the logger service.mp4  
- [x] 	7. Add the logger-service to docker-compose.yml and the Makefile.mp4  
- [x] 	6. Adding MongoDB to our docker-compose.yml file.mp4  
- [x] 	5. Getting up routes, handlers, helpers, and a web server in our logger-service.mp4  
- [x] 	4. Finishing up the Logger data models.mp4  
- [x] 	3. Getting up the Logger data models.mp4  
- [x] 	2. Getting started with the Logger service.mp4  
- [x] 	1. What we'll cover in this section.mp4  
- [x] 	10. Add basic logging to the Authentication service.mp4  
  
###  **✅ **5. Building a Mail Service:  
- [x] 	10. A note about mail and security.mp4  
- [x] 	9. Updating the front end to send mail.mp4  
- [x] 	8. Modifying the Broker service to handle mail.mp4  
- [x] 	7. Solution to challenge.mp4  
- [x] 	6. Challenge Adding the Mail service to docker-compose.yml and the Makefile.mp4  
- [x] 	5. Building the routes, handlers, and email templates.mp4  
- [x] 	4. Building the logic to send email.mp4  
- [x] 	3. Setting up a stub Mail microservice.mp4  
- [x] 	2. Adding Mailhog to our docker-compose.yml.mp4  
- [x] 	1. What we'll cover in this section.mp4  
  
### ** ✅ **6. Building a Listener service AMQP with RabbitMQ:  
- [x] 	13. Trying things out.mp4  
- [x] 	12. Adding a new function in the Broker to log items via RabbitMQ.mp4  
- [x] 	11. Writing logic to Emit events to RabbitMQ.mp4  
- [x] 	10. Updating the broker to interact with RabbitMQ.mp4  
- [x] 	9. Creating a Docker image and updating the Makefile.mp4  
- [x] 	8. Change the RabbitMQ server URL to the Docker address.mp4  
- [x] 	7. Updating main.go to start the Listener function.mp4  
- [x] 	6. Adding a logEvent function to our Listener microservice.mp4  
- [x] 	5. Writing functions to interact with RabbitMQ.mp4  
- [x] 	4. Connecting to RabbitMQ.mp4  
- [x] 	3. Adding RabbitMQ to our docker-compose.yml.mp4  
- [x] 	2. Creating a stub Listener service.mp4  
- [x] 	1. What we'll cover in this section.mp4  
  
### ** ✅ **7. Communicating between services using Remote Procedure Calls (RPC):  
- [x] 	5. Trying things out.mp4  
- [x] 	4. Calling the Logger from the Broker using RPC.mp4  
- [x] 	3. Listening for RPC calls in the Logger microservice.mp4  
- [x] 	2. Setting up an RPC server in the Logger microservice.mp4  
- [x] 	1. What we'll cover in this section.mp4  
  
### ** ✅ **8. Speeding things up (potentially) with gRPC:  
- [x] 	9. Trying things out.mp4  
- [x] 	8. Updating the front end code.mp4  
- [x] 	7. Writing the client code.mp4  
- [x] 	6. Listening for gRPC connections in the Logger microservice.mp4  
- [x] 	5. Getting started with the gRPC server.mp4  
- [x] 	4. Generating the gRPC code from the command line.mp4  
- [x] 	3. Defining a Protocol for gRPC the .proto file.mp4  
- [x] 	2. Installing the necessary tools for gRPC.mp4  
- [x] 	1. What we'll cover in this section.mp4  
  
### 9. Deploying our Distributed App using Docker Swarm:  
- [ ] 	13. Modifying our hosts file to add a backend entry and bringing up our swarm.mp4  
- [ ] 	14. Challenge correcting the URL to the broker service in the front end.mp4  
- [ ] 	15. Solution to challenge.mp4  
- [ ] 	16. Updating Postgres to 14.2 - why monitoring is important!.mp4  
- [ ] 	17. Spinning up two new servers on Linode.mp4  
- [ ] 	18. Setting up a non-root account and putting a firewall in place..mp4  
- [ ] 	19. Installing Docker on the servers.mp4  
- [ ] 	20. Setting the hostname for our server.mp4  
- [ ] 	21. Adding DNS entries for our servers.mp4  
- [ ] 	22. Adding a DNS entry for the Broker service.mp4  
- [ ] 	23. Initializing a manager, and adding a worker.mp4  
- [ ] 	24. Updating our swarm.yml and Caddy dockerfile for production.mp4  
- [ ] 	25. Trying things out, and correcting some mistakes.mp4  
- [ ] 	26. Populating the remote database using an SSH tunnel.mp4  
- [ ] 	27. Enabling SSL certificates on the Caddy microservice.mp4  
- [x] 	12. Adding Caddy to the mix as a Proxy to our front end and the broker.mp4  
- [x] 	11. Adding the Front end to our swarm.yml deployment file.mp4  
- [x] 	10. Solution to the Challenge.mp4  
- [x] 7. Updating services.mp4  
- [x] 	9. Updating the Broker service, and creating a Dockerfile for the front end.mp4  
- [x] 	8. Stopping Docker swarm.mp4  
- [x] 	6. Scaling services.mp4  
- [x] 	5. Starting the front end and hitting our swarm.mp4  
- [x] 	4. Initalizing and starting Docker Swarm.mp4  
- [x] 	3. Creating a Docker swarm deployment file.mp4  
- [x] 	2. Building images for our microservices.mp4  
- [x] 	1. What we'll cover in this section.mp4  
  
### 10. Deploying our Distributed App to Kubernetes:  
- [ ] 	1. What we'll cover in this section.mp4  
- [ ] 	2. Installing minikube.mp4  
- [ ] 	3. Installing kubectl.mp4  
- [ ] 	4. Initializing a cluster.mp4  
- [ ] 	5. Bringing up the k8s dashboard.mp4  
- [ ] 	6. Creating a deployment file for Mongo.mp4  
- [ ] 	7. Creating a deployment file for RabbitMQ.mp4  
- [ ] 	8. Creating a deployment file for the Broker service.mp4  
- [ ] 	9. When things go wrong....mp4  
- [ ] 	10. Creating a deployment file for MailHog.mp4  
- [ ] 	11. Creating a deployment file for the Mail microservice.mp4  
- [ ] 	12. Creating a deployment file for the Logger service.mp4  
- [ ] 	13. Creating a deployment file for the Listener service.mp4  
- [ ] 	14. Running Postgres on the host machine, so we can connect to it from k8s.mp4  
- [ ] 	15. Creating a deployment file for the Authentication service.mp4  
- [ ] 	16. Trying things out by adding a LoadBalancer service.mp4  
- [ ] 	17. Creating a deployment file for the Front End microservice.mp4  
- [ ] 	18. Adding an nginx Ingress to our cluster.mp4  
- [ ] 	19. Trying out our Ingress.mp4  
- [ ] 	20. Scaling services.mp4  
- [ ] 	21. Updating services.mp4  
- [ ] 	22. Deploying to cloud services.mp4  
