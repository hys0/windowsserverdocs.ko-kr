---
title: 13 단계 NAT 장치 뒤에서 DirectAccess 연결 테스트
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 796825c3-5e3e-4745-a921-25ab90b95ede
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 41701592c0d9b143c84ad3fbad3fd77491eff5a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404718"
---
# <a name="step-13-test-directaccess-connectivity-from-behind-a-nat-device"></a>13 단계 NAT 장치 뒤에서 DirectAccess 연결 테스트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess 클라이언트는 NAT 장치 또는 웹 프록시 서버 뒤에서 인터넷에 연결된 경우 Teredo 또는 IP-HTTPS를 사용하여 원격 액세스 서버에 연결합니다. NAT 장치에서 원격 액세스 서버의 공용 IP 주소에 아웃 바운드 UDP 포트 3544을 사용 하도록 설정 하면 Teredo가 사용 됩니다. Teredo 액세스를 사용할 수 없는 경우 DirectAccess 클라이언트는 기존 SSL 포트를 통해 방화벽이나 웹 프록시 서버에 액세스할 수 있도록 하는 IP-HTTPS(아웃바운드 TCP 포트 443 사용)로 대체합니다. 웹 프록시 인증이 필요한 경우에는 IP-HTTPS 연결에 실패합니다. 또한 웹 프록시에서 아웃바운드 SSL 검사를 수행하는 경우에도 IP-HTTPS 연결에 실패합니다. HTTPS 세션은 원격 액세스 서버가 아니라 웹 프록시에서 종료되기 때문입니다.  
  
다음 절차는 두 클라이언트 컴퓨터 모두에서 수행됩니다.  
  
1. Teredo 연결을 테스트 합니다. 첫 번째 테스트 집합은 DirectAccess 클라이언트가 Teredo를 사용 하도록 구성 된 경우에 수행 됩니다. NAT 장치에서 UDP 포트 3544에 대한 아웃바운드 액세스를 허용하는 경우에는 이 설정이 자동으로 구성됩니다. 먼저 CLIENT1에서 테스트를 실행 한 다음 CLIENT2에서 테스트를 실행 합니다.  
  
2. IP-HTTPS 연결을 테스트 합니다. 두 번째 테스트 집합은 DirectAccess 클라이언트가 IP-HTTPS를 사용 하도록 구성 된 경우에 수행 됩니다. IP-HTTPS 연결을 확인하려면 클라이언트에서 Teredo를 사용하지 않도록 설정해야 합니다. 먼저 CLIENT1에서 테스트를 실행 한 다음 CLIENT2에서 테스트를 실행 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
EDGE1 및 2-EDGE1를 시작 합니다 (아직 실행 중이 아닌 경우). 그리고 인터넷 서브넷에 연결 되어 있는지 확인 합니다.  
  
이러한 테스트를 수행 하기 전에 인터넷 스위치에서 CLIENT1과 CLIENT2를 분리 하 고 Ho Et 스위치에 연결 합니다. 현재 네트워크를 정의할 네트워크 유형을 묻는 메시지가 표시 되 면 **홈 네트워크**를 선택 합니다.  
  
## <a name="TeredoCLIENT1"></a>Teredo 연결 테스트  
  
1. C l i e n t 1에서 관리자 권한 Windows PowerShell 창을 엽니다.  
  
2. Teredo 어댑터를 사용 하도록 설정 하 고 **netsh interface Teredo set state enterpriseclient**를 입력 한 다음 enter 키를 누릅니다.  
  
3. Windows PowerShell 창에서 **ipconfig/all** 을 입력 하 고 enter 키를 누릅니다.  
  
4. ipconfig 명령의 출력을 검사합니다.  
  
   이제 이 컴퓨터가 NAT 장치 뒤에서 인터넷에 연결되고 프라이빗 IPv4 주소가 할당됩니다. DirectAccess 클라이언트가 NAT 장치 뒤에 있고 프라이빗 IPv4 주소가 할당된 경우 기본 설정 IPv6 전환 기술은 Teredo입니다. Ipconfig 명령의 출력을 살펴보면 터널 어댑터 Teredo 터널링 의사 (Pseudo) 인터페이스에 대 한 섹션과 Microsoft Teredo 터널링 어댑터에 대 한 섹션이 표시 됩니다. IP 주소는 2001:0와 일치 하는 IP 주소를 사용 하 여 Teredo로 시작 합니다. 위치. Teredo 터널 어댑터에 대 한 기본 게이트웨이가 ':: '으로 표시 되어야 합니다.  
  
