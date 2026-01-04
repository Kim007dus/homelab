# ☸️ Homelab K3s GitOps Repository

Welcome to my K3s GitOps repository! This repository contains all the Kubernetes configurations for my homelab, managed declaratively using Argo CD and the "App of Apps" pattern with Helm.

## ✨ GitOps Philosophy

The entire state of the Kubernetes cluster is defined in this Git repository. We use the **App of Apps** pattern, where a single root Argo CD application (defined in the `app-of-apps` Helm chart) is responsible for deploying all other applications. This makes the cluster state transparent, version-controlled, and easy to manage.

---

## 📂 Directory Structure

- **`app-of-apps/`**: A Helm chart that acts as the "root" application. Its `values.yaml` defines all other applications that Argo CD should manage.
- **`core/`**: Contains raw Kubernetes manifests for manually installed core components, such as the Ingress for Argo CD.
- **`apps/`**: Contains custom `values.yaml` files for the applications deployed by the `app-of-apps` chart. This keeps the root `values.yaml` clean.
- **`README.md`**: This file.

---

## 🚀 Getting Started: Cluster Bootstrap

Follow these steps for the initial, one-time setup of the cluster.

### Step 1: Install Argo CD

First, install Argo CD using the official manifests. Then, patch it to run in insecure mode (handling TLS at the Ingress level) and apply the Ingress.

```bash
# 1. Create the namespace for Argo CD
kubectl create namespace argocd

# 2. Install Argo CD using the official manifests
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# 3. Patch Argo CD to run without internal TLS (Insecure Mode)
# This allows the Ingress to handle SSL termination.
kubectl patch deployment argocd-server -n argocd --type json -p='[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--insecure"}]'

# 4. Apply the Ingress to expose the Argo CD UI
kubectl apply -f ./core/argocd/ingress.yaml
```

> **Note**: If you ever need to update the Argo CD Ingress, you can re-run `kubectl apply -f ./core/argocd/ingress.yaml`.

### Step 2: Deploy the App of Apps

Next, apply the **Root Application** manifest. This creates an Argo CD Application that watches your Git repository and automatically syncs all your other applications.

**Important:** Ensure you have pushed your changes to Git before running this, as Argo CD needs to pull the `app-of-apps` chart from your repository.

```bash
# Apply the root application manifest
kubectl apply -f root-application.yaml
```

Argo CD will now:

1. Clone your repository.
2. Read the `k3s/app-of-apps` Helm chart.
3. Deploy all the applications defined in `k3s/app-of-apps/values.yaml`.

### Step 3: Configure Local DNS

To access your services (like `argocd.homelab.local`), you need to tell your computer where to find them.

**Example:**
Add the following line to your computer's `hosts` file (`/etc/hosts` on Linux/macOS, `C:\Windows\System32\drivers\etc\hosts` on Windows):

```vim
<K3S_MASTER_NODE_IP> prometheus.homelab.local grafana.homelab.local argocd.homelab.local
```

Replace `<K3S_MASTER_NODE_IP>` with the IP address of your k3s master node.

---

## ⚙️ Daily Workflow: Managing Applications

We use the **Wrapper Chart Pattern**. Every application (even 3rd party ones) gets its own folder in `charts/`.

### Adding a New Application

1. **Create a folder** in `charts/` (e.g., `charts/my-app`).
2. **Create `Chart.yaml`** inside it. Add the upstream chart as a dependency.
3. **Create `values.yaml`** inside it with your configuration.
4. **Register the app** in `app-of-apps/values.yaml` pointing to your local folder.

    **Example `app-of-apps/values.yaml` entry:**

    ```yaml
    apps:
    my-app:
        enabled: true
        name: my-app
        namespace: my-app-ns
        source:
        repoURL: https://github.com/Kim007dus/homelab.git
        path: k3s/charts/my-app
        targetRevision: HEAD
    ```

5. Commit and push. Argo CD will detect the local chart, download the dependencies defined in `Chart.yaml`, and deploy it.

---

## 🔐 Security - todo

### Basic Authentication

You can protect services with a username and password using Traefik's basic authentication middleware.

1. **Create the Middleware**: A `Middleware` and `Secret` manifest can be deployed via Argo CD. (See `core/traefik-auth/` for an example).
2. **Enable on Ingress**: In your application's values file (e.g., `apps/grafana/values.yaml`), add the following annotations to the ingress:

    ```yaml
    # apps/grafana/values.yaml
    ingress:
      # ...
      annotations:
        traefik.ingress.kubernetes.io/router.middlewares: default-basic-auth@kubernetescrd
    ```

---

## 📝 Future Improvements (To-Do)

- [ ] **Automate Bootstrapping**: Create an Ansible playbook to automate the initial `helm install` commands.
- [ ] **Implement Local DNS Server**: Set up Pi-hole or AdGuard Home to handle wildcard DNS (`*.homelab.local`) for the entire network, removing the need to edit `hosts` files.
- [ ] **Implement Sealed Secrets**: Replace plaintext passwords in values files with encrypted secrets for better security.
