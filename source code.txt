@echo off
title Tunn6x Tweaks Utility 9.1 - FREE Edition
mode con: cols=100 lines=40
color 1F
cls

:menu

echo.
echo               Tunn6x Tweaks Utility 9.1 - FREE VERSION                           

echo  Unlock 10x more tweaks and unlock your PC's full potential                             
                                                                




:: MENU
echo ======================== Main Menu ========================
echo [1]  General System Optimizations
echo [2]  Power Optimizations
echo [3]  Mouse and Keyboard Tweaks
echo [4]  GPU Optimizations
echo [5]  CPU Optimizations
echo [6]  PC Clean-Up
echo [7]  System Debloat
echo [8]  Storage Optimizations
echo [9]  Memory Optimizations
echo [10] Tunn6x Network Tweaking Utility
echo ------------------------------------------------------------
echo [F]  Fixes and Reverts
echo [W]  Completely Optimize Your PC
echo [R]  Use Restore Point
echo [P]  View Patch Notes
echo [E]  Join The Discord
echo [T]  Apply All Tweaks
color 1F
echo [X]  Exit Utility
echo ============================================================
echo.

:: USER CHOICE
set /p choice=Enter your option: 
call :handleChoice %choice%
goto menu

:handleChoice
if /i "%~1"=="1" goto general
if /i "%~1"=="2" goto power
if /i "%~1"=="3" goto mousekb
if /i "%~1"=="4" goto gpu
if /i "%~1"=="5" goto cpu
if /i "%~1"=="6" goto pcclean
if /i "%~1"=="7" goto debloat
if /i "%~1"=="8" goto storage
if /i "%~1"=="9" goto memory
if /i "%~1"=="10" goto network
if /i "%~1"=="F" goto fixes
if /i "%~1"=="W" goto fulloptimize
if /i "%~1"=="R" goto restore
if /i "%~1"=="P" goto patch
if /i "%~1"=="E" start https://discord.gg/tunn6x & goto menu
if /i "%~1"=="X" exit
echo Invalid option. Try again.
pause >nul
cls
exit /b

:: Progress bar function
:progress
setlocal enabledelayedexpansion
set "bar="
for /L %%A in (1,1,%1) do (
    set "bar=!bar!#"
    cls
    echo Applying tweaks: [!bar!]
    timeout /nobreak /t 1 >nul
)
endlocal
exit /b

:: SECTIONS (real code implementation)
:general
echo Running General System Optimizations...
call :progress 10
echo Disabling unnecessary startup programs...
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v "OneDrive" /f /d ""
echo Disabling Windows animations...
reg add "HKCU\Control Panel\Desktop\WindowMetrics" /v "MinAnimate" /t REG_SZ /d "0" /f
echo General optimizations applied successfully.
pause >nul
cls
goto menu

:power
echo Applying Power Optimizations...
call :progress 10
echo Setting power plan to High Performance...
powercfg -setactive SCHEME_MIN
echo Disabling USB selective suspend...
powercfg -setacvalueindex SCHEME_CURRENT SUB_USB USBSELECTIVESETTING 0
powercfg -setdcvalueindex SCHEME_CURRENT SUB_USB USBSELECTIVESETTING 0
echo Power optimizations applied successfully.
pause >nul
cls
goto menu

:mousekb
echo Tuning Mouse & Keyboard...
call :progress 10
echo Adjusting mouse sensitivity...
reg add "HKCU\Control Panel\Mouse" /v "MouseSensitivity" /t REG_SZ /d "10" /f
echo Disabling mouse acceleration...
reg add "HKCU\Control Panel\Mouse" /v "MouseSpeed" /t REG_SZ /d "0" /f
reg add "HKCU\Control Panel\Mouse" /v "MouseThreshold1" /t REG_SZ /d "0" /f
reg add "HKCU\Control Panel\Mouse" /v "MouseThreshold2" /t REG_SZ /d "0" /f
echo Mouse & Keyboard tweaks applied successfully.
pause >nul
cls
goto menu

:gpu
echo Optimizing GPU...
call :progress 10
echo Adjusting GPU power settings...
reg add "HKLM\SYSTEM\CurrentControlSet\Control\GraphicsDrivers" /v "TdrDelay" /t REG_DWORD /d "10" /f
echo GPU optimizations applied successfully.
pause >nul
cls
goto menu

:cpu
echo Optimizing CPU...
call :progress 10
echo Disabling CPU core parking...
powercfg -attributes SUB_PROCESSOR CPMAXCORES -ATTRIB_HIDE
powercfg -setacvalueindex SCHEME_CURRENT SUB_PROCESSOR CPMAXCORES 100
powercfg -setdcvalueindex SCHEME_CURRENT SUB_PROCESSOR CPMAXCORES 100

echo Adjusting processor performance settings...
powercfg -setacvalueindex SCHEME_CURRENT SUB_PROCESSOR PROCTHROTTLEMAX 100
powercfg -setdcvalueindex SCHEME_CURRENT SUB_PROCESSOR PROCTHROTTLEMAX 100

echo Enabling ultimate performance power plan...
powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
powercfg -setactive e9a42b02-d5df-448d-aa00-03f14749eb61

echo CPU optimizations applied successfully.
pause >nul
cls
goto menu

:pcclean
echo Performing PC Cleanup...
call :progress 10
echo Clearing temporary files...
del /q /f /s "%TEMP%\*"
echo Cleaning up system files...
cleanmgr /sagerun:1
echo PC cleanup completed successfully.
pause >nul
cls
goto menu

:debloat
echo Removing bloatware...
call :progress 10
echo Uninstalling Xbox app...
powershell -Command "Get-AppxPackage *xbox* | Remove-AppxPackage"
echo Disabling Cortana...
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" /v "AllowCortana" /t REG_DWORD /d "0" /f
echo Debloat completed successfully.
pause >nul
cls
goto menu

:storage
echo Optimizing Storage...
call :progress 10
echo Enabling NTFS memory optimization...
fsutil behavior set memoryusage 2
echo Storage optimizations applied successfully.
pause >nul
cls
goto menu

:memory
echo Tweaking Memory Settings...
call :progress 10
echo Enabling large system cache...
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" /v "LargeSystemCache" /t REG_DWORD /d "1" /f
echo Memory tweaks applied successfully.
pause >nul
cls
goto menu

:network
echo Launching Network Tweaking Utility...
call :progress 10
echo Disabling network throttling...
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "NetworkThrottlingIndex" /t REG_DWORD /d "ffffffff" /f
echo Network tweaks applied successfully.
pause >nul
cls
goto menu

:fixes
echo Opening Fixes & Reverts...
call :progress 10
echo Restoring default power plan...
powercfg -setactive SCHEME_BALANCED
echo Fixes applied successfully.
pause >nul
cls
goto menu

:fulloptimize
echo Running Complete PC Optimization...
call :progress 10
call :general
call :power
call :mousekb
call :gpu
call :cpu
call :pcclean
call :debloat
call :storage
call :memory
call :network
echo Complete PC optimization completed successfully.
pause >nul
cls
goto menu

:restore
echo Launching System Restore...
start SystemPropertiesProtection.exe
pause >nul
cls
goto menu

:patch
echo Tunn6x Tweaks v9.1 Patch Notes:
echo - Improved menu UI
echo - Bug fixes and performance enhancements
echo - Added more deep tweaks (pro version)
pause >nul
cls
goto menu
