---
title: IP 주소에 대 한 Kerberos 구성
description: IP 기반 Spn에 대 한 Kerberos 지원
author: daveba
ms.author: daveba
ms.openlocfilehash: 1061364528100fe005e80f64c6315f9fca69ad98
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980295"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos 클라이언트는 Spn (서비스 사용자 이름)에서 IPv4 및 IPv6 주소 호스트 이름을 허용 합니다.

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows 10 버전 1507 및 Windows Server 2016부터 Spn에서 IPv4 및 IPv6 호스트 이름을 지원 하도록 Kerberos 클라이언트를 구성할 수 있습니다.

기본적으로 Windows는 호스트 이름에 대 한 Kerberos 인증을 시도 하지 않습니다 호스트는 IP 주소입니다. NTLM과 같은 다른 활성화 된 인증 프로토콜을 대체 합니다. 그러나 응용 프로그램이 IP 주소를 사용 하도록 하드 코드 된 경우도 있습니다 .이는 응용 프로그램이 NTLM으로 대체 되 고 Kerberos를 사용 하지 않음을 의미 합니다. 이로 인해 환경을 이동할 때 NTLM을 사용 하지 않도록 설정 하면 호환성 문제가 발생할 수 있습니다.

NTLM을 사용 하지 않도록 설정 하는 영향을 줄이기 위해 관리자가 IP 주소를 서비스 사용자 이름의 호스트 이름으로 사용할 수 있는 새로운 기능이 도입 되었습니다. 이 기능은 클라이언트에서 레지스트리 키 값을 통해 사용 하도록 설정 됩니다.

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Spn의 IP 주소 호스트 이름에 대 한 지원을 구성 하려면 TryIPSPN 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. IP 주소로 Kerberos로 보호 되는 리소스에 액세스 해야 하는 각 클라이언트 컴퓨터에이 레지스트리 값을 설정 해야 합니다.

## <a name="configuring-a-service-principal-name-as-ip-address"></a>IP 주소로 서비스 사용자 이름 구성

서비스 사용자 이름은 Kerberos 인증 중에 네트워크에서 서비스를 식별 하는 데 사용 되는 고유 식별자입니다. SPN은 서비스, 호스트 이름 및 형식 `service/hostname[:port]` ( `host/fs.contoso.com`예:)으로 구성 됩니다. 컴퓨터가 Active Directory에 조인 되 면 Windows에서 컴퓨터 개체에 여러 Spn을 등록 합니다.

Ip 주소는 일반적으로 임시 주소 이기 때문에 일반적으로 호스트 이름 대신 IP 주소를 사용 하지 않습니다. 이로 인해 주소 임대가 만료 되 고 갱신 될 때 충돌 및 인증 오류가 발생할 수 있습니다. 따라서 IP 주소 기반 SPN을 등록 하는 것은 수동 프로세스 이며 DNS 기반 호스트 이름으로 전환할 수 없는 경우에만 사용 해야 합니다.

[Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) 도구를 사용 하는 것이 좋습니다. SPN은 한 번에 Active Directory의 단일 계정에만 등록할 수 있으므로 DHCP를 사용 하는 경우 IP 주소에 고정 임대를 사용 하는 것이 좋습니다.

```
Setspn -s <service>/ip.address> <domain-user-account>  
```

예제:

```
Setspn -s host/192.168.1.1 server01
```
