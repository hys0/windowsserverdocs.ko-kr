---
title: 12 단계 DirectAccess 연결 테스트
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65ac1c23-3a47-4e58-888d-9dde7fba1586
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd0f8ba10536a28479269abafadaaacaffd3d0a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388376"
---
# <a name="step-12-test-directaccess-connectivity"></a>12 단계 DirectAccess 연결 테스트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

인터넷 또는 Ho 네트워크에 있는 클라이언트 컴퓨터에서 연결을 테스트 하려면 먼저 올바른 그룹 정책 설정이 있는지 확인 해야 합니다.  
  
- 클라이언트에 올바른 그룹 정책이 있는지 확인 하려면  
  
- EDGE1를 통해 인터넷에서 DirectAccess 연결 테스트  
  
- CLIENT2을 Win7_Clients_Site2 보안 그룹으로 이동  
  
- EDGE1을 통해 인터넷에서 DirectAccess 연결 테스트  
  
## <a name="prerequisites"></a>사전 요구 사항  
두 클라이언트 컴퓨터를 모두 Corpnet 네트워크에 연결한 후 두 클라이언트 컴퓨터를 모두 다시 시작 합니다.  
  
## <a name="policy"></a>클라이언트에 올바른 그룹 정책이 있는지 확인  
  
1.  CLIENT1에서 **시작**을 클릭 하 고 **powershell**을 입력 한 다음 **powershell**을 마우스 오른쪽 단추로 클릭 하 고 **고급**을 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
2.  Windows PowerShell 창에서 **ipconfig** 를 입력 하 고 enter 키를 누릅니다.  
  
    Corpnet 어댑터 IPv4 주소가 10.0.0로 시작 하는지 확인 합니다.  
  
3.  Windows PowerShell 창에서 **get-dnsclientnrptpolicy** 를 입력 하 고 enter 키를 누릅니다. DirectAccess의 NRPT(이름 확인 정책 테이블) 항목이 표시됩니다.  
  
    -   . corp.contoso.com-이러한 설정은 IPv6 주소 2001: db8:1:: 2 또는 2001: db8:2:: 20을 사용 하 여 DirectAccess DNS 서버 중 하나에서 corp.contoso.com에 대 한 모든 연결을 확인 해야 함을 표시 합니다.  
  
    -   nls.corp.contoso.com-이러한 설정은 이름 nls.corp.contoso.com에 대 한 예외가 있음을 의미 합니다.  
  
4.  다음 절차를 수행 하려면 Windows PowerShell 창을 열어 둡니다.  
  
5.  CLIENT2에서 **시작**, **모든 프로그램**, **보조 프로그램**, **Windows PowerShell**을 차례로 클릭 하 고 **windows powershell**을 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
6.  Windows PowerShell 창에서 **ipconfig** 를 입력 하 고 enter 키를 누릅니다.  
  
    Corpnet 어댑터 IPv4 주소가 10.0.0로 시작 하는지 확인 합니다.  
  
7.  Windows PowerShell 창에서 **netsh namespace show policy** 를 입력 하 고 enter 키를 누릅니다.  
  
    출력에는 두 개의 섹션이 있어야 합니다.  
  
    -   . corp.contoso.com-이러한 설정은 IPv6 주소 2001: db8:1:: 2를 사용 하 여 DirectAccess DNS 서버에서 corp.contoso.com에 대 한 모든 연결을 확인 해야 함을 표시 합니다.  
  
    -   nls.corp.contoso.com-이러한 설정은 이름 nls.corp.contoso.com에 대 한 예외가 있음을 의미 합니다.  
  
8.  다음 절차를 수행 하려면 Windows PowerShell 창을 열어 둡니다.  
  
## <a name="EDGE1"></a>EDGE1를 통해 인터넷에서 DirectAccess 연결 테스트  
  
1. 2-인터넷 네트워크에서 EDGE1를 분리 합니다.  
  
