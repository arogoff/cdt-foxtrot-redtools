Persistent Netcat Listeners
This repository contains scripts for deploying persistent netcat listeners across the CDT-Foxtrot infrastructure using Ansible. It creates multiple listening ports that maintain persistent connections and can collect logs from compromised systems.
Repository Contents

listener.sh - The main bash script that creates multiple netcat listeners on random ports
red.yml - Ansible playbook for deploying the listener script to target systems
rsys1og.service - Systemd service file for ensuring the listener script runs persistently

How It Works
Listener Script (listener.sh)
This bash script establishes multiple persistent netcat listeners:

Creates 50 listeners on random ports between 1024-65535
Each listener uses a named pipe to maintain persistence
Commands received are executed via bash and output is returned to the connecting client
Logs active ports to /etc/.rc6.d/nc_listeners.log
Creates an additional listener on port 9999 that serves the last 50 entries from the log file

Deployment Playbook (red.yml)
The Ansible playbook automates deployment to target systems:

Installs the netcat-openbsd package
Copies the listener script to /etc/apt/.p.sh
Sets up a systemd service to ensure the script runs persistently

Systemd Service (rsys1og.service)
This service file ensures the script runs persistently:

Starts the script after network services are available
Automatically restarts if the process terminates
Runs with root privileges
Hides standard output and error streams

Installation

Clone this repository
Ensure you have Ansible installed
Update the hosts in red.yml to target your systems
Run the Ansible playbook:

bash
