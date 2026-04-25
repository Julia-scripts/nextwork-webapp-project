# Java Web App Deployment with AWS CI/CD

Welcome to this project combining Java web app development and AWS CI/CD tools!

<br>

## Table of Contents
- [Introduction](#introduction)
- [Technologies](#technologies)
- [Setup](#setup)
- [Contact](#contact)
- [Conclusion](#conclusion)

<br>

## Introduction
This project is used for an introduction to creating and deploying a Java-based web app using AWS, especially their CI/CD tools.

The deployment pipeline I'm building around the Java web app in this repository is invisible to the end-user, but makes a big impact by automating the software release processes.

-I am doing this project to expand my knowlege on CI/CD and get hans on experince in automating the flow from developing code to deploying wedapp.
-This fits in to my goals because i want to become a cloud engineer this year
<br>

## Technologies
Here’s what I’m using for this project:

- **Amazon EC2**: I'm developing my web app on Amazon EC2 virtual servers, so that software development and deployment happens entirely on the cloud.
- OS: Ubuntu 24.04 LTS (Optimized with 2Gi Swap space for Maven builds)
- key pairs, ssh connections, Git, Maven and Java.
- **VS Code**: For my IDE, I chose Visual Studio Code. It connects directly to my development EC2 instance, making it easy to edit code and manage files in the cloud.
- **GitHub**: All my web app code is stored and versioned in this GitHub repository.
- **AWS CodeArtifact**: Once it's rolled out, CodeArtifact will store my artifacts and dependencies, which is great for high availability and speeding up my project's build process.
- **AWS CodeBuild**: Once it's rolled out, CodeBuild will take over my build process. It'll compile the source code, run tests, and produce ready-to-deploy software packages automatically.
- **AWS CodeDeploy**: Once it's rolled out, CodeDeploy will automate my deployment process across EC2 instances.
- **AWS CodePipeline**: Once it's rolled out, CodePipeline will automate the entire process from GitHub to CodeDeploy, integrating build, test, and deployment steps into one efficient workflow.


<br>

## Setup

To get this project up and running on your local machine, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/Julia-scripts/nextwork-webapp-project.git
    ```
2. Navigate to the project directory:
    ```bash
    cd nextwork-web-project
    ```
3. Install dependencies:
    ```bash
    mvn install
    ```
 # TIPS

 1. The "Memory Hack" (Swap Space)
Tip to add: "If you are running this on a t2.micro instance, the Maven build might hang due to low RAM (1GiB). I resolved this by creating a 2GiB Swap file to extend the virtual memory.
##  Ubuntu Performance Tuning (Swap Space)
Because `t2.micro` instances only have 1GiB of RAM, Maven builds can often fail or freeze the server. I solved this by allocating **2GiB of Swap Space**:

```bash
# Create a 2GB swap file
sudo fallocate -l 2G /swapfile

# Set the correct permissions (only root should read/write)
sudo chmod 600 /swapfile

# Set up the swap area
sudo mkswap /swapfile

# Enable the swap
sudo swapon /swapfile

# Make it permanent (survives a reboot)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Verify it's working
free -h

2. Security Group Reminders
Tip to add: "Ensure that your AWS Security Group has an Inbound Rule allowing traffic on Port 8080 (or whichever port you use for testing) from your IP address."

3. The GitHub Authentication Change
Tip to add: "When pushing code from the EC2 terminal, use a GitHub Personal Access Token (PAT) instead of your password. For security, I used git config --global credential.helper cache to avoid re-entering it for every push."

## Infrastructure & Artifacts

<details>
<summary><b>Click to see: The CodeArtifact Pivot (Bypass)</b></summary>

### ⚠️ Blockage Encountered
The original plan required **AWS CodeArtifact**. However, due to AWS account activation delays (24-hour verification hold), I pivoted to **GitHub Packages**.

### The Solution
* **Registry:** Used GitHub Package Registry instead of AWS CodeArtifact.
* **Security:** Configured Maven `settings.xml` with a GitHub PAT (Personal Access Token).
* **Build:** Successfully deployed the artifact using `mvn deploy`.

> This pivot allowed the project to remain on schedule while demonstrating the ability to work across different cloud ecosystems (AWS + GitHub).
</details>
<br>

## Contact
If you have any questions or comments about the NextWork Web Project, please contact:
enter your Juliana - [julianarzuk@gmail.com](mailto:email@gail.com)
- [linkedIn](linkedin.com/in/juliana-asahguebui-228890325)

<br>

## Conclusion
Thank you for exploring this project! I'll continue to build this pipeline and apply my learnings to future projects.

A big shoutout to **[NextWork](https://learn.nextwork.org/app)** for their project guide and support. [You can get started with this DevOps series project too by clicking here.](https://learn.nextwork.org/projects/aws-devops-vscode?track=high)

