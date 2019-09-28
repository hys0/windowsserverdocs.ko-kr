---
ms.assetid: aac117a7-aa7a-4322-96ae-e3cc22ada036
title: RID 발급 관리
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: dd265fecce06b849bd14d4d6b81503aba7311656
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390066"
---
# <a name="managing-rid-issuance"></a>RID 발급 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 RID 마스터의 새로운 발급 및 모니터링 기능과 RID 발급 분석 및 문제 해결 방법을 비롯하여 RID 마스터 FSMO 역할의 변경 내용을 설명합니다.  
  
-   [RID 발급 관리](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Manage)  
  
-   [RID 발급 문제 해결](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Tshoot)  
  
자세한 내용은 제공 되는 [AskDS 블로그](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)합니다.  
  
## <a name="BKMK_Manage"></a>RID 발급 관리  
기본적으로 도메인은 사용자, 그룹 및 컴퓨터와 같은 보안 주체를 10억 개 가량 수용할 수 있지만 이처럼 많은 개체가 활발하게 사용되는 도메인은 없습니다. 하지만 Microsoft 고객 지원에서는 다음과 같은 사례를 발견했습니다.  
  
-   소프트웨어 또는 관리 스크립트 프로비전에서 실수로 사용자, 그룹 및 컴퓨터를 대량으로 만든 경우  
  
-   위임된 사용자가 사용되지 않는 많은 보안 및 메일 그룹을 만든 경우  
  
-   많은 도메인 컨트롤러가 강등 또는 복원되었거나 메타데이터가 정리된 경우  
  
-   포리스트 복구가 수행된 경우  
  
-   InvalidateRidPool 작업이 자주 수행된 경우  
  
-   RID 블록 크기 레지스트리 값이 잘못 증가된 경우  
  
이 모든 상황에서 RID가 불필요하게 소진되며, 이는 실수에서 비롯된 경우가 많습니다. 지난 몇 년 동안 일부 소수의 환경에서는 RID가 부족했고, 그로 인해 새 도메인으로 마이그레이션하거나 포리스트를 복구해야 했습니다.  
  
Windows Server 2012에서는 Active Directory의 사용 연한 및 편재로 인해 문제가 되는 경우에만 RID 할당 문제를 해결합니다. 여기에 향상 된 이벤트 로깅, 보다 적절 한 제한 수에-비상시에서 도메인에 대 한 전역 RID 공간의 전체 크기를 두 번 포함 됩니다.  
  
### <a name="periodic-consumption-warnings"></a>정기적인 사용 경고  
Windows Server 2012에서는 주요 지표를 교차한 경우 조기 경고를 제공하는 전역 RID 공간 이벤트 추적 기능이 추가되었습니다. 이 모델은 전역 풀에서 10% 사용 표시를 계산하여 여기에 도달한 경우 이벤트를 로깅합니다. 그런 다음 나머지 공간의 10% 사용을 계산하는 식으로 이벤트 주기가 계속됩니다. 전역 RID 공간이 소진됨에 따라 줄어드는 풀에서 10%에 도달하는 속도가 빨라져 이벤트가 가속화됩니다(하지만 이벤트 로그 완화로 인해 시간당 두 번 이상의 입력이 방지됨). 모든 도메인 컨트롤러의 시스템 이벤트 로그에서 Directory-Services-SAM 경고 이벤트 16658을 기록합니다.  
  
기본 30비트 전역 RID 공간을 가정할 때 첫 번째 이벤트는 107,374,182번째<sup></sup> RID를 포함하는 풀을 할당할 때 로깅됩니다. 총 110개의 이벤트가 생성되는 마지막 검사점(100,000)까지 이벤트 속도가 자연적으로 가속화됩니다. 이 동작은 잠금 해제된 31비트 전역 RID 공간(214,748,365에서 시작하고 117개의 이벤트로 완료됨)에서도 유사합니다.  
  
> [!IMPORTANT]  
> 이 이벤트는 예상치 못한 것이므로 도메인에서 사용자, 컴퓨터 및 그룹 만들기 프로세스를 즉시 조사해야 합니다. 1억 개보다 많은 AD DS 개체를 만드는 것은 일반적인 상황이 아닙니다.  
  
