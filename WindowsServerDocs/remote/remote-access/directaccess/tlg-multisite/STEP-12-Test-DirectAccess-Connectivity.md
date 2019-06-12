---
title: 단계 DirectAccess 연결 12 테스트
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65ac1c23-3a47-4e58-888d-9dde7fba1586
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4e45f0c3c988c86a2428c3beb8bafc29b7b16bc0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446929"
---
# <a name="step-12-test-directaccess-connectivity"></a>단계 DirectAccess 연결 12 테스트

>적용 대상: Windows Server (반기 채널), Windows Server 2016

인터넷 또는 Homenet 네트워크에 있을 때 클라이언트 컴퓨터에서 연결을 테스트할 수 있습니다, 전에 올바른 그룹 정책 설정 인지 확인 해야 합니다.  
  
- 확인 하려면 클라이언트에 올바른 그룹 정책  
  
- EDGE1 통해 인터넷에서 DirectAccess 연결을 테스트  
  
- CLIENT2 Win7_Clients_Site2 보안 그룹으로 이동  
  
- 2-EDGE1를 통해 인터넷에서 DirectAccess 연결을 테스트  
  
## <a name="prerequisites"></a>사전 요구 사항  
Corpnet 네트워크에 두 클라이언트 컴퓨터를 연결한 다음 두 클라이언트 컴퓨터를 다시 시작 합니다.  
  
## <a name="policy"></a>올바른 그룹 정책 클라이언트 확인  
  
1.  CLIENT1에서 클릭 **시작**, 형식 **powershell.exe**를 마우스 오른쪽 단추로 클릭 **powershell**, 클릭 **고급**를 클릭및**관리자 권한으로 실행**합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
2.  Windows PowerShell 창에서 입력 **ipconfig** ENTER 키를 누릅니다.  
  
    회사 네트워크 어댑터 IPv4 주소 10.0.0로 시작 되 고 있는지 확인 합니다.  
  
3.  Windows PowerShell 창 유형에 **Get-dnsclientnrptpolicy** ENTER 키를 누릅니다. DirectAccess의 NRPT(이름 확인 정책 테이블) 항목이 표시됩니다.  
  
    -   . corp.contoso.com-이러한 설정은 corp.contoso.com에 대 한 모든 연결 해야 2001:db8:2::20을 IPv6 주소 2001:db8:1::2를 사용 하 여 DirectAccess DNS 서버 중 하나에서 해결할 수 있음을 나타냅니다.  
  
    -   nls.corp.contoso.com 이러한 설정은 nls.corp.contoso.com 이라는 이름에 대 한 예외가 있는지를 나타냅니다.  
  
4.  Windows PowerShell 창을 다음 절차에 대해 열어 둡니다.  
  
5.  CLIENT2에서 클릭 **시작**, 클릭 **프로그램도**, 클릭 **Accessories**, 클릭 **Windows PowerShell**, 를마우스오른쪽단추로클릭**Windows PowerShell**를 클릭 하 고 **관리자 권한으로 실행**합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
6.  Windows PowerShell 창에서 입력 **ipconfig** ENTER 키를 누릅니다.  
  
    회사 네트워크 어댑터 IPv4 주소 10.0.0로 시작 되 고 있는지 확인 합니다.  
  
7.  Windows PowerShell 창에서 입력 **netsh 네임 스페이스 정책 표시** ENTER 키를 누릅니다.  
  
    출력에서 두 개의 섹션 이어야 합니다.  
  
    -   . corp.contoso.com-이러한 설정은 나타냅니다는 corp.contoso.com에 대 한 모든 연결 된 IPv6 주소 2001:db8:1::2 사용 하 여 DirectAccess DNS 서버를 확인 해야 합니다.  
  
    -   nls.corp.contoso.com 이러한 설정은 nls.corp.contoso.com 이라는 이름에 대 한 예외가 있는지를 나타냅니다.  
  
8.  Windows PowerShell 창을 다음 절차에 대해 열어 둡니다.  
  
## <a name="EDGE1"></a>EDGE1 통해 인터넷에서 DirectAccess 연결을 테스트  
  
1. 2-EDGE1 인터넷 네트워크에서 분리 합니다.  
  
2. 회사 네트워크 스위치에서 CLIENT1 및 CLIENT2 뽑은 인터넷 스위치에 연결 합니다. 30 초 동안 기다립니다.  
  
3. CLIENT1에서 Windows PowerShell 창에서 입력 **ipconfig /all** ENTER 키를 누릅니다.  
  
4. Ipconfig 명령의 출력을 검사 합니다.  
  
   클라이언트 컴퓨터는 이제 인터넷에 연결 되어 있고 공용 IPv4 주소를 합니다. DirectAccess 클라이언트는 공용 IPv4 주소에 있는 경우 DirectAccess 클라이언트와 원격 액세스 서버가 IPv4 인터넷을 통해 IPv6 메시지를 터널링 Teredo 또는 IP-HTTPS IPv6 전환 기술을 사용 합니다. 기본 전환 기술은 Teredo 않음을 유의 합니다.  
  
5. Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다. 이 클라이언트 컴퓨터는 회사 네트워크에 연결 된 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시합니다.  
  
6. 클라이언트 컴퓨터에서 IP-HTTPS를 사용 하 여 다음 명령 사용 하 여 회사 네트워크에 연결할 수 있도록 Teredo 인터페이스를 사용 하지 않도록 설정 합니다.  
  
   ```  
   netsh interface teredo set state disable  
   ```  
  
7. EDGE1를 통해 연결 되어 있어야 합니다. 형식 **인터페이스를 표시 하는 netsh 인터페이스 httpstunnel** ENTER 키를 누릅니다.  
  
   출력 URL을 포함 해야 합니다. https://edge1.contoso.com:443/IPHTTPS합니다.  
  
   > [!TIP]  
   > CLIENT1에서 다음 Windows PowerShell 명령을 실행할 수도 있습니다. **Get-NetIPHTTPSConfiguration**. 출력에는 사용 가능한 서버 URL 연결 및 현재 사용 중인 프로필 보여 줍니다.  
  
8. Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3이 경우에 할당할 표시 되어야 합니다.  
  
9. Windows PowerShell 창에서 입력 **ping app1 2** ENTER 키를 누릅니다. 2-APP1 2001:db8:2::3이 경우에 할당 된 IPv6 주소에 대 한 회신에 표시 됩니다.  
  
10. Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 app2에 fd에이 경우에 할당 한 NAT64 주소에 대 한 회신 나타납니다**c9:9f4e:eb1b**: 7777::a00:4 합니다. 굵게 표시 된 값은 달라 지는 인해 주소 생성 되는 방식을 참고 합니다.  
  
    Ping APP2 수는 성공 APP2 IPv4 전용 리소스를 그대로 NAT64/DNS64를 사용 하 여 연결을 자동으로 연결할 수 있음을 나타내므로 중요 합니다.  
  
11. Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://app1/** ENTER 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
12. Internet Explorer 주소 표시줄에 입력 **https://2-app1/** ENTER 키를 누릅니다. 2-APP1에서 기본 웹 사이트가 표시 됩니다.  
  
13. Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
14. 에 **시작** 화면에서 입력<strong>\\\2-App1\Files</strong>, 한 다음 ENTER를 누릅니다. 예제에서는 텍스트 파일을 두 번 클릭 합니다.  
  
    이 corp2.corp.contoso.com 도메인 EDGE1 통해 연결 된 경우의 파일 서버에 연결할 수 있음을 보여 줍니다.  
  
15. 에 **시작** 화면에서 입력<strong>\\\App2\Files</strong>, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다.  
  
    이 SMB를 사용 하 여 리소스 도메인의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
16. 에 **시작** 화면에서 입력**wf.msc**, 한 다음 ENTER를 누릅니다.  
  
17. 에 **Windows Firewall with Advanced Security** 만 콘솔에서 합니다 **공개 프로필** 활성화 되어 합니다. Windows 방화벽을 제대로 작동 하려면 DirectAccess에 대 한 활성화 되어야 합니다. 를 Windows 방화벽을 비활성화 하는 경우에 DirectAccess 연결 작동 하지 않습니다.  
  
18. 콘솔의 왼쪽된 창에서 확장을 **모니터링** 노드를 차례로 클릭 합니다 **연결 보안 규칙** 노드. 활성 연결 보안 규칙에 표시 됩니다. **DirectAccess 정책을 ClientToCorp**, **DirectAccess 정책을 ClientToDNS64NAT64PrefixExemption**합니다 **DirectAccess 정책을 ClientToInfra**, 및 **DirectAccess 정책 ClientToNlaExempt**합니다. 표시할 오른쪽 가운데 창을 스크롤하여 합니다 **첫 번째 인증 방법** 하 고 **두 번째 인증 방법** 열입니다. 첫 번째 규칙 (ClientToCorp) Kerberos V5를 사용 하 여 인트라넷 터널을 설정 및 세 번째 규칙 (ClientToInfra) NTLMv2를 사용 하 여 인프라 터널을 설정 합니다.  
  
19. 콘솔의 왼쪽된 창에서 확장을 **보안 연결** 노드를 차례로 클릭 합니다 **주 모드** 노드. NTLMv2를 사용 하 여 인프라 터널 보안 연결 및 Kerberos V5를 사용 하 여 인트라넷 터널 보안 연결을 확인 합니다. 보여 주는 항목을 마우스 오른쪽 단추로 클릭 **(Kerberos V5) 사용자** 으로 **두 번째 인증 방법** 클릭 **속성**합니다. 에 **일반** 탭을 확인할 수 있습니다 합니다 **두 번째 인증 로컬 ID** 은 **CORP\User1**, User1을 사용 하 여 CORP 도메인에 정상적으로 인증할 수 있음을 나타내는 Kerberos입니다.  
  
20. CLIENT2에서 3 단계에서이 절차를 반복 합니다.  
  
