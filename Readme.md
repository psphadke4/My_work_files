# Installing Camunda Basic Stack on Self-Hosted Kubernetes

## Prerequisites
To install the Camunda Basic Stack on a self-hosted Kubernetes cluster, you need a Kubernetes engine. The recommended option is:
- **Kind** (for Windows, macOS, and Linux)
- **Minikube
- **Self Hosted Kube using Kubeadm

Ensure you have the following tools installed before proceeding:
- `kubectl` (Kubernetes CLI)
- Helm (for managing Kubernetes applications)
- Docker (for containerized workloads)
- **For Windows Users:** Docker Desktop must be installed before setting up Kind.

### Installing Docker Desktop (Windows & macOS)
1. Download Docker Desktop from the official [Docker website](https://www.docker.com/products/docker-desktop/).
2. Run the installer and follow the setup instructions.
3. Enable **WSL 2** integration (for Windows users) if prompted.
4. Restart your system if necessary.
5. Verify installation by running:
   ```bash
   docker --version
   ```
6. Ensure Docker Desktop is running before proceeding with Kind installation.

### Installing Helm on Windows
1. Open CMD using Administrator
2. Install Helm using Winget:
   ```
   winget install Helm.Helm
   ```
3. Verify Helm installation:
   ```
   helm version
   ```

## Step 1: Set Up a Kubernetes Cluster Using Kind

1. **Ensure Docker Desktop is installed and running**
2. Install Kind:
   ```bash
   curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-windows-amd64
   ```
3. Create a Kind cluster:
   ```bash
   kind create cluster
   ```
4. Create a dedicated namespace for Camunda:
   ```bash
   kubectl create namespace c8
   ```

## Step 2: Deploy Camunda Using Helm
To install the Basic Kubernetes stack of Camunda, you can use a `values.yaml` file. One approach is to clone the official Camunda Helm repository and use this values.yaml


### Option 1: Clone the Repository

1. Clone the Camunda Helm repository:
   ```bash
   git clone https://github.com/camunda/camunda-platform-helm.git
   ```
2. Navigate to the cloned directory:
   ```bash
   cd camunda-platform-helm
   ```
3. Use the provided values file for installation:
   ```bash
   helm install camunda-platform camunda/camunda-platform -f kind/camunda-platform-core-kind-values.yaml -n c8
   ```

Alternatively, you can create and customize your own `values.yaml` file based on the requirements.
Use the command below to install the Camunda stack with the specified values file:
   ```bash
   helm install camunda-platform camunda/camunda-platform -f kind/camunda-platform-core-kind-values.yaml -n c8

```

## Step 3: Verify Deployment
Once the installation is complete, wait for the pods to start. Use the following command to check the status of all pods:
   ```bash
   kubectl get pods -n c8

   ```
Resources:

For an overview of the Camunda Stack, refer to the official documentation:
[Camunda Stack Overview](https://docs.camunda.io/docs/self-managed/setup/overview/)

