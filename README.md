# nextjs-demo-app

Task – 1
Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)


Tools Used:
    • GitHub & GitHub Actions
    • Node.js
    • Docker & DockerHub
    • Personal Access Tokens (GitHub & DockerHub)
Step 1: Prepare the Node.js Project
    1. Created a sample Node.js project with files:
        ◦ app.js → main application file
        ◦ package.json → Node.js dependencies
    2. Created a Dockerfile to containerize the app:
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]

Step 2
Create DockerHub Account & Token

Step 3
Add GitHub Secrets

Step 4
Created GitHub Actions Workflow
.github/workflows/main.yml


main.yml

name: CI/CD Pipeline - Node.js + Docker

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Log in to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Build Docker image
        run: docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/nodejs-demo-app:latest .

      - name: Push Docker image
        run: docker push ${{ secrets.DOCKERHUB_USERNAME }}/nodejs-demo-app:latest

Step 5 : Test the Pipeline

<img width="1920" height="1080" alt="Screenshot from 2025-10-20 18-01-38" src="https://github.com/user-attachments/assets/da2ca043-8861-4e9e-ab54-17993e45146e" />

Step 6 : Running locally

<img width="1920" height="1080" alt="Screenshot from 2025-10-20 18-03-09" src="https://github.com/user-attachments/assets/7d623c3b-3078-463d-a689-d8e875ea6e6b" />

Terminal images
<img width="786" height="533" alt="image" src="https://github.com/user-attachments/assets/22cba200-40b6-4284-b931-b0a9c201889a" />
<img width="786" height="533" alt="Screenshot from 2025-10-20 18-07-47" src="https://github.com/user-attachments/assets/cfc565b4-dd97-47de-8726-6df606e7ac81" />
<img width="786" height="533" alt="Screenshot from 2025-10-20 18-06-17" src="https://github.com/user-attachments/assets/cdfed719-5729-4365-89b0-1da6f86dd212" />


