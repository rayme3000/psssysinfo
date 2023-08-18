# Powershell System Info Script
System Information Script: A Powershell script that gathers and displays essential system information such as operating system version, processor details, memory, disk space, etc.

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
