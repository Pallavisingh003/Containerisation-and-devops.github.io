🟢 STEP 1: Create Lab Folder
Create Lab Foldermkdir docker-lab
cd docker-lab

<img width="486" height="96" alt="Screenshot 2026-04-10 at 5 32 32 PM" src="https://github.com/user-attachments/assets/42fc193d-92ab-467c-8c3a-a7f1fde1370c" />

---
🟢 STEP 2: Create HTML Folder
mkdir html
echo "<h1>Hello Pallavi Docker Lab</h1>" > html/index.html
Check:
ls html

<img width="570" height="56" alt="Screenshot 2026-04-10 at 5 33 48 PM" src="https://github.com/user-attachments/assets/4ad037c6-c056-402d-ab65-5095a9b7f11f" />

<img width="412" height="31" alt="Screenshot 2026-04-10 at 5 34 07 PM" src="https://github.com/user-attachments/assets/4b66c0cd-2a68-42f8-9e8c-291822206a7a" />

<img width="489" height="30" alt="Screenshot 2026-04-10 at 5 34 23 PM" src="https://github.com/user-attachments/assets/f6c3a5a2-0c9c-444d-944b-3db347e02b49" />

---
🟢 STEP 3: Run Nginx (Docker Run)
docker run -d --name lab-nginx -p 8081:80 -v $(pwd)/html:/usr/share/nginx/html nginx:alpine

<img width="568" height="229" alt="Screenshot 2026-04-10 at 8 32 50 PM" src="https://github.com/user-attachments/assets/27c5f1da-d6ef-483f-b4e5-5477e3e3a38e" />

---
🟢 STEP 4: Verify Container
docker ps

<img width="547" height="34" alt="Screenshot 2026-04-10 at 8 30 53 PM" src="https://github.com/user-attachments/assets/2a51aeb0-67ff-4186-9b20-1f992d90a7ba" />

---
🟢 STEP 5: Open Browser

http://localhost:8081

<img width="887" height="492" alt="Screenshot 2026-04-10 at 8 33 13 PM" src="https://github.com/user-attachments/assets/68177fbb-4023-4ab4-a73f-43b8ee1603ae" />

---
🟢 STEP 6: Stop & Remove
docker stop lab-nginx
docker rm lab-nginx

<img width="491" height="55" alt="Screenshot 2026-04-10 at 8 34 08 PM" src="https://github.com/user-attachments/assets/56a2a5b4-dc4c-4cfb-a184-efe8d9601e56" />

---
🟢 STEP 7: Docker Compose
touch docker-compose.yml
nano docker-compose.yml

version: '3.8'

services:
  nginx:
    image: nginx:alpine
    container_name: lab-nginx
    ports:
      - "8081:80"
    volumes:
      - ./html:/usr/share/nginx/html
Save:
CTRL + X
Y
Enter

<img width="538" height="37" alt="Screenshot 2026-04-10 at 8 34 41 PM" src="https://github.com/user-attachments/assets/654047c2-3e72-4009-b17a-b87dfb83d825" />

---
🟢 STEP 8: Run Compose
docker compose up -d

<img width="569" height="102" alt="Screenshot 2026-04-10 at 8 35 13 PM" src="https://github.com/user-attachments/assets/40d703e1-e8ad-4e40-9a8f-8b2af2ceb562" />

---
🟢 STEP 9: Verify
docker compose ps

<img width="566" height="92" alt="Screenshot 2026-04-10 at 8 35 33 PM" src="https://github.com/user-attachments/assets/758e2009-77d2-4591-bffa-e9001ee13a7f" />

---
🟢 STEP 10: Open Again
http://localhost:8081

<img width="894" height="376" alt="Screenshot 2026-04-10 at 8 36 45 PM" src="https://github.com/user-attachments/assets/d91a0ca1-2f4b-480b-b719-f3caf097fae0" />

--- 
🟢 STEP 11: Stop Compose
docker compose down

<img width="571" height="88" alt="Screenshot 2026-04-10 at 8 37 26 PM" src="https://github.com/user-attachments/assets/cea8e49d-1c6b-4ecd-a60c-8ae57d973332" />

--- 
🟢 STEP 12: Multi-Container (WordPress + MySQL)

nano docker-compose.yml
Paste:
version: '3.8'

services:
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: wordpress
    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    ports:
      - "8082:80"
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_PASSWORD: secret
    depends_on:
      - mysql

volumes:
  mysql_data:
  
<img width="572" height="322" alt="Screenshot 2026-04-10 at 8 43 27 PM" src="https://github.com/user-attachments/assets/bc828bb1-4f40-47f3-ba12-0c04a6a33e0a" />

 --- 
🟢 STEP 13: Run
docker compose up -d

<img width="1440" height="575" alt="Screenshot 2026-04-10 at 8 41 10 PM" src="https://github.com/user-attachments/assets/99efcada-56b5-4977-9b1a-1ff3c49989cd" />

---
🟢 STEP 14: Open WordPress
http://localhost:8082

<img width="880" height="580" alt="Screenshot 2026-04-10 at 8 48 16 PM" src="https://github.com/user-attachments/assets/8e46aa3a-0f47-4379-ae8b-e612b4a04c05" />

<img width="881" height="786" alt="Screenshot 2026-04-10 at 8 48 29 PM" src="https://github.com/user-attachments/assets/4b280350-8e1c-43d0-b10d-750426453d1a" />

<img width="893" height="795" alt="Screenshot 2026-04-10 at 8 49 16 PM" src="https://github.com/user-attachments/assets/4e9fdff5-dfd3-4a1d-92b6-40c47549186f" />

<img width="888" height="529" alt="Screenshot 2026-04-10 at 8 49 28 PM" src="https://github.com/user-attachments/assets/8215d792-bbd3-4110-abbe-3c488d3b5723" />

<img width="890" height="795" alt="Screenshot 2026-04-10 at 8 50 55 PM" src="https://github.com/user-attachments/assets/2c0b6240-fd04-4e1e-bdde-73e51fa81f0a" />

<img width="885" height="733" alt="Screenshot 2026-04-10 at 8 51 05 PM" src="https://github.com/user-attachments/assets/5316849a-7948-4947-8fea-27bf2e24896e" />

--- 

🟢 STEP 15: Stop Everything
docker compose down -v

<img width="561" height="113" alt="Screenshot 2026-04-10 at 8 52 26 PM" src="https://github.com/user-attachments/assets/13c1b961-5db1-4db7-b691-4bbeb370f97c" />


