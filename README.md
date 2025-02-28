# Jenkins Cheatsheet

## **Jenkins Overview**
Jenkins is an open-source automation server used for CI/CD pipeline automation.

---

## **Installing Jenkins (Step-by-Step Guide)**

### **For Ubuntu/Debian**
```sh
sudo apt update
sudo apt install openjdk-11-jdk -y   # Install Java (required for Jenkins)
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
echo "deb https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt update
sudo apt install jenkins -y          # Install Jenkins
sudo systemctl enable jenkins        # Enable Jenkins to start on boot
sudo systemctl start jenkins         # Start Jenkins service
```

### **For CentOS/RHEL**
```sh
sudo yum update -y
sudo yum install java-11-openjdk -y  # Install Java
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install jenkins -y          # Install Jenkins
sudo systemctl enable jenkins        # Enable Jenkins to start on boot
sudo systemctl start jenkins         # Start Jenkins service
```

### **Access Jenkins Web Interface**
- Default URL: `http://localhost:8080`
- Default admin password is stored in:
  ```sh
  cat /var/lib/jenkins/secrets/initialAdminPassword
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

## **Creating a Jenkins Pipeline to Fetch Daily Coding Challenge**

### **Step 1: Open Jenkins Dashboard**
- Navigate to `http://localhost:8080`
- Login using the admin password (found in `/var/lib/jenkins/secrets/initialAdminPassword`)

### **Step 2: Create a New Pipeline Job**
- Click on `New Item`
- Enter a name for your job and select `Pipeline`
- Click `OK`

### **Step 3: Define the Pipeline Script**
- Scroll down to the `Pipeline` section
- Choose `Pipeline script`
- Add the following script to fetch today's coding challenge:
  ```groovy
  pipeline {
      agent any
      parameters {
          choice(name: 'PLATFORM', choices: ['LeetCode', 'CodeForces', 'HackerRank'], description: 'Select the coding platform')
      }
      stages {
          stage('Fetch Daily Challenge') {
              steps {
                  script {
                      def platform = params.PLATFORM.toLowerCase()
                      def url = ''
                      if (platform == 'leetcode') {
                          url = 'https://leetcode.com/api/problems/daily'
                      } else if (platform == 'codeforces') {
                          url = 'https://codeforces.com/api/problemset.recentStatus'
                      } else if (platform == 'hackerrank') {
                          url = 'https://www.hackerrank.com/rest/contests/master/challenges'
                      }
                      sh "curl -s ${url} | jq ."
                  }
              }
          }
      }
  }
  ```

### **Step 4: Save and Run the Pipeline**
- Click `Save`
- Click `Build Now`
- Select a platform when prompted

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

