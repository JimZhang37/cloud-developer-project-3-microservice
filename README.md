# Microservice practice in cloud-developer udacity course
content for Udacity's cloud developer nanodegree
[![Build Status](https://travis-ci.com/JimZhang37/cloud-developer-project-3-microservice.svg?branch=04-k8s)](https://travis-ci.com/JimZhang37/cloud-developer-project-3-microservice)

In this new branch, I will try to bring new features of k8s to this code base. For example,
* DNS, loadbalance, CA from cloud provider
* DFx features, like monitor, logs, etc
* CICD with jenkins with a complete pipeline
* deployment strategies like blue/green, A/B test, 


# Table of Contents
* [General Info](#General-Info)
* [Tasks](#Tasks)
* [Getting Setup](#Getting-Setup)
* [Configuration](#Configuration)
* [Verification Testing](#Verification-Testing)
* [Features](#Features)

# General Info

This is the third task run the app in k8s. In previous tasks, I have built docker images with docker-compose in travis ci and push these images to to dockerhub in travis ci. I was able to run command `docker-compose up` in my local pc to launch the app.

In this task, I successfully run all microservices in a k8s cluster created at by AWS EKS. For the sake of testing, I created a new user and the frontend displayed images from AWS S3 bucket. Clearly, configuremap and secret are properperly set. 

* By debugging the problem, I used `kubectl logs pod-name` command to fetch logs from pods. I found that one of my configuremap parameter, database's dialogue, is forgotten and services couldn't run because of this reason. 
* How to specify an IP to a service. Currently I use `kubectl port-forwarding service/*`, which mapping a remote service in a cluster to my localhost.

Remaining tasks:
* How to apply service mesh to this project for A/B test.
* container logs to STDOUT and configue cloud watch log.

Completed:
* I run a cluster in AWS EKS. Once I delete this cluster, can I delete local kubectl's configuration to this cluster. (If I use `eksctl delete cluster`, kubeconfig will be updated.)
* How to quickly run all service in a cluster. Currently, I will run commands `kubectl apply -f *` several times to a few files from secrets, deployments to services. (Create a Makefile to automate this task.)
# Tasks
## Task 1: 
```
1 For simplicity we use a single repo
2 Create a new folder for feed service
3 Copy the backend service into the the new folders repo
4 Remove the feed part from the user service
5 Remove and adjust the user part from the feed service; The Authorizer is needed!
6 Start all service locally. Two backend services share one port, so they can't run together. This issue will be addressed in the next task.
```
## Task 2: Docker
```
1 Create a Dockerfile for all the services
2 Create a ngnix proxy as Dockerfile
3 Build the images. When you push a new commit to Github, Travis CI will automatically build your docker images and push them to docker hub for you. Aternatively, you can build all images together with `docker-compose -f course-03/exercises/udacity-c3-deployment/docker/docker-compose-build.yaml build --parallel`, or you can build each image separately with `docker build -t zhangyhgg/udacity-restapi-feed .`
4 Run the images as container `docker run --publish 8080:8080 --name feed zhangyhgg/udacity-restapi-feed`
5 Use docker-compose to deploy the completed application `docker-compose up` in the folder where file `docker-compose.yaml` is located.
```
In docker-compose's yaml file, parameters from environment are read from local enviornment. Please make sure you have all the values in `~/.bash_profile` or specify all values in the yaml file.

## Task 3: K8s
```
1 Create your first kubernetes cluster on AWS with KubeOne https://github.com/kubermatic/kubeone/blob/master/docs/quickstart-aws.md
2 Create a pod for the feed service. kubectl apply -f pod.yaml
3 Convert the pod into a deployment. kubectl apply -f *deployment.ymal.
4 Write deployment for images
```
## Task 4: Service Config
```
1 Create configmaps and secrets for your application. It's used to provide configurations, like database id, aws credentials, etc. 
2 Create kubernetes service for the deployments. Service is used for service discovery when two or more instance from the same type is running. 
3 Expose the application locally (check kubectl port-forward). Therefore, if you type http://localhost:8100, your traffic will be forwarded to frontend service inside k8s.
4 Scale your application. You are able to scale each service independently when you specify the replicas number. 
```

```

k port-forward service/reverseproxy 8080:8080
kubectl scale deployment/user --replicas=10
```

## Task 5: CI
```
1 Connect TravisCI with you Github repository
2 Add a .travis.yml to you repo
3 Build the container with TRavis. In .travis.yml file, the docker-compose build command is specified.
```


# Getting Setup

* Node and NPM
* Ionic CLI
* Python3 and PIP
* AWS account
* AWS CLI
* Postbird
* Postman
* Microsoft Code

### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from https://nodejs.com/en/download.

Node (aka NodeJs) is a powerful framework to build network applications using JavaScript (in our case using TypeScript) outside of browsers. It has an asynchronous concurrent model which releases the developer from many concerns involving threading and dead-locking. Node is used as our server framework along with Express to handle web http requests and responses.

#### Introduction to TypeScript
Typescript is a flavor of JavaScript that forces hard typing on variables and methods. This prevents implementation errors like passing a string instead of a number. It compiles to pure JavaScript.

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the Ionic Framework Docs.

### Installing Python3
Python is a powerful programming language used for anything from quick scripts through data science. We'll use Python for the final project and it is required for some development tools like the AWS CLI. Instructions to download and install Python for your OS can be found here: https://www.python.org/downloads/

### Amazon Web Services (AWS)
#### Account Setup
We'll be provisioning cloud resources throughout the next few lessons. You'll need an AWS account to set up these resources. We'll be taking advantage of the free tier offerings so there should be no costs to set up the resources we'll be using. Create a new account here: https://portal.aws.amazon.com/billing/signup#/

#### AWS CLI
We'll interface with AWS using the Command Line Interface (CLI). Instructions to download and install the AWS CLI for your OS can be found here: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html

### Installing useful tools
#### Postbird
Postbird is a useful client GUI (graphical user interface) to interact with our provisioned Postgres database. We can establish a remote connection and complete actions like viewing data and changing the schema (tables, columns, ect).

#### Postman
Postman is a useful tool to issue and save requests. Postman can create GET, PUT, POST, etc. requests complete with bodies. It can also be used to test endpoints automatically. We've included a collection in the starter code repository (./udacity-c2-restapi.postman_collection.json) which contains example requests.

# Configuration
### Installing project dependencies
Both backend and frontend use NPM to manage software dependencies. NPM Relies on the package.json file located in the roots of backend and frontend folders. After cloning, open your terminal in each folder run:

```
npm install
```
tip: npm i is shorthand for npm install

### Place to store secrets

Secrets are stored in a local terminal profile, for example `~/.bash_profile`. You must write the following variables in your terminal profile. 

```
export POSTGRESS_USERNAME=1
export POSTGRESS_PASSWORD=2
export POSTGRESS_DB=3
export POSTGRESS_HOST=4
export dialect=postgres
export AWS_REGION=6
export AWS_PROFILE=7
export AWS_BUCKET=8
export JWT_SECRET=9
```
I don't have `~/.profile` in my Mac, so I use `~/.bash_profile`.[about ~/.profile and ~/.bash_profile](https://unix.stackexchange.com/questions/83742/what-is-the-difference-between-profile-and-bash-profile-and-why-dont-i-have-a)

### Configure Database(AWS:RDS)
In your chosen AWS region, you can create a postgres db instance. You can use postbird to connect to this db instance once its status is running. I find that its database name is not the value I specified in the console. It is named `template1` in my case. Once its connection is ready, you can put it down in a local file when you run your backend in your local computer.

In `/udacity/src/sequelize.ts`, we use these parameters to instantiate a connection with a database.

```
// Instantiate new Sequelize instance!
export const sequelize = new Sequelize({
  "username": c.username,
  "password": c.password,
  "database": c.database,
  "host":     c.host,

  dialect: 'postgres',
  storage: ':memory:',
});
```
### Configure File Storage(AWS:S3)
You need to create a S3 bucket.
* encryption, server-side encryption with s3 managed key
* permission, don't give public access as this is a bucket used for application
* CORS policy, please copy `udacity-c3-restapi/s3_cors.xml` when you specify CORS in your bucket

You also need to create a new S3 bucket and save its bucket address in the `~/.bash_profile`.

In `/udacity-c3-restapi/src/aws.ts`, we establish a connection with AWS S3 bucket.

```
const c = config.dev;

//Configure AWS
var credentials = new AWS.SharedIniFileCredentials({profile: 'default'});
AWS.config.credentials = credentials;

export const s3 = new AWS.S3({
  signatureVersion: 'v4',
  region: c.aws_reigion,
  params: {Bucket: c.aws_media_bucket}
});
```

Your AWS credentials are stored in `~/.aws/credentials` and `~/.aws/config`. You can use editor or `aws configure` to edit them. When you specify `default` for your `AWS_PROFILE` in `~/.bash_profile`, the corresponding value for AWS credentials will be fetched. You need to set up your AWS credential when you install AWS CLI.

After the application is deployed in cloud, AWS role will be used instead of user with programmatic access.
### Authentication
In `udacity-c3-restapi/src/controllers/v0/users/routes/auth.router.ts`, we use jwt secret to authorize users.

How do we get JWT secret?

```
function generateJWT(user: User): string {
    console.log("generateJWT")
    return jwt.sign(user.short(), c.config.jwt.secret)
}
```
### Configure udacity-c3-frontend
In this file, `/udacity-c3-frontend/src/environments/environment.ts`, you must specify the Host used for backend.

```
export const environment = {
  production: false,
  appName: 'Udagram',
  apiHost: 'http://localhost:8080/api/v0'
};
```

You also need to run `npm i` and ``(if you didn't install ionic) in your frontend folder.

To run your frontend, you run the command:
```
ionic serve
```

[Install ionic](https://ionicframework.com/docs/cli)
### add new package with npm
```
npm i bcrypt --save
npm i --save-dev @type/bcrypt
```

# Verification Testing

### Unit Tests
Ensure our atomic functions and methods perform their tasks correctly or fail appropriately. We'll be playing with Mocha and Chai as our unit testing framework. We'll be covering the basics so checkout the docs!

### Integration Tests
Integration Tests ensure every endpoint in our software package perform their tasks correctly, fails appropriately, and communicates with other systems in a predictable manner (so they integrate properly). We'll be playing with Postman as our integration testing framework. We'll be covering the basics so checkout the docs!

#### Running Mocha and Chai Tests
The command npm test is used to run all files that match the pattern *.tests.ts and is defined in package.json.

No tests definded here.
```
npm test
```

### Using Postman to Define Integration Tests


#### Choosing a Postman Environment
We've included a postman configuration file in the example repo. *.postman_collection.js. This can be imported into your local Postman.

When Gabe is showing how to run all integration tests at once in Postman, and says "we can choose our environment", he is selecting the "udacity-c2-basic-server" folder.

## Run Docker
you need to specify environment variables in docker run when you want to run a single docker image for backend. If you use docker composer, the environment variables are specified in the yml file. 
# Features

### To do: