

# CI/CD Pipeline with GitHub Actions, SonarQube, Docker, AWS ECR, and ArgoCD
![image](https://github.com/user-attachments/assets/6eac4d63-f02c-4960-a26c-d2ff528cae27)


---

## 🧩 Architecture Overview
- Developer commits code to the Source Code Repository.
- GitHub Actions is triggered to run the CI pipeline.
- Code is built, tested, analyzed, containerized, and the image is pushed to AWS ECR.
- Kubernetes manifests in the CD repo are updated with the new image tag.
- ArgoCD watches the CD repo and deploys the changes to the EKS cluster.

---

## 🛠 Components Used

| Component        | Purpose                                  |
|------------------|------------------------------------------|
| GitHub Actions   | CI tool to automate build/test/deploy    |
| Maven            | Java application build system            |
| SonarQube        | Code quality and static analysis         |
| Docker           | Containerization                         |
| AWS ECR          | Docker image storage                     |
| ArgoCD           | GitOps-based CD to Kubernetes            |
| Amazon EKS       | Managed Kubernetes cluster               |  |

---

## 🚀 CI/CD Workflow (Step-by-Step)

1. **Code Push**: Developer pushes code to the source repo.
2. **CI Pipeline Triggers**:
    - Build and test Java app using Maven
    - Perform static analysis with SonarQube
    - Build Docker image
    - Push image to AWS ECR
    - Update the image tag in Kubernetes manifests in the CD repo
3. **CD Repo Webhook Fires**:
    - ArgoCD detects changes in the CD repo
    - ArgoCD syncs the manifests to the EKS cluster
4. **Kubernetes Deploys**: Updated application is rolled out using ArgoCD in a GitOps manner.

---


CICD Implementation using GitHub Actions(Self Hosted Runners)


  buils_docker_image_and_push:
  1. Install docker on self-hosted VM
  2. sudo chmod 666 /var/run/docker.sock
  3. Update your image tag: <dockerhub username>/<repo name>:latest

  deploy_to_kubernetes:
  1. Create VM
  2. Install AWS CLI and configure it
  3. Install Terraform
  4. Terraform init
  5. Terraform apply
  6. aws eks update-kubeconfig --region <region-name> --name <cluster-name>
  7. Install kubectl
  8. cat ~/.kube/config
  9. Create secrets.EKS_KUBECONFIG