![RID 발급](media/Managing-RID-Issuance/ADDS_RID_TR_EventWaypoints2.png)  
  
### <a name="rid-pool-invalidation-events"></a>RID 풀 무효화 이벤트  
로컬 DC RID 풀이 삭제되었음을 알리는 새로운 이벤트가 있습니다. 이는 정보 이벤트이며, 특히 새로운 VDC 기능으로 인해 예상할 수 있습니다. 이 이벤트에 대한 자세한 내용은 아래의 이벤트 목록을 참조하세요.  
  
### <a name="BKMK_RIDBlockMaxSize"></a>RID 블록 크기 제한  
일반적으로 도메인 컨트롤러는 한 번에 500개의 RID 블록에서 RID 할당을 요청합니다. 도메인 컨트롤러에서 다음 레지스트리 REG_DWORD 값을 사용하여 이 기본값을 재정의할 수 있습니다.  
  
```  
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\RID Values  
RID Block Size  
  
```  
  
Windows Server 2012 이전에는 값이 0xffffffff 또는 4294967295인 암시적 DWORD 최대값 외에는 이 레지스트리 키에 적용되는 최대값이 없었습니다. 이 값은 전체 전역 RID 공간보다 훨씬 큽니다. 관리자는 부적절하거나 실수로 전역 RID를 매우 빠르게 소진하는 값으로 RID 블록 크기를 구성할 때가 있습니다.  
  
Windows Server 2012에서는 이 레지스트리 값을 10진수 15,000(16진수 0x3A98)보다 크게 설정할 수 없습니다. 따라서 의도하지 않은 대규모 RID 할당이 방지됩니다.  
  
15,000보다 *큰* 값을 설정하면 15,000으로 간주되며, 값이 수정될 때까지 도메인 컨트롤러에서는 다시 부팅할 때마다 디렉터리 서비스에 이벤트 16653을 로깅합니다.  
  
### <a name="BKMK_GlobalRidSpaceUnlock"></a>전역 RID 공간 크기 잠금 해제  
Windows Server 2012 이전 전역 RID 공간이 2 개로 제한 되었습니다<sup>30</sup> (또는 1073741823) 개의 Rid 총 합니다. 이 제한에 도달하면 도메인을 마이그레이션하거나 이전 기간으로 포리스트를 복구하는 경우에만 새 SID를 만들 수 있었습니다(어떤 기준에서든 재해 복구에 해당). Windows Server 2012부터 전역 풀을 2,147,483,648개의 RID로 늘리기 위해 2<sup>31</sup>비트의 잠금을 해제할 수 있습니다.  
  
AD DS에서는 모든 도메인 컨트롤러의 RootDSE 컨텍스트에서 **SidCompatibilityVersion**이라는 특수한 숨겨진 특성에 이 설정을 저장합니다. 이 특성은 ADSIEdit, LDP 또는 기타 도구를 사용하여 읽을 수 없습니다. 전역 RID 공간의 증가를 확인하려면 시스템 이벤트 로그에서 Directory-Services-SAM의 경고 이벤트 16655를 검토하거나 다음 Dcdiag 명령을 사용합니다.  
  
```  
Dcdiag.exe /TEST:RidManager /v | find /i "Available RID Pool for the Domain"  
  
```  
  
전역 RID 풀을 늘리면 사용 가능한 풀이 기본 1,073,741,823에서 2,147,483,647로 변경됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![RID 발급](media/Managing-RID-Issuance/ADDS_RID_TR_Dcdiag.png)  
  
> [!WARNING]  
> 이 잠금 해제는 RID 부족을 방지하기 의도일 *뿐*이며 RID 최대값 적용(다음 섹션 참조)과 함께 사용하는 경우에*만* 사용할 수 있습니다. 응용 프로그램 호환성 문제는 잠금 해제된 RID 풀에서 생성된 SID에 잠재적으로 존재하므로 수백만 개의 RID가 남아 있고 느리게 증가하는 환경에서는 이를 "미리" 설정하지 마세요.  
>   
> 이 잠금 해제 작업은 이전 백업으로 전체 포리스트 복구를 수행하는 경우 외에는 되돌리거나 제거할 수 없습니다.  
  
#### <a name="important-caveats"></a>중요한 제한 사항  
Windows Server 2003 및 Windows Server 2008 도메인 컨트롤러는 전역 RID 풀의 31번째<sup></sup> 비트가 잠금 해제된 경우 RID를 발급할 수 없습니다. Windows Server 2008 R2 도메인 컨트롤러 *수* 31를 사용 하 여<sup>st</sup> 비트의 Rid *경우에* 핫픽스 있는 [KB 2642658](https://support.microsoft.com/kb/2642658) 설치 합니다. 지원되지 않는 도메인 컨트롤러 및 패치가 적용되지 않은 도메인 컨트롤러는 잠금 해제된 경우 전역 RID 풀을 소진된 것으로 간주합니다.  
  
이 기능은 도메인 기능 수준에서 적용되지 않습니다. 도메인에는 Windows Server 2012 또는 업데이트된 Windows Server 2008 R2 도메인 컨트롤러만 존재합니다.  
  
#### <a name="implementing-unlocked-global-rid-space"></a>잠금 해제된 전역 RID 공간 구현  
RID 풀을 31 번째 잠금을 해제 하려면<sup>st</sup> 비트 (아래 참조)의 RID 최대값 알림을 받은 후 다음 단계를 수행 합니다.  
  
1.  RID 마스터 역할이 Windows Server 2012 도메인 컨트롤러에서 실행되고 있는지 확인합니다. 그렇지 않으면 Windows Server 2012 도메인 컨트롤러로 전송합니다.  
  
2.  LDP.exe를 실행합니다.  
  
3.  **연결** 메뉴를 클릭하고 포트 389에서 Windows Server 2012 RID 마스터에 대해 **연결**한 다음 도메인 관리자로 **바인딩**을 클릭합니다.  
  
4.  클릭 하 고 **찾아보기** 메뉴를 클릭 **수정**합니다.  
  
5.  확인 **DN** 비어 있습니다.  
  
6.  **항목 편집 특성**, 유형:  
  
    ```  
    SidCompatibilityVersion  
    ```  
  
7.  **값**, 유형:  
  
    ```  
    1  
    ```  
  
8.  **작업**에 **추가**가 선택되어 있는지 확인하고 **입력**을 클릭합니다. 이 업데이트는 **항목 목록**합니다.  
  
9. 선택 된 **동기** 및 **확장** 옵션을 차례로 클릭 합니다. **실행**합니다.  
  
    ![RID 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModify.png)  
  
10. 성공한 경우 LDP 출력 창이 표시됩니다.  
  
    ```  
    ***Call Modify...  
     ldap_modify_ext_s(Id, '(null)',[1] attrs, SvrCtrls, ClntCtrls);  
    modified "".  
  
    ```  
  
    ![RID 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModifySuccess.png)  
  
11. 해당 도메인 컨트롤러의 시스템 이벤트 로그에서 Directory-Services-SAM 정보 이벤트 16655를 검토하여 전역 RID 풀이 증가되었는지 확인합니다.  
  
### <a name="rid-ceiling-enforcement"></a>RID 최대값 적용  
보호 조치를 취하고 관리 인식을 강화하기 위해 Windows Server 2012에는 전역 RID 범위에 대한 인공 최대값(전역 공간에 남은 RID가 10%인 상태)이 도입되었습니다. 인공 최대값의 1% 이내에 들면 RID 풀을 요청하는 도메인 컨트롤러에서 해당 시스템 이벤트 로그에 Directory-Services-SAM 경로 이벤트 16656을 기록합니다. 또한 RID 마스터 FSMO에서 10% 상한값에 도달하면 해당 시스템 이벤트 로그에 Directory-Services-SAM 이벤트 16657을 기록하고 최대값을 재정의할 때까지 추가 RID 풀을 할당하지 않습니다. 따라서 도메인의 RID 마스터 상태를 평가하고 잠재적인 RID 할당 급증을 해결해야 합니다. 이는 도메인이 전체 RID 공간을 소진하는 것을 방지하기도 합니다.  
  
이 최대값은 사용 가능한 RID 공간이 10% 남은 수준에서 하드 코드됩니다. 즉, RID 마스터가 전역 RID 공간의 90%에 해당하는 RID가 포함된 풀을 할당할 경우 최대값이 활성화됩니다.  
  
-   기본 도메인의 경우 첫 번째 트리거 시점은 2<sup>30</sup>-1 * 0.90 = 966,367,640(또는 남은 RID 107,374,183개)입니다.  
  
-   잠금 해제된 31비트 RID 공간이 있는 도메인의 경우 트리거 시점은 2<sup>31</sup>-1 * 0.90 = 1,932,735,282개의 RID(또는 남은 RID 214,748,365개)입니다.  
  
트리거되면 RID 마스터가 해당 개체에서 Active Directory 특성 **msDS-RIDPoolAllocationEnabled**(일반 이름 **ms-DS-RID-Pool-Allocation-Enabled**)를 FALSE로 설정합니다.  
  
CN = RID Manager$, CN = System, DC = *<domain>*  
  
그러면 16657 이벤트가 기록되고 모든 도메인 컨트롤러에 대한 추가 RID 블록 발급이 차단됩니다. 도메인 컨트롤러는 이미 발급된 미처리 RID 풀을 계속 사용합니다.  
  
블록을 제거하고 RID 풀 할당이 계속되도록 허용하려면 이 값을 TRUE로 설정합니다. RID 마스터에서 다음에 RID 할당을 수행할 때 특성이 해당 기본값인 NOT SET 값으로 복원됩니다. 이후에는 더 이상 최대값이 없으므로 전역 RID 공간이 소진되어 포리스트를 복구하거나 도메인을 마이그레이션해야 합니다.  
  
#### <a name="removing-the-ceiling-block"></a>최대값 블록 제거  
인공 최대값에 도달한 후 블록을 제거하려면 다음 단계를 수행합니다.  
  
1.  RID 마스터 역할이 Windows Server 2012 도메인 컨트롤러에서 실행되고 있는지 확인합니다. 그렇지 않으면 Windows Server 2012 도메인 컨트롤러로 전송합니다.  
  
2.  LDP.exe를 실행합니다.  
  
3.  **연결** 메뉴를 클릭하고 포트 389에서 Windows Server 2012 RID 마스터에 대해 *연결*한 다음 도메인 관리자로 **바인딩**을 클릭합니다.  
  
4.  클릭 된 **보기** 메뉴를 클릭 **트리**, 에 대 한 다음는 **Base DN** RID 마스터의 자체 도메인 명명 컨텍스트를 선택 합니다. **확인**을 클릭합니다.  
  
5.  탐색 창에서 드릴 다운은 **CN = System** 컨테이너를 클릭은 **CN = RID Manager$** 개체입니다. 마우스 오른쪽 단추로 클릭 하 고 클릭 **수정**합니다.  
  
6.  항목 편집 특성에 다음을 입력합니다.  
  
    ```  
    MsDS-RidPoolAllocationEnabled  
    ```  
  
7.  **값**에 다음(대문자)을 입력합니다.  
  
    ```  
    TRUE  
    ```  
  
8.  **작업**에서 **바꾸기**를 선택하고 **입력**을 클릭합니다. 이 업데이트는 **항목 목록**합니다.  
  
9. 사용 하도록 설정 된 **동기** 및 **확장** 옵션을 차례로 클릭 합니다. **실행**:  
  
    ![RID 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeiling.png)  
  
10. 성공한 경우 LDP 출력 창이 표시됩니다.  
  
    ```  
    ***Call Modify...  
    ldap_modify_ext_s(ld, 'CN=RID Manager$,CN=System,DC=<domain>',[1] attrs, SvrCtrls, ClntCtrls);  
    Modified "CN=RID Manager$,CN=System,DC=<domain>".  
  
    ```  
  
    ![RID 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeilingSuccess.png)  
  
### <a name="other-rid-fixes"></a>기타 RID 수정 프로그램  
이전 Windows Server 운영 체제에서는 rIDSetReferences 특성이 누락된 경우 RID 풀 누수가 발생했습니다. Windows Server 2008 r 2를 실행 하는 도메인 컨트롤러에서이 문제를 해결 하려면에서 핫픽스를 설치 [KB 2618669](https://support.microsoft.com/kb/2618669)합니다.  
  
### <a name="unfixed-rid-issues"></a>해결되지 않은 RID 문제  
지금까지 계정 만들기에 실패한 경우 RID 누수가 발생했습니다. 즉, 계정을 만들 때 오류로 인해 여전히 RID가 소진됩니다. 일반적인 예로, 복잡성을 충족하지 않는 암호로 사용자를 만드는 경우가 있습니다.  
  
### <a name="rid-fixes-for-earlier-versions-of-windows-server"></a>이전 버전의 Windows Server에 대한 RID 수정 프로그램  
위의 모든 수정 프로그램 및 변경 내용에서 Windows Server 2008 R2 핫픽스가 릴리스되었습니다. 현재 계획되거나 진행 중인 Windows Server 2008 핫픽스는 없습니다.  
  
## <a name="BKMK_Tshoot"></a>RID 발급 문제 해결  
  
### <a name="introduction-to-troubleshooting"></a>문제 해결 소개  
RID 발급 문제 해결에는 논리적이고 선형적인 방법이 필요합니다. RID에서 트리거된 경고 및 오류에 대해 이벤트 로그를 신중하게 모니터링하지 않으면 계정 만들기에 실패하는 문제가 가장 먼저 발생할 가능성이 높습니다. RID 발급 문제 해결의 핵심은 증상이 예상된 경우 또는 그렇지 않은 경우를 이해하는 것입니다. 많은 RID 발급 문제는 하나의 도메인 컨트롤러에만 영향을 줄 수 있으며 구성 요소 개선 사항과는 관련이 없습니다. 아래의 간단한 다이어그램은 이러한 사항에 대한 보다 명확한 의사 결정을 도와줍니다.  
  
![RID 발급](media/Managing-RID-Issuance/adds_rid_issuance_troubleshooting.png)  
  
### <a name="troubleshooting-options"></a>문제 해결 옵션  
  
#### <a name="logging-options"></a>로깅 옵션  
RID 발급의 모든 로그는 시스템 이벤트 로그의 원본 Directory-Services-SAM 아래에 기록됩니다. 로깅은 기본적으로 사용하도록 설정되며 최대한의 자세한 표시 수준으로 구성됩니다. Windows Server 2012의 새로운 구성 요소 변경 내용에 대해 로깅된 항목이 없는 경우에는 이 문제를 Windows 2008 R2 또는 이전 운영 체제에서 확인된 기존의(Windows Server 2012 이전의 레거시) RID 발급 문제로 간주합니다.  
  
#### <a name="utilities-and-commands-for-troubleshooting"></a>문제 해결을 위한 유틸리티 및 명령  
앞서 설명한 로그에 설명되지 않은 문제, 특히 이전 RID 발급 문제를 해결하려면 먼저 다음 도구 목록을 사용하는 것에서 시작합니다.  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   Network Monitor 3.4  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>도메인 컨트롤러 구성 문제 해결을 위한 일반적인 방법  
  
1.  단순한 사용 권한 또는 도메인 컨트롤러 가용성 문제로 인해 오류가 발생하나요?  
  
    1.  필요한 권한 없이 보안 주체를 만들려고 했나요? 액세스 거부 오류에 대한 출력을 검토해 보세요.  
  
    2.  도메인 컨트롤러를 사용할 수 있나요? 반환된 오류나 LDAP 또는 도메인 컨트롤러 가용성 메시지를 검토해 보세요.  
  
2.  반환된 오류에 RID가 구체적으로 언급되어 있고 지침으로 사용할 수 있는 구체적인 정보가 포함되어 있나요? 그렇다면 해당 지침을 따르세요.  
  
3.  반환된 오류에 RID가 구체적으로 언급되어 있지만 그 밖에 "디렉터리 서비스가 관련 식별자를 할당할 수 없어 개체를 만들 수 없습니다."와 같은 특정한 정보는 없나요?  
  
    1.  "레거시" (Windows Server 2012)에 대 한 도메인 컨트롤러에 대 한 시스템 이벤트 로그에 자세히 설명 되어 RID 이벤트 [RID 풀 요청](https://technet.microsoft.com/library/ee406152(WS.10).aspx) (16642, 16643, 16644, 16645, 16656).  
  
    2.  도메인 컨트롤러 및 RID 마스터의 시스템 이벤트 로그에서 이 항목의 아래에 자세히 설명된 새 블록을 나타내는 이벤트(16655, 16656, 16657)를 검토해 보세요.  
  
    3.  Repadmin.exe를 사용하여 Active Directory 복제 상태를 확인하고 **Dcdiag.exe /test:ridmanager /v**를 사용하여 RID 마스터 가용성을 확인해 보세요. 이러한 테스트를 통해 결론을 얻지 못한 경우 도메인 컨트롤러와 RID 마스터 간에 양쪽 네트워크 캡처를 사용하도록 설정해 보세요.  
  
### <a name="troubleshooting-specific-problems"></a>특정 문제 해결  
다음 새 메시지는 Windows Server 2012 도메인 컨트롤러의 시스템 이벤트 로그에 로깅됩니다. System Center Operations Manager와 같은 자동화된 AD 상태 추적 시스템에서 이러한 이벤트를 모니터링해야 합니다. 모든 이벤트가 중요하며, 일부는 심각한 도메인 문제를 나타냅니다.  
  
|||  
|-|-|  
|이벤트 ID|16653|  
|Source|Directory-Services-SAM|  
|Severity|경고|  
|메시지|관리자가 구성한 RID(계정 ID)의 풀 크기가 지원되는 최대값보다 큽니다. %1의 최대값은 도메인 컨트롤러가 RID 마스터인 경우 사용됩니다.<br /><br />자세한 내용은 참조 [RID 블록 크기 제한](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_RIDBlockMaxSize)합니다.|  
|참고 사항 및 해결 방법|RID 블록 크기의 최대값은 이제 10진수 15,000(16진수 0x3A98)입니다. 도메인 컨트롤러에서는 15,000개가 넘는 RID를 요청할 수 없습니다. 값이 이 최대값 이하로 설정될 때까지 부팅 시마다 이 이벤트가 로깅됩니다.|  
  
|||  
|-|-|  
|이벤트 ID|16654|  
|Source|Directory-Services-SAM|  
|Severity|정보|  
|메시지|RID(계정 ID)가 무효화되었습니다. 이는 다음과 같은 경우에 발생할 수 있습니다.<br /><br />1. 도메인 컨트롤러가 백업에서 복원되었습니다.<br /><br />2. 가상 컴퓨터에서 실행 중인 도메인 컨트롤러가 스냅샷에서 복원되었습니다.<br /><br />3. 관리자가 풀을 수동으로 무효화했습니다.<br /><br />자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=226247 를 참조하세요.|  
|참고 사항 및 해결 방법|이 이벤트가 예상치 못한 이벤트인 경우 모든 도메인 관리자에게 문의하여 이러한 작업 중 어떤 작업이 수행되었는지 확인하세요. 디렉터리 서비스 이벤트 로그에는 이러한 단계 중 하나가 수행된 시점에 대한 자세한 정보도 포함됩니다.|  
  
|||  
|-|-|  
|이벤트 ID|16655|  
|Source|Directory-Services-SAM|  
|Severity|정보|  
|메시지|RID(계정 ID)의 전역 최대값이 %1(으)로 증가했습니다.|  
|참고 사항 및 해결 방법|이 이벤트가 예상치 못한 이벤트인 경우 모든 도메인 관리자에게 문의하여 이러한 작업 중 어떤 작업이 수행되었는지 확인하세요. 이 이벤트는 전체 RID 풀 크기가 기본값인 2<sup>30</sup>을 넘어 증가했음을 나타내며, 자동으로 발생하지 않습니다. 관리 작업에 의해서만 발생합니다.|  
  
|||  
|-|-|  
|이벤트 ID|16656|  
|Source|Directory-Services-SAM|  
|Severity|경고|  
|메시지|RID(계정 ID)의 전역 최대값이 %1(으)로 증가했습니다.|  
|참고 사항 및 해결 방법|조치가 필요합니다! RID(계정 ID) 풀이 이 도메인 컨트롤러에 할당되었습니다. 풀 값은 이 도메인이 사용 가능한 전체 계정 ID의 많은 부분을 사용했음을 나타냅니다.<br /><br />도메인에는 총 사용 가능한 계정 id의 남은 다음 임계값에 도달 하면 보호 메커니즘이 활성화 됩니다: %1입니다.  이 보호 메커니즘으로 인해 RID 마스터 도메인 컨트롤러에서 계정 ID 할당을 수동으로 다시 사용하도록 설정할 때까지 계정 만들기가 차단됩니다.<br /><br />자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=228610 를 참조하세요.|  
  
|||  
|-|-|  
|이벤트 ID|16657|  
|Source|Directory-Services-SAM|  
|Severity|Error|  
|메시지|조치가 필요합니다! 이 도메인이 사용 가능한 전체 RID(계정 ID)의 많은 부분을 사용했습니다. 사용 가능한 전체 계정 ID 중 남은 ID가 X%개[인공 최대값 인수]보다 적으므로 보호 메커니즘이 활성화되었습니다.<br /><br />이 보호 메커니즘으로 인해 RID 마스터 도메인 컨트롤러에서 계정 ID 할당을 수동으로 다시 사용하도록 설정할 때까지 계정 만들기가 차단됩니다.<br /><br />이 도메인이 비정상적으로 높은 비율의 계정 ID를 사용하지 못하도록 하려면 계정 만들기를 다시 사용하도록 설정하기 전에 특정 진단을 수행해야 합니다. 또한 계정 만들기를 다시 사용하도록 설정하기 전에 식별된 모든 문제를 해결해야 합니다.<br /><br />기본 문제의 진단 및 해결에 실패하면 비정상적으로 높은 비율의 계정 ID 사용으로 인해 도메인의 계정 ID가 소진되어 이후 이 도메인에서 계정을 영구적으로 만들지 못하게 될 수 있습니다.<br /><br />자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=228610 를 참조하세요.|  
|참고 사항 및 해결 방법|모든 도메인 관리자에게 이 보호를 재정의할 때까지 이 도메인에서 더 이상 보안 주체를 만들 수 없음을 알려 주세요. 풀에서 보호를 재정의 하 고 가능한 전체 RID 증가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [전역 RID 공간 크기 잠금 해제](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_GlobalRidSpaceUnlock)합니다.|  
  
|||  
|-|-|  
|이벤트 ID|16658|  
|Source|Directory-Services-SAM|  
|Severity|경고|  
|메시지|이 이벤트는 사용 가능한 RID(계정 ID) 중 남아 있는 총 개수에 대한 정기적인 업데이트입니다. 남아 있는 계정 id 수는 약: %1입니다.<br /><br />계정 ID는 계정이 만들어질 때 사용됩니다. 계정 ID가 모두 소진되면 도메인에서 새 계정이 만들어지지 않습니다.<br /><br />자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=228745 를 참조하세요.|  
|참고 사항 및 해결 방법|모든 도메인 관리자에게 RID 사용량이 주요 지표를 초과했음을 알려 주세요. 또한 보안 트러스티 만들기 패턴을 검토하여 이 동작이 예상된 동작인지 여부를 확인해야 합니다. 이 이벤트가 매우 비정상적인 것으로 간주되는 경우 이는 1억 개 이상의 RID가 할당되었음을 의미합니다.|  
  
## <a name="see-also"></a>관련 항목  
[Windows Server 2012에서 RID 발급 관리](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)  
  


