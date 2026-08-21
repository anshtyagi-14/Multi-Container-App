<div align="center">

# 🌌 Project Nexus: Multi-Container Cloud Architecture
**A Next-Generation, Zero-Downtime Application Infrastructure**

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)]()
[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)]()
[![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)]()
[![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)]()
[![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)]()

*Seamless. Scalable. Bulletproof.*

</div>

Welcome to the future of deployments. This repository isn't just a full-stack application; it is a **blueprint for modern cloud-native engineering**. It demonstrates a scalable, highly available architecture utilizing Docker, Nginx, and MongoDB, fully automated with CI/CD pipelines, Infrastructure as Code, and **zero-downtime Blue-Green deployments**.

---

## 🏗️ System Architecture

Our infrastructure is designed for high availability and instant rollbacks. Nginx acts as the gatekeeper, routing traffic dynamically between deployment states.

```mermaid
graph TD
    User([🌐 Internet Traffic]) --> |Port 80| Nginx[🚦 Nginx Reverse Proxy]
    
    subgraph "Docker Bridge Network"
        Nginx -.-> |Staging/New Release| Green[🟩 App-Green :3002]
        Nginx ==> |Active Traffic| Blue[🟦 App-Blue :3001]
        
        Green --> |Port 27017| DB[(🍃 MongoDB)]
        Blue --> |Port 27017| DB
    end
    
    subgraph "Persistent Storage"
        DB --> Volume[💾 Docker Volume: mongo-data]
    end
    
    classDef proxy fill:#2b2b2b,stroke:#00ffcc,stroke-width:2px,color:#fff;
    classDef blue fill:#0055ff,stroke:#fff,stroke-width:2px,color:#fff;
    classDef green fill:#00ff55,stroke:#000,stroke-width:2px,color:#000;
    classDef db fill:#004d00,stroke:#fff,stroke-width:2px,color:#fff;
    
    class Nginx proxy;
    class Blue blue;
    class Green green;
    class DB db;
```

---

## ✨ Core Capabilities

- 🔵🟢 **Zero-Downtime Blue/Green Deployments:** Updates happen invisibly. We stand up the new version (Green) in the shadows, test it, and instantly redirect the Nginx router from the old version (Blue).
- 🔄 **Automated CI/CD Pipeline:** From push to production. GitHub Actions automates Docker image builds, registry pushes, and remote EC2 deployments.
- 📦 **100% Containerized:** Frontend, API, and Database are isolated in Docker, guaranteeing absolute consistency from local dev to AWS.
- 💾 **Stateful Persistence:** MongoDB is wired to persistent Docker Volumes. Containers may die, but your data is eternal.
- 🛠️ **Infrastructure as Code (IaC):** AWS EC2 instances are provisioned via **Terraform**, and configured dynamically via **Ansible**.

---

## 🧬 Tech Stack

| Domain | Technologies |
| :--- | :--- |
| **Frontend** | ⚛️ React.js, HTML5, CSS3 |
| **Backend** | 🟢 Node.js, Express.js |
| **Database** | 🍃 MongoDB (Dockerized) |
| **Orchestration**| 🐳 Docker, Docker Compose |
| **Routing** | 🚦 Nginx (Reverse Proxy & Load Balancing) |
| **CI/CD** | 🐙 GitHub Actions |
| **Infrastructure**| ☁️ AWS (EC2), 🏗️ Terraform, ⚙️ Ansible |

---

## 🌀 The Deployment Matrix (CI/CD Flow)

Watch how a simple code push evolves into a live production update without dropping a single packet:

```mermaid
sequenceDiagram
    participant Dev as 👩‍💻 Developer
    participant GH as 🐙 GitHub / Actions
    participant Hub as 🐳 Docker Hub
    participant AWS as ☁️ AWS EC2
    participant Nginx as 🚦 Nginx Proxy

    Dev->>GH: 1. Push code to 'main'
    GH->>GH: 2. Build new Docker Image (v2)
    GH->>Hub: 3. Push Image to Registry
    GH->>AWS: 4. SSH & Trigger Deployment Script
    AWS->>Hub: 5. Pull new Image (v2)
    AWS->>AWS: 6. Spin up App-Green container
    AWS->>Nginx: 7. Reload Nginx config
    Note over Nginx: Traffic instantly switches<br/>from Blue to Green
    AWS->>AWS: 8. Spin down App-Blue
```

---

## 🚀 Getting Started

Deploy this architecture locally in seconds.

### Prerequisites
- Docker & Docker Compose
- Git

### Ignition Sequence

1. **Clone the repository:**
   ```bash
   git clone https://github.com/anshtyagi-14/multi-container-app.git
   cd multi-container-app
   ```

2. **Verify Configuration:**
   Ensure `nginx.conf` and your frontend build (`./frontend/build`) are present in the root directory.

3. **Launch the Matrix:**
   Start the multi-container environment in detached mode:
   ```bash
   docker-compose up -d
   ```

4. **Monitor the Systems:**
   ```bash
   docker ps
   ```

---

<div align="center">
  <i>"Any sufficiently advanced technology is indistinguishable from magic." - Arthur C. Clarke</i><br>
  Built with ⚡️ by Ansh Tyagi
</div>
