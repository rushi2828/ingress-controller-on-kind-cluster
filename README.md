# Ingress Controller on kind Cluster

This project demonstrates how to deploy and test an **NGINX Ingress Controller** on a **local Kubernetes kind cluster**, routing multiple services (`app1`, `app2`, `app3`) through a single ingress.

---

## 🧰 Prerequisites

- Docker
- kind
- kubectl

---

## 🚀 Steps

### 🧱 1. Create kind Cluster with Port Mapping

Create a `kind-config.yaml` with port mappings for HTTP (80) and HTTPS (443):

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    extraPortMappings:
      - containerPort: 80
        hostPort: 80
      - containerPort: 443
        hostPort: 443

```
---
Then create the cluster:
```bash
kind create cluster --config kind-config.yaml

```
<img width="1408" height="190" alt="image" src="https://github.com/user-attachments/assets/52818a72-3a4b-42a4-86f1-eeba1ccf6c78" />

---
## 🌐 2. Install NGINX Ingress Controller
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.1/deploy/static/provider/kind/deploy.yaml

```

<img width="1510" height="407" alt="image" src="https://github.com/user-attachments/assets/b8379629-f525-44be-9c0f-3bdbf595701b" />

---

## 🐳 3. Build, Tag, and Push Docker Images

<img width="1360" height="138" alt="image" src="https://github.com/user-attachments/assets/b0cbe70c-0b2c-4b2b-a363-02f6f47e92a6" />
<img width="1242" height="415" alt="image" src="https://github.com/user-attachments/assets/3698ab06-d34e-4d0c-b2f3-794964c863a1" />

---

## 🧾 4. Update `/etc/hosts`
Add the following entry to your **`/etc/hosts`** file:
```bash
127.0.0.1 demo.local

```

<img width="753" height="85" alt="image" src="https://github.com/user-attachments/assets/713f4ea5-bf97-40db-9fce-80b315b69921" />

---
## 📦 5. Deploy App Manifests

Deploy deployments and services for all apps (app1, app2, app3):

<img width="1310" height="460" alt="image" src="https://github.com/user-attachments/assets/d5caf62a-834d-4c21-a879-1a3cf2e58f89" />

---

## ⚙️ 6. Deploy Ingress Resource
`kubectl apply -f ./k8s/ingress.yaml`

<img width="1521" height="152" alt="image" src="https://github.com/user-attachments/assets/df3751e3-01fe-41bd-9b65-a41fda158248" />

---
## ✅ Verify
### 🔗 Access the services via Ingress:
`👉 http://demo.local/app1`

<img width="1900" height="957" alt="image" src="https://github.com/user-attachments/assets/26d4c6fd-501e-46bc-b013-0406ceb09a64" />

`👉 http://demo.local/app2`

<img width="1912" height="962" alt="image" src="https://github.com/user-attachments/assets/9e78fbac-e230-4ce5-afd2-a9ef5374dbae" />

`👉 http://demo.local/app3`

<img width="1907" height="963" alt="image" src="https://github.com/user-attachments/assets/6fd4f482-f042-4235-a987-b65ea49a0254" />

---
## 🧹 Cleanup

`kind delete cluster`

---






