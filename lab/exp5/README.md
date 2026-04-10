PART 1: Docker Volumes
🔹 Step 1: Run container without volume
docker run -it --name test ubuntu bash
Inside container:
echo "Hello" > file.txt
cat file.txt
exit
<img width="570" height="104" alt="Screenshot 2026-04-10 at 4 15 57 PM" src="https://github.com/user-attachments/assets/3484258c-d2ef-4007-89d5-8b53d5be9aad" />

🔹 Step 2: Restart container
docker start test
docker exec test cat file.txt
<img width="548" height="63" alt="Screenshot 2026-04-10 at 4 16 18 PM" src="https://github.com/user-attachments/assets/e2da1b42-4483-466d-9fa0-4106d2e01ec4" />

🔹 Step 3: Run container with volume
docker run -it --name mycontainer -v myvolume:/data ubuntu bash
Inside:
echo "Saved Data" > /data/file.txt
exit
<img width="520" height="99" alt="Screenshot 2026-04-10 at 4 16 56 PM" src="https://github.com/user-attachments/assets/619c7ecb-4e3b-425a-859b-7d102ebae51b" />

🔹 Step 4: Check data persistence
docker start mycontainer
docker exec mycontainer cat /data/file.txt
<img width="548" height="63" alt="Screenshot 2026-04-10 at 4 16 18 PM" src="https://github.com/user-attachments/assets/5afdf205-3330-4445-bb51-7b142bb3cad9" />


🔹 Step 5: List volumes
docker volume ls


---
PART 2: Environment Variables
🔹 Step 1: Run container with env variable
docker run -d --name envtest -e NAME=Pallavi nginx
<img width="570" height="127" alt="Screenshot 2026-04-10 at 4 19 45 PM" src="https://github.com/user-attachments/assets/8b73429a-d464-469f-bd63-f76a8e5a3f9f" />

🔹 Step 2: Check variable
docker exec envtest printenv NAME
<img width="568" height="103" alt="Screenshot 2026-04-10 at 4 18 24 PM" src="https://github.com/user-attachments/assets/5a25d928-9b35-4d26-9829-76d2d3de11ac" />

🔹 Step 3: Create .env file
nano myenv.env
Add:
CITY=Dehradun
COURSE=Cloud
<img width="570" height="127" alt="Screenshot 2026-04-10 at 4 19 45 PM" src="https://github.com/user-attachments/assets/24b11b06-2688-4bbb-b273-3eb8845e1242" />

🔹 Step 4: Run using env file
docker run -d --name envfiletest --env-file myenv.env nginx
<img width="551" height="87" alt="Screenshot 2026-04-10 at 4 19 12 PM" src="https://github.com/user-attachments/assets/52e6e00a-d606-4009-98bc-2841e0f4d262" />

🔹 Step 5: Verify variable
docker exec envfiletest printenv CITY

---
PART 3: Monitoring
🔹 Step 1: Check running containers
docker ps

🔹 Step 2: Check resource usage
docker stats

🔹 Step 3: Check logs
docker logs envtest

🔹 Step 4: Check processes
docker top envtest

---
PART 4: Docker Networks
🔹 Step 1: Create network
docker network create netpal

🔹 Step 2: Run containers on network
docker run -d --name c1 --network netpal nginx
docker run -d --name c2 --network netpal nginx

🔹 Step 3: Test communication
docker exec c1 curl http://c2

---
PART 5: Mini Application
🔹 Step 1: Create network
docker network create appnet

🔹 Step 2: Run database
docker run -d --name db --network appnet -e POSTGRES_PASSWORD=123 postgres

🔹 Step 3: Run web container
docker run -d --name web --network appnet -p 5000:80 nginx

🔹 Step 4: Verify
docker ps

---
Cleanup
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker volume prune -f
docker network prune -f

