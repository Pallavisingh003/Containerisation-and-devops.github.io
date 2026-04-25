Step 1: Create Project Folder
mkdir swarm-app
cd swarm-app

<img width="521" height="32" alt="Screenshot 2026-04-25 at 8 47 32 AM" src="https://github.com/user-attachments/assets/d21f35cb-ca4c-4aea-ade1-403c834dfd26" />

---
Step 2: Create Compose File
touch docker-compose.yml

<img width="557" height="31" alt="Screenshot 2026-04-25 at 8 47 49 AM" src="https://github.com/user-attachments/assets/90dd6fee-05b4-4bc0-a907-adfac3adf2ce" />

<img width="578" height="411" alt="Screenshot 2026-04-25 at 9 06 13 AM" src="https://github.com/user-attachments/assets/4d1c2874-1ede-4f1c-9717-fcbeb72a6ce9" />

---
Step 3: Stop Old Containers
docker compose down -v
docker ps

<img width="705" height="47" alt="Screenshot 2026-04-25 at 8 50 47 AM" src="https://github.com/user-attachments/assets/51109eb7-a62c-4802-a397-56197acc94da" />

<img width="582" height="30" alt="Screenshot 2026-04-25 at 8 50 54 AM" src="https://github.com/user-attachments/assets/9f3abc60-4161-4dee-9115-7605af03cba9" />

---
Step 4: Initialize Swarm
docker swarm init
Verify:
docker node ls

<img width="697" height="125" alt="Screenshot 2026-04-25 at 8 51 06 AM" src="https://github.com/user-attachments/assets/1f153df1-3c4f-44c5-9da8-4e3bfedc26d8" />

<img width="708" height="64" alt="Screenshot 2026-04-25 at 8 51 53 AM" src="https://github.com/user-attachments/assets/e49b9ee9-2c1b-4e95-8589-567c353ae365" />

<img width="708" height="64" alt="Screenshot 2026-04-25 at 8 51 53 AM" src="https://github.com/user-attachments/assets/7725a326-5b63-44fa-8e69-44c0b48d1df2" />

---
Step 5: Deploy Stack
docker stack deploy -c docker-compose.yml mystack

<img width="702" height="101" alt="Screenshot 2026-04-25 at 8 52 22 AM" src="https://github.com/user-attachments/assets/88ae7f06-25f4-4f94-a260-8e5eb4d6df2c" />

---
Step 6: Verify Services
docker service ls
docker ps

<img width="645" height="64" alt="Screenshot 2026-04-25 at 8 52 42 AM" src="https://github.com/user-attachments/assets/af443f62-cca6-4f31-8a1d-39dab8279fc6" />

<img width="698" height="72" alt="Screenshot 2026-04-25 at 8 53 08 AM" src="https://github.com/user-attachments/assets/a3e1f4e9-732d-44b0-92f2-161e4ebd6e3a" />

---
Step 7: Access Application
Open browser:
http://localhost:8080
WordPress setup page appears.

<img width="1253" height="479" alt="Screenshot 2026-04-25 at 8 57 29 AM" src="https://github.com/user-attachments/assets/6ad536e4-c155-4015-8cee-71946b39d107" />

---
Step 8: Scale Application
docker service scale mystack_app=3
Verify:
docker service ls

---
Step 9: Test Self-Healing
docker ps
docker kill <container-id>
docker service ps mystack_app
Observation:
Failed container is replaced automatically

<img width="645" height="64" alt="Screenshot 2026-04-25 at 8 52 42 AM" src="https://github.com/user-attachments/assets/af6626ee-a50b-44a9-ba90-462ccd82fe8b" />

---
Step 10: Remove Stack
docker stack rm mystack

<img width="551" height="57" alt="Screenshot 2026-04-25 at 9 14 52 AM" src="https://github.com/user-attachments/assets/fd8a0b9c-fcbe-4dfe-a927-6b4d9b92b4f8" />

---
