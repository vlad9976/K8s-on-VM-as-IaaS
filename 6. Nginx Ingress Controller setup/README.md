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
Lets create an Ingress:

```sh
# ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress-example
  namespace: ingress-nginx
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: www.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: hello-server
                port:
                  number: 80

```

Lets create a Service:

```sh
#service.yaml

apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: hello-server
  name: hello-server
  namespace: ingress-nginx
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: hello-server
  type: LoadBalancer
status:
  loadBalancer: {}

```

Map in your /etc/hosts file the domain we choose "www.example.com" to LoadBalancer IP

<img src="./images/Screenshot_6.png" width="600" height="20">

# Test Ingress.

```sh
curl www.exaple.com
```

Output:

<img src="./images/Screenshot_7.png" width="500" height="100">

```sh
for i in {1..5}; do curl www.example.com; done
```

Output:

<img src="./images/Screenshot_8.png" width="500" height="100">
