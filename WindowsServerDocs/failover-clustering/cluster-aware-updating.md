---
title: "개요 클러스터 인식 업데이트"
ms.topic: article
ms.prod: windows-server-threshold
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 3/23/2017
description: "클러스터 업데이트 (CAU) 자동화 Windows Server 실행 클러스터에서 소프트웨어 업데이트를 설치 합니다."
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: 68336741accabd6e4cb0da5dbd708be707f68df6
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-overview"></a>개요 클러스터 인식 업데이트

> 에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Cluster\ 인식 업데이트 \(CAU\), 자동화 소프트웨어 공급 일을 하면서 클러스터 서버에서는 프로세스를 업데이트 하는 기능을 소개 합니다.

> [!NOTE]
> 업데이트할 때 [Storage Spaces Direct](../storage/storage-spaces/storage-spaces-direct-overview.md) 클러스터, 것이 좋습니다 클러스터 업데이트를 사용 합니다.
  
## <a name="BKMK_OVER"></a>기능 설명  
클러스터 인식 업데이트는 업데이트 서버에 수 있는 자동화 된 기능을 [클러스터 장애 조치](failover-clustering-overview.md) 사용 가능한 업데이트 프로세스 도중 거의 또는 전혀 손실 됩니다. 업데이트를 실행 하는 동안 다음과 같은 작업을 수행 투명 하 게 인식 클러스터 업데이트:  

1. 각 노드에서 클러스터 노드에서 유지 관리 모드로 모드로 전환 합니다.
2. 클러스터 노드에서 끄기 역할으로 이동합니다.
3. 업데이트 및 종속 업데이트를 모두 설치합니다.
4. 필요한 경우 컴퓨터를 다시 시작을 수행 합니다.
5. 유지 관리 모드 노드를 제공 합니다.
6. 클러스터 노드에서 역할을 복원합니다.
7. 다음 노드 업데이트를 이동 합니다.

자동 업데이트 프로세스가 트리거하는 클러스터의 많은 클러스터 역할에 대 한 계획된 장애 조치입니다. 연결 된 클라이언트에 대 한 일시적인 서비스가 중단을 발생할 수 있습니다. 그러나 같은 실시간 마이그레이션 Hyper\ V 또는 파일 서버 SMB 투명 장애 조치를 계속 사용할 수 있는 작업의 경우 업데이트 클러스터 인식 서비스 사용 가능성에 영향을 주지 클러스터 업데이트 조정할 수 있습니다.    
  
## <a name="practical-applications"></a>실용적인 응용 프로그램  
  
-   CAU 클러스터 서비스의 서비스 중단을 줄일 수 하 고 해결, 업데이트 수동에 대 한 필요성을 줄일 수 end\ to\ 엔드 클러스터 더욱 신뢰할 수 있는 프로세스는 관리자에 대 한 업데이트 하면 됩니다. 계속 해 서 사용 가능한 클러스터 작업 파일을 계속 사용할 수 있는 서버의 등와 함께에서 CAU 기능을 사용할 경우 \ (파일 서버 작업이 SMB 투명 Failover\로) 또는 Hyper\ V를 클러스터 클라이언트에 대 한 서비스 제공에 0 영향을 주는 업데이트를 수행할 수 있습니다.  
  
-   CAU 엔터프라이즈 일관 되 게 IT 프로세스의 채택을 수 있습니다. 프로필 실행 업데이트 다양 한 종류의 클러스터 장애 조치를 생성 하 고 관리할 수 중앙 다른 lines\ of\-비즈니스 또는 관리자가 클러스터 관리 하는 경우에 CAU 배포 IT 조직에서 업데이트를 적용을 일관 되 게 수 있도록 파일 공유 합니다.  
  
-   CAU 업데이트 실행 일, 주 또는 월 정기적 클러스터 업데이트 다른 IT 관리 프로세스를 제어 하는 데 도움이 예약할 수 있습니다.  
  
-   CAU extensible 아키텍처 cluster\ 인식 방식에서 클러스터 소프트웨어 업데이트를 제공 합니다. 이 조정 소프트웨어 업데이트 Microsoft 또는 Windows 업데이트를 게시 되지 않은 또는 예를 들어, Microsoft에서 제공 되지 않은 non\ Microsoft 디바이스 드라이버에 대 한 업데이트를 설치 하는 데 게시자가 사용할 수 있습니다.  
  
-   CAU self\ 업데이트 모드에서는 "클러스터 상자에" 기기 \ (일반적으로 한 chassis\ 포장 클러스터 물리적 컴퓨터 설정)를 자동으로 업데이트 합니다. 일반적으로 이러한 기기 클러스터 관리 최소화 로컬 IT 지원 지점에서 배포 됩니다. 모드 Self\ 업데이트 배포 이러한 시나리오에서 멋진 가치를 제공 합니다.  
  
## <a name="important-functionality"></a>중요 한 기능  
다음은 중요 업데이트 클러스터 인식 기능에 대 한 설명을입니다.  
  
