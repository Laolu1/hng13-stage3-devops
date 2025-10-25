# HNG Stage 2 - Blue/Green Deployment

# Setup
1. Copy `.env.example` to `.env`
2. Update the image URLs in `.env`
3. Run: `docker-compose up -d`

## Testing
- Check version: `curl http://localhost:8080/version`
- Trigger Blue failure: `curl -X POST http://localhost:8081/chaos/start?mode=error`
- Verify Green takes over: `curl http://localhost:8080/version`
- Stop chaos: `curl -X POST http://localhost:8081/chaos/stop`
```

---

## **Part B: Backend.im Research Task**

This is a **research/proposal task**, not implementation. You need to write a Google Doc explaining:

### What They're Asking:
"How would you build a system where developers can deploy code to Backend.im using just Claude Code CLI (or AI tools) with minimal setup?"

### Your Google Doc Should Cover:

1. Proposed Architecture (2-3 paragraphs)
- Describe the overall system: developer → CLI → deployment platform
- Mention components: Git repos, CI/CD, container registry, hosting

**2. Tools You'd Use (with reasoning)**
```
- Git/GitHub: Version control
- Docker: Containerization
- GitHub Actions: CI/CD (free for public repos)
- Caddy/Traefik: Reverse proxy (simpler than Nginx for auto HTTPS)
- Your chosen hosting: DigitalOcean/Fly.io/Railway
```

**3. Local Setup Flow**
```
1. Developer runs: `claude-code deploy init`
2. CLI generates Dockerfile, docker-compose.yml
3. Developer commits code
4. CLI pushes to Git
5. Automated deployment triggers
```

**4. Deployment Sequence Diagram**
Draw or describe:
```
Developer → Claude CLI → Git Push → GitHub Actions → Build Image → Deploy to Server → Live URL