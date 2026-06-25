DOCKER HUB IMAGE LINK;-https://hub.docker.com/r/abiny432/portfolio-website
 
 
 Portfolio Website: Automated CI Pipeline with GitHub Actions

This repository implements an automated Continuous Integration (CI) pipeline using **GitHub Actions** and **Docker Hub** to streamline the containerization and delivery of a static portfolio website.

---

🚀 Workflow Overview

The CI pipeline automatically triggers on every `git push` to the `main` branch. It automates the following manual steps:

1. Code Checkout: Retrieves the latest website and configuration files from the repository.
2. Docker Hub Authentication:Logs securely into Docker Hub using credentials stored in GitHub Secrets.
3. Build Image: Packages the HTML, CSS, and asset files into a lightweight Nginx web server image.
4. Push Image: Uploads the built image to Docker Hub under the `latest` tag, making it instantly available for deployment.

📂 Repository Structure


project-root/
├── index.html          # Main portfolio layout
├── styles.css          # Styling rules
├── Dockerfile          # Configuration for Nginx container
├── README.md           # CI process documentation
└── .github/
    └── workflows/
        └── docker-ci.yml  # GitHub Actions pipeline definition
    
  To avoid hardcoding sensitive credentials in the source code, this pipeline utilizes GitHub Actions Secrets. The following secrets are configured in the repository's settings:

    DOCKER_USERNAME: Stores the Docker Hub username securely.

    DOCKER_PASSWORD: Stores a Personal Access Token (PAT) with write access, ensuring secure authentication without exposing account passwords.

    Once the GitHub Actions run succeeds and the image is published to Docker Hub, the application can be pulled and executed on any system (such as an AWS EC2 VM) running Docker:

# 1. Pull the automated image from Docker Hub
docker pull abiny432/portfolio-website:latest

# 2. Run the container on standard port 80
docker run -d -p 80:80 abiny432/portfolio-website:latest
    
