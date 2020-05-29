---
title: DHCP 서버 없이 TCP/IP 주소 자동 지정을 사용 하는 방법
description: DHCP 서버 없이 TCP/IP 주소 자동 지정을 사용 하는 방법을 소개 합니다.
ms.date: 5/26/2020
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.reviewer: robsmi
ms.openlocfilehash: 8fbde77381141b76959f70e824eac22ee2121fa3
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150191"
---
# <a name="how-to-use-automatic-tcpip-addressing-without-a-dhcp-server"></a>DHCP 서버 없이 TCP/IP 주소 자동 지정을 사용 하는 방법

이 문서에서는 네트워크에 DHCP (Dynamic Host Configuration Protocol) 서버가 없는 TCP/IP (자동 전송 제어 프로토콜/인터넷 프로토콜) 주소 지정을 사용 하는 방법을 설명 합니다. 이 문서의 "적용 대상" 섹션에 나열 된 운영 체제 버전에는 APIPA (자동 개인 IP 주소 지정) 이라는 기능이 있습니다. 이 기능을 사용 하면 Windows 컴퓨터에서 DHCP 서버를 사용할 수 없거나 네트워크에 존재 하지 않는 경우 자체 IP (인터넷 프로토콜) 주소를 할당할 수 있습니다. 이 기능을 사용 하면 TCP/IP를 실행 하는 작은 LAN (Local Area Network)을 구성 하 고 지 원하는 것 보다 어렵습니다.

## <a name="more-information"></a>추가 정보

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)해 두세요.

Dhcp를 사용 하도록 구성 된 Windows 기반 컴퓨터는 DHCP 서버를 사용할 수 없는 경우 자동으로 IP (인터넷 프로토콜) 주소를 할당할 수 있습니다. 예를 들어 dhcp 서버가 없는 네트워크에서 또는 DHCP 서버가 유지 관리를 위해 일시적으로 중단 된 경우 네트워크에서이 문제가 발생할 수 있습니다.

IANA (Internet 169.254.0.0)에는 자동 개인 IP 주소 지정을 위해 예약 된-169.254.255.255가 있습니다. 결과적으로 APIPA는 라우팅할 수 있는 주소와 충돌 하지 않도록 보장 된 주소를 제공 합니다.

네트워크 어댑터에 IP 주소를 할당 한 후에는 컴퓨터가 TCP/IP를 사용 하 여 동일한 LAN에 연결 되어 있고 APIPA에 대해 구성 된 다른 컴퓨터와 통신할 수 있습니다. 또한 IP 주소는 169.254 (여기서 x-y는 클라이언트의 고유 식별자) 주소 범위에 서브넷 마스크 255.255.0.0으로 설정 되어 있습니다. 컴퓨터는 다른 서브넷에 있는 컴퓨터 또는 자동 개인 IP 주소 지정을 사용 하지 않는 컴퓨터와 통신할 수 없습니다. 자동 개인 IP 주소 지정은 기본적으로 사용 하도록 설정 되어 있습니다.

다음과 같은 경우에는 사용 하지 않도록 설정할 수 있습니다.

- 네트워크에서 라우터를 사용 합니다.

- 네트워크가 NAT 또는 프록시 서버 없이 인터넷에 연결 되어 있습니다.

