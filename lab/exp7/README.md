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

<img width="562" height="33" alt="Screenshot 2026-04-10 at 9 36 27 PM" src="https://github.com/user-attachments/assets/0f82144e-ba8d-4d4e-90cd-a767b676ae72" />
<img width="569" height="44" alt="Screenshot 2026-04-10 at 9 36 39 PM" src="https://github.com/user-attachments/assets/4ad0d0d6-8c19-48dd-bc64-e264b9cc4bcc" />
<img width="1183" height="296" alt="Screenshot 2026-04-10 at 9 36 54 PM" src="https://github.com/user-attachments/assets/b9841763-9706-44a9-a037-48a66db4aedc" />
![Uploading Screenshot 2026-04-10 at 9.37.22 PM.png…]()
<img width="1072" height="48" alt="Screenshot 2026-04-10 at 9 37 02 PM" src="https://github.com/user-attachments/assets/0cf00506-46cc-4f3c-82fb-97ac73948b49" />

----
STEP 4: Unlock Jenkins
Retrieve initial admin password from Docker container
Enter password in Jenkins setup page
Select Install Suggested Plugins
Wait for installation to complete
Create admin user
Access Jenkins dashboard

<img width="843" height="636" alt="Screenshot 2026-04-10 at 9 37 44 PM" src="https://github.com/user-attachments/assets/153d15d5-877f-49ff-ab98-217910c46576" />
<img width="829" height="788" alt="Screenshot 2026-04-10 at 9 39 24 PM" src="https://github.com/user-attachments/assets/6cd9cd25-e9dd-4277-b721-3c1813e12b9a" />
<img width="542" height="787" alt="Screenshot 2026-04-10 at 9 43 14 PM" src="https://github.com/user-attachments/assets/d123d9a9-004f-4282-b9e3-4a1dad0f96da" />

----
STEP 5: Add Credentials
Go to Manage Jenkins
Open Manage Credentials
Select global credentials
Add new credentials
Enter Docker Hub username and password
Assign credential ID
Save credentials

<img width="502" height="697" alt="Screenshot 2026-04-10 at 9 49 59 PM" src="https://github.com/user-attachments/assets/b3f20e79-10a4-4f91-9c85-13b63882c49b" />
<img width="545" height="743" alt="Screenshot 2026-04-10 at 9 51 44 PM" src="https://github.com/user-attachments/assets/7ffe7ce4-311c-4d10-9ff7-47db5dd2d170" />
<img width="529" height="672" alt="Screenshot 2026-04-10 at 9 57 27 PM" src="https://github.com/user-attachments/assets/673d62b4-24c0-41d2-b969-b026afa861bb" />
<img width="551" height="471" alt="Screenshot 2026-04-10 at 10 01 33 PM" src="https://github.com/user-attachments/assets/0acf8980-6ce5-4392-b22b-7baf658817e3" />

----
STEP 6: Create Pipeline Job
Click on New Item
Enter job name as ci-cd-pipeline
Select Pipeline option
Click OK


<img width="557" height="742" alt="Screenshot 2026-04-10 at 10 02 27 PM" src="https://github.com/user-attachments/assets/c2833923-cef3-4098-8195-627c8043c03d" />
<img width="547" height="732" alt="Screenshot 2026-04-10 at 10 07 38 PM" src="https://github.com/user-attachments/assets/5ee746db-aea1-4e5c-acc2-7cd8641bc7f4" />
<img width="547" height="785" alt="Screenshot 2026-04-10 at 10 09 42 PM" src="https://github.com/user-attachments/assets/0b9ed3c6-81fc-40d3-bc2d-5124e794931f" />

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
