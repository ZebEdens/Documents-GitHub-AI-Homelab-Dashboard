# AI Homelab PowerShell Dashboard

$PiUser = "YOUR_PI_USERNAME"
$PiHost = "YOUR_PI_IP"  
$ReportPath = "$env:USERPROFILE\Desktop\AI-Homelab-Dashboard.html"

function Run-PiCommand {
    param([string]$Command)

    try {
        ssh "$PiUser@$PiHost" $Command
    }
    catch {
        "ERROR: Unable to run command"
    }
}

$Date = Get-Date -Format "yyyy-MM-dd HH:mm:ss"

$Hostname = Run-PiCommand "hostname"
$Uptime = Run-PiCommand "uptime -p"
$CpuLoad = Run-PiCommand "top -bn1 | grep 'Cpu'"
$RamUsage = Run-PiCommand "free -h"
$DiskUsage = Run-PiCommand "df -h / /mnt/nas"
$Temperature = Run-PiCommand "vcgencmd measure_temp"
$DockerContainers = Run-PiCommand "docker ps --format 'table {{.Names}}\t{{.Status}}\t{{.Ports}}'"
$OllamaModels = Run-PiCommand "ollama list"
$TailscaleStatus = Run-PiCommand "tailscale status --self | awk '{print `$1, `$2}'"

$html = @"
<html>
<head>
<title>AI Homelab Dashboard</title>
<style>
body {
    font-family: Arial;
    background-color: #111827;
    color: #f9fafb;
    padding: 20px;
}
h1 {
    color: #38bdf8;
}
.card {
    background-color: #1f2937;
    padding: 18px;
    margin: 15px 0;
    border-radius: 10px;
}
pre {
    background-color: #030712;
    color: #e5e7eb;
    padding: 12px;
    border-radius: 8px;
    overflow-x: auto;
}
.good {
    color: #22c55e;
    font-weight: bold;
}
</style>
</head>
<body>

<h1>AI Homelab Status Dashboard</h1>
<p>Last Updated: $Date</p>

<div class="card">
<h2>Raspberry Pi</h2>
<p>Status: <span class="good">Online</span></p>
<pre>Hostname: $Hostname
Uptime: $Uptime</pre>
</div>

<div class="card">
<h2>CPU Usage</h2>
<pre>$CpuLoad</pre>
</div>

<div class="card">
<h2>RAM Usage</h2>
<pre>$RamUsage</pre>
</div>

<div class="card">
<h2>Disk and NAS Capacity</h2>
<pre>$DiskUsage</pre>
</div>

<div class="card">
<h2>Pi Temperature</h2>
<pre>$Temperature</pre>
</div>

<div class="card">
<h2>Docker Containers</h2>
<pre>$DockerContainers</pre>
</div>

<div class="card">
<h2>Ollama Models</h2>
<pre>$OllamaModels</pre>
</div>

<div class="card">
<h2>Tailscale Status</h2>
<pre>$TailscaleStatus</pre>
</div>

</body>
</html>
"@

$html | Out-File -FilePath $ReportPath -Encoding UTF8

Start-Process "chrome.exe" $ReportPath

Write-Host "Dashboard created at $ReportPath"
