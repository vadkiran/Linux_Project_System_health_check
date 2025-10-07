Linux Project
System Health Check Report Automation

This project involves creating a command-line utility to generate a comprehensive system health report on a Linux machine and packaging it for easy sharing. The entire process relies exclusively on native shell commands, effectively demonstrating proficiency in essential Linux system diagnostics, file redirection, and archival techniques. This report structure is crucial for baseline performance checks and initial troubleshooting steps.

🎯 Objective
The primary goal is to generate a detailed, multi-part system health report containing critical state information (time, kernel, memory, disk, processes, and networking) using only standard command-line tools. This practice ensures that diagnostic information can be captured reliably, even in headless or minimal system environments where graphical tools are unavailable.

🛠️ Implementation Steps & Commands
The report generation is a sequential process. All diagnostic output is captured using shell redirection (>) and placed inside the dedicated system_report directory, which is located in the user's home path (~/).

Step 1: Create Report Directory
The first step establishes the necessary, centralized structure to cleanly store all generated report files, preventing clutter in the home directory.

mkdir ~/system_report

Step 2: Generate Report Files
Each command serves a specific diagnostic purpose, capturing immutable data points about the system's current performance and configuration.

Report Component

Command Used

Output File

Diagnostic Value

Current Date & Time

date > ~/system_report/date_time.txt

date_time.txt

Provides a crucial timestamp for when the health check was performed, essential for comparing reports over time or correlating system events.

Kernel & Architecture

uname -a > ~/system_report/system_info.txt

system_info.txt

Reports the kernel version, build date, and system architecture (e.g., x86_64). This is vital for security auditing and ensuring software compatibility.

Memory Usage (Human readable)

free -h > ~/system_report/memory_usage.txt

memory_usage.txt

Shows the total, used, and available physical and swap memory in human-readable format. High swap usage or low free memory can indicate performance bottlenecks.

Disk Usage (Mounted filesystems)

df -h > ~/system_report/disk_usage.txt

disk_usage.txt

Lists disk space usage for all mounted filesystems. Monitoring the % Used column is critical to prevent system instability caused by full partitions.

Top 10 Processes (By CPU usage)

ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -11 > ~/system_report/top_processes.txt

top_processes.txt

Captures a snapshot of running processes, sorted by CPU usage in descending order. This immediately identifies potential CPU-hogging applications or rogue background tasks.

Network Interfaces

ip a > ~/system_report/network_info.txt

network_info.txt

Displays detailed configuration for all network interfaces, including IP addresses, MAC addresses, and interface state (UP/DOWN). Essential for diagnosing connectivity issues.

Step 3: Compress the Report
The final step archives the entire contents of the system_report directory into a single, compressed file using the popular tar utility with Gzip compression. This is standard practice for transferring diagnostic data.

tar -czvf system_report.tar.gz ~/system_report/

The flags used (c for create, z for gzip compression, v for verbose output, and f for file name) are the most common combination for creating portable archives.

📂 Verification
To verify that the project was executed correctly and all files were successfully generated and archived, run the following verification commands:

Check the compressed file size and creation:

ls -lh system_report.tar.gz


This confirms the archive file exists and shows its size in a human-readable format.

Verify the contents of a specific generated file (e.g., memory):

cat ~/system_report/memory_usage.txt


Viewing the file directly confirms the command executed correctly and that the data was successfully redirected and persisted.

Confirm all files were captured within the archive:

tar -tf system_report.tar.gz


This command lists the table of contents (t) of the compressed file, ensuring no critical diagnostic reports were missed during the archival process.
