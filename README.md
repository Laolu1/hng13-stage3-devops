# HNG Stage 3 - Blue/Green Deployment with Observability & Alerts

## Project Overview
This project extends the Stage 2 Blue/Green deployment with comprehensive observability and Slack alerts. It automatically monitors Nginx logs, detects failovers and error rates, and sends real-time alerts to Slack.

## Features
- **Blue/Green Deployment**: Automatic failover between two identical services
- **Real-time Monitoring**: Python log watcher tails Nginx access logs
- **Slack Alerts**: Automatic notifications for failovers and high error rates
- **Error Rate Tracking**: Sliding window calculation for 5xx errors
- **Fast Failover**: Sub-3 second automatic switch between pools
- **Dockerized**: Complete Docker Compose setup



