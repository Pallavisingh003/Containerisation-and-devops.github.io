STEP 1: Create GitHub Repository
Open GitHub website
Sign in to your account
Click on New Repository
Enter repository name as my-app
Select visibility as Public
Initialize with README
Click on Create Repository

<img width="1039" height="724" alt="Screenshot 2026-04-10 at 9 25 40 PM" src="https://github.com/user-attachments/assets/d3eee385-87d7-4aba-9b16-78b86d19a52c" />

----
STEP 2: Add Project Files
Open the created repository
Click on Add File → Create New File
Create required project files (application file, dependency file, Dockerfile, Jenkinsfile)
Commit all files to the repository
<img width="847" height="499" alt="Screenshot 2026-04-10 at 9 28 11 PM" src="https://github.com/user-attachments/assets/b19950a7-9bc2-4fb1-8a64-28db94240675" />
<img width="845" height="455" alt="Screenshot 2026-04-10 at 9 35 07 PM" src="https://github.com/user-attachments/assets/fd500e3f-0b1c-4f02-8229-e7e26e20729a" />
src="https://github.com/user-attachments/assets/1e4a1236-0d0b-448c-84cf-2210a8b97db8" />
<img width="853" height="508" alt="Screenshot 2026-04-10 at 9 35 20 PM" src="https://github.com/user-attachments/assets/266b3de2-fe3f-4d80-b7f1-f2e5dd31b0cd" />
<img width="845" height="627" alt="Screenshot 2026-04-10 at 9 35 31 PM" src="https://github.com/user-attachments/assets/57c6af8e-f58e-4901-bcf7-e21264998566" />
<img width="1192" height="568" alt="Screenshot 2026-04-10 at 9 36 07 PM" src="https://github.com/user-attachments/assets/44d1de77-9937-4ca3-b869-e9072a4c95c2" />

----
STEP 3: Start Jenkins using Docker
Open terminal
Navigate to project directory
Create a Docker Compose configuration file
Start Jenkins container using Docker Compose
Verify container is running
Open Jenkins in browser using localhost

----
STEP 4: Unlock Jenkins
Retrieve initial admin password from Docker container
Enter password in Jenkins setup page
Select Install Suggested Plugins
Wait for installation to complete
Create admin user
Access Jenkins dashboard

----
STEP 5: Add Credentials
Go to Manage Jenkins
Open Manage Credentials
Select global credentials
Add new credentials
Enter Docker Hub username and password
Assign credential ID
Save credentials

----
STEP 6: Create Pipeline Job
Click on New Item
Enter job name as ci-cd-pipeline
Select Pipeline option
Click OK

----
STEP 7: Configure Pipeline
Scroll to Pipeline section
Select Pipeline script from SCM
Choose Git as SCM
Enter GitHub repository URL
Set branch to main
Provide script path as Jenkinsfile
Save configuration

----
STEP 8: Run Pipeline
Click on Build Now
Monitor build progress
Open Console Output
Verify successful execution

----
