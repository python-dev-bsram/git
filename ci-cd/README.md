| **Topic**                      | **Details**                                                                                                                                                                                                                                                                                                    |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Git Branching**              | 1. `git branch branch-name`: Creates a branch but does not switch to it; you’ll need to run `git checkout branch-name` separately. <br> 2. `git checkout -b branch-name`: Creates and switches to the new branch in one step.                                                                               |
| **Staging with Exclusions**    | `git add -- .':!.pycache'`: Stages all files except `.pycache` (useful for avoiding unnecessary files in commits).                                                                                                                                                                                           |
| **Pushing Branches**           | `git push --set-upstream origin branch-name`: Pushes a new branch to the remote repository and sets up tracking if the branch doesn’t already exist there.                                                                                                                                                    |
| **Pipeline Structure**         | - Pipelines consist of **Jobs** (individual tasks) and **Stages** (groups of jobs executed in a specific order). <br> - Common pipeline types include: **Basic Pipeline**, **DAG Pipeline**, **Parent-Child Pipeline**, and **Multi-Project Pipeline**.                                                    |
| **Purpose of Stages**          | Stages define the job execution sequence in pipelines. This ensures jobs with dependencies run sequentially, while allowing parallel execution for independent jobs, thus optimizing resource use.                                                                                                          |
| **Stage Definition**           | 1. **Default Order**: GitLab by default runs jobs in pre-defined pre and post-stages within each job. <br> 2. **Explicit Definition**: Manually list stages in the pipeline configuration file to control exact job ordering.                                       |
| **Artifacts in CI/CD**         | Artifacts are files or directories produced by jobs in one stage. These are stored and passed to subsequent stages, making it easier to reuse outputs (e.g., build files or test results) across stages.                                                                                                   |
| **Manual Process (No CI/CD)**  | 1. **Branch Creation**: Separate branches are created for specific tasks, which are merged later. <br> 2. **Build & Integration Team**: Manually performs code review and testing. <br> 3. **Operations Team**: Manually deploys code based on instructions, which is prone to human error and delays. <br> 4. **Limitations**: Lacks automation, making it a slower, unstreamlined process. |
| **Benefits of CI/CD Automation** | 1. **Shared Repository**: A central codebase accessible to the entire team. <br> 2. **Frequent Commits**: Team members frequently commit and merge, keeping the codebase current. <br> 3. **Automated Testing**: Build server automatically tests code, reducing manual intervention for Build and Integration Team. <br> 4. **Operational Scripts**: Deployment scripts, often in Unix, automate deployment steps. <br> 5. **End-to-End Pipeline**: CI/CD pipeline automates testing, building, deployment, and release, making the deployment process faster and more reliable. |


## GitLab Runner Setup Guide

This guide walks you through the process of installing and configuring a GitLab Runner on a Debian-based system, using commands to set up, register, and customize the runner.

---

### Prerequisites
- **Operating System**: Debian-based (e.g., Ubuntu)
- **Permissions**: Ensure you have `sudo` privileges for installation and configuration.
- **GitLab Account**: Access to a GitLab project or group with **CI/CD settings**.

---

## Steps to Install and Configure GitLab Runner

| Step | Command | Description | Notes |
|------|---------|-------------|-------|
| 1 | `gitlab-runner --version` | Verify if GitLab Runner is already installed. | **Output**: GitLab Runner version or command not found. |
| 2 | `curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" \| sudo bash` | Download and prepare the GitLab Runner installation script for Debian-based systems. | Adds the official GitLab Runner repository. |
| 3 | `sudo apt install gitlab-runner` | Install the GitLab Runner. | Confirms successful installation via package manager. |
| 4 | `gitlab-runner --version` | Verify GitLab Runner installation. | Displays installed version. |

---

## Registering the GitLab Runner

Run the registration command to link your runner with GitLab. During registration, you’ll be prompted for the following inputs:

| Command | Description |
|---------|-------------|
| `sudo gitlab-runner register` | Registers the GitLab Runner to your GitLab instance. Prompts for specific input values as outlined below. |

| Field | Description | Example Value / Options |
|-------|-------------|-------------------------|
| **GitLab Instance URL** | The URL of your GitLab server instance. | `https://gitlab.com` or your self-hosted GitLab URL. |
| **Registration Token** | Unique token found in GitLab under **Settings > CI/CD > Runners**. | (Token string provided by GitLab) |
| **Description** | A short identifier for your runner (useful when managing multiple runners). | `My CI Runner - Docker` |
| **Tags** | Tags to associate with the runner for targeted job assignments. | `docker, linux`, or `test-runner` |
| **Executor** | The method GitLab Runner uses to run jobs. Options include: <br> - `docker` <br> - `shell` <br> - `virtualbox` <br> - `ssh` <br> - `kubernetes` <br> - `custom` | Select based on your environment (e.g., `docker` for containerized builds). |

---
## Check GitLab Runner Settings:

After registering runner with requireured credentilas follow to open gitlab >settings >ci/cd > Runnner. If you obeserve in the Image there are tags and Label which need to configure in the `gitlab-ci.yml` 
![image](https://github.com/user-attachments/assets/3384e164-7e09-4af1-9a9b-232101bf491d)

## Configuring the Runner

After registration, you may want to customize the runner’s configuration file for advanced settings. This file is located at `/etc/gitlab-runner/config.toml`.

```bash
sudo vi /etc/gitlab-runner/config.toml
```

## GitLab Runner Setup with Docker Executor

--

This guide will install Docker, configure it for GitLab Runner, and verify the Docker setup.

```bash
# 1. Install Docker
sudo apt update
sudo apt install -y docker.io

# 2. Check Docker service status
sudo systemctl status docker

# 3. Add the GitLab Runner user to the Docker group
# (Required to allow GitLab Runner to access Docker)
sudo usermod -aG docker gitlab-runner

# 4. Restart Docker to apply group changes
sudo systemctl restart docker

# 5. Verify Docker installation by listing Docker images
# (This should return an empty list if no images are downloaded yet)
sudo docker images
```

## SSH Configuration in GitLab



### Step 1: Generate SSH Key

In Linux, execute the following command to generate an SSH key:

```bash
ssh-keygen -t rsa -b 2048 -C "name of key" -y
```

### Step 2: Copy the SSH Key

Now, open the .ssh/id_rsa.pub file to view your SSH public key. You can use the cat or vim command:

```bash
cat ~/.ssh/id_rsa.pub
```

### Step 3: Add SSH Key in GitLab
In GitLab, go to the top navigation and click on your user profile.
- Go to Preferences > SSH Keys.
- Paste the copied SSH key in the Key field.
- Add a Title and Expiration date if required.

### Step 4: Verify SSH Key Addition

To ensure the SSH key was added properly, use the following command:
```bash
ssh -T git@domain.com
```

