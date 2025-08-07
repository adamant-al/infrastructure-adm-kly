# Infrastructure

This project provides an automated ADAMANT & Klayr infrastructure deployment and management solution using Docker and Ansible. It sets up a server cluster with nodes and monitoring services.

## Overview

This infrastructure automation project consists of several key components that work together to create a robust and scalable environment:

### Components

1. **Bootstrap System**
   - Initial server setup and configuration
   - System updates and security hardening
   - Base software installation

2. **Docker Swarm Cluster**
   - Container orchestration setup
   - High availability configuration
   - Service discovery implementation

3. **Node Services**
   - Klayr node deployment and configuration
   - ADAMANT node setup and management
   - Node synchronization and maintenance

4. **Monitoring Stack**
   - Grafana for data visualization
   - Prometheus for metrics collection
   - AlertManager for notifications
   - Traefik for reverse proxy

## Structure

```
.
├── bootstrap/          # Initial server setup and configuration
├── docker_swarm/       # Docker Swarm cluster configuration
├── klayr_node/         # Klayr blockchain node setup
├── adamant_node/       # ADAMANT blockchain node setup
├── grafana/            # Grafana dashboard and visualization
├── metrics_stack/      # Monitoring and metrics collection
├── playbook.yml        # Main Ansible playbook
├── inventory.ini       # Server inventory configuration
└── ansible.cfg         # Ansible configuration
```

## Important Notes

### Hostname Changes

When changing `/etc/hostname`:

- Some containers require rebuild/restart
- Check configuration files for hostname dependencies

### Password Management

- Prometheus basic auth credentials need to be updated across all instances
- Grafana datasource configuration requires Prometheus authentication details

### Pending Tasks

- AlertManager configuration
- Traefik setup and configuration

## Prerequisites

- Ubuntu servers (target machines)
- Ansible installed on control machine
- SSH access to target servers
- Sudo privileges on target servers

## Quick Start

1. Configure `inventory.ini` with your server IPs
2. Ensure SSH access to all servers
3. Run the playbook:

   ```bash
   ansible-playbook -i inventory.ini playbook.yml
   ```

## Re-installing ADAMANT nodes

1. Run the playbook:

   ```bash
   ansible-playbook -i inventory.fix_adm.ini playbook.fix_adm.yml
   ```

## Security

- All configuration files contain example settings
- Production deployments require custom secrets and passwords