5. Windows PowerShell 창에서 **ipconfig/flushdns** 를 입력 하 고 enter 키를 누릅니다.  
  
   그러면 클라이언트 컴퓨터가 인터넷에 연결된 이후 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
6. Windows PowerShell 창에서 **ping app1** 을 입력 하 고 enter 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3의 응답이 표시됩니다.  
  
7. Windows PowerShell 창에서 **ping app2** 을 입력 하 고 enter 키를 누릅니다. EDGE1에 의해 할당 된 NAT64 주소에서 APP2로의 응답이 표시 되어야 합니다 .이 경우에는 fd**c9:9f4e:** eb1b: 7777:: a00:4입니다. 굵게 표시 된 값은 주소가 생성 되는 방식에 따라 달라 집니다.  
  
8. Windows PowerShell 창에서 **ping app1** 를 입력 하 고 enter 키를 누릅니다. 2-APP1, 2001: db8:2:: 3의 IPv6 주소에서 응답이 표시 되어야 합니다.  
  
9. Internet Explorer를 열고 Internet Explorer 주소 표시줄에 **https://2-app1/** 을 입력 한 다음 enter 키를 누릅니다. 기본 IIS 웹 사이트가 2-APP1에 표시 됩니다.  
  
10. Internet Explorer 주소 표시줄에 **https://app2/** 을 입력 하 고 enter 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
11. **시작** 화면에서<strong>\\ \ App2\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다. 이는 SMB를 사용하여 IPv4 전용 호스트의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
12. CLIENT2에 대해이 절차를 반복 합니다.  
  
## <a name="IPHTTPS_CLIENT1"></a>IP-HTTPS 연결 테스트  
  
1. C l i e n t 1에서 관리자 권한 Windows PowerShell 창을 열고 **netsh interface teredo set state disabled** 를 입력 한 다음 enter 키를 누릅니다. 그러면 클라이언트 컴퓨터에서 Teredo가 사용하지 않도록 설정되고, 자체적으로 IP-HTTPS를 사용하도록 구성할 수 있게 됩니다. 명령이 완료되면 **확인** 응답이 나타납니다.  
  
2. Windows PowerShell 창에서 **ipconfig/all** 을 입력 하 고 enter 키를 누릅니다.  
  
3. ipconfig 명령의 출력을 검사합니다. 이제 이 컴퓨터가 NAT 장치 뒤에서 인터넷에 연결되고 프라이빗 IPv4 주소가 할당됩니다. Teredo가 사용하지 않도록 설정되고 DirectAccess 클라이언트가 IP-HTTPS로 대체합니다. Ipconfig 명령의 출력을 보면 터널 어댑터 iphttpsinterface에 대해 2001: db8:1: 1000 또는 2001: db8:2: 2000과 일치 하는 IP 주소를 사용 하는 섹션이 표시 됩니다. DirectAccess를 설정할 때 구성 됩니다. IPHTTPSInterface 터널 어댑터에 대해 나열 된 기본 게이트웨이는 표시 되지 않습니다.  
  
4. Windows PowerShell 창에서 **ipconfig/flushdns** 를 입력 하 고 enter 키를 누릅니다. 그러면 클라이언트 컴퓨터가 corpnet에 연결된 이후 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
5. Windows PowerShell 창에서 **ping app1** 을 입력 하 고 enter 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3의 응답이 표시됩니다.  
  
6. Windows PowerShell 창에서 **ping app2** 을 입력 하 고 enter 키를 누릅니다. EDGE1에 의해 할당 된 NAT64 주소에서 APP2로의 응답이 표시 되어야 합니다 .이 경우에는 fd**c9:9f4e:** eb1b: 7777:: a00:4입니다. 굵게 표시 된 값은 주소가 생성 되는 방식에 따라 달라 집니다.  
  
7. Windows PowerShell 창에서 **ping app1** 를 입력 하 고 enter 키를 누릅니다. 2-APP1, 2001: db8:2:: 3의 IPv6 주소에서 응답이 표시 되어야 합니다.  
  
8. Internet Explorer를 열고 Internet Explorer 주소 표시줄에 **https://2-app1/** 을 입력 한 다음 enter 키를 누릅니다. 기본 IIS 웹 사이트가 2-APP1에 표시 됩니다.  
  
9. Internet Explorer 주소 표시줄에 **https://app2/** 을 입력 하 고 enter 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
10. **시작** 화면에서<strong>\\ \ App2\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다. 이는 SMB를 사용하여 IPv4 전용 호스트의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
11. CLIENT2에 대해이 절차를 반복 합니다.  
  


