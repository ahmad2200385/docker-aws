# Docker AWS Realtime Editor

A full-stack project with:

- `Frontend`: React + Vite + Monaco Editor
- `Backend`: Express + Socket.IO + Yjs (`y-socket.io`)
- Containerized deployment using Docker
- AWS ECS deployment (already deployed)

## Project Structure

```text
.
├─ Backend/
│  ├─ server.js
│  ├─ package.json
│  └─ public/
├─ Frontend/
│  ├─ src/
│  ├─ package.json
│  └─ vite.config.js
└─ Dockerfile
```

## Local Development

### 1) Frontend

```bash
cd Frontend
npm install
npm run dev
```

### 2) Backend

```bash
cd Backend
npm install
npm run dev
```

Backend default port: `3000`

Health check:

```bash
curl http://localhost:3000/health
```

## Docker

Build image from project root:

```bash
docker build -t docker-aws
```

Run container:

```bash
docker run -p 4000:3000 docker-aws
```

Then open:

- `http://localhost:3000`
- `http://localhost:3000/health`

## AWS ECS Deployment

This project is deployed on AWS ECS.

Typical ECS flow used for this app:

1. Build Docker image
2. Push image to ECR
3. Create/update ECS Task Definition
4. Deploy/update ECS Service
5. Configure security groups and load balancer
6. Use `/health` for container/target health checks


## Live Demo
App URL: http://docker-aws-lb-1862360322.ap-southeast-2.elb.amazonaws.com/


## Notes

- Dockerfile builds `Frontend` first, then copies `dist` output into `Backend/public`.
- Backend serves static files from `public` and also runs Socket.IO/Yjs collaboration server.

## Troubleshooting (Windows)

If you see `EPERM` or `spawn EPERM` while running npm commands:

- Close terminals/editors that may lock files
- Run terminal as Administrator
- Check antivirus protection for Node/npm folders
- Remove `node_modules` and reinstall

## License

MIT.
