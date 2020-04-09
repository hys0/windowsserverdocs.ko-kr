---
title: 5 단계 인터넷 및 클러스터를 통해 DirectAccess 연결 테스트
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 8399bdfa-809a-45e4-9963-f9b6a631007f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f8880f60104cc67ca5c25c9c4fbf4ee6c9c1d1f1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819206"
---
# <a name="step-5-test-directaccess-connectivity-from-the-internet-and-through-the-cluster"></a>5 단계 인터넷 및 클러스터를 통해 DirectAccess 연결 테스트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이제 c l i e n t 1이 DirectAccess를 테스트할 준비가 되었습니다.  
  
- 인터넷에서 DirectAccess 연결을 테스트 합니다. CLIENT1을 시뮬레이트된 인터넷에 연결 합니다. 시뮬레이트된 인터넷에 연결 된 경우 클라이언트에 공용 IPv4 주소가 할당 됩니다. DirectAccess 클라이언트에 공용 IPv4 주소가 할당 된 경우 IPv6 전환 기술을 사용 하 여 원격 액세스 서버에 대 한 연결을 설정 하려고 시도 합니다.  
  
- 클러스터를 통해 DirectAccess 클라이언트 연결을 테스트 합니다. 클러스터 기능을 테스트 합니다. 테스트를 시작 하기 전에 EDGE1와 EDGE2를 모두 5 분 이상 종료 하는 것이 좋습니다. 이에 대 한 여러 가지 이유가 있습니다. 여기에는 ARP 캐시 시간 제한과 NLB와 관련 된 변경 사항이 포함 됩니다. 테스트 랩에서 NLB 구성의 유효성을 검사 하는 경우 시간이 경과 될 때까지 구성의 변경 내용이 연결에 즉시 반영 되지 않으므로 환자를 해야 합니다. 이는 다음 작업을 수행할 때 유의 해야 합니다.  
  
    > [!TIP]  
    > 이 절차를 수행 하기 전에 Internet Explorer 캐시를 지우고 다른 원격 액세스 서버를 통해 연결을 테스트 하 여 연결을 테스트 하 고 캐시에서 웹 페이지를 검색 하지 않도록 설정 하는 것이 좋습니다.  
  
## <a name="test-directaccess-connectivity-from-the-internet"></a>인터넷에서 DirectAccess 연결 테스트  
  
1. Corpnet 스위치에서 CLIENT1을 분리 하 고 인터넷 스위치에 연결 합니다. 30 초 동안 기다립니다.  
  
2. 관리자 권한 Windows PowerShell 창에서 **ipconfig/flushdns** 를 입력 하 고 enter 키를 누릅니다. 그러면 클라이언트 컴퓨터가 corpnet에 연결 된 경우 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
3. Windows PowerShell 창에서 **get-dnsclientnrptpolicy** 를 입력 하 고 enter 키를 누릅니다.  
  
   NRPT(이름 확인 정책 테이블)에 대한 현재 설정이 출력에 표시됩니다. 이러한 설정은 원격 액세스 DNS 서버에서 IPv6 주소 2001: db8:1:: 2를 사용 하 여 corp.contoso.com에 대 한 모든 연결을 확인 해야 함을 표시 합니다. 또한 nls.corp.contoso.com이라는 이름에 대한 예외가 있음을 나타내는 NRPT 항목을 확인합니다. 예외 목록에 있는 이름에는 원격 액세스 DNS 서버에서 응답하지 않습니다. 원격 액세스 DNS 서버 IP 주소를 ping 하 여 원격 액세스 서버에 대 한 연결을 확인할 수 있습니다. 예를 들어 2001: db8:1:: 2를 ping 할 수 있습니다.  
  
4. Windows PowerShell 창에서 **ping app1** 을 입력 하 고 enter 키를 누릅니다. APP1에 대 한 IPv6 주소에서 응답이 표시 되어야 합니다 .이 경우에는 2001: db8:1:: 3입니다.  
  
5. Windows PowerShell 창에서 **ping app2** 을 입력 하 고 enter 키를 누릅니다. EDGE1에서 APP2에 할당한 NAT64 주소(이 예제의 경우 fdc9:9f4e:eb1b:7777::a00:4)의 응답이 표시됩니다.  
  
   APP2는 APP2이 IPv4 전용 리소스 이므로 NAT64/DNS64를 사용 하 여 연결을 설정할 수 있음을 나타내므로 ping을 ping 할 수 있습니다.  
  
