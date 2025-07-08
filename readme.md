# 🐳 Docker CI Workflows

Reusable **GitHub Actions** for building and publishing Docker images to Docker Hub and GHCR.

---

## 📦 Available Workflows

| Workflow                    | Runs On                               | Purpose                                                            |
|-----------------------------|---------------------------------------|--------------------------------------------------------------------|
| `docker-build-push.yaml`    | `push` to `main`, `workflow_dispatch` | Build & push Docker images (main branch)                           |
| `docker-build-push-pr.yaml` | `pull_request`                        | Build & push Docker images for PRs, post a comment with image tags |

---

### 🚀 Build & Push (`docker-build-push.yaml`)

> ✅ Triggered on `push` to `main` or manually via `workflow_dispatch`.  
> ✅ Builds and pushes Docker images to DockerHub and GHCR.

```yaml
jobs:
  build:
    uses: nstwf-docker/docker-ci/.github/workflows/docker-build-push.yaml@v1
    with:
      image_version: 1.0
      dockerhub_image: nstwfdev/my-app
      ghcr_image: ghcr.io/nstwf-docker/my-app
      docker_extra_build_args: |
        MY_ENV_VAR=value
    secrets: inherit
```

---

### 🛠 Build & Push for Pull Requests (`docker-build-push-pr.yaml`)

> ✅ Triggered automatically on every `pull_request`.  
> ✅ Builds Docker images for the PR branch, pushes images (optional), and adds a PR comment with image tags.

```yaml
jobs:
  build-pr:
    uses: nstwf-docker/docker-ci/.github/workflows/docker-build-push-pr.yaml@v1
    with:
      image_version: 1.0
      dockerhub_image: nstwfdev/my-app
      docker_extra_build_args: |
        MY_ENV_VAR=value
    secrets: inherit
```