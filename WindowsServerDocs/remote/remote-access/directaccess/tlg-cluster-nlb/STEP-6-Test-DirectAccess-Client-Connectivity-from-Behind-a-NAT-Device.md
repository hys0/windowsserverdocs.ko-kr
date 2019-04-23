---
title: 단계 6 NAT 장치 뒤에서 DirectAccess 클라이언트 연결 테스트
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aded2881-99ed-4f18-868b-b765ab926597
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a48bb9b012a81e91fbbe0ad914637dacac5a8a5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883004"
---
# <a name="step-6-test-directaccess-client-connectivity-from-behind-a-nat-device"></a>단계 6 NAT 장치 뒤에서 DirectAccess 클라이언트 연결 테스트

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DirectAccess 클라이언트는 NAT 장치 또는 웹 프록시 서버 뒤에서 인터넷에 연결된 경우 Teredo 또는 IP-HTTPS를 사용하여 원격 액세스 서버에 연결합니다. 

NAT 장치를 원격 액세스 서버의 공용 IP 주소 아웃 바운드 UDP 포트 3544을 사용 하도록 설정할 경우에 Teredo 사용 됩니다. Teredo 액세스를 사용할 수 없는 경우 DirectAccess 클라이언트는 기존 SSL 포트를 통해 방화벽이나 웹 프록시 서버에 액세스할 수 있도록 하는 IP-HTTPS(아웃바운드 TCP 포트 443 사용)로 대체합니다. 

웹 프록시 인증이 필요한 경우에는 IP-HTTPS 연결에 실패합니다. 또한 웹 프록시에서 아웃바운드 SSL 검사를 수행하는 경우에도 IP-HTTPS 연결에 실패합니다. HTTPS 세션은 원격 액세스 서버가 아니라 웹 프록시에서 종료되기 때문입니다. 이 섹션에서는 이전 섹션에서 6to4 연결을 사용하여 연결할 때 수행한 동일한 테스트를 수행합니다.  
  
다음 절차는 두 클라이언트 컴퓨터 모두에서 수행됩니다.  
  
1. Teredo 연결 테스트. 첫 번째 테스트 집합은 DirectAccess 클라이언트가 Teredo를 사용 하도록 구성 된 경우 수행 됩니다. NAT 장치에서 UDP 포트 3544에 대한 아웃바운드 액세스를 허용하는 경우에는 이 설정이 자동으로 구성됩니다.  
  
2. IP-HTTPS 연결을 테스트 합니다. 두 번째 테스트 집합은 DirectAccess 클라이언트가 IP-HTTPS를 사용 하도록 구성 된 경우 수행 됩니다. IP-HTTPS 연결을 확인하려면 클라이언트에서 Teredo를 사용하지 않도록 설정해야 합니다.  
  
> [!TIP]  
> 연결을 테스트를 확인 하려면 다음이 절차를 수행 하 고 캐시에서 웹 사이트 페이지를 검색 하지 하기 전에 Internet Explorer 캐시를 지우는 것이 좋습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항

이러한 테스트를 수행하기 전에 CLIENT1을 인터넷 스위치에서 분리하여 Homenet 스위치에 연결합니다. 현재 네트워크를 정의할 네트워크 유형을 묻는 메시지가 표시되면 **홈 네트워크**를 선택합니다.  
  
EDGE1 및 EDGE2를 시작합니다(아직 실행하지 않은 경우).  
  
## <a name="test-teredo-connectivity"></a>Teredo 연결 테스트  
  
1.  CLIENT1에서 관리자 권한 Windows PowerShell 창을 열고 유형 **ipconfig /all** ENTER 키를 누릅니다.  
  
