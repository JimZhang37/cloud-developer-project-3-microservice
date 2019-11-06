# Microservice practice in cloud-developer udacity course
content for Udacity's cloud developer nanodegree

## Table of Contents
* [General Info](#General-Info)
* [Getting Setup](#Getting-Setup)
* [Configuration](#Configuration)
* [Verification Testing](#Verification-Testing)
* [Features](#Features)

## General Info


## Getting Setup

* Node and NPM
* Ionic CLI
* Python3 and PIP
* AWS account
* AWS CLI
* Postbird
* Postman

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

## Configuration
### Installing project dependencies
Both backend and frontend use NPM to manage software dependencies. NPM Relies on the package.json file located in the roots of backend and frontend folders. After cloning, open your terminal in each folder run:

```
npm install
```
tip: npm i is shorthand for npm install

### Configure Database(AWS:RDS)
Secrets about AWS RDS are stored in a local file, for example `~/.profile`
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
The problem is `~/.profile` can't be run when a terminal is open. Should I use `~/.bash_profile` or run command `source ~/.profile` after a terminal is opened?
[about ~/.profile and ~/.bash_profile](https://unix.stackexchange.com/questions/83742/what-is-the-difference-between-profile-and-bash-profile-and-why-dont-i-have-a)
### Configure File Storage(AWS:S3)

## Verification Testing

### Unit Tests
Ensure our atomic functions and methods perform their tasks correctly or fail appropriately. We'll be playing with Mocha and Chai as our unit testing framework. We'll be covering the basics so checkout the docs!

### Integration Tests
Integration Tests ensure every endpoint in our software package perform their tasks correctly, fails appropriately, and communicates with other systems in a predictable manner (so they integrate properly). We'll be playing with Postman as our integration testing framework. We'll be covering the basics so checkout the docs!

#### Running Mocha and Chai Tests
The command npm test is used to run all files that match the pattern *.tests.ts and is defined in package.json.

### Using Postman to Define Integration Tests


#### Choosing a Postman Environment
We've included a postman configuration file in the example repo. *.postman_collection.js. This can be imported into your local Postman.

When Gabe is showing how to run all integration tests at once in Postman, and says "we can choose our environment", he is selecting the "udacity-c2-basic-server" folder.

## Features

### To do: