---
title: 13 NAT 장치 뒤에서 DirectAccess 연결 테스트 단계
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 796825c3-5e3e-4745-a921-25ab90b95ede
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 34a65434a0035c60c888170e779496653ad0ab6d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283205"
---
# <a name="step-13-test-directaccess-connectivity-from-behind-a-nat-device"></a>13 NAT 장치 뒤에서 DirectAccess 연결 테스트 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DirectAccess 클라이언트는 NAT 장치 또는 웹 프록시 서버 뒤에서 인터넷에 연결된 경우 Teredo 또는 IP-HTTPS를 사용하여 원격 액세스 서버에 연결합니다. NAT 장치를 원격 액세스 서버의 공용 IP 주소 아웃 바운드 UDP 포트 3544을 사용 하도록 설정할 경우에 Teredo 사용 됩니다. Teredo 액세스를 사용할 수 없는 경우 DirectAccess 클라이언트는 기존 SSL 포트를 통해 방화벽이나 웹 프록시 서버에 액세스할 수 있도록 하는 IP-HTTPS(아웃바운드 TCP 포트 443 사용)로 대체합니다. 웹 프록시 인증이 필요한 경우에는 IP-HTTPS 연결에 실패합니다. 또한 웹 프록시에서 아웃바운드 SSL 검사를 수행하는 경우에도 IP-HTTPS 연결에 실패합니다. HTTPS 세션은 원격 액세스 서버가 아니라 웹 프록시에서 종료되기 때문입니다.  
  
다음 절차는 두 클라이언트 컴퓨터 모두에서 수행됩니다.  
  
1. Teredo 연결 테스트. 첫 번째 테스트 집합은 DirectAccess 클라이언트가 Teredo를 사용 하도록 구성 된 경우 수행 됩니다. NAT 장치에서 UDP 포트 3544에 대한 아웃바운드 액세스를 허용하는 경우에는 이 설정이 자동으로 구성됩니다. 먼저 CLIENT1에서 테스트를 실행 하 고 CLIENT2에서 테스트를 실행 합니다.  
  
2. IP-HTTPS 연결을 테스트 합니다. 두 번째 테스트 집합은 DirectAccess 클라이언트가 IP-HTTPS를 사용 하도록 구성 된 경우 수행 됩니다. IP-HTTPS 연결을 확인하려면 클라이언트에서 Teredo를 사용하지 않도록 설정해야 합니다. 먼저 CLIENT1에서 테스트를 실행 하 고 CLIENT2에서 테스트를 실행 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
아직 실행 하지 않은 하며 인터넷 서브넷에 연결 되어 있는지 확인 하는 경우 EDGE1 및 2 EDGE1를 시작 합니다.  
  
이러한 테스트를 수행 하기 전에 CLIENT1 및 CLIENT2 인터넷 스위치에서 분리 하 고 Homenet 스위치에 연결 합니다. 현재 네트워크 정의를 선택 하려는 네트워크 유형을 묻는 메시지가 나타나면 **홈 네트워크**합니다.  
  
## <a name="TeredoCLIENT1"></a>Teredo 연결 테스트  
  
1. CLIENT1에서 관리자 권한 Windows PowerShell 창을 엽니다.  
  
2. Teredo 어댑터 사용 유형 **netsh 인터페이스 teredo 설정 상태 enterpriseclient**, 한 다음 ENTER를 누릅니다.  
  
3. Windows PowerShell 창에서 입력 **ipconfig /all** ENTER 키를 누릅니다.  
  
4. ipconfig 명령의 출력을 검사합니다.  
  
   이제 이 컴퓨터가 NAT 장치 뒤에서 인터넷에 연결되고 프라이빗 IPv4 주소가 할당됩니다. DirectAccess 클라이언트가 NAT 장치 뒤에 있고 프라이빗 IPv4 주소가 할당된 경우 기본 설정 IPv6 전환 기술은 Teredo입니다. Ipconfig 명령의 출력을 보면 경우 터널 어댑터 Teredo 터널링 의사 (pseudo) 인터페이스에 대 한 섹션을 한 다음 설명을 Microsoft Teredo 터널링 어댑터는 Teredo와 일치 하도록 2001:0로 시작 하는 IP 주소를 사용 하 여 표시 됩니다. 주소입니다. Teredo 터널 어댑터에 대해 나열 된 기본 게이트웨이 다시 표시 ': '.  
  
5. Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다.  
  
   그러면 클라이언트 컴퓨터가 인터넷에 연결된 이후 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
6. Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3의 응답이 표시됩니다.  
  
7. Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 app2에 fd에이 경우에 할당 한 NAT64 주소에 대 한 회신 나타납니다**c9:9f4e:eb1b**: 7777::a00:4 합니다. 굵게 표시 된 값은 달라 지는 인해 주소 생성 되는 방식을 참고 합니다.  
  
8. Windows PowerShell 창에서 입력 **ping app1 2** ENTER 키를 누릅니다. 2-APP1 2001:db8:2::3의 IPv6 주소에 대 한 회신에 표시 됩니다.  
  
9. Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://2-app1/** ENTER 키를 누릅니다. 2-APP1에서 기본 IIS 웹 사이트가 표시 됩니다.  
  
10. Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
11. 에 **시작** 화면에서 입력<strong>\\\App2\Files</strong>, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다. 이는 SMB를 사용하여 IPv4 전용 호스트의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
12. CLIENT2에서이 절차를 반복 합니다.  
  
## <a name="IPHTTPS_CLIENT1"></a>IP-HTTPS 연결 테스트  
  
1. CLIENT1에서 열고 관리자 권한 Windows PowerShell 창을 **netsh 인터페이스 teredo 사용 하지 않도록 설정 하는 상태를 설정할** ENTER 키를 누릅니다. 그러면 클라이언트 컴퓨터에서 Teredo가 사용하지 않도록 설정되고, 자체적으로 IP-HTTPS를 사용하도록 구성할 수 있게 됩니다. 명령이 완료되면 **확인** 응답이 나타납니다.  
  
2. Windows PowerShell 창에서 입력 **ipconfig /all** ENTER 키를 누릅니다.  
  
3. ipconfig 명령의 출력을 검사합니다. 이제 이 컴퓨터가 NAT 장치 뒤에서 인터넷에 연결되고 프라이빗 IPv4 주소가 할당됩니다. Teredo가 사용하지 않도록 설정되고 DirectAccess 클라이언트가 IP-HTTPS로 대체합니다. 2001:db8:1:1000 또는 2001:db8:2:2000 된 접두사를 기반으로 하는 IP-HTTPS 주소와 일치를 사용 하 여 시작 하는 IP 주소를 사용 하 여 터널 어댑터 iphttpsinterface는 섹션을 참조 하세요 ipconfig 명령의 출력을 보면 DirectAccess를 설정할 때 구성 됩니다. IPHTTPSInterface 터널 어댑터에 대해 나열 된 기본 게이트웨이 표시 되지 않습니다.  
  
4. Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다. 그러면 클라이언트 컴퓨터가 corpnet에 연결된 이후 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
5. Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3의 응답이 표시됩니다.  
  
6. Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 app2에 fd에이 경우에 할당 한 NAT64 주소에 대 한 회신 나타납니다**c9:9f4e:eb1b**: 7777::a00:4 합니다. 굵게 표시 된 값은 달라 지는 인해 주소 생성 되는 방식을 참고 합니다.  
  
7. Windows PowerShell 창에서 입력 **ping app1 2** ENTER 키를 누릅니다. 2-APP1 2001:db8:2::3의 IPv6 주소에 대 한 회신에 표시 됩니다.  
  
8. Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://2-app1/** ENTER 키를 누릅니다. 2-APP1에서 기본 IIS 웹 사이트가 표시 됩니다.  
  
9. Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
10. 에 **시작** 화면에서 입력<strong>\\\App2\Files</strong>, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다. 이는 SMB를 사용하여 IPv4 전용 호스트의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
11. CLIENT2에서이 절차를 반복 합니다.  
  


