# Udacity Udagram Microservice

Cloud microservice project deployed on kubernetes.

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:

1. [The Simple Frontend](/udacity-c3-frontend) A basic Ionic client web application which consumes the RestAPI Backend.
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

## Links

- Docker hub images found [here](https://hub.docker.com/u/chedburgh)
- Screenshots are documented and found in the [screenshots](screenshots) directory

## Getting Setup

> _tip_: this frontend is designed to work with the RestAPI backends). It is recommended you stand up the backend first, test using Postman, and then the frontend should integrate.

### Installing Node and NPM

This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli

The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:

```bash
npm install
```

> _tip_: **npm i** is shorthand for **npm install**

### Setup Backend Node Environment

You'll need to create a new node server. Open a new terminal within the project directory and run:

1. Initialize a new project: `npm init`
2. Install express: `npm i express --save`
3. Install typescript dependencies: `npm i ts-node-dev tslint typescript @types/bluebird @types/express @types/node --save-dev`
4. Look at the `package.json` file from the RestAPI repo and copy the `scripts` block into the auto-generated `package.json` in this project. This will allow you to use shorthand commands like `npm run dev`

### Configure The Backend Endpoint

Ionic uses enviornment files located in `./src/enviornments/enviornment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `enviornment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

---

### Running the Development Server

Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files

Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:

```bash
ionic build
```

---

### Docker Build

As follows:

```bash
cd udacity-c3-deployment/docker
docker-compose -f docker-compose-build.yaml build --paralell
```

To push images:

```bash
docker-compose -f docker-compose-build.yaml push
```

## Deployment

### Cloud Deployment

Create the aws cluster:

```bash
cd /udacity-c3-deployment/eks
eksctl create cluster -f udagram-cluster.yaml --kubeconfig=./udagram-config.yaml
```

The cluster can be destroyed by:

```bash
cd /udacity-c3-deployment/eks
eksctl delete cluster -f udagram-config.yaml
```





eksctl create cluster \
--name "Udagram" \
--version 1.14 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto \
--kubeconfig=./Udagram.yaml

### Local Deployment

The project can be deployed and tested locally using the docker-compose file under /udacity-c3-deployment/docker as follows:

Set the variables in the /udacity-c3-deployment/docker/.env file. These are:

```
POSTGRESS_USERNAME=
POSTGRESS_PASSWORD=
POSTGRESS_DB=
POSTGRESS_HOST=
AWS_REGION=
AWS_PROFILE=
AWS_BUCKET=
JWT_SECRET=
```

Now run the system:

```bash
cd /udacity-c3-deployment/docker/
docker-compose up -d
```

Open localhost:8100 in a browser to check the docker deployment.




export POSTGRESS_USERNAME=udagramjamesdev
export POSTGRESS_PASSWORD=iliketoeatpies
export POSTGRESS_DB=udagramjamesdev
export POSTGRESS_HOST=udagramjamesdev.cbxnlirhetmb.eu-west-1.rds.amazonaws.com
export AWS_REGION=eu-west-1
export AWS_PROFILE=udagram
export AWS_BUCKET=udagram-file-store

eksctl create cluster \
--name "Udagram" \
--version 1.14 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto \
--kubeconfig=./Udagram.yaml

919 curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube
920 sudo install minikube /usr/local/bin/
sudo apt install conntrack socat
sudo minikube start --vm-driver=none
sudo kubectl config use-context minikube

sudo kubectl apply -f aws-secret.yaml
sudo kubectl apply -f env-secret.yaml
sudo kubectl apply -f env-configmap.yaml
sudo kubectl apply -f .
sudo kubectl get pod

minikube start --vm-driver=none
kubectl config use-context minikube
kubectl --kubeconfig=./Udagram.yaml apply -f aws-secret.yaml
kubectl --kubeconfig=./Udagram.yaml apply -f env-secret.yaml
kubectl --kubeconfig=./Udagram.yaml apply -f env-configmap.yaml
kubectl --kubeconfig=./Udagram.yaml apply -f .
kubectl --kubeconfig=./Udagram.yaml get pod
