# Jenkins Cheatsheet

## **Jenkins Overview**
Jenkins is an open-source automation server used for CI/CD pipeline automation.

---

## **Jenkins Installation & Version Check**
```sh
jenkins --version                 # Check installed Jenkins version
```

---

## **Starting & Stopping Jenkins**
```sh
sudo systemctl start jenkins      # Start Jenkins service
sudo systemctl stop jenkins       # Stop Jenkins service
sudo systemctl restart jenkins    # Restart Jenkins service
sudo systemctl status jenkins     # Check Jenkins service status
```

---

## **Accessing Jenkins Web Interface**
- Default URL: `http://localhost:8080`
- Default admin password is stored in:
  ```sh
  cat /var/lib/jenkins/secrets/initialAdminPassword
  ```

---

## **Managing Jenkins Jobs**
```sh
jenkins-cli create-job <job_name>  # Create a new job
jenkins-cli delete-job <job_name>  # Delete a job
jenkins-cli build <job_name>       # Trigger a job build
jenkins-cli disable-job <job_name> # Disable a job
jenkins-cli enable-job <job_name>  # Enable a job
```

---

## **Managing Plugins**
```sh
jenkins-cli install-plugin <plugin_name>   # Install a plugin
jenkins-cli list-plugins                   # List installed plugins
jenkins-cli uninstall-plugin <plugin_name> # Uninstall a plugin
```

---

## **Jenkins Pipeline Syntax**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```

---

## **Environment Variables in Jenkins**
```sh
BUILD_NUMBER      # Current build number
JOB_NAME         # Name of the current job
WORKSPACE        # Workspace directory path
GIT_COMMIT       # Latest commit hash (if applicable)
JENKINS_URL      # Jenkins base URL
```

---

## **Jenkins Log Management**
```sh
tail -f /var/log/jenkins/jenkins.log   # View live Jenkins logs
```

---

## **Backup & Restore Jenkins**
```sh
cp -r /var/lib/jenkins /backup/        # Backup Jenkins home directory
```

---

## **Useful Jenkins Resources**
- [Jenkins Official Docs](https://www.jenkins.io/doc/)
- [Jenkins Plugins](https://plugins.jenkins.io/)
- [Jenkins Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/)

---

This cheatsheet provides a quick reference for working with Jenkins efficiently. Let me know if you have any suggestions or improvements!

