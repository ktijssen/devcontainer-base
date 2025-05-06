# 🚀 Development Container

This repository provides a **Dev Container** setup for Kubernetes, Golang, and cloud-native development using **VS Code Dev Containers**. It includes various CLI tools, automation features, and Kubernetes utilities.

## 📦 Container Configuration

The container is built using a **multi-stage Dockerfile** and a **Dev Container configuration** (`devcontainer.json`).  

### 🔨 Base Images

1. **Go 1.23.6** (Builder stage)  
   - Installs **Jsonnet** tools and **jsonnet-bundler**.
2. **Microsoft DevContainers Python 3.13** (Final image)  
   - Includes Python environment with DevContainer optimizations.

### 🛠 Installed Tools

#### ✅ From Dockerfile

- **Jsonnet** (`jsonnet`, `jsonnet-lint`, `jsonnetfmt`) – JSON templating
- **Jsonnet Bundler** (`jb`) – Package manager for Jsonnet
- **Git & Entr** – Version control and file watching
- **Kubernetes alias** (`alias k=kubectl`)
- Ripgrep - Fast grepping (<https://github.com/BurntSushi/ripgrep>)
- Carapace - Multishell completion (<https://github.com/carapace-sh/carapace-bin>)
- fzf - A command line fuzzy finder (<https://github.com/junegunn/fzf>)

#### ✅ From DevContainer Features

| Feature | Description |
|---------|------------|
| **argo-cd** | GitOps continuous delivery tool. |
| **chezmoi** | Dotfile manager for managing configurations. |
| **Cilium** | eBPF-based networking, security, and observability. |
| **docker-in-docker** | Enables running Docker inside the container. |
| **go-task** | Task runner for automation. |
| **gum** | Command-line tool for interactive scripts. |
| **jq & yq** | CLI tools for processing JSON (`jq`) and YAML (`yq`). |
| **kind** | Kubernetes IN Docker (KinD) for local clusters. |
| **k3d** | Lightweight Kubernetes (K3s) cluster in Docker. |
| **k9s** | Terminal UI for managing Kubernetes clusters. |
| **kubectl, Helm, Minikube** | Kubernetes CLI tools. (Minikube disabled.) |
| **pre-commit** | Framework for managing pre-commit hooks. |
| **skaffold** | Continuous development and deployment for Kubernetes. |
| **talosctl** | Command-line tool for managing Talos clusters. |

## 🔄 Automated Builds & Updates

The container image is **automatically built and pushed using GitHub Actions every Sunday**. This ensures that all dependencies, tools, and base images stay up to date.

### ⚙️ CI/CD Workflow

- GitHub Actions triggers a **monthly build**.
- The updated image is pushed to **Docker Hub** under the name **`kevintijssen/devcontainer-base`**.

## 🔧 Customization

- Modify `.devcontainer/devcontainer.json` to add/remove features.
- Update the `Dockerfile` to install additional tools or dependencies.

## 📝 Notes

- **`k` is aliased to `kubectl`** for convenience.
- The **Go builder stage** ensures Jsonnet tools are available without bloating the final image.

## 📜 License

This project is licensed under the **MIT License**.
