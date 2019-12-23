# Turbine
A Python 3 tool to harness the google cloud to run shell scripts. In particular, if you have
1. a docker image, and
2. many independent, idempotent tasks for that image written as shell scripts,

Turbine allows you to run those tasks on many VMs in parallel on GCE. Turbine is a lot like
* [Google Cloud Run](https://cloud.google.com/run/) except you don't need to hit an HTTP endpoint and it supports large machine types and accelerators;
* [Google Cloud Functions](https://cloud.google.com/functions/) except it supports large machine types and accelerators; and
* [Batch on GKE](https://cloud.google.com/kubernetes-engine/docs/how-to/batch/running-job) except I understand it, it is significantly lighter-weight than Kubernetes, and it provides a path for TPU access.

# Installation
Turbine consists of two components:
1. A controller on the local machine to setup cloud components, enter tasks, and provision VMs.
2. A small shim to run inside of the docker image and retrieve tasks.

For most users, the recommended method to install the controller is via pip:

```
pip install turbine
```

To attach turbine to a docker image, install turbine on the image via pip and set  the `ENTRYPOINT` of the docker image as below (see [this example Dockerfile](demo/Dockerfile)):
```
RUN pip install turbine

ENTRYPOINT ["python", "-c", "'import turbine; turbine.run()'"]
```


## Dependencies:
* google-cloud-pubsub
* google-cloud-storage
* google-cloud-logging
* google-api-python-client

See [requirements.txt](requirements.txt) for detailed version information, if needed.