Dhcp 관련 메시지를 사용 하지 않도록 설정 하지 않는 한 dhcp 메시지는 DHCP 주소 지정 및 자동 개인 IP 주소 지정을 변경 하는 경우 알림을 제공 합니다. DHCP 메시징을 실수로 사용 하지 않도록 설정한 경우에는 다음 레지스트리 키의 PopupFlag 값 값을 00에서 01로 변경 하 여 DHCP 메시지를 다시 켤 수 있습니다.  
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\DHCP` 

변경 내용을 적용 하려면 컴퓨터를 다시 시작 해야 합니다. 또한 Windows Millennium Edition, Windows 98 또는 Windows 98 Second Edition에서 Winipcfg 도구를 사용 하 여 컴퓨터에서 APIPA를 사용 하 고 있는지 확인할 수 있습니다.

시작, 실행을 차례로 클릭 하 고 "winipcfg" (따옴표 제외)를 입력 한 다음 확인을 클릭 합니다. 추가 정보를 클릭 합니다. IP 자동 구성 주소 상자에 169.254 범위 내에 있는 IP 주소가 있으면 자동 개인 IP 주소 지정이 사용 됩니다. IP 주소 상자가 있으면 자동 개인 IP 주소 지정이 현재 사용 하도록 설정 되어 있지 않습니다.
Windows 2000, Windows XP 또는 Windows Server 2003의 경우 명령 프롬프트에서 IPconfig 명령을 사용 하 여 컴퓨터에서 APIPA를 사용 하 고 있는지 여부를 확인할 수 있습니다.

시작, 실행을 차례로 클릭 하 고 "cmd" (따옴표 제외)를 입력 한 다음 확인을 클릭 하 여 MS-DOS 명령줄 창을 엽니다. "Ipconfig/all" (따옴표 제외)을 입력 한 다음 ENTER 키를 누릅니다. ' 자동 구성 사용 ' 줄에 "예"가 표시 되 고 ' 자동 구성 IP 주소 '가 169.254 (여기서 x-y는 클라이언트의 고유 식별자) 이면 컴퓨터에서 APIPA를 사용 합니다. ' 자동 구성 사용 ' 줄에 "아니요"가 표시 되 면 컴퓨터에서 현재 APIPA를 사용 하 고 있지 않습니다.
다음 방법 중 하나를 사용 하 여 자동 개인 IP 주소 지정을 사용 하지 않도록 설정할 수 있습니다.

TCP/IP 정보를 수동으로 구성할 수 있습니다. 그러면 DHCP를 모두 사용 하지 않도록 설정 합니다. 레지스트리를 편집 하 여 자동 개인 IP 주소 지정 (DHCP 제외)을 사용 하지 않도록 설정할 수 있습니다. 이렇게 하려면 0x0 값을 가진 "IPAutoconfigurationEnabled" DWORD 레지스트리 항목을 Windows Millennium Edition, Windows98 또는 Windows 98 Second Edition의 다음 레지스트리 키에 추가 합니다.`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\DHCP`

Windows 2000, Windows XP 및 Windows Server 2003의 경우 다음 레지스트리 키에 0x0 값을 포함 하는 "IPAutoconfigurationEnabled" DWORD 레지스트리 항목을 추가 하 여 APIPA를 사용 하지 않도록 설정할 수 있습니다.  
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\<Adapter GUID>`  
> [!NOTE]
> **어댑터 guid** 하위 키는 컴퓨터의 LAN 어댑터에 대 한 guid (globally unique identifier)입니다.

IPAutoconfigurationEnabled DWORD 항목에 값 1을 지정 하면 레지스트리에서이 값이 생략 되는 기본 상태인 APIPA를 사용할 수 있습니다.

## <a name="examples-of-where-apipa-may-be-useful"></a>APIPA가 유용할 수 있는 경우의 예

### <a name="example-1-no-previous-ip-address-and-no-dhcp-server"></a>예 1: 이전 IP 주소 없음 및 DHCP 서버 없음

Windows 기반 컴퓨터 (DHCP 용으로 구성 됨)를 초기화 하는 경우 3 개 이상의 "검색" 메시지를 브로드캐스트합니다. 여러 검색 메시지가 브로드캐스트 된 후에도 DHCP 서버가 응답 하지 않는 경우 Windows 컴퓨터는 자신에 게 클래스 B (APIPA) 주소를 할당 합니다. 그러면 Windows 컴퓨터에 컴퓨터의 사용자에 게 오류 메시지가 표시 됩니다 (이전에는 DHCP 서버에서 IP 주소를 할당 받지 않음). 그러면 Windows 컴퓨터가 DHCP 서버와의 통신을 설정 하는 데 3 분 마다 검색 메시지를 전송 합니다.

### <a name="example-2-previous-ip-address-and-no-dhcp-server"></a>예 2: 이전 IP 주소 및 DHCP 서버 없음

컴퓨터에서 DHCP 서버를 확인 하 고, 찾을 수 없는 경우 기본 게이트웨이에 연결 하려고 시도 합니다. 기본 게이트웨이가 회신 하는 경우 Windows 컴퓨터는 이전에 임대 된 IP 주소를 유지 합니다. 그러나 컴퓨터에서 기본 게이트웨이의 응답이 수신 되지 않거나 할당 된 내용이 없는 경우 자동 개인 IP 주소 지정 기능을 사용 하 여 자체 IP 주소를 할당 합니다. 사용자에 게 표시 되는 오류 메시지 및 검색 메시지는 3 분 마다 전송 됩니다. DHCP 서버가 온라인 상태가 되 면 DHCP 서버와의 통신이 다시 설정 되었다는 메시지가 생성 됩니다.

### <a name="example-3-lease-expires-and-no-dhcp-server"></a>예 3: 임대가 만료 되 고 DHCP 서버가 없음

Windows 기반 컴퓨터는 IP 주소의 임대를 다시 설정 하려고 시도 합니다. Windows 컴퓨터가 DCHP 서버를 찾지 못하면 오류 메시지를 생성 한 후 IP 주소를 자동으로 할당 합니다. 그러면 컴퓨터에서 4 개의 검색 메시지를 브로드캐스트한 후 5 분 마다 전체 절차를 반복 합니다. 그러면 DHCP 서버와의 통신이 다시 설정 되었다는 메시지가 생성 됩니다.
