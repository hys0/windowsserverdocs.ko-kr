---
title: AD FS에 대 한 SSL/TLS 프로토콜 및 암호 그룹 관리
description: AD FS 2016에 대 한 질문과 대답
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 44fb4c02421a431edb502daecaa38f00fb4dd2ad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407532"
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>AD FS에 대 한 SSL/TLS 프로토콜 및 암호 그룹 관리
다음 설명서에서는에서 사용 되는 특정 TLS/SSL 프로토콜 및 암호 그룹을 사용 하지 않도록 설정 하 고 사용 하도록 설정 하는 방법에 대 한 정보를 제공 AD FS

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>AD FS의 TLS/SSL, SChannel 및 암호 그룹

TLS (전송 계층 보안) 및 SSL (SSL(Secure Sockets Layer))은 보안 통신을 위해 제공 하는 프로토콜입니다.  Active Directory Federation Services은 통신에 이러한 프로토콜을 사용 합니다.  현재 이러한 프로토콜의 여러 버전이 있습니다.

Schannel은 SSL, TLS 및 DTLS 인터넷 표준 인증 프로토콜을 구현한 SSP(Security Support Provider)입니다. SSPI(Security Support Provider Interface)는 인증을 비롯한 보안 관련 기능을 수행하기 위해 Windows 시스템에서 사용되는 API입니다. SSPI는 Schannel SSP를 포함한 몇몇 SSP(Security Support Provider)의 공용 인터페이스로 사용됩니다.

암호 그룹은 암호화 알고리즘 집합입니다. TLS/SSL 프로토콜의 schannel SSP 구현에서는 암호 그룹의 알고리즘을 사용 하 여 키를 만들고 정보를 암호화 합니다. 암호 그룹은 다음 작업에 대해 각각 하나의 알고리즘을 지정합니다.

- 키 교환
- 대량 암호화
- 메시지 인증

AD FS는 Schannel을 사용 하 여 보안 통신 상호 작용을 수행 합니다.  현재 AD FS은 Schannel에서 지원 되는 모든 프로토콜 및 암호 그룹을 지원 합니다.

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>TLS/SSL 프로토콜 및 암호 그룹 관리
> [!IMPORTANT]
> 이 섹션에는 레지스트리를 수정 하는 방법을 설명 하는 단계가 포함 되어 있습니다. 그러나 레지스트리를 잘못 수정 하면 심각한 문제가 발생할 수 있습니다. 따라서 이러한 단계를 신중 하 게 수행 해야 합니다. 
> 
> SCHANNEL의 기본 보안 설정을 변경 하면 특정 클라이언트와 서버 간의 통신을 중단 하거나 차단할 수 있습니다.  이 문제는 보안 통신이 필요 하며 통신을 협상 하는 프로토콜이 없는 경우에 발생 합니다.
> 
> 이러한 변경 내용을 적용 하는 경우 팜의 모든 AD FS 서버에 적용 해야 합니다.  이러한 변경 내용을 적용 한 후에는 다시 부팅이 필요 합니다.

Todays와 age에서 서버를 강화 하 고 이전 또는 취약 한 암호 그룹을 제거 하는 것은 많은 조직에서 중요 한 우선 순위를 갖습니다.  서버를 테스트 하 고 이러한 프로토콜 및 도구 모음에 대 한 자세한 정보를 제공 하는 소프트웨어 제품군을 사용할 수 있습니다.  규격을 유지 하거나 보안 등급을 확보 하기 위해 약한 프로토콜이 나 암호 그룹을 제거 하거나 사용 하지 않도록 설정 해야 합니다.  이 문서의 나머지 부분에서는 특정 프로토콜 및 암호 그룹을 사용 하거나 사용 하지 않도록 설정 하는 방법에 대 한 지침을 제공 합니다.

아래 레지스트리 키는 동일한 위치에 있습니다. HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols.  Regedit 또는 PowerShell을 사용 하 여 이러한 프로토콜 및 암호 그룹을 사용 하거나 사용 하지 않도록 설정 합니다.

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>SSL 2.0 사용 및 사용 안 함
SSL 2.0를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키와 해당 값을 사용 합니다.

### <a name="enable-ssl-20"></a>SSL 2.0 사용
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "DisabledByDefault" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ 클라이언트] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ 클라이언트] "DisabledByDefault" = dword: 00000000 

### <a name="disable-ssl-20"></a>SSL 2.0 사용 안 함
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "DisabledByDefault" = dword: 00000001 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ 클라이언트] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ 클라이언트] "DisabledByDefault" = dword: 00000001

### <a name="using-powershell-to-disable-ssl-20"></a>PowerShell을 사용 하 여 SSL 2.0 사용 안 함

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>SSL 3.0 사용 및 사용 안 함
SSL 3.0를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키와 해당 값을 사용 합니다.

### <a name="enable-ssl-30"></a>SSL 3.0 사용
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "DisabledByDefault" = dword: 00000000 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ 클라이언트] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ 클라이언트] "DisabledByDefault" = dword: 00000000 

