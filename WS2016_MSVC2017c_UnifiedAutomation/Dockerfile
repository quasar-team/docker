# escape=`

# Use windows server 2016 with python 2.7.15 (also installs pip)
FROM python:2.7.15-windowsservercore-ltsc2016

# Batch process in powershell
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN Install-PackageProvider -Name "Nuget" -Force; `
    Install-PackageProvider -Name "Chocolatey" -Force; `
    Install-PackageProvider -Name "ChocolateyGet" -Force; `
    Install-Package -Name "git" -Provider "Chocolatey" -Force; `
    Install-Package -Name "xsltproc, astyle" -Provider "ChocolateyGet" -Force; `
    Install-Package -Name "nuget.commandline" -Provider "Chocolatey" -RequiredVersion 4.9.1 -Force; `
    Install-Package -Name "microsoft-build-tools" -Provider "Chocolatey" -RequiredVersion 15.0.26228.0 -Force; `
    choco install cmake --version 3.12.4 --yes --installargs 'ADD_CMAKE_TO_PATH=System';

RUN md -Path 'C:\3rdPartySoftware'; `
    $Env:Path += ';C:\Chocolatey\lib\NuGet.CommandLine.4.9.1\tools'; `
    $Env:Path += ';C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin'; `
    nuget install xercesc -NonInteractive -ExcludeVersion -OutputDirectory C:\3rdPartySoftware\; `
    nuget install openssl-vc141-static-x86_64 -NonInteractive -ExcludeVersion -OutputDirectory  C:\3rdPartySoftware\; `
    nuget install boost-vc141 -Version 1.67.0 -NonInteractive -ExcludeVersion -OutputDirectory  C:\3rdPartySoftware\;
    
ENTRYPOINT ["powershell"]

RUN md -Path 'C:\Downloads'; `
    Invoke-WebRequest https://codesynthesis.com/download/xsd/4.0/windows/i686/xsd-4.0.msi -OutFile C:\Downloads\xsd-4.0.msi; `
    Start-Process 'C:\Downloads\xsd-4.0.msi' -Wait -ArgumentList /quiet; `
    if(Test-Path 'C:\Program Files (x86)\CodeSynthesis XSD 4.0\bin\xsd.exe') { `
        Write-Output 'Must change xsd.exe to xsdcxx.exe to avoid clash with built-in windows xsd.exe (on some systems)'; `
        Copy-Item -Path 'C:\Program Files (x86)\CodeSynthesis XSD 4.0\bin\xsd.exe' -Destination 'C:\Program Files (x86)\CodeSynthesis XSD 4.0\bin\xsdcxx.exe'; `
    } else { `
        Write-Output "ERROR! Failed to locate installed xsdcxx binary file, required for generating C++ handler code from XSD schema"; `
        Exit 1; `
    }; `
    Write-Output 'Installed xsdcxx';

RUN Write-Output 'Installing python packages...'; `
  python -m pip install --upgrade pip; `
  python -m pip install lxml==3.6.0 ; `
  python -m pip install pygit2; `
  python -m pip install enum34; `
  Write-Output 'Installed python packages';

RUN Write-Output 'Extending path var and adding environment variables...' `
  refreshenv; `
  [Environment]::SetEnvironmentVariable('Path', $env:Path + ';C:\Program Files\Git\bin;C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin;C:\Program Files (x86)\CodeSynthesis XSD 4.0\bin', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('QUASAR_TEST_PROJECT_DIR', 'C:\workspace\OPC-UA\quasar-test-project', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('CODE_SYNTHESYS_XSD_PATH_HEADERS', 'C:\Program Files (x86)\CodeSynthesis XSD 4.0\include', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('BOOST_PATH_HEADERS', 'C:\3rdPartySoftware\boost\lib\native\include', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('BOOST_PATH_LIBS', 'C:\3rdPartySoftware', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('OPENSSL_PATH_HEADERS', 'C:\3rdPartySoftware\openssl-vc141-static-x86_64\build\native\include', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('OPENSSL_PATH_LIBS', 'C:\3rdPartySoftware\openssl-vc141-static-x86_64\build\native\lib\x64\static\Release', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('XERCESC_PATH_HEADERS', 'C:\3rdPartySoftware\xercesc\build\native\include', [EnvironmentVariableTarget]::Machine); `
  [Environment]::SetEnvironmentVariable('XERCESC_PATH_LIBS', 'C:\3rdPartySoftware\xercesc\build\native\lib\x64\v110\Release', [EnvironmentVariableTarget]::Machine); `
  refreshenv; `
  ls env: ; 