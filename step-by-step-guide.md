# Step-by-Step Guide: Minikube and Snyk Security Testing

This guide walks through the process of deploying applications to Minikube and scanning them for vulnerabilities using Snyk.

## 1. Start Minikube

First, we need to start our Minikube cluster:

```bash
minikube start
```

## 2. Install Snyk CLI

Install the Snyk CLI tool using Homebrew:

```bash
brew install snyk-cli
```

## 3. Authenticate with Snyk

Authenticate with your Snyk account:

```bash
snyk auth
```

Follow the browser-based authentication flow to complete the process.

## 4. Deploy Basic NGINX Application

Create a basic NGINX deployment file (`nginx-deployment.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
  type: NodePort
```

Deploy it to Minikube:

```bash
kubectl apply -f nginx-deployment.yaml
```

## 5. Scan for Vulnerabilities

Scan the Kubernetes manifest for security issues:

```bash
snyk iac test nginx-deployment.yaml
```

Scan the container image for vulnerabilities:

```bash
snyk container test nginx:1.14.2
```

## 6. Deploy Secure NGINX Application

Create an improved NGINX deployment file (`secure-nginx-deployment.yaml`) with security enhancements:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: secure-nginx-deployment
  labels:
    app: secure-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: secure-nginx
  template:
    metadata:
      labels:
        app: secure-nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.28.0-alpine  # Using a more secure Alpine-based image
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: "0.5"
            memory: "256Mi"
          requests:
            cpu: "0.2"
            memory: "128Mi"
        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 30
          periodSeconds: 30
        imagePullPolicy: Always
---
apiVersion: v1
kind: Service
metadata:
  name: secure-nginx-service
spec:
  selector:
    app: secure-nginx
  ports:
  - port: 80
    targetPort: 80
  type: NodePort
```

Deploy it to Minikube:

```bash
kubectl apply -f secure-nginx-deployment.yaml
```

## 7. Scan Secure Deployment

Scan the improved Kubernetes manifest:

```bash
snyk iac test secure-nginx-deployment.yaml
```

Scan the improved container image:

```bash
snyk container test nginx:1.28.0-alpine
```

## 8. Access the Application

Get the URL to access your NGINX service:

```bash
minikube service secure-nginx-service --url
```

## 9. Fully Secure Deployment (Optional)

For a fully secure deployment, implement all Snyk recommendations:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: fully-secure-nginx-deployment
  labels:
    app: fully-secure-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: fully-secure-nginx
  template:
    metadata:
      labels:
        app: fully-secure-nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.28.0-alpine  # Using a more secure Alpine-based image
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: "0.5"
            memory: "256Mi"
          requests:
            cpu: "0.2"
            memory: "128Mi"
        securityContext:
          runAsNonRoot: true
          runAsUser: 10000
          allowPrivilegeEscalation: false
          readOnlyRootFilesystem: true
          capabilities:
            drop:
            - ALL
        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 30
          periodSeconds: 30
        imagePullPolicy: Always
        volumeMounts:
        - name: tmp-volume
          mountPath: /tmp
        - name: var-run-volume
          mountPath: /var/run
        - name: nginx-cache
          mountPath: /var/cache/nginx
        - name: nginx-conf
          mountPath: /etc/nginx/conf.d
      volumes:
      - name: tmp-volume
        emptyDir: {}
      - name: var-run-volume
        emptyDir: {}
      - name: nginx-cache
        emptyDir: {}
      - name: nginx-conf
        emptyDir: {}
```

## 10. Clean Up

When you're done, you can delete the deployments:

```bash
kubectl delete -f nginx-deployment.yaml
kubectl delete -f secure-nginx-deployment.yaml
```

And stop Minikube:

```bash
minikube stop
```
