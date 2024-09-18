# Orange-Jenkins

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

### Jenkins Data Location
- Jenkins primarily stores its data in `/var/lib/jenkins`.

### Installing and Configuring ThinBackup Plugin
- **Install ThinBackup Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "ThinBackup" and install it.

- **Configure ThinBackup:**
  - Go to **Manage Jenkins** -> **ThinBackup** -> Configure the backup directory as `/var/lib/jenkins/jenkins_backup`.

### Creating Jenkins User
- **Create Jenkins User:**
  - **Manage Jenkins** -> **Manage Users** -> **Create User**.
  - Username: `jenkins`
  - Password: `jenk!n$`
  - Full Name: `Orange DevOps`

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

### Installing SSH Build Agents Plugin
- **Install Plugin:**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "SSH Build Agents" and install it.

### Creating Simple Jenkins Job
- **Create a Freestyle Job:**
  - Add a build step with a shell command:
    ```bash
    echo "Hello, World!"
    ```

### Configuring Job to Pull from GitHub
- **Configure GitHub Repository:**
  - **Source Code Management** -> **Git** -> Enter the repository URL.

### Triggering Job Every 5 Minutes
- **Configure Build Periodically:**
  - **Build Triggers** -> **Build periodically** -> Add cron syntax `*/5 * * * *`.

### Installing Jenkins Plugin from Plugin Manager
- **Install Plugin (e.g., Docker Plugin):**
  - **Manage Jenkins** -> **Manage Plugins** -> **Available** tab -> Search for "Docker" and install it.

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
