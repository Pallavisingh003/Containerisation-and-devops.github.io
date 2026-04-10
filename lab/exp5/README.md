🧩 PART 1: Docker Volumes
🔹 Step 1: Run container without volume
docker run -it --name test ubuntu bash
👉 Inside container:
echo "Hello" > file.txt
cat file.txt
exit
📸 Screenshot 1: File created inside container
🔹 Step 2: Restart container
docker start test
docker exec test cat file.txt
📸 Screenshot 2: File missing (data lost)
🔹 Step 3: Run container with volume
docker run -it --name mycontainer -v myvolume:/data ubuntu bash
👉 Inside:
echo "Saved Data" > /data/file.txt
exit
📸 Screenshot 3: File created in volume
🔹 Step 4: Check data persistence
docker start mycontainer
docker exec mycontainer cat /data/file.txt
📸 Screenshot 4: Data persists
🔹 Step 5: List volumes
docker volume ls
📸 Screenshot 5: Volume list
🌍 PART 2: Environment Variables
🔹 Step 1: Run container with env variable
docker run -d --name envtest -e NAME=Pallavi nginx
📸 Screenshot 6: Container running
🔹 Step 2: Check variable
docker exec envtest printenv NAME
📸 Screenshot 7: Output showing NAME
🔹 Step 3: Create .env file
nano myenv.env
Add:
CITY=Dehradun
COURSE=Cloud
📸 Screenshot 8: .env file
🔹 Step 4: Run using env file
docker run -d --name envfiletest --env-file myenv.env nginx
📸 Screenshot 9: Container running
🔹 Step 5: Verify variable
docker exec envfiletest printenv CITY
📸 Screenshot 10: Output showing CITY
📊 PART 3: Monitoring
🔹 Step 1: Check running containers
docker ps
📸 Screenshot 11: Running containers
🔹 Step 2: Check resource usage
docker stats
📸 Screenshot 12: CPU & memory usage
🔹 Step 3: Check logs
docker logs envtest
📸 Screenshot 13: Logs output
🔹 Step 4: Check processes
docker top envtest
📸 Screenshot 14: Running processes
🌐 PART 4: Docker Networks
🔹 Step 1: Create network
docker network create netpal
📸 Screenshot 15: Network created
🔹 Step 2: Run containers on network
docker run -d --name c1 --network netpal nginx
docker run -d --name c2 --network netpal nginx
📸 Screenshot 16: Containers running
🔹 Step 3: Test communication
docker exec c1 curl http://c2
📸 Screenshot 17: Successful connection
🔥 PART 5: Mini Application
🔹 Step 1: Create network
docker network create appnet
📸 Screenshot 18: Network created
🔹 Step 2: Run database
docker run -d --name db --network appnet -e POSTGRES_PASSWORD=123 postgres
📸 Screenshot 19: DB container running
🔹 Step 3: Run web container
docker run -d --name web --network appnet -p 5000:80 nginx
📸 Screenshot 20: Web container running
🔹 Step 4: Verify
docker ps
📸 Screenshot 21: Both containers running
🧹 Cleanup
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker volume prune -f
docker network prune -f
📸 Screenshot 22: Cleanup done
