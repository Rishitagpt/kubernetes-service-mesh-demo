# Custom Service Mesh on Kubernetes

This project demonstrates a manual implementation of a **Service Mesh** architecture using **Envoy Proxy** sidecars on Kubernetes. It evolves from a standard microservices setup to a fully observed mesh with traffic splitting and fault injection capabilities.

## 🚀 Architecture
- **Microservices:** Frontend (Node.js), Backend (Go), Data Service.
- **Infrastructure:** Kubernetes (Kind/Minikube).
- **Service Mesh:** Envoy Proxy injected as sidecar containers.
- **Observability:** Prometheus & Grafana.

## 🛠️ Key Implementations

### 1. Sidecar Pattern (Service Mesh)
- Manually injected `envoy` containers into Pods.
- Configured traffic interception (`Service -> Envoy -> App`).
- Enabled deep observability (Request rates, Latency, Success %) in Grafana.

### 2. Canary Deployments
- Implemented **Traffic Splitting** using Envoy.
- **90%** traffic routed to Stable (V1).
- **10%** traffic routed to Experimental (V2).
- Verified using load testing scripts.

### 3. Chaos Engineering (Fault Injection)
- Injected artificial failures using Envoy Fault Filters.
- Simulated **50% HTTP 503 Errors** to test frontend resilience.

### 4. Resource Management
- Defined CPU and Memory requests/limits for all containers to ensure cluster stability.

## 📂 Project Structure
- `k8s/configs/pinger-sidecar.yaml`: Full Service Mesh configuration.
- `k8s/configs/frontend-canary.yaml`: Configuration for 90/10 traffic splitting.
- `k8s/configs/frontend-fault.yaml`: Fault injection configuration.

## 💻 How to Run
1. Apply the mesh: `kubectl apply -f k8s/configs/pinger-sidecar.yaml`
2. Apply canary split: `kubectl apply -f k8s/configs/frontend-canary.yaml`
3. Generate load: `powershell scripts/load_test.ps1`