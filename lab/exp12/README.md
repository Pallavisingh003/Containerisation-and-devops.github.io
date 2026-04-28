
STEP 1 — Install Requirements on Mac
Install Homebrew 
Install Docker Desktop
Install Minikube
brew install minikube
Install kubectl
brew install kubectl

<img width="1020" height="561" alt="Screenshot 2026-04-28 at 12 59 05 PM" src="https://github.com/user-attachments/assets/8f41dc85-adba-449f-8047-f480ade6d12e" />

<img width="489" height="92" alt="Screenshot 2026-04-28 at 12 59 12 PM" src="https://github.com/user-attachments/assets/08803f79-99ec-4b1c-bad1-a99165f64384" />

---
STEP 2 — Start Kubernetes
minikube start
kubectl get nodes

<img width="783" height="255" alt="Screenshot 2026-04-28 at 1 01 42 PM" src="https://github.com/user-attachments/assets/0761a0c1-a205-4200-a6e4-27df32aa5bfd" />

<img width="451" height="62" alt="Screenshot 2026-04-28 at 1 02 00 PM" src="https://github.com/user-attachments/assets/e6514b79-bc33-40ce-bf3b-8e093a086bfd" />

---
STEP 3 — Create Deployment File
wordpress-deployment.yaml

<img width="544" height="40" alt="Screenshot 2026-04-28 at 1 03 01 PM" src="https://github.com/user-attachments/assets/bc614972-f8d1-4cf8-8e62-191752b8dbcd" />

<img width="774" height="540" alt="Screenshot 2026-04-28 at 1 02 45 PM" src="https://github.com/user-attachments/assets/16b72323-c28a-4e45-8969-d64df1fae32c" />

---
STEP 4 — Run Deployment
kubectl apply -f wordpress-deployment.yaml

<img width="637" height="46" alt="Screenshot 2026-04-28 at 1 03 39 PM" src="https://github.com/user-attachments/assets/e5dcc8bf-fb18-44af-bf47-7eb2b55fffd3" />

---
STEP 5 — Check Pods
kubectl get pods



---
STEP 6 — Create Service File
Create:
wordpress-service.yaml

<img width="540" height="36" alt="Screenshot 2026-04-28 at 1 05 09 PM" src="https://github.com/user-attachments/assets/73f46de4-2953-4386-b4e1-98d7a47eaafe" />

<img width="777" height="521" alt="Screenshot 2026-04-28 at 1 04 55 PM" src="https://github.com/user-attachments/assets/f5ad3cb3-984e-42e0-9b64-73ec98888d9e" />

---
STEP 7 — Apply Service
kubectl apply -f wordpress-service.yaml

<img width="650" height="44" alt="Screenshot 2026-04-28 at 1 05 34 PM" src="https://github.com/user-attachments/assets/0e96527f-53e5-4523-b7bd-5bbc5499d1ab" />

---
STEP 8 — Check Service
kubectl get svc

<img width="526" height="61" alt="Screenshot 2026-04-28 at 1 04 08 PM" src="https://github.com/user-attachments/assets/2b4b1bd7-b9cc-4c90-9214-7d2ed4c04244" />

---
STEP 9 — Open WordPress
minikube service wordpress-service

<img width="730" height="216" alt="Screenshot 2026-04-28 at 1 05 58 PM" src="https://github.com/user-attachments/assets/4a07c80e-a701-43d7-8ae1-88220491d0e6" />

<img width="1119" height="731" alt="Screenshot 2026-04-28 at 1 06 22 PM" src="https://github.com/user-attachments/assets/ed399a8c-9f5a-41b5-b382-d10f1f860fd8" />

<img width="1128" height="791" alt="Screenshot 2026-04-28 at 1 07 16 PM" src="https://github.com/user-attachments/assets/1116e2e3-192d-4a0a-9518-434a62a3d28e" />

---
STEP 10 — Scaling (Increase Copies)
kubectl scale deployment wordpress --replicas=4
kubectl get pods

<img width="740" height="35" alt="Screenshot 2026-04-28 at 1 10 44 PM" src="https://github.com/user-attachments/assets/3bac0411-e947-4a04-af9d-b2c5db801af7" />

---
STEP 11 — Self-Healing Demo
kubectl get pods
kubectl delete pod <pod-name>

<img width="480" height="101" alt="Screenshot 2026-04-28 at 1 10 56 PM" src="https://github.com/user-attachments/assets/4d4e9c89-7c9e-4d0e-ab21-60df165d305f" />

---
