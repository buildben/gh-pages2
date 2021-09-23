---
layout: default
title: Installation
---

# Buildben Trial Version EKS Cluster Installation

**1.** Login to ec2 instance with executor admin user

**2.** Run the following command to create Amazon EKS cluster:

```eksctl create cluster --name=buildben-eks --instance-types=m5.large --nodes-min=3 --nodes-max=3```

The command will create an EKS cluster named **buildben-eks** in the default `eu-central-1` region with 3 nodes of `m5.large` type.
The process can take up to 15 mins.

**3.** After the cluster creation was completed run the following command to label the created nodes to be used in Buildben agents management process

`ITER=1; for i in $(kubectl get nodes --no-headers | awk '{printf "%s ",}'); do kubectl label nodes "$i" number=$ITER; ((ITER++)); done`

**4.** Run the following command to create a `dev` namespace

`kubectl create namespace dev`

**5.** Download Buildben helm chart

  **5.1** Create directory to store Buildben helm chart

  `mkdir ~/buildben`

  **5.2** Change to new directory

  `cd ~/buildben`

  **5.3** Pull the latest version of Buildben helm chart

  `helm pull https://buildben.github.io/trials/buildben-0.0.1.tgz`

  **5.4** Unarchive the helm chart files

  `tar -xvf buildben-0.0.1.tgz`

**6.** From the same directory, run the following command to install BuildBen helm chart

`helm upgrade --install -n dev buildben -f values.yaml .`
  
Even if the command is completed; the actual process can take several minutes until all the services are up and running.

**7.** Validate the process completion by the following command

`kubectl -n dev get pods`

  The expected output example: 


  All pods are in **RUNNING** status.

**8.** Run the following command to get the Buildben backend link

`kubectl get svc -n dev | grep buildben-load-balancer | awk '{printf "http://%s:8080",}'`

The expected output example:

`axxxxx531ff9a194erggfg4566-4556677.eu-central-1.elb.amazonaws.com:8080`

**Copy the printed link for future use.**

**9.** Run the following command to get the Buildben MinIO link

`kubectl get svc -n dev | grep 'buildben-minio ' | awk '{printf "http://%s:9000",}'`

The expected output example:

`44hfmdm123412csdfsdfsds-0090901.eu-central-1.elb.amazonaws.com:9000`

**Copy the printed link for future use.**
