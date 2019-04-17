---
title: 네트워크 부하 분산
description: 이 항목 Windows Server 2016에 네트워크 NLB (부하 분산) 기능에 대 한 개요를 제공 하 고 만드는 구성 하 고 NLB 클러스터 관리에 대 한 추가 지침은에 대 한 링크를 포함 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-nlb
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b9fd39381316a8bcd06328e7aa75492ed99bc7f1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-load-balancing"></a>네트워크 부하 분산

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 네트워크 부하 분산 \(NLB\) 기능 Windows Server 2016에 대 한 개요를 제공 하 고 만드는 구성 하 고 NLB 클러스터 관리에 대 한 추가 지침은에 대 한 링크를 포함 합니다.

NLB 단일 가상 클러스터로 두 개 이상의 서버 관리에 사용할 수 있습니다. NLB 향상 사용 가능 시간 및 확장성 FTP 웹에서 사용 되는 인터넷 서버 응용 프로그램, 방화벽 프록시, 가상 개인 네트워크 \(VPN\), 및 기타 중요 한 mission\ 서버 합니다.   

>[!NOTE]
>Windows Server 2016 소프트웨어 네트워킹 정의 \(SDN\) infrastructure의 구성 요소로 새로운 Azure 표하고자 부하 분산 소프트웨어가 \(SLB\) 포함 되어 있습니다. 사용 하는 대신 NLB SLB SDN를 사용 하는 경우 사용 하는 작업 비 Windows, 네트워크 아웃 바운드 주소 변환 필요 \(NAT\), 표시 하거나 계층 3 \(L3\) 비 TCP 기반 부하 분산 있어야 합니다. Windows Server 2016와 NLB 비 SDN 배포에 대 한 사용 하 여 계속 수 있습니다. SLB에 대 한 자세한 내용은 참조 [소프트웨어 부하 분산 SLB () SDN에 대 한](../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.

네트워크 부하 분산 \(NLB\) 기능 TCP\/IP 네트워킹 프로토콜을 사용 하 여 여러 가지 서버에서 교통량을 배포 합니다. 단일 가상 클러스터로 응용 프로그램을 실행 하는 두 개 이상의 컴퓨터에 결합 NLB 안정성 및 성능을 웹 서버에 대 한 기타 중요 한 mission\ 서버를 제공 합니다.  
  
서버 NLB 클러스터의 라고 *호스트*, 각 호스트 별도 서버 응용 프로그램의 복사본을 실행 하 고 있습니다. 클러스터의 호스트 들어오는 클라이언트 요청 nlb. 각 호스트에서 처리 하는 것을 로드를 구성할 수 있습니다. 클러스터 하기 위해 동적으로 호스트 증가 로드 처리할 수 추가할 수 있습니다. NLB 라고 하는 지정 된 단일 호스트 모든 트래픽을 보낼 수도 수 있는 *기본 호스트*합니다.  
  
NLB 컴퓨터의 모든 클러스터의 IP 주소 같은 집합으로 해결할 수 있도록 하 고 각 호스트 고유한 IP 주소 전용된 집합을 유지 관리 합니다. Load\ 균형 응용 프로그램에 대 한 호스트 실패 하거나, 오프 라인 로드 자동으로 짧은 여전히 작동 하는 컴퓨터 간에. 준비 되 면 오프 라인 컴퓨터 클러스터에 가입 고 적게 트래픽을 처리할 수에서 있는 다른 컴퓨터 수 있는 작업의 다시 투명 하 게 수 있습니다.  
  
## <a name="BKMK_APP"></a>실용적인 응용 프로그램  
NLB 비저장 등의 응용 프로그램, 인터넷 정보 서비스 \(IIS\) 실행 하는 웹 서버를의 업무 중단으로 사용할 수 있는지 확인 하는 데 유용 하 고 확장 가능 하도록 만들기 되는지 \ (부하 increases\로 서버 추가) 하 여 합니다. 다음 섹션 NLB 높은 가용성, 확장성 및 응용이 프로그램을 실행 하는 클러스터 서버 관리 효율성 지 원하는 방법을 설명 합니다.  
  
### <a name="high-availability"></a>높은 공급 일  
안정적으로 높은 가용성 시스템 적절 한 수준의 업무 중단 된 서비스를 제공합니다. NLB 높은 사용 가능 여부를 제공 하기 위해 자동으로 수행할 수 있는 built\에서 기능이 포함 됩니다.  
  
-   클러스터 호스트 실패 하거나, 오프 라인를 감지 하 고 복구 합니다.  
  
-   호스트 추가 하거나 제거 하는 경우 네트워크 부하를 분산 합니다.  
  
-   복구 하 고 10 초 내는 작업을 재배포할.  
  
### <a name="scalability"></a>확장성  
확장성은 컴퓨터, 서비스 또는 응용 프로그램 증가 성능 요구에 맞게 자랄 수 얼마나 잘 정도의입니다. NLB 클러스터 확장성 증분 클러스터의 전반적인 로드 초과 외양 하나 이상의 시스템 기존 클러스터에 추가 하는 기능입니다. 확장성을 지원 하기 위해 nlb 다음을 수행할 수 있습니다.  
  
-   개별 TCP\/IP 서비스에 대 한을 NLB 클러스터 잔액 로드 요청 합니다.  
  
-   단일 클러스터에서 최대 32 컴퓨터를 지원 합니다.  
  
-   여러 서버 로드 요청 균형 \ (같은 클라이언트 또는에서 여러 clients\) 여러 명의 호스트 클러스터에서 합니다.  
  
-   클러스터 장애를 않고도 로드 증가 함에 따라 호스트 NLB 클러스터에 추가 합니다.  
  
-   로드 감소 하는 경우 클러스터에서 호스트를 제거 합니다.  
  
-   고성능 및 파이프라인 완전히 구현 낮은 오버 사용 하도록 설정 합니다. 파이프라인 사용 요청을 이전 요청에 응답을 기다리는 없이 nlb 보낼 수 있습니다.  
  
### <a name="manageability"></a>관리  
관리 기능을 지원 하기 위해 nlb 다음을 수행할 수 있습니다.  
  
-   관리 하 고 NLB 관리자를 사용 하 여 여러 NLB 클러스터와 한 컴퓨터에서 클러스터 호스트 구성 또는 [Windows powershell에서 Cmdlet 네트워크 NLB (부하 분산)](https://technet.microsoft.com/library/hh801274.aspx)합니다.
  
-   부하 분산 동작 단일 IP 포트 또는 그룹에 대 한 포트 관리 규칙을 사용 하 여 지정 합니다.  
  
-   각 웹 사이트에 대 한 다른 포트 규칙 정의 합니다. 포트 규칙 대상 가상 IP 주소를 기초로 여러 응용 프로그램 또는 웹 사이트에 대 한 서버 load\ 균형 같은 집합을 사용 하는 경우 \(using virtual clusters\) 합니다.  

-   모든 단일 호스트 사용 하 여 옵션에 대 한 클라이언트 요청, single\ 호스트 규칙 직접 합니다. 특정 응용 프로그램을 실행 하는 특정 호스트 NLB 경로 클라이언트 요청 합니다.  

-   특정 IP 포트에 원치 않는 네트워크 액세스를 차단 합니다.  

-   그룹 관리 인터넷 프로토콜 \(IGMP\) 지원 클러스터 호스트 스위치 포트 초과 제어를 사용 하도록 설정 \ (여기서 수신 네트워크 패킷을 보낸 모든 포트에 있는 switch\) 멀티 캐스트 모드에서 작동 합니다.  

-   시작, 중지 및 Windows PowerShell 명령이 나 스크립트를 사용 하 여 원격 제어 NLB 동작 합니다.  

-   NLB 이벤트를 확인 하려면 Windows 이벤트 로그 봅니다. NLB 모든 작업과 클러스터 변경 이벤트 로그에 기록합니다.  

## <a name="important-functionality"></a>중요 한 기능  
 
표준 Windows Server 네트워킹 드라이버 구성 NLB 설치 됩니다. 해당 작업은 TCP\/IP 네트워킹 스택의 투명 하 게 됩니다. 다음 그림은 일반적인 구성 NLB 및 기타 소프트웨어 구성 요소 간의 관계 보여 줍니다.  
  
![네트워크 부하 분산 및 기타 소프트웨어 구성 요소](../media/NLB/nlb.jpg)  
  
다음은에 기본 기능입니다.  
  
- 하드웨어 변경 되지 실행 해야 합니다.  
  
- 구성 하 고 여러 클러스터와 호스트 모든에서 단일 원격 또는 로컬 컴퓨터 관리 네트워크 부하 분산 도구를 제공 합니다.  
  
- 클라이언트가 단일 논리적 인터넷 이름과 클러스터 IP 주소를 이라고 가상 IP 주소를 사용 하 여 클러스터에 액세스할 수 있게 \ (computer\ 각 개별 이름이 유지 됨). NLB 다중 홈 서버에 대 한 여러 가상 IP 주소 수 있게합니다.  
  
> [!NOTE]  
> 가상 클러스터로 Vm 배포할 때 NLB 다중 여러 가상 IP 주소를 홈 서버 필요 하지 않습니다.  
  
- 여러 네트워크 어댑터에 연결 하는 각 호스트 다중 독립 클러스터 구성할 수 있습니다 NLB 수 있습니다. 여러 개의 네트워크 어댑터에 대 한 지원 단일 네트워크 어댑터에 여러 개의 클러스터 구성할 수 있다는 가상 클러스터에서 다릅니다.  
  
- NLB 클러스터에서 실행할 수 있도록 서버 응용 프로그램에 대 한 수정 하지 필요 합니다.  
  
- 자동으로 추가 호스트 해당 클러스터 호스트 실패 하 고 이후 클러스터를 다시 온라인 상태가 구성할 수 있습니다. 추가 된 호스트 하는 클라이언트에서 새 서버 요청을 처리 시작할 수 있습니다.  
  
-   클러스터 작업 다른 호스트에 영향을 주지 않고 컴퓨터 예방 관리에 대 한 오프 라인으로 사용할 수 있습니다.  
  
## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
다음은 NLB 클러스터 실행 하는 하드웨어 요구 사항입니다.  
  
-   클러스터의 모든 호스트 같은 서브넷에 있어야 합니다.  
  
-   각 호스트에 네트워크 어댑터의 수에 제한이 이며 서로 다른 호스트 어댑터의 다른 수 있을 수 있습니다.  
  
-   내에서 각 클러스터 멀티 캐스트 또는 유니캐스트 모든 네트워크 어댑터가 있어야 합니다. NLB 멀티 캐스트 및 단일 클러스터 내 유니캐스트의 혼합된 환경을 지원 하지 않습니다.  
  
-   미디어 액세스 제어 \(MAC\) 주소 변경 유니캐스트 모드를 사용 하는 경우 네트워크 어댑터 client\ to\ 멀티 처리 하는 데 사용 되는 지원 해야 합니다.  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
다음은 NLB 클러스터 실행 하는 소프트웨어 요구 합니다.  
  
-   만 TCP\/IP NLB 사용할 수 있는 각 호스트에서 어댑터에 사용할 수 있습니다. 다른 프로토콜을 추가 하지 않고 \ (예를 들어 IPX\)이이 어댑터에 있습니다.  
  
-   서버 클러스터에 IP 주소 고정 해야 합니다.  
  
> [!NOTE]  
> NLB Dynamic Host Configuration Protocol \(DHCP\) 지원 하지 않습니다. NLB DHCP을 구성 각 인터페이스에서 사용할 수 없습니다.  
  
## <a name="BKMK_INSTALL"></a>설치 정보  
NLB NLB에 대 한 서버 관리자 또는 Windows PowerShell 명령을 사용 하 여 설치할 수 있습니다.

필요에 따라 네트워크 부하 분산 도구 로컬 또는 원격 nlb 관리를 설치할 수 있습니다. 도구 분산 관리자 및 NLB Windows PowerShell 명령 포함 됩니다.

### <a name="installation-with-server-manager"></a>서버 관리자를 사용 하 여 설치

서버 관리자에서 사용할 수 있습니다 역할 추가 및 기능 마법사 추가 하 고 **네트워크 부하 분산** 기능입니다. 마법사를 완료 NLB, 설치 하 고 컴퓨터를 다시 시작 해야 합니다.


### <a name="installation-with-windows-powershell"></a>설치를 Windows PowerShell로  

Windows PowerShell를 사용 하 여 NLB를 설치 하려면 다음 명령을 실행 Windows PowerShell 관리자 권한 프롬프트 컴퓨터에서 NLB 설치 하려는 합니다.

    
    Install-WindowsFeature NLB -IncludeManagementTools
    
설치가 완료 되 면 컴퓨터를 다시 시작 하지 필요 합니다.

자세한 내용은 참조 [설치-WindowsFeature](https://technet.microsoft.com/library/jj205467.aspx)합니다.

### <a name="network-load-balancing-manager"></a>균형 조정 관리자
균형 조정 관리자 서버 관리자에서를 열려면 클릭 **도구**, 클릭 한 다음 **분산 관리자**합니다.
  
## <a name="BKMK_LINKS"></a>추가 리소스  
다음 표에서 NLB 기능에 대 한 자세한 정보 링크를 제공합니다.  
  
|콘텐츠 종류|참조|  
|----------------|--------------|  
|배포|[균형 배포 가이드 네트워크](https://technet.microsoft.com/library/cc754833(WS.10).aspx) & #124; [구성 네트워크 부하 분산 터미널 서비스](https://technet.microsoft.com/library/cc771300(v=WS.10).aspx)|  
|작업|[네트워크 부하 분산 클러스터 관리](https://technet.microsoft.com/library/cc753954(WS.10).aspx) & #124; [네트워크 부하 분산 매개 변수 설정](https://technet.microsoft.com/library/cc731619(WS.10).aspx) & #124; [호스트 네트워크 부하 분산 클러스터에 제어](https://technet.microsoft.com/library/cc770870(WS.10).aspx)|  
|문제 해결|[문제 해결 네트워크 부하 분산 클러스터](https://technet.microsoft.com/library/cc732592(WS.10).aspx) & #124; [NLB 클러스터 이벤트 및 오류](https://technet.microsoft.com/library/cc731678(WS.10).aspx)|
|도구 및 설정|[네트워크 부하 분산 Windows PowerShell cmdlet](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|커뮤니티 리소스|[높은 가용성 \(Clustering\) 포럼](https://go.microsoft.com/fwlink/p/?LinkId=230641)