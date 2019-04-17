---
title: "Adfs SSL/TLS 프로토콜 및 암호 그룹 관리"
description: "AD FS 2016에 대 한 질문과 대답"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 23055a1b727e4f1a6b1ccafdea9a410c6021c432
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2018
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>Adfs SSL/TLS 프로토콜 및 암호 그룹 관리
이 문서를 사용 하지 않도록 설정 하 고 특정 TLS/SSL 프로토콜 활성화 하 고 암호화 된 제품군 Adfs에서 사용 되는 방법에 대해 설명

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>TLS/SSL, SChannel 및 암호 그룹 adfs

Transport Layer Security TLS ()과 소켓 SSL (Secure Layer)는 보안 통신을 위해 제공 하는 프로토콜 합니다.  Active Directory Federation Services 통신에 대 한 이러한 프로토콜을 사용합니다.  오늘 여러 버전의 이러한 프로토콜 존재합니다.

Schannel는 보안 지원 SSP 표준 인증 SSL, TLS 및 DTLS 인터넷 프로토콜을 구현 하는입니다. 보안 지원 공급자 Interface (SSPI)은 API Windows 시스템 인증을 포함 하 여 보안 관련 기능을 수행 하는 데 사용 합니다. SSPI는 Schannel SSP 포함 하 여 여러 보안 지원 (규칙이) 공급자에 게 일반 인터페이스 같은 기능을

암호화 제품군 암호화 알고리즘 집합입니다. TLS/SSL 프로토콜 schannel SSP 구현 키를 생성 하 고 정보를 암호화 하 암호화 제품군에서 알고리즘을 사용 합니다. 암호화 제품군 각 다음 작업에 대해 한 알고리즘을 지정합니다.

- 키 교환
- 대량 암호화
- 메시지 인증

ADFS Schannel.dll는 보안 통신 상호 작용 하는 데 사용 합니다.  현재 ADFS 프로토콜 및 Schannel.dll에서 지원 되는 암호 그룹의 모든을 지원 합니다.

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>TLS/SSL 프로토콜 및 암호 그룹 관리
> [!IMPORTANT]
> 이 섹션 레지스트리를 수정 하는 방법을 설명 하는 단계 포함 되어 있습니다. 그러나 레지스트리를 올바르게 수정 심각한 문제가 발생할 수 있습니다. 따라서 다음이 단계를 신중 하 게 수행 있는지 확인 합니다. 
> 
> 손상 시키거나 클라이언트 및 서버 특정 간 통신 방지 SCHANNEL에 대 한 기본 보안 설정을 변경 하는 주의 해야 합니다.  이 보안 통신 필수 이며 협상와 통신 하는 데 사용 되는 프로토콜인 없는 경우 발생 합니다.
> 
> 이러한 변경 내용을 적용 하는 모든 사용자 농장의 ADFS 서버에 적용 합니다.  이러한 변경 내용이 적용 한 후 다시 부팅 필요 합니다.

오늘날의 날짜 및 연령, 서버 보안 강화 및 이전 제거 또는 약한 암호 그룹은 많은 조직에 대 한 주요 우선 순위를을 최대화 합니다.  소프트웨어를 사용할 수 있는 하는 서버에 테스트 하 고 이러한 프로토콜 및 제품군에서 자세한 정보를 제공 됩니다.  호환 유지 또는 보안 등급 달성 하기 위해 제거 하거나 비활성화 약한 프로토콜 또는 암호 그룹 자세로 되었습니다.  이 문서의 나머지 사용 하도록 설정 하거나 특정 프로토콜을 사용 하지 않도록 설정 하 고 암호화 된 제품군 하는 방법에 지침을 제공 합니다.

아래 레지스트리 키 동일한 위치에 있는: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols 합니다.  Regedit 또는 PowerShell 사용 하도록 설정 하거나 이러한 프로토콜을 사용 하지 않도록 설정 하 고 암호화 된 제품군을 사용 합니다.

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>설정 / 해제 2.0 SSL
다음 레지스트리 키와 값을 사용 하 여 설정 / 해제 SSL 2.0.

### <a name="enable-ssl-20"></a>2.0 SSL 사용 하도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "DisabledByDefault" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "DisabledByDefault" dword:00000000 = 

### <a name="disable-ssl-20"></a>2.0 SSL 사용 안 함
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SL 2.0\Server] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "DisabledByDefault" = dword: 00000001 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "DisabledByDefault" = dword: 00000001

### <a name="using-powershell-to-disable-ssl-20"></a>PowerShell을 사용 하 여 SSL 2.0 사용 하지 않도록 설정 하려면

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>설정 / 해제 SSL 3.0
다음 레지스트리 키와 값을 사용 하 여 설정 / 해제 SSL 3.0.

### <a name="enable-ssl-30"></a>3.0 SSL 사용 하도록 설정
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "DisabledByDefault" dword:00000000 = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "DisabledByDefault" dword:00000000 = 

### <a name="disable-ssl-30"></a>3.0 SSL 사용 안 함
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>PowerShell을 사용 하 여 SSL 3.0를 사용 하지 않도록 설정 하려면

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>설정 / 해제 TLS 1.0
다음 레지스트리 키와 값을 사용 하 여 설정 / 해제 TLS 1.0.

