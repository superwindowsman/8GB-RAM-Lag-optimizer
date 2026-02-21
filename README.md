# 8GB-RAM-Lag-optimizer
This simple optimizer made in NOTEPAD actually optimizes 8gb ram pc/laptops!

---------- CODE --------







@echo off
:: Admin check
net session >nul 2>&1
if %errorlevel% neq 0 (
    echo Requesting administrator privileges...
    powershell -Command "Start-Process '%~f0' -Verb runAs"
    exit /b
)
echo info: you need admin privs, because the cmds wont work without it!
echo =========================
echo 8GB RAM Optimizer v1.0 
echo Made by 7umi.
echo This bat file was made to reduce lag on some games!
echo WARNING! i am not responsible for anything that happens to your computer!
echo SECOND WARNING! This will edit stuff on the registry editor!
echo Remember this was made for 8gb ram pcs/laptops!
echo =========================
pause

echo =========================
echo 1 - Optimize
echo 2 - Exit
echo =========================

choice /c 12 /n /m "Optimize or not: "

if errorlevel 2 goto exit
if errorlevel 1 goto optimizer

:optimizer
powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
reg add "HKCU\System\GameConfigStore" /v GameDVR_Enabled /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\GameDVR" /v AllowGameDVR /t REG_DWORD /d 0 /f
wmic computersystem where name="%computername%" set AutomaticManagedPagefile=False
wmic pagefileset where name="C:\\pagefile.sys" set InitialSize=8192,MaximumSize=12288


echo Optimized! restart your computer for the changes!
pause
goto exit

:exit
exit
