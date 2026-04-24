Step 1: Install Ansible
brew install ansible
Check version:
ansible --version


<img width="1015" height="843" alt="Screenshot 2026-04-24 at 8 32 25 PM" src="https://github.com/user-attachments/assets/76caaff2-719d-413d-8737-6d3cf67ed17b" />
<img width="711" height="869" alt="Screenshot 2026-04-24 at 8 32 37 PM" src="https://github.com/user-attachments/assets/e9168bdf-7acf-42d2-afcf-0c4cef37ae1f" />
<img width="1319" height="837" alt="Screenshot 2026-04-24 at 8 32 53 PM" src="https://github.com/user-attachments/assets/c74f6fd5-e7f3-4afe-af33-f45401b90d43" />
<img width="1083" height="873" alt="Screenshot 2026-04-24 at 8 33 03 PM" src="https://github.com/user-attachments/assets/97866130-2309-43af-9593-a2bfa3871170" />
<img width="468" height="30" alt="Screenshot 2026-04-24 at 8 42 03 PM" src="https://github.com/user-attachments/assets/06120339-180b-4bfb-ba5f-b38bd39538d0" />
<img width="566" height="214" alt="Screenshot 2026-04-24 at 8 33 36 PM" src="https://github.com/user-attachments/assets/27c8efcb-c08a-4065-8e70-7471a34f74ea" />

---
Step 2: Install and Start Docker
Install Docker Desktop
Open Docker and ensure it is running
Check:
docker info


---
Step 3: Create SSH Key
ssh-keygen -t rsa -b 4096
Press ENTER three times
Keys generated:
Private key → ~/.ssh/id_rsa
Public key → ~/.ssh/id_rsa.pub

---
Step 4: Create Project Directory
mkdir ansible-lab
cd ansible-lab
Copy keys:
cp ~/.ssh/id_rsa .
cp ~/.ssh/id_rsa.pub .


<img width="468" height="30" alt="Screenshot 2026-04-24 at 8 42 03 PM" src="https://github.com/user-attachments/assets/d6438aea-8098-4750-bbb6-97e56079a805" />
<img width="554" height="32" alt="Screenshot 2026-04-24 at 8 43 01 PM" src="https://github.com/user-attachments/assets/e9ae3085-1d3a-4015-8a77-70160efb6d21" />


---
Step 5: Create Dockerfile


<img width="550" height="31" alt="Screenshot 2026-04-24 at 8 43 07 PM" src="https://github.com/user-attachments/assets/978c99fc-a34f-4b50-b3c3-1b1ff1d2c650" />
<img width="840" height="304" alt="Screenshot 2026-04-24 at 8 43 23 PM" src="https://github.com/user-attachments/assets/bffdda36-d90c-44bf-813b-b6d4c96689bb" />

---
Step 6: Build Docker Image
docker build -t ubuntu-server .


<img width="1437" height="427" alt="Screenshot 2026-04-24 at 8 46 30 PM" src="https://github.com/user-attachments/assets/a052acb2-f09b-4038-b1cf-4830f2d6763c" />

---
Step 7: Run 4 Servers
docker run -d -p 2201:22 --name server1 ubuntu-server
docker run -d -p 2202:22 --name server2 ubuntu-server
docker run -d -p 2203:22 --name server3 ubuntu-server
docker run -d -p 2204:22 --name server4 ubuntu-server


<img width="645" height="124" alt="Screenshot 2026-04-24 at 8 48 33 PM" src="https://github.com/user-attachments/assets/173c257e-3135-4a05-add0-3c5ad158ab1f" />

---
Step 8: Create Inventory File
nano inventory.ini
[servers]
server1 ansible_host=localhost ansible_port=2201
server2 ansible_host=localhost ansible_port=2202
server3 ansible_host=localhost ansible_port=2203
server4 ansible_host=localhost ansible_port=2204


<img width="533" height="21" alt="Screenshot 2026-04-24 at 8 49 07 PM" src="https://github.com/user-attachments/assets/4cbc2ed0-9cc9-43b8-a322-540485352e8d" />
<img width="563" height="338" alt="Screenshot 2026-04-24 at 8 48 55 PM" src="https://github.com/user-attachments/assets/3eb232d8-bff9-4b81-8c33-d33270d5aa27" />

---
Step 9: Test SSH (One Time)
ssh -i ~/.ssh/id_rsa root@localhost -p 2201
Type yes, then:
exit
Repeat for all servers.

---
Step 10: Test Ansible Connection
ansible all -i inventory.ini -m ping


<img width="568" height="258" alt="Screenshot 2026-04-24 at 8 50 30 PM" src="https://github.com/user-attachments/assets/ef2bc4c2-5d1a-4484-8f2a-0481d5bccc50" />

---
Step 11: Create Playbook


<img width="540" height="26" alt="Screenshot 2026-04-24 at 8 53 06 PM" src="https://github.com/user-attachments/assets/e69b0ebd-7608-4165-af75-c14eeb753da6" />
<img width="549" height="24" alt="Screenshot 2026-04-24 at 8 50 47 PM" src="https://github.com/user-attachments/assets/924b75f1-7d07-4239-9448-f12c72e41ef4" />
<img width="567" height="339" alt="Screenshot 2026-04-24 at 8 54 59 PM" src="https://github.com/user-attachments/assets/e9579cb5-92d3-40e9-8273-31dc81d364a0" />

---
Step 12: Run Playbook
ansible-playbook -i inventory.ini playbook.yml


<img width="937" height="476" alt="Screenshot 2026-04-24 at 8 54 30 PM" src="https://github.com/user-attachments/assets/960b8b21-3cdf-4477-aa70-16f8ce8cbdef" />

---
Step 13: Verify Output
ansible all -i inventory.ini -m command -a "cat /root/ansible_test.txt"


<img width="570" height="147" alt="Screenshot 2026-04-24 at 8 55 45 PM" src="https://github.com/user-attachments/assets/65366911-26e3-4654-a3ba-ac5daa45520e" />

---
Step 14: Cleanup
for i in {1..4}; do
  docker rm -f server${i}
done


<img width="546" height="98" alt="Screenshot 2026-04-24 at 8 56 03 PM" src="https://github.com/user-attachments/assets/60b19023-1472-4c84-8a8a-a75b217bb075" />

---

