# Orange-Jenkins

# Lab-1

Here's a detailed response to each of your queries related to Jenkins:

### Prerequisite Package for Installing Jenkins
- **Java Development Kit (JDK)** is a prerequisite for installing Jenkins. Ensure you have JDK installed on your system before proceeding with Jenkins installation.

### SSH Port Command
- To find the SSH port using the command you provided:
  ```bash
  curl -Lv http://localhost:8085/login 2>&1 | grep -i 'x-ssh-endpoint'
  ```
No Output

 
### Jenkins Plugins
- **B. Plugins are the primary means of enhancing the functionality of a Jenkins environment to suit organization or user-specific needs.**

### Installing .hpi Plugin File
- Yes, you can install `.hpi` plugin files from the Jenkins web UI. Go to **Manage Jenkins** -> **Manage Plugins** -> **Advanced** tab -> **Upload Plugin** section.

### Git and GitHub Plugins Installation
- Make sure to install Git and GitHub plugins if they're not already installed:
  1. **Manage Jenkins** -> **Manage Plugins**.
  2. Search for "Git Plugin" and "GitHub Plugin" in the **Available** tab and install them.

Done installed 

### Jenkins Installation
- **Normal Service Installation:**
  - Follow the official Jenkins installation guide for your operating system (e.g., using apt for Debian-based systems, yum for RedHat-based systems).

- **Docker Container Installation:**
  ```bash
  docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins/jenkins:lts
  ```
  
- **Ansible Installation:**
  - Install Jenkins using an Ansible playbook:
    ```yaml
    - name: Install Jenkins
      hosts: localhost
      become: yes
      tasks:
        - name: Add Jenkins repository
          apt_repository:
            repo: ppa:jenkins-ci
        - name: Install Jenkins
          apt:
            name: jenkins
            state: present
        - name: Ensure Jenkins is started
          service:
            name: jenkins
            state: started
            enabled: yes
    ```
