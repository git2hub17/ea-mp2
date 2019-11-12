# Enterprise Architecture --> Mini Project2 - eCommerce

# Design decisions:
First of all, the project was developed with spring-boot 
and deployed with Google Kubernetes Engine.

We chose Google K8s Engine because 
 - Google Kubernetes Engine (GKE) is a managed, 
 production-ready environment for deploying containerized applications.
    Deploying on Google Cloud manages Spaces for us. Minikube is heavy on local systems.
    
 - Kubernetes Engine enables rapid application development and iteration by making it easy to deploy,
  update, and manage your applications and services.
  
 - Go from a single machine to thousands: Kubernetes Engine autoscaling 
  allows you to handle increased user demand for your services'

# Microservice Interactions: 

# Deployment 
       
The deployment has several steps:

#### Step 1
Open Google Cloud shell and
clone the source code from GitHub link:
 [GitHub](https://github.com/git2hub17/ea-eCommerce)

#### Step 2
Run following command:
```
$ cd Mini-Project-2/deployment
```
#### Step 3
Push all docker images for all microservices. It would 
compile source codes and push to Docker Hub, automatically.

```
$ make docker-push-all  
```

#### Step 4
Create static public IP address for gateway! If have problem 
you can use [this IP address](http://34.102.164.129/users/) after deploying all
services including ingress gateway.  
```
$ make apply-static-IP
```
#### Step 5
Deploy docker images to pods in Kubernetes cluster.
```
$ make kubectl-apply-all-services 
```
It should be apply all pods and services with secrets which
will be used to connect MySQL DB and running arguments for Spring 
Boot Rest Application (services).

#### Step 6
Wait for mysql service runnig and then execute following 
command to create schema databases for running Spring Boot App.
```
$ make kubectl-create-init-db:
```

#### Step 7
Apply for Ingress Proxy using following command.

```shell script
$ make kubectl-apply-ingress
```

#### Step last (checking services working)
The ingress proxy should be delayd for creating related mappings
for front end services. Check this status following command:
```shell script
$ kubectl get ingress

NAME          HOSTS   ADDRESS          PORTS   AGE
ea2-ingress   *       34.102.164.200   80      161m
```
Now we can open any web browsers or postman to check functionality
of our application.

- example: 
    - http://34.102.164.200/orders/ 
     
      --> can be point to our orders-service inside k8s

##### Thank you!



#Adding Account - Account Service
url: 
# format:
{
	"firstName": "Chinedu",
	"lastName": "Ugwu",
	"address": "No 1000N 4th Strret",
	"username": "eduurb42@gmail.com",
	"password": "chinedu",
	"defaultPaymentMethod": "credit",
	
	"paymentMethods" : [
			{
				"title":	"credit",
				"csv": "123",
				"creditNumber": "0033 4455 5554 4554",
				"phoneNumber": "000123444"
			},
			{
				"title":	"bank",
				"routingNumber": "1235544",
				"bankNumber": "00334554",
				"phoneNumber": "000123444"
			},
			{
				"title":	"paypal",
				"username": "eduurb42@gmail.com",
				"phoneNumber": "000123444"
			}
		]
}

# authenticating user
Url: 
# format:
{
  "username": "eduurb42@gmail.com",
  "password": "chinedu"
}

Students: EA-Mini-Project-2
Purevdemberel Byambatogtokh 986799
Chinedu Ugwu 
