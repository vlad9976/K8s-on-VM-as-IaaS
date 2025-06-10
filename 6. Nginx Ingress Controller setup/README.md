# 🌐 NGINX Ingress Controller Setup

<img src="/img/icons8-nginx-accelerates-content-and-application-delivery-improves-security-96.png" width="60" height="60" />  
📘 [NGINX Ingress Docs](https://docs.nginx.com/nginx-ingress-controller/)

<img src="./images/0_DJNFUH_Bx-tKHZsj.png" width="580" height="650" />

---

## 🏗️ 1. Create Namespace

```bash
kubectl create namespace ingress-nginx
```

---

## 📦 2. Create Deployment

Create a file `deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-server-deployment
  namespace: ingress-nginx
spec:
  selector:
    matchLabels:
      app: hello-server
  replicas: 3
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

---

## 🌐 3. Create Ingress Rule

Create a file `ingress.yaml`:

```yaml
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

---

## 🔁 4. Create Service

Create a file `service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
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
```

---

## 🗺️ 5. Map Domain to LoadBalancer IP

Update `/etc/hosts`:

```plaintext
192.168.13.247   www.example.com
```

📸  
<img src="./images/Screenshot_6.png" width="600" height="20" />

---

## 🧪 6. Test Ingress Access

```bash
curl www.example.com
```

📸 Output:  
<img src="./images/Screenshot_7.png" width="500" height="100" />

💡 Load Balancer Demo:

```bash
for i in {1..5}; do curl www.example.com; done
```

📸 Output:  
<img src="./images/Screenshot_8.png" width="600" height="200" />

🎉 Watch requests cycle across all 3 pods!

---

## 🎉 Final Message

Congratulations! 🥳  
You’ve successfully:

- Created a Kubernetes Cluster 🧱  
- Deployed MetalLB ⚖️  
- Installed & Verified NGINX Ingress Controller 🌐

Happy Kubernetes-ing in your on-prem lab!

---

🔙 [< Back to Start](../)
