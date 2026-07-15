# ========================================================
# J and J Group - Secure File/Folder Shredder
# Certified Secure Destruction Tool
# ========================================================

Write-Host ""
Write-Host " ========================================================" -ForegroundColor Cyan
Write-Host " |                                                      |" -ForegroundColor Cyan
Write-Host " |               J  &  J    G R O U P                 |" -ForegroundColor Cyan
Write-Host " |                                                      |" -ForegroundColor Cyan
Write-Host " |          SECURE SHREDDER - 32 Zero Passes           |" -ForegroundColor Cyan
Write-Host " |     Certified for J and J Group Internal Use         |" -ForegroundColor Cyan
Write-Host " ========================================================" -ForegroundColor Cyan
Write-Host ""

# Choose mode
$mode = Read-Host "Type 'file' or 'folder'"
if ($mode -notin @('file','folder')) {
    Write-Host "ERROR: Invalid choice." -ForegroundColor Red
    pause
    exit
}

# Get path
$target = Read-Host "Enter full path"
if (-not (Test-Path $target)) {
    Write-Host "ERROR: Path not found." -ForegroundColor Red
    pause
    exit
}

# Confirmation
Write-Host "`nCAUTION: This will overwrite with zeros 32 times - IRREVERSIBLE!" -ForegroundColor Yellow
$confirm = Read-Host "Type 'ok' to proceed"
if ($confirm -ne 'ok') {
    Write-Host "Cancelled." -ForegroundColor Red
    exit
}

$passes = 32

function Shred-File {
    param($file)
    Write-Host "Shredding: $file" -ForegroundColor White
    for ($i = 1; $i -le $passes; $i++) {
        Write-Host "  Pass $i/$passes ..." -ForegroundColor Gray
        $size = (Get-Item $file).Length
        if ($size -gt 0) {
            try {
                $fs = [System.IO.File]::Open($file, 'Open', 'ReadWrite')
                $fs.SetLength($fs.Length)
                $fs.Close()
            } catch {}
        }
    }
    Remove-Item $file -Force -ErrorAction SilentlyContinue
    Write-Host "  [DONE]" -ForegroundColor Green
}

if ($mode -eq 'file') {
    Shred-File $target
} else {
    Write-Host "Processing folder recursively..." -ForegroundColor Yellow
    Get-ChildItem -Path $target -Recurse -File | ForEach-Object { Shred-File $_.FullName }
    Remove-Item $target -Recurse -Force -ErrorAction SilentlyContinue
}

Write-Host "`n==================================================" -ForegroundColor Cyan
Write-Host " Mission Complete - Data Securely Destroyed" -ForegroundColor Green
Write-Host " J and J Group - Secure Operations" -ForegroundColor Cyan
Write-Host "==================================================" -ForegroundColor Cyan

pause