## <a name="secgroup"></a>CLIENT2 Win7_Clients_Site2 보안 그룹으로 이동  
  
1.  Dc1 **시작**, 형식 **dsa.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  Active Directory 사용자 및 컴퓨터 콘솔에서 엽니다 **corp.contoso.com/Users** 를 두 번 클릭 **Win7_Clients_Site1**합니다.  
  
3.  에 **Win7_Clients_Site1 속성** 대화 상자에서 클릭 합니다 **멤버** 탭을 클릭 **CLIENT2**, 클릭 **제거**, 클릭 **Yes**를 클릭 하 고 **확인**합니다.  
  
4.  두 번 클릭 **Win7_Clients_Site2**, 한 후 합니다 **Win7_Clients_Site2 속성** 대화 상자에서 클릭 합니다 **멤버** 탭 합니다.  
  
5.  클릭 **추가**, 및를 **사용자 선택, 연락처, 컴퓨터 또는 서비스 계정** 대화 상자에서 클릭 **개체 유형**선택, **컴퓨터**를 클릭 하 고 **확인**합니다.  
  
6.  **선택할 개체 이름을 입력 하십시오**, 형식 **CLIENT2**를 클릭 하 고 **확인**합니다.  
  
7.  CLIENT2를 다시 시작 하 고 corp/User1 계정으로 로그온 합니다.  
  
8.  CLIENT2에서 관리자 권한 Windows PowerShell 창을 열고 유형 **netsh 네임 스페이스 정책 표시** ENTER 키를 누릅니다.  
  
    출력에서 두 개의 섹션 이어야 합니다.  
  
    -   . corp.contoso.com-이러한 설정은 나타냅니다는 corp.contoso.com에 대 한 모든 연결 된 IPv6 주소 2001:db8:2::20 DirectAccess DNS 서버를 확인 해야 합니다.  
  
    -   nls.corp.contoso.com 이러한 설정은 nls.corp.contoso.com 이라는 이름에 대 한 예외가 있는지를 나타냅니다.  
  
## <a name="DAConnect"></a>2-EDGE1를 통해 인터넷에서 DirectAccess 연결을 테스트  
  
1. 2-EDGE1 인터넷 네트워크에 연결 합니다.  
  
2. EDGE1 인터넷 네트워크에서 분리 합니다.  
  
3. CLIENT1에서 관리자 권한 Windows PowerShell 창을 엽니다.  
  
4. Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다. 이 클라이언트 컴퓨터는 회사 네트워크에 연결 된 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시합니다.  
  
5. 2-EDGE1를 통해 연결 되어 있어야 합니다. 형식 **인터페이스를 표시 하는 netsh 인터페이스 httpstunnel** ENTER 키를 누릅니다.  
  
   출력 URL을 포함 해야 합니다. https://2-edge1.contoso.com:443/IPHTTPS합니다.  
  
   > [!TIP]  
   > CLIENT1에서 명령을 실행할 수도 있습니다. **Get-NetIPHTTPSConfiguration**. 출력에는 사용 가능한 서버 URL 연결 및 현재 사용 중인 프로필 보여 줍니다.  
  
   > [!NOTE]  
   > CLIENT1 회사 리소스에 연결 하는 서버를 자동으로 변경 합니다. EDGE1에 연결을 표시 하는 명령의 출력을 약 5 분 동안 기다린 후 다시 시도 하십시오.  
  
6. Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. IPv6 주소 APP1, 2001:db8:1::3이 경우에 할당할 표시 되어야 합니다.  
  
7. Windows PowerShell 창에서 입력 **ping app1 2** ENTER 키를 누릅니다. 2-APP1 2001:db8:2::3이 경우에 할당 된 IPv6 주소에 대 한 회신에 표시 됩니다.  
  
8. Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 app2에 fd에이 경우에 할당 한 NAT64 주소에 대 한 회신 나타납니다**c9:9f4e:eb1b**: 7777::a00:4 합니다. 굵게 표시 된 값은 달라 지는 인해 주소 생성 되는 방식을 참고 합니다.  
  
   Ping APP2 수는 성공 APP2 IPv4 전용 리소스를 그대로 NAT64/DNS64를 사용 하 여 연결을 자동으로 연결할 수 있음을 나타내므로 중요 합니다.  
  
9. Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://app1/** ENTER 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
10. Internet Explorer 주소 표시줄에 입력 **https://2-app1/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
11. Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP3에 기본 웹 사이트가 표시 됩니다.  
  
12. 에 **시작** 화면에서 입력<strong>\\\App1\Files</strong>, 한 다음 ENTER를 누릅니다. 예제에서는 텍스트 파일을 두 번 클릭 합니다.  
  
    이 2 EDGE1 통해 연결 된 경우 corp.contoso.com 도메인의 파일 서버에 연결할 수 있음을 보여 줍니다.  
  
13. 에 **시작** 화면에서 입력<strong>\\\App2\Files</strong>, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다.  
  
    이 SMB를 사용 하 여 리소스 도메인의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
14. CLIENT2에서 3 단계에서이 절차를 반복 합니다.  
  