-   사용자 인터페이스 \(UI\)-인식 업데이트 클러스터 창-및 cmdlet 적용, 모니터, 미리 보기를 사용 하 고 업데이트를 보고 수 있는  
  
-   Cluster\ 업데이트 작업의 end\ to\ 엔드 자동화 \ 하나 이상의 업데이트 Coordinator 컴퓨터도 잘 배합 (된 업데이트 Run\),  
  
-   중요 한 적용할 기존 Windows 업데이트 에이전트 \(WUA\) 및 Windows Server Update Services \(WSUS\) Windows server에서는 인프라와 통합 된 plug\에서 기본 Microsoft 업데이트  
  
-   두 번째 plug\에서 사용할 수 있는 Microsoft 핫픽스 적용 하 고 non\ Microsoft 업데이트를 적용 하려면 사용자 지정할 수 있습니다  
  
-   업데이트를 실행 프로필을 최대 시간을 업데이트 노드 당 다시 시도 됩니다 등 실행 업데이트 옵션을 설정으로 구성 됩니다. 업데이트를 실행 프로필을 사용 하 여 신속 하 게 실행 업데이트를 통해 하면 같은 설정을 다시 사용 하 고 다른 장애 클러스터와 업데이트 설정을 쉽게 공유할 수 있습니다.  
  
-   새로운 plug\ 기능 개발 도구 업데이트 BIOS 사용자 지정 소프트웨어 설치 관리자 같은 클러스터에서 다른 node\ 업데이트 도구를 조정 하 고 네트워크 어댑터 또는 호스트 버스 어댑터 \(HBA\) 업데이트 도구를 지 원하는 extensible 아키텍처 합니다.  
  
클러스터 인식 업데이트 전체 클러스터 업데이트 두 가지 모드에서 작업을 조정할 수 있습니다.  
  
-   **모드 Self\ 업데이트** 이 모드에 대 한 CAU 클러스터 역할 업데이트 하는 장애 클러스터에서 작업으로 구성 되어 있고 관련 된 업데이트 일정 정의 됩니다. 클러스터 업데이트에 기본 또는 사용자 지정 실행 업데이트 프로필을 사용 하 여 시간을 예약 합니다. 업데이트를 실행 하는 동안 현재 CAU 클러스터 역할 소유 하 고 노드에서 CAU 업데이트 Coordinator 프로세스를 시작 하 고 프로세스 클러스터 노드에서 각 업데이트를 순서 대로 수행 합니다. 현재 클러스터 노드에서 업데이트 하려면 CAU 클러스터 역할 장애 조치를 다른 클러스터 노드에서 되 고 해당 노드에서 새 업데이트 Coordinator 프로세스 가정 실행 업데이트를 제어 합니다. Self\ 업데이트 모드로 CAU 완벽 하 게 자동화 된 end\ to\ 엔드 업데이트 프로세스를 사용 하 여 클러스터 장애 조치를 업데이트할 수 있습니다. 관리자가 수도 트리거 on\ 주문형이이 모드에서는 업데이트나 간단 하 게 사용 하는 경우 접근 remote\ 업데이트 필요 합니다. Self\ 업데이트 모드로 관리자 열 수 있는 업데이트를 실행 하는 것에 대 한 요약 정보 진행 중에서 클러스터에 연결 하 고 실행는 **Get\ CauRun** Windows PowerShell cmdlet 합니다.  
  
-   **모드 Remote\ 업데이트** 이 모드에 대 한 업데이트 Coordinator 라는 원격 컴퓨터 CAU 도구 구성 되어 있습니다. 업데이트 Coordinator 업데이트 실행 하는 동안 업데이트 되는 클러스터의 구성원이 아닙니다. 원격 컴퓨터에서 관리자 트리거하 기본 또는 사용자 지정 실행 업데이트 프로필을 사용 하 여는 on\ 수요 업데이트를 실행 합니다. 모드 Remote\ 업데이트의 업데이트를 실행 하는 동안 real\ 시간 진행 상태를 모니터링 하 고 서버 Core 설치에서 실행 되는 클러스터에 유용 합니다.  
  
## <a name="hardware-and-software-requirements"></a>하드웨어 및 소프트웨어 요구 사항  

CAU 서버 Core 설치를 비롯 한 Windows Server의 모든 버전에서 사용할 수 있습니다. 요구 사항 세부 정보를 참조 하세요. [클러스터 인식 업데이트 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)합니다.

### <a name="installing-cluster-aware-updating"></a>클러스터 인식 업데이트 설치
CAU을 사용 하려면 Windows Server의 클러스터링 기능을 설치 하 고 클러스터 장애 조치를 생성 합니다. 구성 요소 CAU 기능을 지 원하는 각 클러스터 노드에서 자동으로 설치 됩니다.

장애 조치 클러스터링 기능을 설치 하려면 다음 도구를 사용할 수 있습니다.
- 역할 및 기능 마법사 서버 관리자에서 추가
- [설치 WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature) Windows PowerShell cmdlet
- 배포 이미지 서비스 및 관리 (DISM) 명령줄 도구

