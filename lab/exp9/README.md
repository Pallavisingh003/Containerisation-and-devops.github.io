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

---
Step 5: Create Dockerfile

---
Step 6: Build Docker Image
docker build -t ubuntu-server .

---
Step 7: Run 4 Servers
docker run -d -p 2201:22 --name server1 ubuntu-server
docker run -d -p 2202:22 --name server2 ubuntu-server
docker run -d -p 2203:22 --name server3 ubuntu-server
docker run -d -p 2204:22 --name server4 ubuntu-server

---
Step 8: Create Inventory File
nano inventory.ini
[servers]
server1 ansible_host=localhost ansible_port=2201
server2 ansible_host=localhost ansible_port=2202
server3 ansible_host=localhost ansible_port=2203
server4 ansible_host=localhost ansible_port=2204

---
Step 9: Test SSH (One Time)
ssh -i ~/.ssh/id_rsa root@localhost -p 2201
Type yes, then:
exit
Repeat for all servers.

---
Step 10: Test Ansible Connection
ansible all -i inventory.ini -m ping

---
Step 11: Create Playbook

---
Step 12: Run Playbook
ansible-playbook -i inventory.ini playbook.yml

---
Step 13: Verify Output
ansible all -i inventory.ini -m command -a "cat /root/ansible_test.txt"

---
Step 14: Cleanup
for i in {1..4}; do
  docker rm -f server${i}
done

---

