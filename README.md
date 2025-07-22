
# 🚀 Nginx Pod with Liveness Probe on Minikube

This project demonstrates how to deploy an Nginx pod in a Minikube Kubernetes cluster with a configured **livenessProbe** to automatically restart the container if it becomes unhealthy.

---

## 📁 Project Structure

```
nginx-liveness/
├── nginx-liveness.yaml   # Kubernetes pod definition with livenessProbe
└── README.md             # Project documentation
```

---

## 🛠️ Prerequisites

- ✅ Minikube installed and running
- ✅ kubectl configured for Minikube

Start Minikube if it’s not already running:
```bash
minikube start
```

---

## 🧾 Step-by-Step Instructions

### 📄 1. Create the YAML file

Create a file named `nginx-liveness.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-liveness
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 10
      periodSeconds: 5
```

---

### 🚀 2. Apply the configuration

Deploy the pod to Minikube:

```bash
kubectl apply -f nginx-liveness.yaml
```

---

### 📋 3. Verify pod and probe

Check the pod status:
```bash
kubectl get pods
```

Describe the pod to view probe details:
```bash
kubectl describe pod nginx-liveness
```

---

## 🔍 Test Liveness Probe (Optional)

Simulate a failure to test if Kubernetes restarts the pod:

```bash
kubectl exec -it nginx-liveness -- /bin/bash
rm -rf /usr/share/nginx/html/index.html
exit
```

Now watch for container restarts:
```bash
kubectl get pods
```

You should see `RESTARTS` count increase.

---

## 📸 Screenshots

> Place your screenshots in the root of your repo and update the paths below.


![Liveness Output](./liveness-restart-screenshot.jpg)

---

## 🧹 Cleanup

To remove the pod:
```bash
kubectl delete pod nginx-liveness
```

---

## 📦 Author

**Your Name**  
[GitHub Profile](https://github.com/yourusername)

---

## 🏷️ Tags

`#kubernetes` `#nginx` `#minikube` `#devops` `#livenessprobe` `#yaml`
