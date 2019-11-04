# Jenkins in Kubernetes
This repository has a `Dockerfile` and a `helm` chart for setting up a simple Jenkins master for running in Kubernetes.

This Jenkins has the required tools to work in and with Kubernetes
- Jenkins application with pre-loaded plugins (see [plugins.txt](plugins.txt))
- Skipped setup wizard
  - You can control admin user and password with `--set adminUser=${USER},adminPassword=${PASSWORD}`
  - You can add and remove plugins by editing the [plugins.txt](plugins.txt) file


### Get the example Docker image
You can pull an already built version of this Jenkins image from [bintray.com](https://bintray.com).
```bash
# Pull the image
$ docker pull anuphnu/jenkins:v0.0.2
```

### Build the Jenkins Docker image
You can build the image yourself
```bash

# Build the image
$ docker build -t anuphnu/jenkins:v0.0.1 .

# Push the image
$ docker push anuphnu/jenkins:v0.0.1
```

### Deploy Jenkins helm chart to Kubernetes
```bash
# Init helm and tiller on your cluster
$ helm init
$ kubectl apply -f rbac-config.yaml

# Deploy the Jenkins helm chart
# (same command for install and upgrade)
$ helm upgrade --install jenkins ./helm/jenkins-k8s
```

### Data persistence
By default, in Kubernetes, the Jenkins deployment uses a persistent volume claim that is mounted to `/var/jenkins_home`.
This assures your data is saved across crashes, restarts and upgrades.   

