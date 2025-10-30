## Mini Microservices Blog App

A microservices-based blog application built with Node.js, React, Docker, Kubernetes, and Skaffold for seamless local development.

This project demonstrates how independent services like posts, comments, query, moderation, and event-bus interact through events and APIs, orchestrated by Kubernetes and reverse-proxied through Ingress NGINX.

## 🚀 Tech Stack

Node.js + Express.js → Backend microservices

React.js → Frontend client

Docker → Containerization

Kubernetes (K8s) → Container orchestration

Skaffold → Automated local builds & deployments

Ingress-NGINX → Routing & domain management

## 🏗️ Project Architecture

**BLOG-BOILERPLATE/**

├── client/         → React frontend

├── comments/       → Comments service

├── posts/          → Posts service

├── query/          → Query service

├── moderation/     → Moderation service

├── event-bus/      → Event bus for inter-service communication

├── infra/          → Kubernetes deployment & service configs

└── skaffold.yaml   → Skaffold config for automated builds & deploys

**⚙️ Prerequisites**

Before starting, ensure the following are installed:

🐳 Docker Desktop (with Kubernetes enabled)

🧩 kubectl — Kubernetes CLI

🏗️ Skaffold — Download and add to PATH

## 💻 Git

**🔧 Setup Instructions**

Clone the repository
   
`git clone https://github.com/InsideAmber/mini-microservice-app.git`

`cd mini-microservices-app`

Enable Kubernetes in Docker Desktop

Open Docker Desktop → Settings → Kubernetes → ✅ Enable Kubernetes

Wait until the status shows “Kubernetes is running”

**Start the app with Skaffold**

Run the following command in your project root:

`skaffold dev`


This will:

Build Docker images for all microservices.

Apply Kubernetes manifests from /infra.

Continuously watch for code changes and automatically redeploy services.

🌀 Live Reload:
When you modify a file in any service, Skaffold rebuilds and redeploys it automatically — your changes appear live within seconds.

**Configure local domain**

To route traffic through Ingress NGINX, you need to map posts.com to your local system.

Open this file as Administrator:

`C:\Windows\System32\drivers\etc\hosts`


Add the following line at the bottom:

`127.0.0.1 posts.com`


Save and close the file.

**Access the app**

Once Skaffold has finished deploying, open your browser and visit:

👉 `http://posts.com`

That’s the entry point served through Ingress NGINX, routing requests to your client service and internally connecting to other services like posts, comments, etc.

### 📦 Common Kubernetes Commands

| Command                          | Description                     |
| -------------------------------- | ------------------------------- |
| `kubectl get pods`               | List all running pods           |
| `kubectl logs [pod_name]`        | View logs of a pod              |
| `kubectl delete pod [pod_name]`  | Restart a specific pod          |
| `kubectl apply -f [config.yaml]` | Apply Kubernetes configurations |
| `skaffold dev`                   | Start dev mode with auto-reload |
| `skaffold delete`                | Remove all deployed resources   |

### 🧠 Key Kubernetes Concepts

| Term           | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| **Cluster**    | The entire Kubernetes environment (nodes + master)               |
| **Node**       | A VM or worker machine that runs containers                      |
| **Pod**        | The smallest deployable unit that wraps containers               |
| **Deployment** | Manages pod scaling and restarts                                 |
| **Service**    | Provides stable networking access to pods                        |
| **Ingress**    | Routes external traffic (e.g., `posts.com`) to internal services |

### 🧩 Microservices Overview

| Service        | Responsibility                                 |
| -------------- | ---------------------------------------------- |
| **Posts**      | Creates and manages blog posts                 |
| **Comments**   | Handles user comments                          |
| **Moderation** | Filters inappropriate content                  |
| **Query**      | Aggregates and returns combined data           |
| **Event Bus**  | Publishes and listens to service events        |
| **Client**     | React-based frontend, accessed via `posts.com` |

**🧹 `.gitignore` Example**

At the project root, include a `.gitignore` like this:
```bash
# Node modules (ignore for all services)
**/node_modules
**/build
**/dist

# Environment files
**/.env

# IDE and OS files
.vscode/
.DS_Store
```

This ensures all dependencies are excluded across your microservices.

🧾 License
This project is open-source and available under the MIT License.
