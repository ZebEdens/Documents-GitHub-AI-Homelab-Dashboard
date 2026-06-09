# Documents-GitHub-AI-Homelab-Dashboard
PowerShell-based monitoring dashboard for a Raspberry Pi homelab, providing automated health reporting for Docker containers, Ollama AI services, NAS storage, and system performance via SSH.
AI Homelab Dashboard

A PowerShell-based monitoring dashboard for a Raspberry Pi homelab.

Features
SSH-based remote monitoring
CPU utilization reporting
RAM utilization reporting
Disk and NAS capacity monitoring
Raspberry Pi temperature monitoring
Docker container status
Ollama model inventory
Tailscale connectivity monitoring
HTML dashboard generation
Environment
Raspberry Pi 5
Raspberry Pi OS
Docker
Portainer
Ollama
Open WebUI
Tailscale
Samba NAS
Requirements
Windows PowerShell
SSH key authentication
Raspberry Pi running Linux
Usage
.\AI-Homelab-Dashboard.ps1

The script connects to the Raspberry Pi over SSH, gathers system information, and generates an HTML dashboard.
