## Run container images in Azure Container Instances

Azure Container Instances helps to quickly deploy containers

- Benefits of Azure Container Instances and how resources are grouped.

- Deploy a container instance in Azure by using the Azure CLI.

- Start and stop containers using policies.

- Set environment variables in your container instances.

- Mount file shares in your container instances.

### Azure Container Instances (ACI) Overview

**Key Benefits:**
- **Fast startup**: Launch containers in seconds without VM provisioning
- **Container access**: Direct internet exposure via IP address and FQDN
- **Hypervisor-level security**: VM-level isolation
- **Custom sizes**: Exact CPU core and memory specifications
- **Persistent storage**: Mount Azure Files shares directly
- **Cross-platform**: Support for both Linux and Windows containers

**When to use AKS instead**: Use Azure Kubernetes Service for full orchestration needs (service discovery, automatic scaling, coordinated upgrades)

### Container Groups

- **Definition**: Collection of containers scheduled on the same host machine
- **Shared resources**: Lifecycle, resources, local network, storage volumes
- **Similar to**: Kubernetes pods

**Characteristics:**
- Single DNS name label per group
- Single public IP address with exposed ports
- Multi-container groups support Linux only (Windows supports single instance only)

### Deployment Options

1. **Resource Manager template**: Deploy when additional Azure services needed
2. **YAML file**: More concise, recommended for container instances only

### Resource Allocation

- Resources (CPUs, memory, GPUs) allocated by adding requests of all instances
- Example: 2 instances requesting 1 CPU each = 2 CPUs allocated to group

### Networking

- Container groups share IP address and port namespace
- Must expose ports on IP address and container for external access
- Containers communicate via `localhost` on exposed ports
- Port mapping NOT supported

### Storage Volumes

Supported external volumes:
- Azure file share
- Secret
- Empty directory
- Cloned git repo

### Common Multi-Container Scenarios

- Web app + content puller from source control
- Application + logging container (centralized logging)
- Application + monitoring container (health checks/alerts)
- Front-end + back-end service containers

