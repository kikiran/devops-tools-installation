# Ubuntu Server Setup Guide: Java & Jenkins

A quick reference guide for updating system packages, installing Java 17, and setting up the Jenkins repository.

## 1. System Package Update
Keep your local package index fresh and upgrade existing out-of-date files.
```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Install Java 17 (OpenJDK)
Jenkins requires a Java runtime environment to operate. Install the development kit using the following commands.
```bash
sudo apt install fontconfig openjdk-21-jre
```
To verify the installation:
```bash
java -version
```

## 3. Configure Jenkins Repository (Weekly Release)
Import the official cryptographic signing keys and map the repository path to your local package manager sources.
```bash
# Add the security keyring
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io-2026.key

# Append the repository source
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

## 4. Install Jenkins & Dependencies
Update your software index again to pull the repository metadata and deploy the service engine.
```bash
sudo apt update
sudo apt install fontconfig jenkins -y
```

## 5. Manage the Jenkins Service
Control the background daemon initialization settings.
```bash
# Start the automation server
sudo systemctl start jenkins

# Enable auto-start on server boot
sudo systemctl enable jenkins

# Inspect service operational health
sudo systemctl status jenkins
```

## 6. Access and Unlock Jenkins
Open your web browser and travel to `http://localhost:8080`. Fetch your primary unlock credential from the host directory file:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