6. 다음 절차를 수행 하려면 Windows PowerShell 창을 열어 둡니다.  
  
7. Internet Explorer를 열고 Internet Explorer 주소 표시줄에 **https://app1/** 를 입력 한 다음 enter 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
8. Internet Explorer 주소 표시줄에 **https://app2/** 를 입력 하 고 enter 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
9. **시작** 화면에서<strong>\\\App2\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다.  
  
    이는 SMB를 사용 하 여 리소스 도메인의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
10. **시작** 화면에서**wf**를 입력 한 다음 enter 키를 누릅니다.  
  
11. **고급 보안이 포함 된 Windows 방화벽** 콘솔에서 **개인** 또는 **공개 프로필만** 활성화 되어 있는지 확인 합니다. DirectAccess가 제대로 작동 하려면 Windows 방화벽이 사용 하도록 설정 되어 있어야 합니다. Windows 방화벽을 사용 하지 않도록 설정 된 경우 DirectAccess 연결이 작동 하지 않습니다.  
  
12. 콘솔의 왼쪽 창에서 **모니터링** 노드를 확장 하 고 **연결 보안 규칙** 노드를 클릭 합니다. 활성 연결 보안 규칙: **Directaccess 정책-ClientToCorp**, **Directaccess 정책-ClientToDNS64NAT64PrefixExemption**, **Directaccess 정책-ClientToInfra**및 **directaccess 정책-ClientToNlaExempt**이 표시 됩니다. 가운데 창을 오른쪽으로 스크롤하여 **첫 번째 인증 방법과** **두 번째 인증 방법** 열을 표시 합니다. 첫 번째 규칙 (ClientToCorp)은 Kerberos V5를 사용 하 여 인트라넷 터널을 설정 하 고 세 번째 규칙 (ClientToInfra)은 NTLMv2를 사용 하 여 인프라 터널을 설정 합니다.  
  
13. 콘솔의 왼쪽 창에서 **보안 연결** 노드를 확장 하 고 **주 모드** 노드를 클릭 합니다. Kerberos V5를 사용 하는 인트라넷 터널 보안 연결 및 NTLMv2를 사용 하는 인프라 터널 보안 연결을 확인 합니다. **사용자 (Kerberos V5)** 를 표시 하는 항목을 **두 번째 인증 방법** 으로 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다. **일반** 탭에서 **두 번째 인증 로컬 ID** 는 **CORP\User1**입니다 .이는 u s e r 2가 회사 도메인에 Kerberos를 사용 하 여 성공적으로 인증할 수 있음을 나타냅니다.  
  
## <a name="test-directaccess-client-connectivity-through-the-cluster"></a>클러스터를 통해 DirectAccess 클라이언트 연결 테스트  
  
1. EDGE2에서 정상 종료를 수행 합니다.  
  
   네트워크 부하 분산 관리자를 사용 하 여 이러한 테스트를 실행할 때 서버의 상태를 확인할 수 있습니다.  
  
2. C l i e n t 1의 Windows PowerShell 창에서 **ipconfig/flushdns** 를 입력 하 고 enter 키를 누릅니다. 이렇게 하면 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
3. Windows PowerShell 창에서 ping APP1 및 APP2를 수행 합니다. 이러한 두 리소스의 응답이 모두 수신 됩니다.  
  
4. **시작** 화면에서<strong>\\\app2\files</strong>를 입력 합니다. APP2 컴퓨터에 공유 폴더가 표시 됩니다. APP2에서 파일 공유를 여는 기능은 사용자에 대 한 Kerberos 인증을 요구 하는 두 번째 터널이 제대로 작동 하 고 있음을 나타냅니다.  
  
5. Internet Explorer를 열고 https://app1/ 웹 사이트를 열고 https://app2/합니다. 두 웹 사이트를 열 수 있는 기능은 첫 번째 및 두 번째 터널이 모두 작동 하는지 확인 합니다. Internet Explorer를 닫습니다.  
  
6. EDGE2 컴퓨터를 시작 합니다.  
  
7. EDGE1에서 정상적인 종료를 수행 합니다.  
  
8. 5 분 동안 기다린 다음, CLIENT1로 돌아갑니다. 2-5 단계를 수행 합니다. 이렇게 하면 EDGE1을 사용할 수 없게 된 후에는 c l i e n t 1이 EDGE2에 투명 하 게 장애 조치할 수