### <a name="disable-ssl-30"></a>SSL 3.0 사용 안 함
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ 클라이언트] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ 클라이언트] "DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>PowerShell을 사용 하 여 SSL 3.0 사용 안 함

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>TLS 1.0 사용 및 사용 안 함
TLS 1.0를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키와 해당 값을 사용 합니다.

> [!IMPORTANT]
> TLS 1.0을 사용 하지 않도록 설정 하면 WAP AD FS 신뢰로 전환 됩니다.  TLS 1.0을 사용 하지 않도록 설정 하는 경우 응용 프로그램에 대해 강력한 인증을 사용 해야 합니다.  [강력한 인증 사용](#enabling-strong-authentication-for-net-applications) 을 참조 하세요. 



### <a name="enable-tls-10"></a>TLS 1.0 사용
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "DisabledByDefault" = dword: 00000000 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ 클라이언트] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ 클라이언트] "DisabledByDefault" = dword: 00000000 

### <a name="disable-tls-10"></a>TLS 1.0 사용 안 함
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ 클라이언트] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ 클라이언트] "DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-tls-10"></a>PowerShell을 사용 하 여 TLS 1.0 사용 안 함

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>TLS 1.1 사용 및 사용 안 함
TLS 1.1를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키와 해당 값을 사용 합니다.

### <a name="enable-tls-11"></a>TLS 1.1 사용
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "DisabledByDefault" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ 클라이언트] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ 클라이언트] "DisabledByDefault" = dword: 00000000

### <a name="disable-tls-11"></a>TLS 1.1 사용 안 함
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ 클라이언트] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ 클라이언트] "DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-tls-11"></a>PowerShell을 사용 하 여 TLS 1.1 사용 안 함

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>TLS 1.2 사용 및 사용 안 함

TLS 1.2를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키와 해당 값을 사용 합니다.

### <a name="enable-tls-12"></a>TLS 1.2 사용
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server] "DisabledByDefault" = dword: 00000000 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ 클라이언트] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ 클라이언트] "DisabledByDefault" = dword: 00000000

### <a name="disable-tls-12"></a>TLS 1.2 사용 안 함
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ 클라이언트] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ 클라이언트] "DisabledByDefault" = dword: 00000001

### <a name="using-powershell-to-disable-tls-12"></a>PowerShell을 사용 하 여 TLS 1.2 사용 안 함

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been disabled.'
```

## <a name="enable-and-disable-rc4"></a>RC4 사용 및 사용 안 함 

RC4를 사용 하거나 사용 하지 않도록 설정 하려면 다음 레지스트리 키와 해당 값을 사용 합니다.  이 암호 그룹의 레지스트리 키는 다음 위치에 있습니다.

- HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>RC4 사용

- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Enabled" = dword: 00000001 

### <a name="disable-rc4"></a>RC4 사용 안 함

- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Enabled" = dword: 00000000 

### <a name="using-powershell"></a>PowerShell 사용

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>추가 암호 그룹 사용 또는 사용 안 함

특정 암호화를 HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\00010002에서 제거 하 여 사용 하지 않도록 설정할 수 있습니다. 

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

암호 그룹을 사용 하도록 설정 하려면 해당 문자열 값을 함수 다중 문자열 값 키에 추가 합니다.  예를 들어 TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521를 사용 하도록 설정 하려는 경우 문자열에 추가 합니다.

지원 되는 암호 그룹의 전체 목록은 [TLS/SSL (SCHANNEL SSP)의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)을 참조 하세요.  이 문서에서는 기본적으로 사용 하도록 설정 되어 있지만 기본적으로 사용 하도록 설정 되지 않은 도구 모음 표를 제공 합니다.  암호 그룹의 우선 순위를 지정 하려면 [Schannel 암호 그룹 우선 순위](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)지정을 참조 하세요.

## <a name="enabling-strong-authentication-for-net-applications"></a>.NET 응용 프로그램에 대 한 강력한 인증 사용
.NET Framework 3.5/4.0/4.5. x 응용 프로그램은 SchUseStrongCrypto 레지스트리 키를 사용 하도록 설정 하 여 기본 프로토콜을 TLS 1.2로 전환할 수 있습니다.  이 레지스트리 키를 사용 하면 .NET 응용 프로그램에서 TLS 1.2을 강제로 사용 합니다.

> [!IMPORTANT]
> Windows Server 2016 및 Windows Server 2012 r 2에 대 한 AD FS .NET Framework 4.0/4.5. x 키: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\\를 사용 해야 합니다. NETFramework\v4.0.30319


.NET Framework 3.5의 경우 다음 레지스트리 키를 사용 합니다.

[HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node\Microsoft\\입니다. NETFramework\v2.0.50727] "SchUseStrongCrypto" = dword: 00000001

.NET Framework 4.0/4.5. x의 경우 다음 레지스트리 키를 사용 합니다. HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\\. NETFramework\v4.0.30319 "SchUseStrongCrypto" = dword: 00000001

![강력한 인증](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>추가 정보

- [TLS/SSL (Schannel SSP)의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)
- [Windows 8.1의 TLS 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/mt767781.aspx)
- [Schannel 암호 그룹 우선 순위 결정](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)
- [암호화 및 기타 처럼 tongues 말하기](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
