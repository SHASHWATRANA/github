# Jenkins Installation Guide

This document explains how to install Jenkins on a local system.
Install Java, Jenkins, Git and configure Jenkins using the setup wizard.
📋 Prerequisites
Before starting, ensure your system meets these minimum requirements:

Java: Jenkins requires JDK 17 or 21.

Hardware: At least 1 GB RAM (2 GB+ recommended) and 10 GB drive space.

Browser: Chrome, Firefox, or Edge for the web interface.

🐧 Installation on Linux (Ubuntu/Debian)
Ubuntu is the most common platform for hosting Jenkins. Use the official repository for the most stable version.

Update your system:

Bash
sudo apt update && sudo apt upgrade -y
Install Java (OpenJDK 21):

Bash
sudo apt install openjdk-21-jdk -y
Add Jenkins Repository:

Bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
Install Jenkins:

Bash
sudo apt update
sudo apt install jenkins -y
Start the Service:

Bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
🪟 Installation on Windows
The easiest method for Windows is using the .msi installer.

Download: Get the Windows installer from the Jenkins Official Site.

Run Installer: Open the .msi file and follow the wizard.

Service Logon: You will be prompted to choose a service account.

Recommended: Use a local or domain user for security.

Alternative: Choose "Run service as LocalSystem" for simple local setups.

Port Selection: The default is 8080. Click "Test Port" to ensure it's free.

Java Home: Select the path where JDK 17/21 is installed (e.g., C:\Program Files\Java\jdk-21).

🍎 Installation on macOS
The standard way to install Jenkins on macOS is via Homebrew.

Install Homebrew (if not already installed):

Bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
Install Jenkins (LTS):

Bash
brew install jenkins-lts
Start Jenkins:

Bash
brew services start jenkins-lts
🚀 Post-Installation Setup
Once installed, Jenkins will be running at http://localhost:8080.

Unlock Jenkins: You will need an "Administrator Password."

Linux: sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Windows: Find the password in C:\Program Files\Jenkins\secrets\initialAdminPassword

Install Plugins: Select "Install suggested plugins" to get the standard CI/CD tools.

Create Admin User: Set up your username and password to avoid using the initial secret again.

Instance Configuration: Confirm your Jenkins URL and click Save and Finish.
