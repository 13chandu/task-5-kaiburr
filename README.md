# task-5-kaiburr
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      - name: Build Application
        run: |
          # Replace with your build commands (e.g., npm install and npm build)
          npm install
          npm run build

      - name: Build Docker Image
        run: |
          # Replace with your Docker build commands
          docker build -t your-docker-image-name:latest .

      - name: Push Docker Image to Container Registry
        run: |
          # Replace with your Docker registry login and push commands
          echo ${{ secrets.DOCKERHUB_TOKEN }} | docker login -u ${{ secrets.DOCKERHUB_USERNAME }} --password-stdin
          docker push your-docker-image-name:latest
