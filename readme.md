# This project is a demo of containerizing and deploying a two-tier app.
I containerized all the app's logic to run inside containers, then served
the app from an nginx server - making it a 3-tier app.

> For more info on the logic of this project, visit the original project's [github page](https://github.com/prakhar1989/FoodTrucks). 

## howto:
To run this project, make sure you have the latest docker and docker-compose versions.
Clone the project, cd into the main directory, then run the following command:

> docker-compose up -d  
> curl localhost:8080 # or in your browser, visit localhost:8080

## The three parts of the project:

### server: 
an nginx server which serves the static files (html, style sheets, images,..). if a static file is not found,
a 404-not found page is served.  
Fhe static files were compiled from a reactjs app, then moved inside the nginx file system.  
For anything not static, the server acts as a reverse proxy, proxying all requests to the flask-based backend service.

### backend: 
flask-based app which handles the following routes:
 - `/` returns the index.html file (not really used, since the endpoint is covered on the server side - reducing latency and overhead from the backend).
 - `/search` initiates a query with the passed parameters, to the database to fetch the relevant data, if any.
 - `/debug` validates the database is functioning.
 
 ### es: 
 An elastic search database. if this is a frech instance, the backend service compiles the relevant data and builds the index inside the db.