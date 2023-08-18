## System Information Script (PowerShell)

**Description:** A PowerShell script that gathers and displays essential system information, including operating system version, processor details, memory, disk space, etc.

**Features:**
- Retrieves operating system details, such as version and edition.
- Fetches processor information to provide CPU model details.
- Gathers memory information, including total installed memory capacity.
- Displays available disk space on the system.
- Organizes and presents information in a readable format.

**Script Example:**

#Get System Information
$os = Get-WmiObject Win32_OperatingSystem
$cpu = Get-WmiObject Win32_Processor
$memory = Get-WmiObject Win32_PhysicalMemory
$lastBootUpTime = $os.LastBootUpTime

#Calculate Available Memory
$totalMemory = $memory | Measure-Object -Property Capacity -Sum | Select-Object -ExpandProperty Sum
$availableMemory = $os.FreePhysicalMemory * 1kb

#Display System Information
Write-Host "System Information"
Write-Host "------------------"
Write-Host "Operating System: $($os.Caption) $($os.Version)"
Write-Host "Processor: $($cpu.Name)"
Write-Host "Last Boot Time: $lastBootUpTime"
Write-Host "Available Memory: $([math]::Round($availableMemory / 1GB)) GB"
