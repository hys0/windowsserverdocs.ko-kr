---
title: 인터넷에서 클러스터를 통해 5 테스트 DirectAccess 연결 단계
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8399bdfa-809a-45e4-9963-f9b6a631007f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 23aed915edb827fd0cd61e6778167108647269ea
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283339"
---
# <a name="step-5-test-directaccess-connectivity-from-the-internet-and-through-the-cluster"></a>인터넷에서 클러스터를 통해 5 테스트 DirectAccess 연결 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

CLIENT1은 DirectAccess 테스트할 준비가 완료 되었습니다.  
  
- 인터넷에서 DirectAccess 연결을 테스트 합니다. CLIENT1 시뮬레이션된 된 인터넷에 연결 합니다. 시뮬레이션된 된 인터넷에 연결 되 면 클라이언트는 공용 IPv4 주소가 할당 됩니다. DirectAccess 클라이언트는 공용 IPv4 주소를 할당할 때 IPv6 전환 기술을 사용 하는 원격 액세스 서버에 연결 하려고 합니다.  
  
- 클러스터를 통해 DirectAccess 클라이언트 연결을 테스트 합니다. 클러스터 기능을 테스트 합니다. 테스트를 시작 하기 전에 5 분 이상 EDGE1 및 EDGE2를 종료 하는 것이 좋습니다. 이 대 한 ARP 캐시 시간 제한 및 NLB에 관련 된 변경 내용을 포함 하는 이유는 많습니다. 테스트 환경에서 NLB 구성의 유효성을 검사 하는 경우 구성의 변경 내용을 반영 되지 것입니다 즉시 연결 될 때까지 기간 경과 후으로 환자의 되도록 해야 합니다. 이 다음 태스크를 수행할 때 유의 해야 합니다.  
  
    > [!TIP]  
    > 이 절차를 수행 하기 전에 Internet Explorer 캐시를 삭제 하는 연결을 테스트 하는 캐시에서 웹 페이지를 검색 하지 않도록 할 다른 원격 액세스 서버를 통해 연결을 테스트할 때마다 것이 좋습니다.  
  
## <a name="test-directaccess-connectivity-from-the-internet"></a>인터넷에서 DirectAccess 연결을 테스트  
  
1. CLIENT1을 회사 네트워크 스위치에서 분리 하 고 인터넷 스위치에 연결 합니다. 30 초 동안 기다립니다.  
  
2. 관리자 권한 Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다. 이 클라이언트 컴퓨터는 회사 네트워크에 연결 된 클라이언트 DNS 캐시에 남아 있을 수 있는 이름 확인 항목이 플러시합니다.  
  
3. Windows PowerShell 창에서 입력 **Get-dnsclientnrptpolicy** ENTER 키를 누릅니다.  
  
   NRPT(이름 확인 정책 테이블)에 대한 현재 설정이 출력에 표시됩니다. 이러한 설정을 표시 하는 모든 연결에. corp.contoso.com IPv6 주소 2001:db8:1::2 사용 하 여 원격 액세스 DNS 서버를 확인 해야 합니다. 또한 nls.corp.contoso.com이라는 이름에 대한 예외가 있음을 나타내는 NRPT 항목을 확인합니다. 예외 목록에 있는 이름에는 원격 액세스 DNS 서버에서 응답하지 않습니다. 원격 액세스 서버에 대 한 연결을 확인 하려면 원격 액세스 DNS 서버 IP 주소를 ping 할 수 있습니다. 예를 들어 2001:db8:1::2)를 ping 할 수 있습니다.  
  
4. Windows PowerShell 창에서 입력 **ping app1** ENTER 키를 누릅니다. 2001:db8:1::3이 경우에 APP1을 IPv6 주소에 대 한 회신을 볼 수 있습니다.  
  
5. Windows PowerShell 창에서 입력 **ping app2** ENTER 키를 누릅니다. EDGE1에서 APP2에 할당한 NAT64 주소(이 예제의 경우 fdc9:9f4e:eb1b:7777::a00:4)의 응답이 표시됩니다.  
  
   Ping APP2 수는 성공 APP2 IPv4 전용 리소스를 그대로 NAT64/DNS64를 사용 하 여 연결을 자동으로 연결할 수 있음을 나타내므로 중요 합니다.  
  
6. Windows PowerShell 창을 다음 절차에 대해 열어 둡니다.  
  
7. Internet Explorer 주소 표시줄에 Internet Explorer를 열고를 입력 **https://app1/** ENTER 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
8. Internet Explorer 주소 표시줄에 입력 **https://app2/** ENTER 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시됩니다.  
  
9. 에 **시작** 화면에서 입력<strong>\\\App2\Files</strong>, 한 다음 ENTER를 누릅니다. 새 텍스트 문서 파일을 두 번 클릭합니다.  
  
    이 SMB를 사용 하 여 리소스 도메인의 리소스를 가져오는 IPv4 전용 서버에 연결할 수 있음을 보여 줍니다.  
  
10. 에 **시작** 화면에서 입력**wf.msc**, 한 다음 ENTER를 누릅니다.  
  
11. 에 **Windows Firewall with Advanced Security** 만 콘솔에서 합니다 **개인** 또는 **공개 프로필** 활성화 되어 합니다. Windows 방화벽을 제대로 작동 하려면 DirectAccess에 대 한 활성화 되어야 합니다. 를 Windows 방화벽을 비활성화 하는 경우에 DirectAccess 연결 작동 하지 않습니다.  
  
12. 콘솔의 왼쪽된 창에서 확장을 **모니터링** 노드를 차례로 클릭 합니다 **연결 보안 규칙** 노드. 활성 연결 보안 규칙에 표시 됩니다. **DirectAccess 정책을 ClientToCorp**, **DirectAccess 정책을 ClientToDNS64NAT64PrefixExemption**합니다 **DirectAccess 정책을 ClientToInfra**, 및 **DirectAccess 정책 ClientToNlaExempt**합니다. 표시할 오른쪽 가운데 창을 스크롤하여 합니다 **첫 번째 인증 방법** 하 고 **두 번째 인증 방법** 열입니다. 첫 번째 규칙 (ClientToCorp) Kerberos V5를 사용 하 여 인트라넷 터널을 설정 및 세 번째 규칙 (ClientToInfra) NTLMv2를 사용 하 여 인프라 터널을 설정 합니다.  
  
13. 콘솔의 왼쪽된 창에서 확장을 **보안 연결** 노드를 차례로 클릭 합니다 **주 모드** 노드. NTLMv2를 사용 하 여 인프라 터널 보안 연결 및 Kerberos V5를 사용 하 여 인트라넷 터널 보안 연결을 확인 합니다. 보여 주는 항목을 마우스 오른쪽 단추로 클릭 **(Kerberos V5) 사용자** 으로 **두 번째 인증 방법** 클릭 **속성**합니다. 에 **일반** 탭을 확인할 수 있습니다 합니다 **두 번째 인증 로컬 ID** 은 **CORP\User1**, User1을 사용 하 여 CORP 도메인에 정상적으로 인증할 수 있음을 나타내는 Kerberos입니다.  
  
## <a name="test-directaccess-client-connectivity-through-the-cluster"></a>클러스터를 통해 DirectAccess 클라이언트 연결 테스트  
  
1. EDGE2에서 정상 종료를 수행 합니다.  
  
   이러한 테스트를 실행할 때 서버의 상태를 확인 하려면 네트워크 부하 분산 관리자를 사용할 수 있습니다.  
  
2. CLIENT1에서 Windows PowerShell 창에서 입력 **ipconfig /flushdns** ENTER 키를 누릅니다. 이 클라이언트 DNS 캐시에에서 남아 있을 수 있는 이름 확인 항목이 플러시합니다.  
  
3. Windows PowerShell 창에서 APP1 및 APP2를 ping 합니다. 이러한 리소스에서 응답을 받게 됩니다.  
  
4. 에 **시작** 화면에서 입력<strong>\\\app2\files</strong>합니다. APP2 컴퓨터의 공유 폴더에 표시 됩니다. APP2의 파일 공유를 열 수는 사용자에 대 한 Kerberos 인증을 요구 하는 두 번째 터널을 제대로 작동 하는지 나타냅니다.  
  
5. Internet Explorer를 열고 다음 웹 사이트 https://app1/ 고 https://app2/ 입니다. 첫 번째와 두 번째 터널 구성 되는지 확인 하는 두 웹 사이트를 열 수 있고 작동 합니다. Internet Explorer를 닫습니다.  
  
6. EDGE2 컴퓨터를 시작 합니다.  
  
7. EDGE1에서 정상 종료를 수행 합니다.  
  
8. 5 분 동안 기다린 후 CLIENT1에 반환 합니다. 2 ~ 5 단계를 수행 합니다. CLIENT1를 투명 하 게 장애 조치 EDGE2 EDGE1를 사용할 수 없게 후 수 있음을 확인 합니다.
