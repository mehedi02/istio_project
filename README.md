# Deploy application in kubernetes cluster with istio

## prerequisites
* Setup Kubernetes cluster locally
You can use **minikube** or **DockerDesktop** Kubernetes cluster

* Run Jenkins in container using docker-compose
install docker-compose using [this doc](https://docs.docker.com/compose/install/)
clone [this repo](https://github.com/mehedi02/jenkins_docker-compose)
naviagte to clone folder and run ```docker-compose up```
and follow the repo `readme` file instruction to setup jenkins

## install istio on the cluster
Download `istio` from [this link](https://istio.io/latest/docs/setup/getting-started/#download)
follow `Download Istio` and `Install Istio` section
To install other addons like `kiali`, `Promethus`, `Grafana` follow `View the dashboard` section

After that clone this repo and navigate to `istio` folder and run ```kubectl apply -f .```

it will install `http-gate-way` and `virtual-service` for `ingress gateway`


## Deploy application using Jenkins CI/CD pipepline
In jenkins select `New Item` and select `pipeline` and give it a name and click ok

in new page go to `Pipeline` section at the end and in `Definition` select `Pipeline script from SCM` from drop down menu
In `SCM` section select `git` from drop down
In `Repository URL` give github url of this repo
In `Credentials` section select your github credentials from drop down. if you can't find the github credentials create it by clicking `Add` button.
While creating credentials for github, select `Username and Password` as kind
After that click Save

Now you will see `Build Now` option. if you select that it will automatically deploy the application to the local k8s cluster