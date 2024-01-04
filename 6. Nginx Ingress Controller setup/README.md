# Nginx Ingress Controller Setup

<img src="/img/icons8-nginx-accelerates-content-and-application-delivery-improves-security-96.png" width="180" height="180">

Let’s define a namespace named ingress-nginx where Deployment and Ingress Controller will work together

```sh
kubectl create namespace ingress-nginx
```
Let’s create a backend deployment

```sh
#deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-server-deployment
  namespace: ingress-nginx
spec:
  selector:
    matchLabels:
      app: hello-server
  replicas: 4
  template:
    metadata:
      labels:
        app: hello-server
    spec:
      containers:
        - name: hello-server
          image: gcr.io/google-samples/hello-app:1.0
          ports:
            - containerPort: 8080
```
