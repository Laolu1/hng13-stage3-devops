# Blue/Green Deployment Runbook

## Alert Types and Responses

### 1. Failover Alert
**Message**: "Failover detected: blue → green"
**What it means**: The primary pool (Blue) became unhealthy and traffic automatically switched to backup (Green)

**Operator Actions**:
1. Check Blue container health: `docker-compose logs app_blue`
2. Verify Green is handling traffic: `curl http://localhost:8080/version`
3. Investigate why Blue failed (check resources, logs, chaos testing)
4. When Blue is healthy, it will automatically resume as primary

### 2. High Error Rate Alert
**Message**: "High error rate: 5.5% (threshold: 2%)"
**What it means**: More than 2% of requests are returning 5xx errors

**Operator Actions**:
1. Check application logs: `docker-compose logs app_blue app_green`
2. Verify infrastructure health (CPU, memory, disk)
3. Check if this is expected (chaos testing, deployments)
4. Consider manual failover if errors persist

### 3. Recovery (Automatic)
**No alert sent** - When Blue becomes healthy again, traffic automatically returns to it

## Maintenance Procedures

### Planned Maintenance
Before planned maintenance that might cause errors:
1. Set `ACTIVE_POOL=green` in .env file
2. Restart services: `docker-compose restart`
3. Perform maintenance on Blue
4. Switch back when ready

### Manual Failover
```bash
# Switch to Green manually
export ACTIVE_POOL=green
docker-compose up -d

# Switch back to Blue
export ACTIVE_POOL=blue
docker-compose up -d