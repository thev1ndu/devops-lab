# DevOps Lab Environment

A comprehensive containerized development environment with essential DevOps tools for learning, testing, and development.

![DevOps Tools](https://via.placeholder.com/800x400?text=DevOps+Lab+Environment)

## 🚀 Overview

This project provides a complete DevOps lab environment running in Docker containers. It includes CI/CD tools, infrastructure as code utilities, monitoring solutions, container orchestration, and more - all configured to work together out of the box.

## 📋 Included Tools & Services

| Category | Tools |
|----------|-------|
| **CI/CD & Source Control** | Jenkins, GitLab |
| **Infrastructure as Code** | Terraform, Ansible |
| **Secrets Management** | HashiCorp Vault |
| **Monitoring & Logging** | Prometheus, Grafana, ELK Stack (Elasticsearch, Logstash, Kibana) |
| **Container Orchestration** | Kubernetes (Minikube) |
| **Container Management** | Portainer |
| **Databases** | MySQL, MongoDB |

## 🔧 Prerequisites

- Docker Engine 20.10+ and Docker Compose v2+
- At least 8GB RAM available for Docker
- 50GB+ of free disk space
- Git

## 📦 Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/thev1ndu/devops-lab.git
cd devops-lab
```

### 2. Create the services directory

```bash
mkdir -p /root/services
```

### 3. Start the lab environment

```bash
docker-compose up -d
```

This will download all necessary Docker images and start the containers. The initial setup may take some time depending on your internet connection.

## 🖥️ Accessing the Services

After starting the environment, the following services will be available:

| Service | URL | Default Credentials |
|---------|-----|---------------------|
| Jenkins | http://localhost:7500 | Retrieved from logs |
| GitLab | http://localhost:7501 | Set during first login |
| Vault | http://localhost:7502 | Token: devroot |
| Prometheus | http://localhost:7503 | N/A |
| Grafana | http://localhost:7504 | admin / admin |
| Kibana | http://localhost:7505 | N/A |
| Kubernetes Dashboard | http://localhost:7506 | N/A |
| Portainer | https://localhost:9443 | Set during first login |
| MySQL | localhost:9500 | root / rootpassword |
| MongoDB | localhost:9501 | root / rootpassword |

## 📁 Directory Structure

All service data is stored in the `/root/services/` directory with the following structure:

```
/root/services/
├── ansible/
├── elasticsearch/
├── gitlab/
│   ├── config/
│   ├── data/
│   └── logs/
├── grafana/
├── jenkins/
├── logstash/
│   └── pipeline/
├── minikube/
│   ├── kube/
│   └── minikube/
├── mongodb/
├── mysql/
├── portainer/
├── prometheus/
│   ├── config/
│   └── data/
└── terraform/
```

## 🔍 Initial Configuration

### Jenkins

When accessing Jenkins for the first time, you'll need to retrieve the initial admin password:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

### GitLab

On first access, you'll be prompted to set the admin password. After that, you can create projects and start using GitLab.

### Portainer

On first access, you'll need to create an admin account.

## 🔄 Network Configuration

All services are connected to the `server-net` Docker network with the following IP configuration:

| Service | IP Address |
|---------|------------|
| Jenkins | 172.18.0.10 |
| GitLab | 172.18.0.11 |
| Terraform | 172.18.0.12 |
| Ansible | 172.18.0.13 |
| Vault | 172.18.0.14 |
| Prometheus | 172.18.0.15 |
| Grafana | 172.18.0.16 |
| Elasticsearch | 172.18.0.17 |
| Logstash | 172.18.0.18 |
| Kibana | 172.18.0.19 |
| Minikube | 172.18.0.20 |
| Portainer | 172.18.0.21 |
| MySQL | 172.18.0.22 |
| MongoDB | 172.18.0.23 |

## 🛠️ Common Usage Examples

### Setting up a CI/CD Pipeline

1. Create a repository in GitLab
2. Configure Jenkins to connect to GitLab
3. Create a Jenkinsfile for your pipeline
4. Set up webhook integration between GitLab and Jenkins

### Infrastructure as Code with Terraform and Ansible

Access the Terraform container:

```bash
docker exec -it terraform sh
```

Access the Ansible container:

```bash
docker exec -it ansible sh
```

### Monitoring with Prometheus and Grafana

1. Access Grafana at http://localhost:7504
2. Add Prometheus as a data source (http://prometheus:9090)
3. Import dashboards or create custom ones

## 🔄 Stopping and Starting

To stop all services:

```bash
docker-compose stop
```

To start all services:

```bash
docker-compose start
```

To completely remove all containers (data will be preserved in `/root/services/`):

```bash
docker-compose down
```

## 🧹 Maintenance

### Updating Services

To update all services to their latest versions:

```bash
docker-compose down
docker-compose pull
docker-compose up -d
```

### Backing Up Data

All data is stored in the `/root/services/` directory, which you can back up using standard methods:

```bash
tar -czvf devops-lab-backup.tar.gz /root/services
```

## 🐛 Troubleshooting

### Checking Service Logs

To check logs for a specific service:

```bash
docker-compose logs [service-name]
```

For example:

```bash
docker-compose logs jenkins
```

### Resource Issues

If containers are crashing, check if your system has enough resources available:

```bash
docker stats
```

## 🔒 Security Considerations

This lab environment is designed for development and learning purposes and is not secured for production use. For production:

- Change all default passwords
- Enable TLS/SSL for all services
- Configure proper network security
- Implement proper authentication and authorization

---

Created for DevOps enthusiasts ❤️
