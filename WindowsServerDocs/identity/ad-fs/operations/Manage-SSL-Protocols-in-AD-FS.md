---
title: AD FS에 대 한 SSL/TLS 프로토콜 및 암호 그룹 관리
description: AD FS 2016에 대 한 질문과 대답
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e834c50965c3af569dbe3756d677ec4cb2372542
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883924"
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>AD FS에 대 한 SSL/TLS 프로토콜 및 암호 그룹 관리
다음 문서 특정 TLS/SSL 프로토콜을 사용 하도록 설정 및 AD FS에서 사용 되는 암호 그룹 사용 하지 않도록 설정 하는 방법에 정보를 제공 합니다.

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>AD FS에서 TLS/SSL, SChannel 및 암호 그룹

전송 계층 보안 (TLS)와 Secure Sockets Layer (SSL)는 보안 통신을 위해 제공 하는 프로토콜입니다.  Active Directory Federation Services 통신에 이러한 프로토콜을 사용 합니다.  현재 이러한 프로토콜의 여러 버전이 존재 합니다.

Schannel은 SSL, TLS 및 DTLS 인터넷 표준 인증 프로토콜을 구현한 SSP(Security Support Provider)입니다. SSPI(Security Support Provider Interface)는 인증을 비롯한 보안 관련 기능을 수행하기 위해 Windows 시스템에서 사용되는 API입니다. SSPI는 Schannel SSP를 포함한 몇몇 SSP(Security Support Provider)의 공용 인터페이스로 사용됩니다.

암호 그룹은 암호화 알고리즘 집합입니다. 키를 만들고 정보를 암호화할 암호 도구 모음에서 알고리즘을 사용 하는 TLS/SSL 프로토콜은 schannel SSP 구현 합니다. 암호 그룹은 다음 작업에 대해 각각 하나의 알고리즘을 지정합니다.

- 키 교환
- 대량 암호화
- 메시지 인증

AD FS의 보안 통신 상호 작용 하는 데 Schannel.dll을 사용 합니다.  현재 AD FS는 모든 프로토콜 및 Schannel.dll에서 지원 되는 암호 그룹을 지원 합니다.

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>TLS/SSL 프로토콜 및 암호 그룹 관리
> [!IMPORTANT]
> 이 섹션에서는 레지스트리를 수정 하는 방법을 설명 하는 단계를 포함 합니다. 그러나 레지스트리를 잘못 수정 하면 심각한 문제가 발생할 수 있습니다. 따라서 다음이 단계를 신중 하 게 수행 해야 합니다. 
> 
> 특정 클라이언트와 서버 간의 통신을 방지 또는 중단 하는 수 SCHANNEL에 대해 기본 보안 설정을 변경 하는 주의 확인 하십시오.  이 보안 통신 필수 항목이 며 없는 프로토콜을 사용 하 여 통신을 협상 하는 경우 발생 합니다.
> 
> 이러한 변경 내용을 적용 하는 경우 모든 팜의 AD FS 서버에 적용 되어야 합니다.  이러한 변경 내용을 적용 한 후 다시 부팅 필요 합니다.

오늘의 일 및 나가, 서버를 강화 하 고 이전 제거 또는 약한 암호 도구 모음에서 많은 조직에 대 한 우선 순위를 중요 해지고 있습니다.  소프트웨어 제품군을 사용할 수 있는 서버를 테스트 하 고 이러한 프로토콜 및 도구 모음에 대해 자세한 정보를 제공 합니다.  준수 상태를 유지 또는 안전 등급을 달성 하기 위해 약한 프로토콜 또는 암호 그룹을 사용 하지 않도록 설정 또는 제거에 반드시 되었습니다.  이 문서의 나머지 부분에서는 하거나 사용 하 고, 특정 프로토콜을 사용 하지 않도록 설정 하 고, 도구 모음을 암호화 하는 방법에 지침을 제공 합니다.

다음 레지스트리 키를 동일한 위치에 있습니다.  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols.  Regedit 또는 PowerShell 하거나 사용 하 고, 이러한 프로토콜을 사용 하지 않도록 설정 하 고, 암호 그룹을 사용 합니다.

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>설정 및 SSL 2.0 사용 하지 않도록 설정
SSL 2.0을 사용 하지 않도록 설정 하는 다음 레지스트리 키 및 해당 값을 사용 합니다.

### <a name="enable-ssl-20"></a>SSL 2.0을 사용 하도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "DisabledByDefault"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "DisabledByDefault"=dword:00000000 

### <a name="disable-ssl-20"></a>SSL 2.0을 사용 하지 않도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SL 2.0\Server] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "DisabledByDefault"=dword:00000001 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "DisabledByDefault"=dword:00000001

### <a name="using-powershell-to-disable-ssl-20"></a>SSL 2.0을 사용 하지 않도록 설정 하기 위해 PowerShell 사용

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>설정 및 SSL 3.0 사용 안 함
SSL 3.0을 사용 하지 않도록 설정 하는 다음 레지스트리 키 및 해당 값을 사용 합니다.

### <a name="enable-ssl-30"></a>SSL 3.0 사용
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "DisabledByDefault"=dword:00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "DisabledByDefault"=dword:00000000 

### <a name="disable-ssl-30"></a>SSL 3.0을 사용 하지 않도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "DisabledByDefault"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "DisabledByDefault"=dword:00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>PowerShell을 사용 하 여 SSL 3.0을 사용 하지 않도록 설정

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>설정 및 TLS 1.0 사용 안 함
TLS 1.0을 사용 하지 않도록 설정 하는 다음 레지스트리 키 및 해당 값을 사용 합니다.

