# Jenkins User Manual

This document explains how to use Jenkins jobs created for this project.
A Jenkins User Manual is essentially a guide to the "Big Three" concepts: Items (Jobs), Manage Jenkins (Settings), and Nodes (Where builds happen).

Since you have an interest in Java and Networking, you'll likely find Jenkins' automation logic very intuitive.

🛠️ 1. The Dashboard (The Command Center)
When you log in, the Dashboard shows your list of "Items."

New Item: Create a new project (Pipeline, Freestyle, or Multibranch).

Build History: A timeline of every build attempted.

Manage Jenkins: The brain of the operation (Plugins, Security, Nodes).

🏗️ 2. Creating Your First Job (Pipeline vs. Freestyle)
In 2026, Pipelines are the industry standard because they allow "Configuration as Code."

Freestyle Project (Beginner)
Best for simple tasks. You use the web UI to click buttons and add "Build Steps" (e.g., "Execute shell" or "Invoke top-level Maven targets").

Pipeline Project (Recommended)
You write a Jenkinsfile. This is powerful because it's version-controlled.

Declarative Pipeline Example:

Groovy
pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Compiling Java code...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running JUnit tests...'
            }
        }
    }
}
🔌 3. Managing Plugins
Jenkins is a skeleton; plugins are the muscles.

Where to find: Manage Jenkins > Plugins > Available Plugins.

Essential Plugins: * Git: To pull code from GitHub/GitLab.

Docker: To run builds inside containers.

Blue Ocean: For a modern, visual UI of your pipelines.

Slack/Email Extension: For build notifications.

👤 4. User Management & Security
Never leave Jenkins open to the public.

Roles: Go to Manage Jenkins > Manage and Assign Roles (requires Role-based Strategy plugin).

Credentials: Store passwords, SSH keys, and API tokens securely in Manage Jenkins > Credentials. Never hardcode passwords in your scripts.

🖥️ 5. Nodes and Agents (Distributed Builds)
By default, Jenkins builds everything on the "Built-in Node" (the server where it's installed). For better performance:

Add Agent: Go to Manage Jenkins > Nodes.

Configuration: Connect a second machine via SSH.

Benefit: If one build crashes the agent, the main Jenkins server stays alive.

📂 6. Navigating a Build Page
Once a build runs, click on the Build Number (e.g., #1) to see:

Console Output: The most important tool. It shows the raw logs of exactly what happened.

Changes: See which Git commit triggered the build.

Artifacts: Download the resulting files (like a .jar or .war file).
