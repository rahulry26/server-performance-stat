[project url] (https://roadmap.sh/projects/server-stats)
# Requirements
You are required to write a script server-stats.sh that can analyse basic server performance stats. You should be able to run the script on any Linux server and it should give you the following stats:

Total CPU usage
Total memory usage (Free vs Used including percentage)
Total disk usage (Free vs Used including percentage)
Top 5 processes by CPU usage
Top 5 processes by memory usage
Stretch goal: Feel free to optionally add more stats such as os version, uptime, load average, logged in users, failed login attempts etc.

# server-performance-stat
step1:Created the vm on the portal with linux version
step2:connected with putty
step3: created server-stat.sh file
step4: written the script in server-stat.sh file which as pasted below
---------------------------------------------------------------------------------------
"#!/bin/bash
# server-stats.sh - Script to analyze basic server performance stats

echo "=== Server Stats ==="

# CPU Usage
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
echo "Total CPU Usage: $cpu_usage%"

# Memory Usage
mem_info=$(free -m | awk 'NR==2{printf "Used: %sMB, Free: %sMB (%.2f%%)\n", $3, $4, $3*100/$2 }')
echo "Memory Usage: $mem_info"

# Disk Usage
disk_usage=$(df -h --total | awk '/^total/{printf "Used: %s, Free: %s, Usage: %s\n", $3, $4, $5}')
echo "Disk Usage: $disk_usage"

# Top 5 Processes by CPU
echo "Top 5 Processes by CPU Usage:"
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6

# Top 5 Processes by Memory
echo "Top 5 Processes by Memory Usage:"
ps -eo pid,comm,%mem --sort=-%mem | head -n 6

# OS Version
os_version=$(cat /etc/os-release | grep -w "PRETTY_NAME" | cut -d= -f2 | tr -d '"')
echo "OS Version: $os_version"

# Uptime
uptime_info=$(uptime -p)
echo "Uptime: $uptime_info"

# Load Average
load_avg=$(uptime | awk -F'load average:' '{ print $2 }')
echo "Load Average: $load_avg"

# Logged-in Users
logged_users=$(who | wc -l)
echo "Logged-in Users: $logged_users"

# Failed Login Attempts
failed_logins=$(grep "Failed password" /var/log/auth.log | wc -l)
echo "Failed Login Attempts: $failed_logins"
----------------------------------------------------------------------------------------------------------------------------------------

after running the above script using the "./server-stat.sh" cmd got the output as:
![image](https://github.com/user-attachments/assets/c9f31f58-65bd-4809-86e7-9a666a7e7548)
