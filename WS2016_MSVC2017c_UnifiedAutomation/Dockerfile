# escape=`

# Use the latest Windows Server Core image with .NET Framework 4.7.1.
FROM microsoft/windowsservercore

# Batch process in powershell
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN Install-PackageProvider -Name "Nuget" -Force; `
    Install-PackageProvider -Name "Chocolatey" -Force; `
    Install-PackageProvider -Name "ChocolateyGet" -Force; `
    Install-Package -Name "git" -Provider "Chocolatey" -Force; `
    Install-Package -Name "xsltproc, astyle" -Provider "ChocolateyGet" -Force; `
    Install-Package -Name "nuget.commandline" -Provider "Chocolatey" -RequiredVersion 4.9.1 -Force; `
    Install-Package -Name "microsoft-build-tools" -Provider "Chocolatey" -RequiredVersion 15.0.26228.0 -Force; 

RUN md -Path 'C:\3rdPartySoftware'; `
    $Env:Path += ';C:\Chocolatey\lib\NuGet.CommandLine.4.9.1\tools'; `
    $Env:Path += ';C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin'; `
    nuget install xercesc -NonInteractive -ExcludeVersion -OutputDirectory C:\3rdPartySoftware\; `
    nuget install openssl-vc141-static-x86_64 -NonInteractive -ExcludeVersion -OutputDirectory  C:\3rdPartySoftware\; `
    nuget install boost-vc141 -Version 1.67.0 -NonInteractive -ExcludeVersion -OutputDirectory  C:\3rdPartySoftware\;
    
ENTRYPOINT ["powershell"]

### Download the Build Tools bootstrapper.
##ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe
##
### Download the nuget installer
##ADD https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe C:\Nuget\nuget.exe
##
### Install Build Tools excluding workloads and components with known issues.
##RUN `
##  Start-Process C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
##    --installPath C:\BuildTools `
##    --includeRecommended `
##    --add Microsoft.VisualStudio.Product.BuildTools; `
##  rm C:\TEMP\vs_buildtools.exe
##
##RUN `
##  Start-Process C:\BuildTools\Common7\Tools\VsDevCmd.bat ;`
##  msbuild /?
##
### Add nuget to path and test
##RUN setx /M PATH $($Env:PATH + ';C:\Nuget\')
##RUN `
##  C:\Nuget\nuget help
##
### Start developer command prompt with any other commands specified.
##ENTRYPOINT C:\BuildTools\Common7\Tools\VsDevCmd.bat &&
##
### Default to PowerShell if no other command specified.
##CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
