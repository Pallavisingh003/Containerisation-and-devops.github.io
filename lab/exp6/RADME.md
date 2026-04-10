🟢 STEP 1: Create Lab Folder
mkdir docker-lab
cd docker-lab


🟢 STEP 2: Create HTML Folder
mkdir html
echo "<h1>Hello Pallavi Docker Lab</h1>" > html/index.html
Check:
ls html


🟢 STEP 3: Run Nginx (Docker Run)
docker run -d --name lab-nginx -p 8081:80 -v $(pwd)/html:/usr/share/nginx/html nginx:alpine


🟢 STEP 4: Verify Container
docker ps


🟢 STEP 5: Open Browser

http://localhost:8081


🟢 STEP 6: Stop & Remove
docker stop lab-nginx
docker rm lab-nginx


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


🟢 STEP 8: Run Compose
docker compose up -d


🟢 STEP 9: Verify
docker compose ps


🟢 STEP 10: Open Again
http://localhost:8081


🟢 STEP 11: Stop Compose
docker compose down


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
🟢 STEP 13: Run
docker compose up -d


🟢 STEP 14: Open WordPress
http://localhost:8082


🟢 STEP 15: Stop Everything
docker compose down -v
