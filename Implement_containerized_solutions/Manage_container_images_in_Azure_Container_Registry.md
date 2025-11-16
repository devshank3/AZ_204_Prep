## ACR Azure Container Registry

Learn how to use Azure Container Registry to store your container images, and automate builds and deployments.

- Explain the features and benefits ACR offers.

- Describe how to use ACR Tasks to automate builds and deployments.

- Explain the elements in a Dockerfile.

- Build and run an image in the ACR by using Azure CLI.

### What is Azure Container Registry?

ACR is a managed registry service based on open-source Docker Registry 2.0. It stores and manages container images and related artifacts for use in container development and deployment pipelines.

### Use Cases

**Deployment Targets:**
- Orchestration systems: Kubernetes, DC/OS, Docker Swarm
- Azure services: AKS, App Service, Batch, Service Fabric

**Development Workflows:**
- Push images as part of CI/CD workflows (Azure Pipelines, Jenkins)
- Automate builds with ACR Tasks on code commits or base image updates
- Multi-step tasks for building, testing, and patching multiple images in parallel

### Service Tiers

| Tier | Description |
|------|-------------|
| **Basic** | Cost-optimized for learning. Same programmatic capabilities (Entra ID auth, image deletion, webhooks) but lower storage and throughput for lighter usage. |
| **Standard** | Increased storage and throughput compared to Basic. Suitable for most production scenarios. |
| **Premium** | Highest storage and concurrent operations for high-volume scenarios. Adds geo-replication, content trust for image signing, and private link support. |

### Supported Content

- **Images:** Both Windows and Linux container images
- **Formats:** Docker container images, Helm charts, OCI Image Format Specification images
- **Organization:** Images grouped in repositories as read-only snapshots

### Automated Image Builds (ACR Tasks)

ACR Tasks streamlines the build-test-deploy pipeline:
- Automate container OS and framework patching
- Trigger builds on source code commits to Git repositories
- Trigger builds on base image updates
- Build images directly in Azure without local Docker installation

### Storage Capabilities

All ACR tiers benefit from advanced Azure storage features for data security and protection.

**Encryption-at-rest:**
- All container images and artifacts are automatically encrypted at rest
- Azure encrypts images before storing and decrypts on-the-fly when pulled
- Optional extra encryption layer with customer-managed keys

**Regional Storage:**
- Data stored in the registry creation region for data residency and compliance
- May also store in paired region in same geography (except Brazil South and Southeast Asia)
- Brazil South and Southeast Asia: data confined to region only
- **Note:** Regional outage data is not automatically recovered

**Geo-replication (Premium tier):**
- High-availability across multiple regions
- Protection against regional failure events
- Network-close image storage for faster pushes/pulls in distributed scenarios

**Zone Redundancy (Premium tier):**
- Uses Azure availability zones
- Replicates registry to minimum of three separate zones per enabled region

**Scalable Storage:**
- Create unlimited repositories, images, layers, and tags (up to storage limit)
- **Maintenance tip:** Periodically delete unused resources to maintain performance
- **Warning:** Deleted registry resources cannot be recovered

### Build and Manage Containers with ACR Tasks

ACR Tasks is a suite of features for cloud-based container image building across Linux, Windows, and ARM platforms.

**Task Scenarios:**

1. **Quick Task** - On-demand build and push without local Docker Engine (`az acr build`)
   - Like running `docker build` and `docker push` in the cloud
   - Supports inner-loop development (write, build, test cycle)

2. **Automatically Triggered Tasks:**
   - **Source code update** - Trigger on commits or pull requests to GitHub/Azure DevOps
   - **Base image update** - Auto-rebuild when base image updates in your registry or public repos (Docker Hub)
   - **Schedule** - Run on timer triggers for regular maintenance/testing

3. **Multi-step Tasks** - YAML-defined workflows that:
   - Execute multiple build and push operations
   - Run containers for testing (each step uses container as execution environment)
   - Example flow: Build app → Run app → Build tests → Run tests → Build Helm chart → Deploy

**Supported Platforms:**

| OS | Architectures |
|----|---------------|
| Linux | amd64, arm, arm64, 386 |
| Windows | amd64 |

Use `--platform` flag to specify OS/architecture (e.g., `--platform Linux/arm64/v8`)

