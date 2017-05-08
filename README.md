tagger-kubernetes
====
`Kubernetes .yml files for the tagger cluster`
# Overview
This repository contains all files required to boot the tagger cluster (except for Kafka, which can be deployed using [these .yml files](https://github.com/Yolean/kubernetes-kafka)).

Here is a description of the Kubernetes Object that are defined in this repository (in the order they get created):
* a `tagger` namespace, where everything will live
* `tagger-secrets`, a secrets object used by the backend containing authentification to azure blob storage and a secret used for JWT signing
* `testsites-info-secrets`, which contains the `fullchain.pem` and `privkey.pem` for [gruppe7.testsites.info](https://gruppe7.testsites.info).
* `postgres-deploy`, which deploys postgresql into the cluster
* `postgres-service`, which makes the postgres deployment addressable by the cluster
* `tagger-backend-deploy`, which deploys the [tagger backend](https://github.com/SwaggerTagger/octo-tagger-backend) into the cluster.
* `tagger-backend-service`, which makes the service addressable by the cluster
* `tagger-worker-deploy`, which deploys the worker into the cluster
* `frontend-deploy`, which deploys the [tagger-frontend](https://github.com/SwaggerTagger/octo-tagger-frontend) into the cluster
* `frontend-expose`, which installs a load balancer in front of the frontend deployment and serves as an entry point to the outside world.

Additionally, the following helper objects are defined:
* `get-certs`, a deployment of a letsencrypt docker image that can be used to generate certificates.
* `kafka-manager-deploy`, which is used to deploy an instance of kafka-manager into the cluster.

## Deployment
In order to deploy the tagger into your own kubernetes cluster, do the following:
* Deploy [Kafka](https://github.com/Yolean/kubernetes-kafka) into your cluster
* `git clone https://github.com/SwaggerTagger/tagger-kubernetes && cd tagger-kubernetes`
* `kubectl create -f .`
