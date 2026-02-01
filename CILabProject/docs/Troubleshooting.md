# Troubleshooting Guide

## Jenkinsfile not found
- Ensure Jenkinsfile is present at repository root.

## Git authentication failed
- Use GitHub Personal Access Token instead of password.

## Build failed
- Check console output for error messages.
First Step: Check the LogsBefore changing settings, always look at the logs to find the specific error message.Linux: Run sudo journalctl -u jenkins.service or check /var/log/jenkins/jenkins.log.Windows: Look in the installation folder for jenkins.err.log and jenkins.out.log.Docker: Run docker logs <container_id>.🛠️ 2. Common Issues & SolutionsA. Jenkins Fails to Start (Java Version Mismatch)Jenkins is very picky about Java versions. If you see UnsupportedClassVersionError in the logs, your Java version is likely too old or too new for that specific Jenkins release.Fix: Ensure you are using OpenJDK 17 or 21 (as of 2026).Windows Fix: If you updated Java, Jenkins might still be looking at the old path. Edit jenkins.xml in your installation folder and update the <executable> path to the new java.exe.Linux Fix: Use sudo update-alternatives --config java to set the correct default version.B. Port 8080 Already in UseIf you see java.net.BindException: Address already in use, another service (like Tomcat or a web app) is using port 8080.Fix (Change Jenkins Port):Linux: Run sudo systemctl edit jenkins and add:Ini, TOML[Service]
Environment="JENKINS_PORT=8081"
Windows: Open jenkins.xml, find --httpPort=8080, change it to 8081, and restart the Jenkins service.C. "No space left on device"Jenkins consumes a lot of space for build history and artifacts. If the disk hits 100%, Jenkins will crash or stop running jobs.Fix: * Clear the workspace of old jobs.Increase the disk quota or mount a larger drive to /var/lib/jenkins.In the UI, go to Manage Jenkins > Nodes, and check if the "Disk Space" monitor has marked the node as offline.D. Forgotten Admin PasswordIf you lose access to the admin account:Go to the Jenkins home directory (e.g., /var/lib/jenkins or C:\ProgramData\Jenkins\.jenkins).Open config.xml.Find <useSecurity>true</useSecurity> and change it to false.Restart Jenkins. You can now enter without a password to reset your user, then turn security back on.🚦 3. Service Status CommandsIf Jenkins isn't responding, use these to check its "health":PlatformCommand to Check StatusCommand to RestartLinuxsystemctl status jenkinssudo systemctl restart jenkinsWindowsGet-Service jenkins (PowerShell)Restart-Service jenkinsmacOSbrew services listbrew services restart jenkins-lts
