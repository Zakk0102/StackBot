# Docker Setup for AAI Project

This project includes Docker configuration for both frontend and backend services.

## Prerequisites

- Docker
- Docker Compose
- Environment variables for Azure services

## Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
AZURE_OPENAI_API_KEY=your_azure_openai_api_key
AZURE_OPENAI_ENDPOINT=your_azure_openai_endpoint
AZURE_OPENAI_DEPLOYMENT_NAME=your_azure_openai_deployment_name
AZURE_OPENAI_API_VERSION=2023-05-15
AZURE_SPEECH_KEY=your_azure_speech_key
AZURE_SPEECH_REGION=your_azure_speech_region
```

## Quick Start

1. **Build and run all services:**
   ```bash
   docker-compose up --build
   ```

2. **Run in detached mode:**
   ```bash
   docker-compose up -d --build
   ```

3. **Stop all services:**
   ```bash
   docker-compose down
   ```

## Services

### Frontend (React + Vite + Three.js)
- **Port:** 3000
- **URL:** http://localhost:3000
- **Technology Stack:**
  - React 18
  - Vite
  - Three.js
  - React Three Fiber
  - Tailwind CSS

### Backend (FastAPI + Python)
- **Port:** 8000
- **URL:** http://localhost:8000
- **Technology Stack:**
  - FastAPI
  - Python 3.11
  - Azure OpenAI
  - Azure Speech Services
  - Rhubarb Lip Sync
  - LangChain

## Individual Service Commands

### Build Frontend Only
```bash
cd frontend
docker build -t aai-frontend .
```

### Build Backend Only
```bash
cd backend
docker build -t aai-backend .
```

### Run Frontend Only
```bash
docker run -p 3000:80 aai-frontend
```

### Run Backend Only
```bash
docker run -p 8000:8000 --env-file .env aai-backend
```

## Development

### Frontend Development
For development with hot reload:
```bash
cd frontend
npm install
npm run dev
```

### Backend Development
For development with auto-reload:
```bash
cd backend
pip install -r requirements.txt
uvicorn app:app --reload --host 0.0.0.0 --port 8000
```

## Volumes

The backend service mounts the `./backend/audios` directory to persist audio files generated during lip sync processing.

## Troubleshooting

1. **Port conflicts:** Make sure ports 3000 and 8000 are available
2. **Environment variables:** Ensure all required Azure environment variables are set
3. **Rhubarb issues:** The Dockerfile automatically downloads and configures Rhubarb Lip Sync
4. **Build issues:** Clear Docker cache with `docker system prune -a`

## Production Deployment

For production deployment, consider:
- Using a reverse proxy (nginx)
- Setting up SSL certificates
- Using Docker secrets for sensitive environment variables
- Implementing health checks
- Setting up monitoring and logging 