자세한 내용은 참조 [설치 또는 제거 역할, 역할 서비스 또는 기능](https://technet.microsoft.com/library/hh831809(v=ws.11).aspx)합니다.

또한 원격 서버 관리 도구 포함 되며 서버 관리자의 클러스터링 기능을 설치 하면 기본적으로 설치 되는 장애 클러스터링 도구를 설치 해야 합니다. 클러스터링 도구는 사용자 인터페이스 클러스터 인식 업데이트와 PowerShell cmdlet 포함 됩니다. 

다양 한 CAU 업데이트 모드를 지원 하기 위해 다음과 같은 클러스터링 도구 장애 조치를 설치 해야 합니다.

- CAU self\ 업데이트 모드에서를 사용 하려면 각 클러스터 노드에서 장애 클러스터링 도구를 설치 합니다.   
  
- Remote\ 업데이트 모드를 사용 하려면 장애 조치 클러스터링 도구 클러스터 장애 조치 네트워크 연결 된 컴퓨터에 설치 합니다.  
  
> [!NOTE]  
> -   Windows Server 2012에서 장애 조치 클러스터링 도구를 사용 하 여 최신 버전의 Windows Server에서 클러스터 인식 업데이트를 관리 수 없습니다. 
> -   클러스터 노드에서 장애 클러스터링 도구 설치 CAU 모드로 remote\ 업데이트를 사용 하려면 필요 하지 않습니다. 그러나 일부 CAU 기능이 제공 됩니다. 자세한 내용은 참조 [요구 사항 및 모범 사례 Cluster\ 인식 업데이트에 대 한](cluster-aware-updating-requirements.md)합니다.  
> -   CAU 모드로 self\ 업데이트를 사용 하지 않으면 CAU 도구가 설치 되어 있는 및 업데이트를 조정 하 컴퓨터 장애 클러스터의 회원 수 없습니다.  
  
### <a name="enabling-self-updating-mode"></a>자동으로 업데이트 모드 사용
자동으로 업데이트 모드를 사용 하려면 클러스터 인식 업데이트 클러스터 역할 클러스터 장애 조치를 추가 해야 합니다. 이렇게 하려면 다음 방법 중 하나를 사용 하 여 다음과 같습니다.
- 서버 관리자에서 선택 **도구** > **클러스터 인식 업데이트**, 다음 클러스터 인식 업데이트 창에 선택 **구성 클러스터 자동 업데이트 옵션**합니다. 
- PowerShell 세션에서 실행는 [추가 CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole) cmdlet 합니다.  
  
CAU 제거, 클러스터링 기능 하거나 장애 클러스터링 도구 서버 관리자를 사용 하 여 드라이브를 제거 하는 [제거 WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/uninstall-windowsfeature) cmdlet, 또는 DISM command\ 줄 도구입니다.  
  
### <a name="additional-requirements-and-best-practices"></a>추가 요구 사항 및 모범 사례  

성공적으로, 한 CAU 사용 하 여 클러스터 장애 조치 환경을 구성에 대 한 추가 지침은 CAU 클러스터 노드에서 업데이트할 수 있도록 모범 사례 CAU 분석기 실행할 수 있습니다.  
  
자세한 요구 사항 및 모범 사례 CAU 분석기를 실행 하는 것에 대 한 정보, CAU 사용에 대 한 유용한 참조 [요구 사항 및 모범 사례 Cluster\ 인식 업데이트에 대 한](cluster-aware-updating-requirements.md)합니다.  
  
### <a name="starting-cluster-aware-updating"></a>클러스터 인식 업데이트를 시작합니다.  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>서버에서 관리자 클러스터 인식 업데이트 시작 하려면  
  
1.  서버 관리자를 시작 합니다.  
  
2.  다음 중 하나를 수행 합니다.  
  
    -   에 **도구** 메뉴를 클릭 **Cluster\ 인식 업데이트**합니다.  
  
    -   클러스터 노드가 또는 클러스터에서 서버 관리자에 추가 되 면는 **모든 서버** 페이지, 클릭 right\ 노드의 이름 \ (또는 cluster\ 이름)을 차례로 클릭 하 고 **업데이트 클러스터**합니다.  
  
## <a name="see-also"></a>참조 하십시오  
다음 링크 클러스터 인식 업데이트를 사용 하 여에 대 한 자세한 정보를 제공 합니다.  
  
-   [요구 사항 및 모범 사례 Cluster\ 인식 업데이트에 대 한](cluster-aware-updating.md)  
  
-   [Cluster\ 인식 업데이트: 질문과 대답](cluster-aware-updating-faq.md)  
  
-   [고급 옵션 및 실행된 프로필 CAU에 대 한 업데이트](cluster-aware-updating-options.md)  
  
-   [CAU Plug\ 기능이 작동 방식](cluster-aware-updating-plug-ins.md)  
  
-   [Windows PowerShell Cluster\ 인식 업데이트 Cmdlet](https://go.microsoft.com/fwlink/p/?LinkId=237675)  
  
-   [Cluster\ 인식 Plug\에서 참조 업데이트](https://msdn.microsoft.com/library/hh418084.aspx)  
  

