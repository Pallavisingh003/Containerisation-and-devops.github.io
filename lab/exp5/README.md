<img width="696" height="408" alt="Screenshot 2026-04-10 at 4 29 32 PM" src="https://github.com/user-attachments/assets/6b5425d6-d5ac-4524-9067-6db9927f24dd" />PART 1: Docker Volumes
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

<img width="568" height="238" alt="Screenshot 2026-04-10 at 4 18 13 PM" src="https://github.com/user-attachments/assets/84c3f59a-7e5e-4d13-b30d-15dd957ba9ae" />

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
<img width="570" height="127" alt="Screenshot 2026-04-10 at 4 19 45 PM" src="https://github.com/user-attachments/assets/fe2dbc05-975b-4bef-bd5f-3ccb4ea0cea2" />

---
PART 3: Monitoring
🔹 Step 1: Check running containers
docker ps
<img width="1278" height="146" alt="Screenshot 2026-04-10 at 4 20 02 PM" src="https://github.com/user-attachments/assets/f97d0ac3-6a07-4034-b4b1-cbf39cf717e5" />

🔹 Step 2: Check resource usage
docker stats
<img width="548" height="63" alt="Screenshot 2026-04-10 at 4 16 18 PM" src="https://github.com/user-attachments/assets/666bf84f-0b51-415d-b0bd-18ee95a0c5c1" />

🔹 Step 3: Check logs
docker logs envtest

🔹 Step 4: Check processes
docker top envtest
<img width="1368" height="169" alt="Screenshot 2026-04-10 at 4 21 12 PM" src="https://github.com/user-attachments/assets/33dc4bc2-b171-4999-af08-6b7fdff90b62" />

---
PART 4: Docker Networks
🔹 Step 1: Create network
docker network create netpal

<img width="528" height="31" alt="Screenshot 2026-04-10 at 4 26 23 PM" src="https://github.com/user-attachments/assets/96971110-8f02-407f-8087-c832b2ac60f7" />

🔹 Step 2: Run containers on network
docker run -d --name c1 --network netpal nginx
docker run -d --name c2 --network netpal nginx

<img width="566" height="89" alt="Screenshot 2026-04-10 at 4 26 34 PM" src="https://github.com/user-attachments/assets/1d6e989d-e9e5-473e-bf7e-c4bcf882836c" />

🔹 Step 3: Test communication
docker exec c1 curl http://c2

<img width="814" height="405" alt="Screenshot 2026-04-10 at 4 26 44 PM" src="https://github.com/user-attachments/assets/326917ff-c687-4e95-847a-1dce8507b9d3" />

---
PART 5: Mini Application
🔹 Step 1: Create network
docker network create appnet

<img width="696" height="408" alt="Screenshot 2026-04-10 at 4 29 32 PM" src="https://github.com/user-attachments/assets/649cde19-fc10-4e70-ba83-64d6119c83af" />


🔹 Step 2: Run database
docker run -d --name db --network appnet -e POSTGRES_PASSWORD=123 postgres

<img width="1434" height="728" alt="Screenshot 2026-04-10 at 4 43 04 PM" src="https://github.com/user-attachments/assets/737d17ed-59b5-43cd-a2a3-8f6b1a102e79" />

🔹 Step 3: Run web container
docker run -d --name web --network appnet -p 5000:80 nginx
🔹 Step 4: Verify
docker ps
<img width="559" height="238" alt="Screenshot 2026-04-10 at 5 23 18 PM" src="https://github.com/user-attachments/assets/2e28127d-0108-4ac5-af2b-4de526f55ee4" />

---
Cleanup
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker volume prune -f
docker network prune -f

<img width="927" height="861" alt="Screenshot 2026-04-10 at 4 44 01 PM" src="https://github.com/user-attachments/assets/80b0bf15-3a7a-463f-b312-6f9ac618d852" />

