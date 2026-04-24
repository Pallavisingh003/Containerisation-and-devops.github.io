Step 1: Setup Environment
Install required tools:
Docker Desktop
Apache Maven
Java (JDK 11 or above)
Verify installation:
docker --version
mvn -version
java -version

<img width="569" height="235" alt="Screenshot 2026-04-24 at 11 15 40 PM" src="https://github.com/user-attachments/assets/f0b3885a-0b7c-41e4-810a-7921a5770915" />


---
Step 2: Create SonarQube Setup
Create a new directory:
mkdir sonar-lab
cd sonar-lab
Create a Docker Compose file:
nano docker-compose.yml
Add configuration for:
SonarQube server
PostgreSQL database
Start services:
docker-compose up -d
Check logs:
docker-compose logs -f sonarqube
Wait until:
SonarQube is up

<img width="548" height="46" alt="Screenshot 2026-04-24 at 9 23 23 PM" src="https://github.com/user-attachments/assets/b1002156-cddc-434a-8d74-7a8b575530c0" />

<img width="557" height="25" alt="Screenshot 2026-04-24 at 9 26 33 PM" src="https://github.com/user-attachments/assets/2e46c2cb-eb83-485d-9d5f-cc6ef7ca7a21" />

<img width="1179" height="181" alt="Screenshot 2026-04-24 at 9 27 51 PM" src="https://github.com/user-attachments/assets/04a24084-0ad8-476a-a41c-8d048fbe2f98" />

<img width="1153" height="92" alt="Screenshot 2026-04-24 at 9 28 02 PM" src="https://github.com/user-attachments/assets/e7efb74a-2044-4f4d-b86d-df9b3631d833" />

<img width="1440" height="854" alt="Screenshot 2026-04-24 at 9 28 34 PM" src="https://github.com/user-attachments/assets/833f95b1-54b8-4340-b0b1-a169ce9a4dea" />

<img width="1440" height="826" alt="Screenshot 2026-04-24 at 9 28 46 PM" src="https://github.com/user-attachments/assets/31668f5b-78d7-49a8-96ac-48c897332a23" />


---
Step 3: Access SonarQube Dashboard
Open browser:
http://localhost:9000
Login using:
Username: admin
Password: admin
Change password on first login.

<img width="994" height="458" alt="Screenshot 2026-04-24 at 9 29 18 PM" src="https://github.com/user-attachments/assets/40d23b5e-1fa4-4451-9b77-94039c25ada0" />

<img width="999" height="743" alt="Screenshot 2026-04-24 at 9 31 50 PM" src="https://github.com/user-attachments/assets/90cdae4d-932d-449c-b0e3-4934a40f2103" />

<img width="1120" height="778" alt="Screenshot 2026-04-24 at 9 34 39 PM" src="https://github.com/user-attachments/assets/0c332064-2948-4c86-a23e-a533ff852e38" />

---
Step 4: Generate Authentication Token
Click profile icon (top right)
Go to My Account → Security
Select:
User Token
Enter token name:
my-token
Click Generate
Copy the generated token (used for scanning)

<img width="1292" height="488" alt="Screenshot 2026-04-24 at 9 36 41 PM" src="https://github.com/user-attachments/assets/350404c2-7c52-47fc-9b25-24daa92698d9" />

<img width="984" height="410" alt="Screenshot 2026-04-24 at 9 36 55 PM" src="https://github.com/user-attachments/assets/68d4888b-5af2-470f-aeef-429d31f840d2" />


---
Step 5: Create Sample Java Project
Create project directory:
mkdir my-java-app
cd my-java-app
Create folder structure:
mkdir -p src/main/java/com/example
Create Java file:
nano src/main/java/com/example/Calculator.java
Add sample code containing:
Bugs
Vulnerabilities
Code smells

<img width="529" height="46" alt="Screenshot 2026-04-24 at 9 38 25 PM" src="https://github.com/user-attachments/assets/a823c08d-eb2a-4e46-9924-d6fa40897037" />

<img width="569" height="65" alt="Screenshot 2026-04-24 at 9 38 45 PM" src="https://github.com/user-attachments/assets/0c8eafe4-8451-4163-9dac-4c6da58f5653" />

<img width="494" height="21" alt="Screenshot 2026-04-24 at 10 42 07 PM" src="https://github.com/user-attachments/assets/21697620-0f6c-4396-ac80-f7b5a180b19b" />

<img width="463" height="303" alt="Screenshot 2026-04-24 at 10 42 15 PM" src="https://github.com/user-attachments/assets/76e1b21f-ffb7-49e6-a00a-1ab33070e333" />

---
Step 6: Configure Maven Project
Create Maven file:
nano pom.xml
Add project details and SonarQube configuration.
Replace:
YOUR_TOKEN_HERE
with the generated token.

<img width="465" height="23" alt="Screenshot 2026-04-24 at 10 58 17 PM" src="https://github.com/user-attachments/assets/3e865efd-9d7f-4bd3-bb78-af8b48e43424" />

<img width="567" height="338" alt="Screenshot 2026-04-24 at 10 58 27 PM" src="https://github.com/user-attachments/assets/2fa17da5-cfe7-4efc-bd78-8fc995011474" />

---
Step 7: Run SonarQube Analysis
Navigate to project folder:
cd my-java-app
Execute:
mvn sonar:sonar -Dsonar.login=YOUR_TOKEN
Wait for:
BUILD SUCCESS
ANALYSIS SUCCESSFUL

<img width="1440" height="731" alt="Screenshot 2026-04-24 at 10 59 41 PM" src="https://github.com/user-attachments/assets/c1fc5e4d-2303-4486-9244-fae406c3c4a8" />

<img width="1009" height="761" alt="Screenshot 2026-04-24 at 10 59 49 PM" src="https://github.com/user-attachments/assets/1bc7c2af-5a18-4701-9d92-addd1ecdc692" />


---
Step 8: View Analysis Results
Open:
http://localhost:9000
Select project from dashboard.
Observe:
Bugs
Vulnerabilities
Code Smells
Duplication
Quality Gate status

<img width="1223" height="685" alt="Screenshot 2026-04-24 at 11 01 21 PM" src="https://github.com/user-attachments/assets/56f9bc03-9cf3-4dba-b323-4f78a4b429dd" />

---