2. Corpnet 스위치에서 CLIENT1 및 CLIENT2를 분리 하 고 인터넷 스위치에 연결 합니다. 30 초 동안 기다립니다.  
  
3. C l i e n t 1의 Windows PowerShell 창에서 **ipconfig/all** 을 입력 하 고 enter 키를 누릅니다.  
  
4. Ipconfig 명령의 출력을 검사 합니다.  
  
   이제 클라이언트 컴퓨터가 인터넷에 연결 되어 있고 공용 IPv4 주소가 있습니다. DirectAccess 클라이언트에 공용 IPv4 주소가 있으면 Teredo 또는 IP-HTTPS IPv6 전환 기술을 사용 하 여 DirectAccess 클라이언트와 원격 액세스 서버 간에 IPv4 인터넷을 통해 IPv6 메시지를 터널링 합니다. Teredo는 기본 설정 전환 기술입니다.  
  
5. Windows PowerShell 창에서 **ipconfig/flushdns** 를 입력 하 고 enter 키를 누릅니다. 그러면 클라이언트 컴퓨터가 corpnet에 연결 된 경우 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
6. Teredo 인터페이스를 사용 하지 않도록 설정 하 여 클라이언트 컴퓨터가 IP-HTTPS를 사용 하 여 다음 명령을 사용 하 여 corpnet에 연결 하도록 합니다.  
  
   ```  
   netsh interface teredo set state disable  
   ```  
  
7. EDGE1을 통해 연결 되었는지 확인 합니다. **Netsh interface httpstunnel show interface** 를 입력 하 고 enter 키를 누릅니다.  
  
   출력에는 https://edge1.contoso.com:443/IPHTTPS URL이 포함 되어야 합니다.  
  
   > [!TIP]  
   > CLIENT1에서 다음 Windows PowerShell 명령을 실행할 수도 있습니다. **NetIPHTTPSConfiguration**. 출력은 사용 가능한 서버 URL 연결 및 현재 활성 프로필을 표시 합니다.  
  
8. Windows PowerShell 창에서 **ping app1** 을 입력 하 고 enter 키를 누릅니다. APP1에 할당 된 IPv6 주소에서 응답이 표시 되어야 합니다 .이 경우에는 2001: db8:1:: 3입니다.  
  
9. Windows PowerShell 창에서 **ping app1** 를 입력 하 고 enter 키를 누릅니다. APP1에 할당 된 IPv6 주소에서 응답이 표시 되어야 합니다 .이 경우에는 2001: db8:2:: 3입니다.  
  
10. Windows PowerShell 창에서 **ping app2** 을 입력 하 고 enter 키를 누릅니다. EDGE1에 의해 할당 된 NAT64 주소에서 APP2로의 응답이 표시 되어야 합니다 .이 경우에는 fd**c9:9f4e:** eb1b: 7777:: a00:4입니다. 굵게 표시 된 값은 주소가 생성 되는 방식에 따라 달라 집니다.  
  
    APP2는 APP2이 IPv4 전용 리소스 이므로 NAT64/DNS64를 사용 하 여 연결을 설정할 수 있음을 나타내므로 ping을 ping 할 수 있습니다.  
  
11. Internet Explorer를 열고 Internet Explorer 주소 표시줄에 **https://app1/** 을 입력 한 다음 enter 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
12. Internet Explorer 주소 표시줄에 **https://2-app1/** 을 입력 하 고 enter 키를 누릅니다. 2-APP1에 기본 웹 사이트가 표시 됩니다.  
  
13. Internet Explorer 주소 표시줄에 **https://app2/** 을 입력 하 고 enter 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
14. **시작** 화면에서<strong>\\ \ 2-App1\Files</strong>을 입력 한 다음 enter 키를 누릅니다. 예제 텍스트 파일을 두 번 클릭 합니다.  
  
    이는 EDGE1를 통해 연결 된 경우 corp2.corp.contoso.com 도메인의 파일 서버에 연결할 수 있음을 보여 줍니다.  
  