2.  ipconfig 명령의 출력을 검사합니다.  
  
    이제 CLIENT1이 NAT 장치 뒤에서 인터넷에 연결되고 개인 IPv4 주소가 할당됩니다. DirectAccess 클라이언트가 NAT 장치 뒤에 있고 개인 IPv4 주소가 할당된 경우 기본 설정 IPv6 전환 기술은 Teredo입니다. Ipconfig 명령의 출력을 보면 터널 어댑터 Teredo 터널링 의사 (pseudo) 인터페이스 및 다음 2001로 시작 하는 IP 주소를 사용 하 여 설명을 Microsoft Teredo 터널링 어댑터에 대 한 섹션이 표시 됩니다:는 Teredo와 일치 하도록 주소입니다. Teredo 섹션이 표시되지 않으면 **netsh interface Teredo set state enterpriseclient** 명령을 사용하여 Teredo를 사용하도록 설정한 후 ipconfig 명령을 다시 실행합니다. Teredo 터널 어댑터에 대해 나열된 기본 게이트웨이는 표시되지 않습니다.  
  
3.  Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다.  
  
    그러면 클라이언트 컴퓨터가 인터넷에 연결된 이후 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
4.  Windows PowerShell 창에서 입력 **Get-dnsclientnrptpolicy** ENTER 키를 누릅니다.  
  
    NRPT(이름 확인 정책 테이블)에 대한 현재 설정이 출력에 표시됩니다. 이러한 설정은 원격 액세스 DNS 서버에서 IPv6 주소 2001:db8:1::2를 사용하여 .corp.contoso.com에 대한 모든 연결을 확인해야 함을 나타냅니다. 또한 nls.corp.contoso.com이라는 이름에 대한 예외가 있음을 나타내는 NRPT 항목을 확인합니다. 예외 목록에 있는 이름에는 원격 액세스 DNS 서버에서 응답하지 않습니다. 원격 액세스 DNS 서버 IP 주소(이 예제의 경우 2001:db8:1::2)를 ping하여 원격 액세스 서버에 대한 연결을 확인할 수 있습니다.  
  
5.  Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3의 응답이 표시됩니다.  
  
6.  Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 APP2에 할당한 NAT64 주소(이 예제의 경우 fdc9:9f4e:eb1b:7777::a00:4)의 응답이 표시됩니다.  
  
7.  Windows PowerShell 창을 다음 절차에 대해 열어 둡니다.  
  
8.  Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://app1/** ENTER 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
9. Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
10. 에 **시작** 화면에서 입력**\\\App2\Files**, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다. 이는 SMB를 사용하여 IPv4 전용 호스트의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
## <a name="test-ip-https-connectivity"></a>IP-HTTPS 연결 테스트  
  
1.  열고 관리자 권한 Windows PowerShell 창, 형식 **사용 하지 않도록 설정 하는 상태를 설정 하는 netsh 인터페이스 teredo** ENTER 키를 누릅니다. 그러면 클라이언트 컴퓨터에서 Teredo가 사용하지 않도록 설정되고, 자체적으로 IP-HTTPS를 사용하도록 구성할 수 있게 됩니다. 명령이 완료되면 **확인** 응답이 나타납니다.  
  
2.  Windows PowerShell 창에서 입력 **ipconfig /all** ENTER 키를 누릅니다.  
  
3.  ipconfig 명령의 출력을 검사합니다. 이제 이 컴퓨터가 NAT 장치 뒤에서 인터넷에 연결되고 개인 IPv4 주소가 할당됩니다. Teredo가 사용하지 않도록 설정되고 DirectAccess 클라이언트가 IP-HTTPS로 대체합니다. 터널 어댑터 iphttpsinterface는 IP-HTTPS 주소를 설정할 때 구성 된 접두사에 따라이 사용 하 여 일관 된 2001:db8:1:100로 시작 하는 IP 주소에 대 한 섹션을 참조 하세요 ipconfig 명령의 출력을 보면 DirectAccess입니다. IP-HTTPS 터널 어댑터에 대해 나열된 기본 게이트웨이는 표시되지 않습니다.  
  
4.  Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다. 그러면 클라이언트 컴퓨터가 corpnet에 연결된 이후 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
5.  Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3의 응답이 표시됩니다.  
  
6.  Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 APP2에 할당한 NAT64 주소(이 예제의 경우 fdc9:9f4e:eb1b:7777::a00:4)의 응답이 표시됩니다.  
  
7.  Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://app1/** ENTER 키를 누릅니다. APP1의 기본 IIS 사이트가 표시됩니다.  
  
8.  Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
9. 에 **시작** 화면에서 입력**\\\App2\Files**, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다. 이는 SMB를 사용하여 IPv4 전용 호스트의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.
