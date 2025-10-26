# HNG Stage 2 - Blue/Green Deployment

# Setup
1. Copy `.env.example` to `.env`
2. Update the image URLs in `.env`
3. Run: `docker-compose up -d`

# Testing
- Check version: `curl http://localhost:8080/version`
- Trigger Blue failure: `curl -X POST http://localhost:8081/chaos/start?mode=error`
- Verify Green takes over: `curl http://localhost:8080/version`
- Stop chaos: `curl -X POST http://localhost:8081/chaos/stop`
