---
title: IP 주소에 대 한 Kerberos 구성
description: IP 기반 Spn에 대 한 Kerberos 지원
ms.openlocfilehash: 30741f7a0f1978fcaa6ac83c98a54c07e1ef25c5
ms.sourcegitcommit: c6acac3622e5d34714ca5c569805931681f98779
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66391524"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>서비스 사용자 이름 (Spn)에서 IPv4 및 IPv6 주소 호스트를 허용 하는 Kerberos 클라이언트

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows 10 버전 1507 및 Windows Server 2016 부터는 Kerberos 클라이언트 Spn에서 IPv4 및 IPv6 호스트 이름을 지원 하도록 구성할 수 있습니다.

기본적으로 호스트 이름 IP 주소 이면 Windows 호스트에 대 한 Kerberos 인증을 시도 됩니다. NTLM과 같은 다른 사용 가능한 인증 프로토콜과 다시 대체 됩니다. 그러나 응용 프로그램은 경우에 따라 응용 프로그램을 의미 하는 IP 주소를 사용 하도록 하드 코드 된 NTLM으로 대체 되며 Kerberos를 사용 하지. NTLM을 사용 하지 않도록 설정 하려면 환경 이동 호환성 문제가 발생할 수 있습니다.

새로운 기능을 NTLM을 사용 하지 않도록 설정의 영향을 줄이기 위해 도입 서비스 주체 이름에 대 한 호스트 이름으로 IP 주소를 사용 하는 관리자 수 있도록 합니다. 이 기능은 레지스트리 키 값을 통해 클라이언트에서 사용할 수 있습니다.

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Spn의 IP 주소가 호스트 이름에 대 한 지원을 구성 하려면 TryIPSPN 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 이 레지스트리 값을 IP 주소를 통해 Kerberos로 보호 된 리소스에 액세스 해야 하는 각 클라이언트 컴퓨터에서 설정 해야 합니다.

## <a name="configuring-a-service-principal-name-as-ip-address"></a>IP 주소와 서비스 주체 이름 구성

서비스 사용자 이름에는 Kerberos 인증 중 네트워크에서 서비스를 식별 하는 데 사용 하는 고유 식별자입니다. SPN은 서비스, 호스트 이름 및 필요에 따라 포트의 형태로 이루어져 `service/hostname[:port]` 와 같은 `host/fs.contoso.com`합니다. Windows는 컴퓨터는 Active Directory에 가입 된 경우 컴퓨터 개체를 여러 Spn을 등록 됩니다.

IP 주소 사용 되지 않습니다 일반적으로 호스트 이름 대신 IP 주소 임시 경우가 많기 때문에. 주소 임대 만료 및 갱신 하는 대로이 값이 충돌 및 인증 오류에 발생할 수 있습니다. 따라서 IP 주소를 기준으로 SPN을 등록 하는 수동 프로세스 및 DNS 기반 호스트 이름으로 전환할 수 없는 경우에 사용 해야 합니다.

권장 되는 방법은 사용 하는 [Setspn.exe](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) 도구입니다. Note는 SPN만에 등록할 수 있는 단일 Active Directory 계정에 한 번 되므로 DHCP가 사용 하는 경우 IP 주소는 정적 임대가 것이 좋습니다.

```
Setspn -s <service>/ip.address> <domain-user-account>  
```

예:

```
Setspn -s host/192.168.1.1 server01
```
