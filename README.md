# System Monitoring Script - README

## Overview

This Bash script provides system monitoring capabilities, including CPU usage, memory usage, network activity, and disk usage. It supports sending alerts via email when CPU usage exceeds a defined threshold. The script also allows logging of system metrics to a file.

## Features

- **CPU Usage Monitoring:** Alerts when CPU usage exceeds the specified threshold.
- **Memory (RAM) Usage Monitoring**
- **Network Activity Monitoring:** Tracks download and upload rates.
- **Disk Usage Monitoring**
- **Process Monitoring:** Displays the top 3 processes by CPU usage.
- **Logging:** Logs system metrics to a file at regular intervals.
- **Email Alerts:** Sends email alerts for high CPU usage.

## Usage

### Command Line Options

- `-n`: Enable network monitoring.
- `-s`: Silent mode, disables email alerts.
- `-log`: Enable logging to a file.
- `--mail EMAIL`: Set the email address for alerts.
- `--alert LEVEL`: Set the CPU usage threshold for alerts (0-100).
- `--nodisk`: Disable disk usage monitoring.
- `-h`, `--help`: Show usage information.

### Example Usage

```bash
./monitor.sh -n --mail your-email@example.com --alert 80 -log
```

This command enables network monitoring, sets the email for alerts to `your-email@example.com`, sets the CPU alert threshold to 80%, and enables logging.

### Email and Threshold Validation

- Email addresses are validated using a regex pattern.
- CPU alert thresholds must be an integer between 1 and 100.

## Alert Mechanism

When CPU usage exceeds the defined threshold, an alert email is sent. The email configuration uses SMTP with the Gmail server. Adjust the `smtp_server`, `smtp_port`, `from`, and `password` variables in the `send_alert` function as needed.

## Logging

Logs are saved to a file named `MONITOR_dd_mm_YYYY.log` in the script's directory. The log interval is set to 60 seconds by default.

## Script Details

### Functions

- `usage`: Displays the help message.
- `send_alert`: Sends an email alert when CPU usage exceeds the threshold.
- `network`: Monitors network activity.
- `ram`: Monitors RAM usage.
- `cpu`: Monitors CPU usage.
- `uptime_f`: Gets system uptime.
- `processes`: Lists the top 3 processes by CPU usage.
- `log_data`: Logs the current system metrics to a file.
- `disk`: Monitors disk usage.
- `center_text`: Centers text in the terminal.

### Variables

- `CPU_LEVEL`: CPU usage threshold for alerts (default: 90).
- `NETWORK`: Enable network monitoring (default: false).
- `SILENT`: Disable email alerts (default: true).
- `LOGS`: Enable logging (default: false).
- `NO_DISK`: Disable disk usage monitoring (default: false).
- `GREEN_THRESHOLD`: Threshold for green color in usage (default: 50).
- `ORANGE_THRESHOLD`: Threshold for orange color in usage (default: 80).
- `SLEEP_TIME`: Sleep time between monitoring cycles (default: 5 seconds).
- `ALERT_INTERVAL`: Minimum interval between alerts (default: 180 seconds).
- `LOG_INTERVAL`: Interval between log entries (default: 60 seconds).

## Exit Handling

The script hides the cursor during execution and shows it upon exit using the `trap` command to ensure a clean exit.

## Author

Mikołaj Wiszniewski

---

For additional details, refer to the script source code and the inline comments explaining each function and variable.
