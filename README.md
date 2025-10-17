
---

# k8s-Gateway-API-setup

This project demonstrates the setup and configuration of the **Kubernetes Gateway API** using the **NGINX Gateway Fabric** implementation.
It shows how to deploy the Gateway, create `Gateway` and `HTTPRoute` resources, and expose a frontend application through the new Gateway API model.

---

## 🧱 Project Structure

```bash
.
├── nginx-gateway.yaml              # Defines the Gateway resource
├── httproute-frontend-app.yaml     # Defines HTTPRoute for frontend-app service
└── README.md                       # Documentation
```

---

## ⚙️ Setup Steps

1. **Install Gateway API CRDs**

   ```bash
   kubectl kustomize "https://github.com/nginx/nginx-gateway-fabric/config/crd/gateway-api/standard?ref=v1.5.1" | kubectl apply -f -
   ```

2. **Deploy the NGINX Gateway Fabric**

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/nginx/nginx-gateway-fabric/v1.6.1/deploy/crds.yaml
   kubectl apply -f https://raw.githubusercontent.com/nginx/nginx-gateway-fabric/v1.6.1/deploy/nodeport/deploy.yaml
   ```

3. **Verify Deployment**

   ```bash
   kubectl get all -A
   ```

   You should see the `nginx-gateway` deployment, service, and related CRDs created successfully:

   ```
   service/nginx-gateway NodePort 172.28.229.63  80:30880/TCP,443:30881/TCP
   ```

4. **Apply Gateway and Route Resources**

   ```bash
   kubectl apply -f nginx-gateway.yaml
   kubectl apply -f httproute-frontend-app.yaml
   ```

---

## 🌐 Access the Frontend

Once the Gateway and Route are active, you can access your frontend app through the node’s external IP and exposed NodePort:

```
http://<NodeIP>:30880
```

---

## 🧩 Concepts Demonstrated

* **Gateway API CRDs:** New Kubernetes standard replacing Ingress for more flexible traffic control.
* **NGINX Gateway Fabric:** A production-grade implementation of the Gateway API.
* **HTTPRoute:** Fine-grained routing to backend services.
* **NodePort exposure:** For external access in environments without a LoadBalancer.

---

## 📘 References

* [Gateway API Documentation](https://gateway-api.sigs.k8s.io/)
* [NGINX Gateway Fabric on GitHub](https://github.com/nginx/nginx-gateway-fabric)

---

