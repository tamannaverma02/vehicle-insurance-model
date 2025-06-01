# Vehicle Insurance Prediction with End-to-End CI/CD Deployment on AWS

This project predicts whether a customer will opt for vehicle insurance based on various input features using a machine learning model. Beyond the model, the focus here is on building a complete MLOps pipeline with automated CI/CD, Docker, and deployment on AWS infrastructure.

## Tech Stack

- Python 3.10
- Scikit-learn, Pandas, NumPy
- MongoDB Atlas for data storage
- AWS S3, EC2, ECR, IAM for cloud services
- FastAPI + Jinja2 for web interface
- GitHub Actions for CI/CD
- Docker for containerization

## Key Features
----------------

- End-to-end ML lifecycle: ingestion → validation → transformation → training → evaluation → deployment
- Modular and scalable codebase (follows clean architecture)
- MongoDB Atlas integration for data storage
- AWS S3 model registry and model push/pull
- CI/CD with GitHub Actions and self-hosted EC2 runner
- Web UI built with FastAPI and Jinja2
- Dockerized application deployed on EC2 with exposed port access

## 📁 Project Structure
-------------------
```
vehicle-insurance-model 
├── .github/workflows/   # CI/CD workflow files 
├── Dockerfile # Docker image build 
├── app.py # FastAPI app for web interface 
├── src/ # Source code (core logic) 
│   ├── components/ # ML components like training, ingestion, etc. 
│   ├── entity/ # Configs and data schema definitions 
│   ├── configuration/ # AWS and MongoDB connection setups 
│   ├── utils/ # Utility functions 
│   └── aws_storage/ # S3 interaction code 
├── templates/ # HTML templates (Jinja2)
├── static/ # Static assets (CSS, images) 
├── notebook/ # EDA and MongoDB data loading notebooks 
├── requirements.txt # Python dependencies 
├── setup.py # Local package installation 
├── pyproject.toml # Metadata and build system info 
└── README.md # You're here!
```

## 🧱 Step-by-Step Workflow
------------------------
## ✅ Project Setup

Install Packages:

`conda create -n vehicle python=3.10 -y`
`conda activate vehicle`
`pip install -r requirements.txt`

MongoDB Integration:

Setup MongoDB Atlas project & cluster

Configure access (0.0.0.0/0) and retrieve connection string

Load dataset from notebook to MongoDB collection

## ⚙️ ML Pipeline Components
------------------------
- Data Ingestion: Loads data from MongoDB into a DataFrame
- Data Validation: Validates data based on schema.yaml
- Data Transformation: Scales/encodes features for modeling
- Model Training: Trains a classifier using scikit-learn
- Model Evaluation: Compares new model with existing S3 version
- Model Pusher: Pushes best model to S3 model registry

## 🌐 FastAPI Web Interface
------------------------
Run the app locally:

`uvicorn app:app --host 0.0.0.0 --port 5050`
Navigate to `http://localhost:5000` to access the web UI.

## 🔄 CI/CD & AWS Integration
------------------------
## Docker & GitHub Actions
Dockerfile sets up a lightweight image for deployment

GitHub Actions triggers Docker build → pushes to AWS ECR

EC2 (Ubuntu) instance acts as a self-hosted runner

## AWS Setup
ECR: Container image repository

EC2: Hosts and serves the Docker container

S3: Model registry for evaluated models

IAM: Access control for programmatic access

## ⚙️ CI/CD Pipeline Overview
Push code to GitHub

GitHub Actions builds Docker image

Image pushed to ECR

EC2 instance (self-hosted runner) pulls and runs the container

App live at `http://107.22.132.74:5000/`

## 📦 Training Endpoint
------------------------
To retrain the model manually:

`http://107.22.132.74:5000/training`

## 🔐 Secrets Management
------------------------
GitHub Repository → Settings → Secrets and Variables:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

AWS_DEFAULT_REGION

ECR_REPO

## 📈 Sample Inputs for Prediction
------------------------
| Feature                | Type    | Example       |
|------------------------|---------|---------------|
| Age                    | Integer | 45            |
| Gender                 | String  | Male          |
| Vehicle_Age            | String  | > 2 Years     |
| Previously_Insured     | Boolean | 1             |
| Annual_Premium         | Float   | 30000.0       |
| Policy_Sales_Channel   | Integer | 152           |

## Final Deployment Link
------------------------

`http://107.22.132.74:5000/`