15. **시작** 화면에서<strong>\\ \ App2\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다.  
  
    이는 SMB를 사용 하 여 리소스 도메인의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
16. **시작** 화면에서**wf**를 입력 한 다음 enter 키를 누릅니다.  
  
17. **고급 보안이 포함 된 Windows 방화벽** 콘솔에서 **공개 프로필만** 활성화 됨을 확인 합니다. DirectAccess가 제대로 작동 하려면 Windows 방화벽이 사용 하도록 설정 되어 있어야 합니다. Windows 방화벽을 사용 하지 않도록 설정 된 경우 DirectAccess 연결이 작동 하지 않습니다.  
  
18. 콘솔의 왼쪽 창에서 **모니터링** 노드를 확장 하 고 **연결 보안 규칙** 노드를 클릭 합니다. 활성 연결 보안 규칙이 표시 되어야 합니다. **Directaccess 정책-ClientToCorp**, **Directaccess 정책-ClientToDNS64NAT64PrefixExemption**, **Directaccess 정책-ClientToInfra**및 **directaccess 정책-ClientToNlaExempt**. 가운데 창을 오른쪽으로 스크롤하여 **첫 번째 인증 방법과** **두 번째 인증 방법** 열을 표시 합니다. 첫 번째 규칙 (ClientToCorp)은 Kerberos V5를 사용 하 여 인트라넷 터널을 설정 하 고 세 번째 규칙 (ClientToInfra)은 NTLMv2를 사용 하 여 인프라 터널을 설정 합니다.  
  
19. 콘솔의 왼쪽 창에서 **보안 연결** 노드를 확장 하 고 **주 모드** 노드를 클릭 합니다. Kerberos V5를 사용 하는 인트라넷 터널 보안 연결 및 NTLMv2를 사용 하는 인프라 터널 보안 연결을 확인 합니다. **사용자 (Kerberos V5)** 를 표시 하는 항목을 **두 번째 인증 방법** 으로 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다. **일반** 탭에서 **두 번째 인증 로컬 ID** 는 **CORP\User1**입니다 .이는 u s e r 2가 회사 도메인에 Kerberos를 사용 하 여 성공적으로 인증할 수 있음을 나타냅니다.  
  
20. CLIENT2의 3 단계에서이 절차를 반복 합니다.  
  
## <a name="secgroup"></a>CLIENT2을 Win7_Clients_Site2 보안 그룹으로 이동  
  
1.  DC1에서 **시작**을 클릭 하 고 **dsa.msc**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  Active Directory 사용자 및 컴퓨터 콘솔에서 **corp.contoso.com/Users** 을 열고 **Win7_Clients_Site1**를 두 번 클릭 합니다.  
  
3.  **Win7_Clients_Site1 속성** 대화 상자에서 **구성원** 탭을 클릭 하 고, **CLIENT2**, **제거**, **예**를 차례로 클릭 한 다음 **확인**을 클릭 합니다.  
  
4.  **Win7_Clients_Site2**를 두 번 클릭 한 다음 **Win7_Clients_Site2 속성** 대화 상자에서 **구성원** 탭을 클릭 합니다.  
  
5.  **추가**를 클릭 하 고 **사용자, 연락처, 컴퓨터 또는 서비스 계정 선택** 대화 상자에서 **개체 유형**을 클릭 하 고 **컴퓨터**를 선택한 다음 **확인**을 클릭 합니다.  
  
6.  **선택할 개체 이름을 입력**하십시오 .에 **CLIENT2**을 입력 한 다음 **확인**을 클릭 합니다.  
  
7.  CLIENT2를 다시 시작 하 고 corp/User1 계정을 사용 하 여 로그온 합니다.  
  