> [!IMPORTANT]
> TLS 1.0을 사용 하지 않도록 설정 하면 AD FS 신뢰 하도록 WAP 중단 됩니다.  TLS 1.0을 사용 하지 않도록 설정 하는 경우에 응용 프로그램에 대 한 강력한 인증을 사용 해야 합니다.  참조 [강력한 인증을 사용 하도록 설정](#enabling-strong-authentication-for-net-applications) 



### <a name="enable-tls-10"></a>TLS 1.0을 사용 하도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "DisabledByDefault"=dword:00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "DisabledByDefault"=dword:00000000 

### <a name="disable-tls-10"></a>TLS 1.0을 사용 하지 않도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "DisabledByDefault"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "DisabledByDefault"=dword:00000001 

### <a name="using-powershell-to-disable-tls-10"></a>PowerShell을 사용 하 여 TLS 1.0을 사용 하지 않도록 설정

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>설정 및 TLS 1.1 사용 안 함
사용 하도록 설정 하 고 TLS 1.1을 사용 하지 않도록 설정 하려면 다음 레지스트리 키 및 해당 값을 사용 합니다.

### <a name="enable-tls-11"></a>TLS 1.1을 사용 하도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "DisabledByDefault"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "DisabledByDefault"=dword:00000000

### <a name="disable-tls-11"></a>TLS 1.1을 사용 하지 않도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "DisabledByDefault"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "DisabledByDefault"=dword:00000001 

### <a name="using-powershell-to-disable-tls-11"></a>PowerShell을 사용 하 여 TLS 1.1을 사용 하지 않도록 설정

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>설정 및 TLS 1.2 사용 안 함

사용 하도록 설정 하 고 TLS 1.2를 사용 하지 않도록 설정 하려면 다음 레지스트리 키 및 해당 값을 사용 합니다.

### <a name="enable-tls-12"></a>TLS 1.2 사용
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000

### <a name="disable-tls-12"></a>TLS 1.2를 사용 하지 않도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000001

### <a name="using-powershell-to-disable-tls-12"></a>PowerShell을 사용 하 여 TLS 1.2를 사용 하지 않도록 설정

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been disabled.'
```

## <a name="enable-and-disable-rc4"></a>RC4를 사용 하지 않도록 설정 하 고 사용 하도록 설정 

RC4를 사용 하지 않도록 설정 하는 다음 레지스트리 키 및 해당 값을 사용 합니다.  이 암호화 suite의 레지스트리 키 위치는 다음과 같습니다.

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>RC4를 사용 하도록 설정

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Enabled"=dword:00000001 

### <a name="disable-rc4"></a>RC4를 사용 하지 않도록 설정

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Enabled"=dword:00000000 

### <a name="using-powershell"></a>PowerShell 사용

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>사용 하도록 설정 하거나 추가 암호 그룹을 사용 하지 않도록 설정

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\00010002에서 제거 하 여 특정 특정 암호화를 비활성화할 수 있습니다. 

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

암호 그룹을 사용 하려면 문자열 값 함수 다중 문자열 값 키에 추가 합니다.  예를 들어 TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521를 사용 하도록 설정 하려는 경우 다음는 추가 문자열입니다.

지원 되는 암호의 전체 목록은 도구 모음 참조 [TLS/SSL (Schannel SSP)의 암호 그룹](https://msdn.microsoft.com/en-us/library/windows/desktop/aa374757.aspx)합니다.  이 문서는 테이블 및 지원 되지만 기본적으로 사용 되지 않은 기본적으로 사용할 수 있는 도구 모음을 제공 합니다.  우선 순위를 지정 하는 암호 그룹 참조 [우선 순위 지정 Schannel 암호 그룹](https://msdn.microsoft.com/en-us/library/windows/desktop/bb870930.aspx)합니다.

## <a name="enabling-strong-authentication-for-net-applications"></a>.NET 응용 프로그램에 대 한 강력한 인증을 사용 하도록 설정
.NET Framework 3.5/4.0/4.5.x 응용 프로그램 TLS 1.2를 기본 프로토콜로 SchUseStrongCrypto 레지스트리 키를 사용 하 여 전환할 수 있습니다.  이 레지스트리 키는 TLS 1.2를 사용 하도록.NET 응용 프로그램을 강제로 됩니다.

> [!IMPORTANT]
> Windows Server 2016 및 Windows Server 2012 R2에서 AD FS에 대 한.NET Framework 4.0/4.5.x 키를 사용 해야 합니다.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319


.NET Framework 3.5에 대 한 다음 레지스트리 키를 사용 합니다.

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\v2.0.50727] "SchUseStrongCrypto"=dword:00000001

.NET Framework 4.0/4.5.x 다음 레지스트리 키를 사용 합니다. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319 "SchUseStrongCrypto"=dword:00000001

![강력한 인증](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>추가 정보

- [TLS/SSL (Schannel SSP)의 암호 그룹](https://msdn.microsoft.com/en-us/library/windows/desktop/aa374757.aspx)
- [Windows 8.1에서 TLS 암호 도구 모음](https://msdn.microsoft.com/en-us/library/windows/desktop/mt767781.aspx)
- [Schannel 암호 그룹을 우선 순위 지정](https://msdn.microsoft.com/en-us/library/windows/desktop/bb870930.aspx)
- [암호화 및 기타 기술을 적군 말하기](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