![Screenshot from 2024-09-18 16-56-18](https://github.com/user-attachments/assets/d75322ae-4712-4085-bc6a-35fea0d639a0)


### Jenkins Data Location
- Jenkins primarily stores its data in `/var/lib/jenkins`.

### Installing and Configuring ThinBackup Plugin
- **Install ThinBackup Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "ThinBackup" and install it.

DONE

- **Configure ThinBackup:**
  - Go to **Manage Jenkins** -> **ThinBackup** -> Configure the backup directory as `/var/lib/jenkins/jenkins_backup`.
 
![Screenshot from 2024-09-18 17-15-15](https://github.com/user-attachments/assets/5d1850f4-9368-4e7d-88b6-e8b219a86677)


### Creating Jenkins User
- **Create Jenkins User:**
  - **Manage Jenkins** -> **Manage Users** -> **Create User**.
  - Username: `jenkins`
  - Password: `jenk!n$`
  - Full Name: `Orange DevOps`

![Create-User](https://github.com/user-attachments/assets/dcb561c9-6f06-4e24-968a-0a1c4c915d37)


### Installing Role-Based Authorization Strategy Plugin
- **Install Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "Role-based Authorization Strategy" and install it.

- **Enable Role-Based Strategy:**
  - **Manage Jenkins** -> **Configure Global Security** -> Select **Role-Based Strategy** and configure as needed.

### Creating Roles and Assigning Permissions
- **Create Role `developers`**:
  - Go to **Manage Jenkins** -> **Manage and Assign Roles** -> **Manage Roles**.
  - Add a role named `developers` with **Overall Read** permission.

- **Assign Role to User `jenkins`**:
  - Go to **Manage Jenkins** -> **Manage and Assign Roles** -> **Assign Roles**.
  - Assign the `developers` role to the user `jenkins`.
 
![rolebased](https://github.com/user-attachments/assets/c27ac60f-62bb-49c6-a742-066c4bb3eb82)
![Developers-role](https://github.com/user-attachments/assets/a149f8d8-1a52-4802-98a2-176b9fb6cf0f)


### Installing Matrix Authorization Strategy Plugin
- **Install Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "Matrix Authorization Strategy" and install it.

- **Configure Project-Based Matrix Authorization Strategy:**
  - **Manage Jenkins** -> **Configure Global Security** -> Select **Matrix-based security** and set permissions for the job `mytest`.

### Building `mytest` Job with Jenkins User
- Use credentials for user `jenkins` (Username: `jenkins`, Password: `jenk!n$`) to build the `mytest` job.

### Installing Pipeline Jenkins Plugin
- **Install Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "Pipeline" and install it.

### Creating Pipeline Job
- **Create a Pipeline Job `hello-world`:**
  - Configure the pipeline script:
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Print Message') {
                steps {
                    echo 'Hello World'
                }
            }
        }
    }
    ```
![hello-word-pipline](https://github.com/user-attachments/assets/95af3a45-834a-44b1-b962-79f1b6b96477)


### Installing SSH Build Agents Plugin
- **Install Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "SSH Build Agents" and install it.

### Creating Simple Jenkins Job
- **Create a Freestyle Job:**
  - Add a build step with a shell command:
    ```bash
    echo "Hello, World!"
    ```
![hello-world2](https://github.com/user-attachments/assets/8c054cd9-7b80-4c59-9228-5da7423af7c2)


### Configuring Job to Pull from GitHub
- **Configure GitHub Repository:**
  - **Source Code Management** -> **Git** -> Enter the repository URL.
    
![git-repo](https://github.com/user-attachments/assets/4ec44aee-5d6b-46f4-be3a-f97b6eb470fe)


### Triggering Job Every 5 Minutes
- **Configure Build Periodically:**
  - **Build Triggers** -> **Build periodically** -> Add cron syntax `*/5 * * * *`.

![build5](https://github.com/user-attachments/assets/8e3481fd-ceb9-4fdc-8b18-c95a958556bf)


### Installing Jenkins Plugin from Plugin Manager
- **Install Plugin (e.g., Docker Plugin):**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "Docker" and install it.
 
![Docker](https://github.com/user-attachments/assets/eed7c456-ef23-48da-83f8-51196db9b2e5)


### Email Notifications on Build Failure
- **Configure Email Notifications:**
  - **Manage Jenkins** -> **Configure System** -> **Extended E-mail Notification** -> Set up email server and recipient list.

### Creating Pipeline with Two Stages
- **Pipeline Job:**
  - Use the following pipeline script:
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Pull Code') {
                steps {
                    git 'https://github.com/your-repo/your-project.git'
                }
            }
            stage('List Files') {
                steps {
                    sh 'ls -al'
                }
            }
        }
    }
    ```

### Archiving Log Files
- **Archive Build Artifacts:**
  - **Post-build Actions** -> **Archive the artifacts** -> Enter file paths to archive.

### Cleaning Up Old Builds
- **Configure Build Discarder:**
  - **Build Discarder** -> **Discard Old Builds** -> Set to keep only the last 5 builds.

### Parameterized Job
- **Create Parameterized Job:**
  - **This build is parameterized** -> Add a String Parameter:
    ```bash
    echo "Hello, ${NAME}!"
    ```

### Building Java Project
- **Java Project Job:**
  - **Build** -> Add a build step to compile Java code:
    ```bash
    javac MyJavaFile.java
    ```

### Checking Disk Space
- **Disk Space Job:**
  - **Build** -> Add a shell command:
    ```bash
    df -h
    ```

### Running Python Script
- **Python Script Job:**
  - **Build** -> Add a build step to run Python script:
    ```bash
    python script.py
    ```

### Configuring Jenkins Job on Specific Agent
- **Node Configuration:**
  - **Manage Jenkins** -> **Manage Nodes and Clouds** -> Add a node with label `linux`.
  - Configure the job to run on nodes with the label `linux`.

If you have any specific questions or need further details on any of these tasks, let me know!