8.  CLIENT2에서 관리자 권한 Windows PowerShell 창을 열고 **netsh namespace show policy** 를 입력 한 다음 enter 키를 누릅니다.  
  
    출력에는 두 개의 섹션이 있어야 합니다.  
  
    -   . corp.contoso.com-이러한 설정은 IPv6 주소 2001: db8:2: 20을 사용 하 여 DirectAccess DNS 서버에서 corp.contoso.com에 대 한 모든 연결을 확인 해야 함을 표시 합니다.  
  
    -   nls.corp.contoso.com-이러한 설정은 이름 nls.corp.contoso.com에 대 한 예외가 있음을 의미 합니다.  
  
## <a name="DAConnect"></a>EDGE1을 통해 인터넷에서 DirectAccess 연결 테스트  
  
1. 2-EDGE1를 인터넷 네트워크에 연결 합니다.  
  
2. 인터넷 네트워크에서 EDGE1를 분리 합니다.  
  
3. C l i e n t 1에서 관리자 권한 Windows PowerShell 창을 엽니다.  
  
4. Windows PowerShell 창에서 **ipconfig/flushdns** 를 입력 하 고 enter 키를 누릅니다. 그러면 클라이언트 컴퓨터가 corpnet에 연결 된 경우 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시됩니다.  
  
5. 2-EDGE1을 통해 연결 되었는지 확인 합니다. **Netsh interface httpstunnel show interface** 를 입력 하 고 enter 키를 누릅니다.  
  
   출력에는 https://2-edge1.contoso.com:443/IPHTTPS URL이 포함 되어야 합니다.  
  
   > [!TIP]  
   > CLIENT1에서 다음 명령을 실행할 수도 있습니다. **NetIPHTTPSConfiguration**. 출력은 사용 가능한 서버 URL 연결 및 현재 활성 프로필을 표시 합니다.  
  
   > [!NOTE]  
   > CLIENT1은 회사 리소스에 연결 하는 서버를 자동으로 변경 합니다. 명령 출력에 EDGE1에 대 한 연결이 표시 되 면 약 5 분 정도 기다린 후 다시 시도 합니다.  
  
6. Windows PowerShell 창에서 **ping app1** 을 입력 하 고 enter 키를 누릅니다. APP1에 할당 된 IPv6 주소에서 응답이 표시 되어야 합니다 .이 경우에는 2001: db8:1:: 3입니다.  
  
7. Windows PowerShell 창에서 **ping app1** 를 입력 하 고 enter 키를 누릅니다. APP1에 할당 된 IPv6 주소에서 응답이 표시 되어야 합니다 .이 경우에는 2001: db8:2:: 3입니다.  
  
8. Windows PowerShell 창에서 **ping app2** 을 입력 하 고 enter 키를 누릅니다. EDGE1에 의해 할당 된 NAT64 주소에서 APP2로의 응답이 표시 되어야 합니다 .이 경우에는 fd**c9:9f4e:** eb1b: 7777:: a00:4입니다. 굵게 표시 된 값은 주소가 생성 되는 방식에 따라 달라 집니다.  
  
   APP2는 APP2이 IPv4 전용 리소스 이므로 NAT64/DNS64를 사용 하 여 연결을 설정할 수 있음을 나타내므로 ping을 ping 할 수 있습니다.  
  
9. Internet Explorer를 열고 Internet Explorer 주소 표시줄에 **https://app1/** 을 입력 한 다음 enter 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
10. Internet Explorer 주소 표시줄에 **https://2-app1/** 을 입력 하 고 enter 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
11. Internet Explorer 주소 표시줄에 **https://app2/** 을 입력 하 고 enter 키를 누릅니다. APP3에 기본 웹 사이트가 표시 됩니다.  
  
12. **시작** 화면에서<strong>\\ \ App1\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 예제 텍스트 파일을 두 번 클릭 합니다.  
  
    이는 2-EDGE1를 통해 연결 된 경우 corp.contoso.com 도메인의 파일 서버에 연결할 수 있음을 보여 줍니다.  
  
13. **시작** 화면에서<strong>\\ \ App2\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다.  
  
    이는 SMB를 사용 하 여 리소스 도메인의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
14. 3 단계에서 CLIENT2에 대해이 절차를 반복 합니다.  
  


