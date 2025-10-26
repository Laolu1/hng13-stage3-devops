
# HNG Stage 2 - Design Decisions & Implementation Notes

# Project Overview
This document explains the design decisions and implementation approach for the Blue/Green deployment system using Nginx reverse proxy.

# Architecture Decisions

# 1. Nginx Configuration Approach
Choice: Used upstream blocks with backup directive
Reasoning: 
- `backup` directive ensures Green only receives traffic when Blue fails
- `max_fails=2` and `fail_timeout=5s` provide fast failover detection
- Simple configuration that meets all requirements

Alternative Considered: 
- Using `least_conn` or `ip_hash` load balancing
- Rejected as they don't provide the required primary/backup behavior

# 2. Docker Compose Structure
Choice: Separate services for Blue, Green, and Nginx
Reasoning:
- Clear separation of concerns
- Easy to manage and scale individually
- Follows microservices best practices

# 3. Port Mapping Strategy
Choice: 
- Nginx: 8080 → 80
- Blue: 8081 → 3000  
- Green: 8082 → 3000

Reasoning:
- Meets task requirements exactly
- Allows direct access to individual services for testing
- Standard port conventions

# Key Configuration Choices

# Nginx Failover Settings
nginx
server app_blue:3000 max_fails=2 fail_timeout=5s;
server app_green:3000 backup;