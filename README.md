Used Car Price Prediction Web Application — Assignment 2
An end-to-end Machine Learning web application designed to predict used car prices based on user-inputted vehicle specifications. The application is containerized using Docker and deployed on the AIT CSIM ml-brain Server integrated with Traefik Reverse Proxy.
🔗 Live Demo & Deployment Information
Live Web App URL: https://st127260.ml.brain.cs.ait.ac.th
Docker Hub Image: nchau2201/car-price-a2:v2
Student ID: st127260
🛠 Features & System Architecture
Interactive User Interface: Developed using Dash / Plotly (Flask backend), enabling users to enter vehicle specifications (year of manufacture, mileage driven, fuel type, engine capacity, max power, etc.) and receive real-time price predictions.
Model Inference: Leverages a pre-trained Machine Learning model (.pkl / .joblib) to process input features and generate price predictions.
Containerization: Packaged with all necessary dependencies inside a lightweight Docker container built for the linux/amd64 architecture.
Reverse Proxy & Security: Automatically routed through Traefik Proxy on the server with SSL/TLS certificate resolution.
📂 Project Structure
.
├── app.py                 # Entry point running the Dash/Flask web application
├── models.py              # Model architecture and preprocessing pipelines
├── car_price_model.joblib # Serialized Machine Learning model file
├── requirements.txt       # Python package dependencies
├── Dockerfile             # Docker image configuration
├── docker-compose.yml     # Orchestration and Traefik routing configuration
└── README.md              # Project documentation and deployment setup


🚀 Local Setup & Docker Execution
To build and run the application locally from the root folder of this project:
1. Build the Docker Image
docker build -t car-price-app .
2. Run the Container
docker run -p 8050:8050 car-price-app
Once running, access the application locally at http://localhost:8050.
🌐 Server Deployment Setup (AIT ml-brain)
The following steps were executed to deploy the web application to the server environment:
Build Cross-Platform Image (linux/amd64):
docker buildx build --platform linux/amd64 -t nchau2201/car-price-a2:v2 --push .
Server Configuration (docker-compose.yml):
version: '3.8'
services:
  web:
    image: nchau2201/car-price-a2:v2
    container_name: app_a2-web-1
    restart: always
    expose:
      - "8050"
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.st127260.rule=Host(`st127260.ml.brain.cs.ait.ac.th`)"
      - "traefik.http.routers.st127260.entrypoints=websecure"
      - "traefik.http.routers.st127260.tls.certresolver=myresolver"
      - "traefik.http.services.st127260.loadbalancer.server.port=8050"
    
Deploy Container on Server:
docker compose up -d
📝 Author & Course Information
Student Name: Nguyen Cong Hau
Student ID: st127260
Course: Machine Learning / Machine Learning Web Application Deployment
Institution: Asian Institute of Technology (AIT)