> [!IMPORTANT]
> TLS 1.0 비활성화 ADFS 신뢰 하 고 WAP 끊어집니다.  TLS 1.0를 사용 하지 않도록 설정 하는 경우 auth 강력한 응용 프로그램에 대 한 사용 해야 합니다.  참조 [강력한 인증 설정](#enabling-strong-authentication-for-net-applications) 



### <a name="enable-tls-10"></a>1.0 TLS 사용
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "DisabledByDefault" dword:00000000 = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "DisabledByDefault" dword:00000000 = 

### <a name="disable-tls-10"></a>1.0 TLS 사용 안 함
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client] "DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-tls-10"></a>PowerShell을 사용 하 여 TLS 1.0 사용 하지 않도록 설정 하려면

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>설정 / 해제 TLS 1.1
다음 레지스트리 키와 값을 사용 하 여 활성화 하 고 TLS 1.1 사용 하지 않도록 설정 합니다.

### <a name="enable-tls-11"></a>1.1 TLS 사용
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "DisabledByDefault" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "DisabledByDefault" dword:00000000 =

### <a name="disable-tls-11"></a>1.1 TLS 사용 안 함
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-tls-11"></a>PowerShell을 사용 하 여 TLS 1.1 사용 하지 않도록 설정 하려면

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>설정 / 해제 TLS 1.2

다음 레지스트리 키와 값을 사용 하 여 활성화 하 고 TLS 1.2 사용 안 함.

### <a name="enable-tls-12"></a>1.2 TLS 사용
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault" dword:00000000 = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault" dword:00000000 =

### <a name="disable-tls-12"></a>1.2 TLS 사용 안 함
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault" = dword: 00000001

### <a name="using-powershell-to-disable-tls-12"></a>PowerShell을 사용 하 여 TLS 1.2 사용 하지 않도록 설정 하려면

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been disabled.'
```

## <a name="enable-and-disable-rc4"></a>설정 / 해제 r c 4 

다음 레지스트리 키와 값을 사용 하 여 설정 / 해제 r c 4.  이 암호화 제품군 레지스트리 키 여기에 있습니다.

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>R c 4 설정

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "설정" = dword: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "설정" = dword: 00000001 

### <a name="disable-rc4"></a>R c 4 사용 안 함

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "설정" dword:00000000 =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "설정" dword:00000000 = 

### <a name="using-powershell"></a>PowerShell을 사용 하 여

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>활성화 또는 비활성화 추가 암호 그룹

특정 특정 암호 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\0010002에서 제거 하 여 비활성화할 수 있습니다. 

![레지스트리 위치](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

멀티 문자열 값 기능 키를의 문자열 가치 암호화 제품군을 사용 합니다.  예를 들어, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521 사용 하려고 하는 경우 다음 우리는에 추가 문자열 합니다.

지원 되는 암호의 전체 목록은 제품군 참조 [TLS/SSL (Schannel SSP)에서 암호 그룹](https://msdn.microsoft.com/en-us/library/windows/desktop/aa374757.aspx)합니다.  이 문서는 기본적으로 지원 되는 기본적으로 활성화 되지 않는 활성화 되어 있는 제품군 목차를 제공 합니다.  암호 그룹 우선 순위를 확인 [Schannel 암호 그룹 우선 순위를 지정](https://msdn.microsoft.com/en-us/library/windows/desktop/bb870930.aspx)합니다.

## <a name="enabling-strong-authentication-for-net-applications"></a>.NET 응용 프로그램에 대 한 강력한 인증 설정
.NET Framework 3.5/4.0/4.5.x 응용 프로그램 SchUseStrongCrypto 레지스트리 키를 사용 하 여 TLS 1.2로 기본 프로토콜을 전환할 수 있습니다.  이 레지스트리 키 TLS 1.2 사용 하 여 응용 프로그램을.NET 새로 고쳐집니다.

> [!IMPORTANT]
> ADFS Windows Server 2016 및 Windows Server 2012 r 2에 대 한.NET Framework 4.0/4.5.x 키를 사용 하 여 필요한: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ 합니다. NETFramework\v4.0.30319


.NET Framework 3.5 다음 레지스트리 키를 사용 합니다.

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ 합니다. NETFramework\v2.0.50727] "SchUseStrongCrypto" = dword: 00000001

.NET Framework 4.0/4.5.x 사용 다음 레지스트리 키: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ 합니다. "SchUseStrongCrypto" NETFramework\v4.0.30319 = dword: 00000001

![강력한 인증](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>자세한 내용

- [암호 그룹 TLS/SSL (Schannel SSP)에서](https://msdn.microsoft.com/en-us/library/windows/desktop/aa374757.aspx)
- [Windows 8.1에서 암호 그룹 TLS](https://msdn.microsoft.com/en-us/library/windows/desktop/mt767781.aspx)
- [Schannel 암호 그룹 우선 순위를 지정](https://msdn.microsoft.com/en-us/library/windows/desktop/bb870930.aspx)
- [암호 및 기타 Enigmatic 적군 말하기](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
