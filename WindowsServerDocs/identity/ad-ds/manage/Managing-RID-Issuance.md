---
ms.assetid: aac117a7-aa7a-4322-96ae-e3cc22ada036
title: "RID 발급 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f84bcc1aa32e9993903e094fc43feffcbe16a05b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="managing-rid-issuance"></a>RID 발급 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 RID 마스터 FSMO 역할을 포함 하 여 새 발급 및 모니터링 RID 마스터 및 분석과 RID 발급 문제를 해결 하는 방법에 대 한 기능을 변경에 설명 합니다.  
  
-   [RID 발급 관리](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Manage)  
  
-   [RID 발급 문제 해결](../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_Tshoot)  
  
더 많은 정보를에서 사용할 수 있는 [AskDS 블로그](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)합니다.  
  
## <a name="BKMK_Manage"></a>RID 발급 관리  
기본적으로 도메인 용량은 약 1 십억 보안 사용자 등 사용자가, 그룹과 컴퓨터에 있습니다. 물론 적극적으로 사용 되는 많은 개체 사용 하는 도메인 가지가 있습니다. 그러나 Microsoft 고객 지원의 경우 찾았습니다 위치:  
  
-   소프트웨어 또는 실수로 대량 관리 스크립트 프로비저닝 사용자가, 그룹 및 컴퓨터를 만들었습니다.  
  
-   사용 하지 않는 한 보안과 메일 그룹 위임된 사용자가 만든  
  
-   복원 된 많은 도메인 컨트롤러 내리는 또는 메타 데이터 치료  
  
-   숲 복구 수행한  
  
-   자주 InvalidateRidPool 작업을 수행  
  
-   지우려는 블록 크기 레지스트리 값 올바르게 증가  
  
이러한 상황이 모든 위치 불필요, 자주 실수로 Rid을 사용합니다. 많은 년 동안 Rid 부족 하 여는 몇 가지 환경 이며이 강제 새 도메인 마이그레이션 또는 숲 복구 수행할 수 있습니다.  
  
Windows Server 2012 RID 할당 있는 문제가 있는 연령 및 Active Directory 널리 사용 되는 문제를 해결 합니다. 여기에 더 나은 이벤트 로깅에서, 더 적합 한 제한 전체 크기의 글로벌 RID 공간 도메인에 대 한 두 번 하는 기능을--비상시에 포함 됩니다.  
  
### <a name="periodic-consumption-warnings"></a>주기적 소비 경고  
Windows Server 2012 추가 글로벌 RID 공간 이벤트 추적 하는 중요 시점 교차 때 조기 경고를 제공 합니다. 모델 계산 열 (10) % 부호 글로벌 풀의 사용에 도달 하면 이벤트를 기록 합니다. 다음 사용 하 고 남은 다음 10 %를 계산 하 고 이벤트 주기 계속 됩니다. 글로벌 RID 공간 소모 되는 대로 이벤트는 더욱 빠르게 이용할 10% 성공적으로 더 빠르게 줄어드는 풀의 (이벤트 로그 불필요 한 방지 발생 하지만 시간별 개 이상의 항목). 모든 도메인 컨트롤러의 시스템 이벤트 로그 디렉터리-서비스-삼로 경고 이벤트를 16658 씁니다.  
  
가정는 기본 30 비트 글로벌 RID 공간을 포함 하 여 107,374,182 풀 할당 때 첫 번째 이벤트 로그<sup>일</sup> RID 합니다. 이벤트 속도 전체에서 생성 110 이벤트와 함께 100, 000의 마지막 체크 포인트 될 때까지 자연스럽 게 가속 합니다. 동작은 잠금 해제 한 31 비트 글로벌 RID 공간에 대 한 유사: 214,748,365에서 시작 하 고 117 이벤트를 완료 합니다.  
  
> [!IMPORTANT]  
> 이 이벤트는 사용할 수 없습니다. 사용자, 컴퓨터 및 즉시 도메인에 있는 그룹 만들기 프로세스 조사 합니다. 100 백만 더 이상 광고 DS 개체 만들기 매우 않은입니다.  
  
![제거 발급](media/Managing-RID-Issuance/ADDS_RID_TR_EventWaypoints2.png)  
  
### <a name="rid-pool-invalidation-events"></a>풀 무효화 이벤트 제거  
새는 이벤트 경고 DC 제거 풀을 삭제 했습니다. 이들 알림 되며 특히 VDC의 새로운 기능으로 인해 발생할 수 있습니다. 이벤트에 대 한 자세한 내용은 아래 이벤트 목록을 참조 하세요.  
  
### <a name="BKMK_RIDBlockMaxSize"></a>블록 크기 제한을 제거합니다  
일반적으로 도메인 컨트롤러의 500 rid 블록 RID 할당 한 번에 요청합니다. 다음 레지스트리 REG_DWORD 값 도메인 컨트롤러에서 사용 하 여이 기본을 무시할 수 있습니다.  
  
```  
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\RID Values  
RID Block Size  
  
```  
  
Windows Server 2012 전에 최대 값 암묵적인 DWORD 최대 (있음 0xffffffff 또는 4294967295 값은)을 제외 하 고 해당 레지스트리 키에서 적용 했습니다. 이 값은 전체 글로벌 RID 공간 보다 상당히 큰. 관리자 부적절 하 게 또는 실수로 경우도 블록 크기 제거 값으로 구성 거 대 한 속도로 글로벌 RID 모두 사용 하는 합니다.  
  
Windows Server 2012에서이 레지스트리 값 15, 000 소수점 (16 진 0x3A98) 보다 높은 설정할 수 없습니다. 의도 하지 않은 거 대 한 RID 할당을 수 없습니다.  
  
값 설정 *높은* 15, 000 보다 값 15, 000으로 간주 되 고 도메인 컨트롤러에서 16653 이벤트를 기록 디렉터리 서비스 이벤트 로그 값 해결 될 때까지 재부팅할에 있습니다.  
  
### <a name="BKMK_GlobalRidSpaceUnlock"></a>글로벌 RID 공간 크기를 잠금 해제  
Windows Server 2012 전에 글로벌 RID 공간 2 제한적 이었습니다<sup>30</sup> (또는 1073741823) Rid 총 합니다. 에 도달 하면만 도메인 마이그레이션 또는 숲 하는 복구 오래 된 기간에 모든 측정 하 여 새 Sid 만들기 복구를 사용할 수 있습니다. 2, Windows Server 2012에서 시작<sup>31</sup> 비트 글로벌 풀 2,147,483,648 Rid 향상 하기 위해 잠금을 해제할 수 있습니다.  
  
AD DS 라는 특별 한 숨겨진된 특성에서이 설정을 저장 **SidCompatibilityVersion** 모든 도메인 컨트롤러의 RootDSE 컨텍스트가에 있습니다. 이 특성 ADSIEdit, LDP 또는 기타 도구를 사용 하 여 읽을 수 없는 경우 글로벌 RID 공간 증가 보려면의 시스템 이벤트 삼로-디렉터리-서비스에서 16655 경고 이벤트에 대 한 로그를 또는 다음 Dcdiag 명령을 사용:  
  
```  
Dcdiag.exe /TEST:RidManager /v | find /i "Available RID Pool for the Domain"  
  
```  
  
글로벌 RID 풀을 강화 하는 경우 사용 가능한 풀 기본 1,073,741,823 대신 2147483647으로 변경 됩니다. 예를 들어:  
  
![제거 발급](media/Managing-RID-Issuance/ADDS_RID_TR_Dcdiag.png)  
  
> [!WARNING]  
> 이 잠금 해제를 위한 것입니다 *만* RID 부족 방지 하기 위해 사용 되 고 *만* 최대 집행 제거와 함께에서 (다음 섹션 참조). 응용 프로그램 호환성 문제 Sid 잠금이 해제 되어 RID 풀에서 생성 된 사용자 존재 Rid 낮은 성장 하 고 남은 수백만 있는 환경에서 설정 하지 "선점 하 여"을 수행 합니다.  
>   
> 이 작업을 잠금 해제 하 여 이전 백업 하는 전체 숲 복구 제외를 제거 하거나 되돌릴 수 없습니다.  
  
#### <a name="important-caveats"></a>중요 한  
Windows Server 2003 및 Windows Server 2008 도메인 컨트롤러의 글로벌 RID 31 풀 때 Rid를 실행할 수 없는<sup>세인트</sup> 비트 잠금이 해제 되어 있습니다. Windows Server 2008 R2 domain controllers *can* use 31<sup>st</sup> bit RIDs *but only if* they have hotfix [KB 2642658](https://support.microsoft.com/kb/2642658) installed. 지원 되지 않는 및 패치되지 도메인 컨트롤러 잠금을 해제 하는 경우 본으로 글로벌 RID 풀을 처리 합니다.  
  
이 기능은 도메인 기능 수준;에서 적용 되지 Windows Server 2012 또는 Windows Server 2008 R2 도메인 컨트롤러 업데이트 된 도메인의 존재 하는 훌륭한 주의 수행 합니다.  
  
#### <a name="implementing-unlocked-global-rid-space"></a>구현 공간 잠금이 해제 되어 글로벌 제거  
31 RID 풀의 잠금을 해제 하려면<sup>세인트</sup> 비트 (아래 참조) RID 최대 알림을 받은 후 다음 단계를 수행 합니다.  
  
1.  지우려는 마스터 역할 도메인 컨트롤러 Windows Server 2012에서 실행 되 고 있는지 확인 합니다. 그렇지 않은 경우 Windows Server 2012 도메인 컨트롤러로 전송할 수도 있습니다.  
  
2.  LDP.exe 실행  
  
3.  클릭 하 고 **연결** 메뉴를 클릭 **연결** Windows Server 2012 제거 마스터에 389를 포트를 누른 **연결** 도메인 관리자 권한으로 합니다.  
  
4.  클릭 하 고 **찾아보기** 메뉴를 클릭 **수정**합니다.  
  
5.  되도록 **DN** 비어 있습니다.  
  
6.  **항목 특성 편집**를 입력 합니다.  
  
    ```  
    SidCompatibilityVersion  
    ```  
  
7.  **값**를 입력 합니다.  
  
    ```  
    1  
    ```  
  
8.  되도록 **추가** 에서 선택한 **작업** 클릭 **Enter**합니다. 이 업데이트는 **항목 목록**합니다.  
  
9. 선택는 **동기** 및 **추가** 옵션을 클릭 한 다음 **실행**합니다.  
  
    ![제거 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModify.png)  
  
10. 성공적으로 실행 되는 LDP 출력 창에 표시 합니다.  
  
    ```  
    ***Call Modify...  
     ldap_modify_ext_s(Id, '(null)',[1] attrs, SvrCtrls, ClntCtrls);  
    modified "".  
  
    ```  
  
    ![제거 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPModifySuccess.png)  
  
11. 전 세계 RID 풀 증가 디렉터리-서비스-삼로 정보 이벤트 16655 해당 도메인 컨트롤러의 시스템 이벤트 로그를 검사 하 여 확인 합니다.  
  
### <a name="rid-ceiling-enforcement"></a>최대 집행 제거  
하기 위해 보호에 게 제공 하 고 관리 인식 상승, Windows Server 2012 인공 있는 최대를 열 (10) %Rid 글로벌 공간에서 남은 글로벌 RID 범위 내에 도입 되었습니다. 개 (1) 인공 최대 %, 내에 있는 경우 도메인 컨트롤러 RID 풀 요청 디렉터리-서비스-삼로 경고 이벤트 16656 로그에 기록의 시스템 이벤트 합니다. 지우려는 FSMO 마스터에 최대 10 %에 도달 디렉터리-서비스-삼로 이벤트 16657의 시스템 이벤트 로그에 기록 하 고는 할당할 더 이상 RID 풀 최대 재정의까지 합니다. 이렇게 하면 도메인에 있는 RID 마스터 상태 평가 하 고 잠재적인 런어웨이 RID 할당; 해결할 수 있습니다. 이 전체 RID 공간 낭비에서 도메인 보호 됩니다.  
  
이 최대 10 %의 사용 가능한 RID 공간 남은에서 하드 코드입니다. 즉, 최대 RID 마스터 할당 풀의 글로벌 RID 공간 90 비율에 맞게 RID 포함 된 때를 활성화 합니다.  
  
-   기본 도메인에 대 한 첫 번째 트리거 점은 2<sup>30</sup>-1 * 0.90 = 966,367,640 (또는 남은 107,374,183 Rid).  
  
-   트리거 지점은 2 잠금이 해제 되어 31 비트 RID 공간이 도메인에 대 한<sup>31</sup>-1 * 0.90 = 1,932,735,282 Rid (또는 남은 214,748,365 Rid).  
  
RID 마스터 Active Directory 특성 설정 때 **를 RIDPoolAllocationEnabled** (일반 이름 **ms-DS-RID-Pool-Allocation-Enabled**) 개체에 대해 다음과 같습니다.  
  
CN RID 관리자 CN$ = 시스템, DC = =*<domain>*  
  
16657 이벤트 쓰고 방지 RID 블록 발급 모든 도메인 컨트롤러에 추가 합니다. 도메인 컨트롤러 계속 이미 발행 된 모든 뛰어난 RID 풀 사용 합니다.  
  
차단이 해제 하 고 계속 풀 할당 RID 하도록, 값을 참을 설정 합니다. RID 마스터 수행한 다음 RID 할당에 특성 기본 하지 설정 값으로 돌아갑니다. 그 후 없는 추가 방 되며 결국 글로벌 RID 공간 소진 숲 복구 또는 도메인 마이그레이션 요구 합니다.  
  
#### <a name="removing-the-ceiling-block"></a>최대 차단 제거  
인공 최대를 한 번에 도달 블록을 제거 하려면 다음 단계를 수행 합니다.  
  
1.  지우려는 마스터 역할 도메인 컨트롤러 Windows Server 2012에서 실행 되 고 있는지 확인 합니다. 그렇지 않은 경우 Windows Server 2012 도메인 컨트롤러로 전송할 수도 있습니다.  
  
2.  LDP.exe 실행 합니다.  
  
3.  클릭 하 고 **연결** 메뉴를 클릭 *연결* Windows Server 2012 제거 마스터에 389를 포트를 누른 **연결** 도메인 관리자 권한으로 합니다.  
  
4.  클릭는 **보기** 메뉴를 클릭 **트리**에 대 한 다음는 **Base DN** 제거 마스터의 고유한 도메인 이름 컨텍스트를 선택 합니다. 클릭 **확인**합니다.  
  
5.  탐색 창에서 자세히는 **CN 시스템 =** 컨테이너 클릭 하 고 있는 **CN RID 관리자 $ =** 개체 합니다. 마우스 오른쪽 단추로 클릭 하 고 클릭 **수정**합니다.  
  
6.  항목 특성 편집에 입력 합니다.  
  
    ```  
    MsDS-RidPoolAllocationEnabled  
    ```  
  
7.  **값**, 형식 (대문자):  
  
    ```  
    TRUE  
    ```  
  
8.  선택 **교체** 에 **작업** 클릭 **Enter**합니다. 이 업데이트는 **항목 목록**합니다.  
  
9. 설정에서 **동기** 및 **추가** 옵션을 클릭 한 다음 **실행**:  
  
    ![제거 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeiling.png)  
  
10. 성공적으로 실행 되는 LDP 출력 창에 표시 합니다.  
  
    ```  
    ***Call Modify...  
    ldap_modify_ext_s(ld, 'CN=RID Manager$,CN=System,DC=<domain>',[1] attrs, SvrCtrls, ClntCtrls);  
    Modified "CN=RID Manager$,CN=System,DC=<domain>".  
  
    ```  
  
    ![제거 발급](media/Managing-RID-Issuance/ADDS_RID_TR_LDPRaiseCeilingSuccess.png)  
  
### <a name="other-rid-fixes"></a>다른 RID 수정 사항  
이전 Windows Server 운영 체제 RID 풀 때 누수 있었습니다 누락 rIDSetReferences 특성 합니다. To resolve this problem on domain controllers that run Windows Server 2008 R2, install the hotfix from [KB 2618669](https://support.microsoft.com/kb/2618669).  
  
### <a name="unfixed-rid-issues"></a>고정 되지 않은 RID 문제  
여기 역사적 RID 누수를 켜 둬야 계정 만들기 실패 합니다. 계정 만들기, 오류 RID을 계속 사용 됩니다. 일반적인 예 사용자 복잡성 만족 하지 않는 한 암호를 만드는 것입니다.  
  
### <a name="rid-fixes-for-earlier-versions-of-windows-server"></a>이전 버전의 Windows Server에 대 한 수정 프로그램 제거  
모든 수정 및 변경 사항을 위의 출시 된 Windows Server 2008 R2 핫픽스 합니다. 현재 없는 Windows Server 2008 핫픽스 계획 된 나 사항이 진행 중에서입니다.  
  
## <a name="BKMK_Tshoot"></a>RID 발급 문제 해결  
  
### <a name="introduction-to-troubleshooting"></a>문제 해결 소개  
제거 발급 문제 해결을 논리 선형 방법은 필요합니다. 로그 신중 하 게 경고 RID 발생 한 오류를 모니터링 하는 하지 않는 한 첫 번째에 문제가 있는지 실패 계정 만들기 될 수 있습니다. 여부; 증상 예상 되는 때를 파악 하는 RID 발급 문제를 해결 하는 키 많은 RID 발급 문제 하나만 도메인 컨트롤러에 영향을 줄 수 있으며, 구성 요소 개선와 관련이 없는 수 있습니다. 아래 간단한이 다이어그램 그러한 결정 명확 하 게 있습니다.  
  
![제거 발급](media/Managing-RID-Issuance/adds_rid_issuance_troubleshooting.png)  
  
### <a name="troubleshooting-options"></a>문제 해결 옵션  
  
#### <a name="logging-options"></a>로그인 옵션  
시스템 이벤트 로그 디렉터리-서비스-삼로 원본에서 발급 RID에에서 로그인 발생 합니다. 로깅 사용 되며, 최대 세부 정보 표시 수준에 기본적으로 구성 수도 있습니다. Windows Server 2012에서 새 구성 변경 없이 항목이 기록 하는 경우 문제 축제 (레거시 즉, 이전 Windows Server 2012)으로 취급 RID 발급 문제 Windows 2008 R2 또는 이전 운영 체제에 표시 됩니다.  
  
#### <a name="utilities-and-commands-for-troubleshooting"></a>유틸리티 및 문제 해결에 대 한 명령  
앞에서 언급 한 로그-으로 하지 설명 하는 문제를 해결 하려면 특히 이전 RID 발급 문제-다음과 같은 도구를 사용 하 여 시작 지점으로:  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   네트워크 3.4 모니터  
  
### <a name="general-methodology-for-troubleshooting-domain-controller-configuration"></a>일반 방법론 도메인 컨트롤러 구성 문제 해결  
  
1.  간단한 인해 발생 한 오류 사용 권한이 나 도메인 컨트롤러 가용성 문제가 있나요?  
  
    1.  보안 필요한 권한 없이 계정 만들기 하려고 하면? 액세스 거부 오류에 대 한 출력을 검사 합니다.  
  
    2.  도메인 컨트롤러를 사용할 수 있나요? 반환된 오류 또는 LDAP 도메인 컨트롤러 가용성 메시지를 검사 합니다.  
  
2.  특히 반환 오류 Rid, 언급 관련 지침으로 사용 되 고 있나요? 그렇다면 제공 된 지침을 따릅니다.  
  
3.  그렇지 않으면 비 특정 하지만 특히 반환 오류 Rid 언급 수 있을까요? 예를 들어, "Windows 만들 수 없습니다 개체 디렉터리 서비스 관련 식별자 할당 하지 못했습니다."  
  
    1.  Examine the System Event log on the domain controller for "legacy" (pre-Windows Server 2012) RID events detailed in [RID Pool Request](https://technet.microsoft.com/en-us/library/ee406152(WS.10).aspx) (16642, 16643, 16644, 16645, 16656).  
  
    2.  도메인 컨트롤러의 시스템 이벤트와 제거 마스터 아래에 자세히 설명 (16655, 16656, 16657)이이 항목의 새로운 블록 나타내는 이벤트를 검사 합니다.  
  
    3.  Repadmin.exe 및 제거 마스터 공개 된 Active Directory 복제 건강의 유효성을 검사 **Dcdiag.exe /test:ridmanager /v**합니다. 이러한 테스트 최종 없는 경우 도메인 컨트롤러 및 제거 마스터 간에 양면 네트워크 캡처를 사용 하도록 설정 합니다.  
  
### <a name="troubleshooting-specific-problems"></a>특정 문제 해결  
다음 새 메시지의 시스템 이벤트 로그 Windows Server 2012 도메인 컨트롤러에에 로그인 합니다. 이러한 이벤트에 대 한 추적 System Center Operations Manager 같은 시스템 자동화 된 광고 건강 모니터링 해야 모든 눈에 띄는, 되며 몇 가지 중요 한 도메인 문제의 표시기 됩니다.  
  
|||  
|-|-|  
|이벤트 ID|16653|  
|원본|삼-디렉터리-서비스|  
|심각도|경고|  
|메시지|관리자 권한으로 구성 된 계정-Rid (식별자)에 대 한 풀 크기는 지원 되는 최대 보다 더 깁니다. 도메인 컨트롤러 RID 마스터 때 %1의 최대 값 사용 됩니다.<br /><br />자세한 내용은 참조 [제거 블록 크기 제한을](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_RIDBlockMaxSize)합니다.|  
|노트 및 해결 방법|지우려는 블록 크기 최대 값 15000 소수점 (16 진 3A98) 됩니다. 도메인 컨트롤러 15, 000 개 이상의 Rid 요청할 수 없습니다. 이 이벤트는 값이이 최대 이하로 값으로 설정 되어 있을 때까지 부팅할 때마다 로그입니다.|  
  
|||  
|-|-|  
|이벤트 ID|16654|  
|원본|삼-디렉터리-서비스|  
|심각도|알림|  
|메시지|계정-Rid (식별자)의 풀 무효화 되었습니다. 예상 되는 다음과 같은 경우에 발생할 수 있습니다.<br /><br />1. 도메인 컨트롤러 백업에서 복원 됩니다.<br /><br />2. 실행 가상 컴퓨터에서 도메인 컨트롤러 스냅숏을에서 복원 됩니다.<br /><br />3. 관리자 풀을 무효화 수동으로 했습니다.<br /><br />See https://go.microsoft.com/fwlink/?LinkId=226247 for more information.|  
|노트 및 해결 방법|이 이벤트 예기치 않은 모든 도메인 관리자에 게 문의 하 고 있는 작업을 수행 하는 중 확인 합니다. 디렉터리 서비스 이벤트 로그도 한 자세한 정보에 경우이 단계 중 하나를 수행 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|16655|  
|원본|삼-디렉터리-서비스|  
|심각도|알림|  
|메시지|%1 계정-Rid (식별자)에 대 한 전 세계 최대 증가 되었습니다.|  
|노트 및 해결 방법|이 이벤트 예기치 않은 모든 도메인 관리자에 게 문의 하 고 있는 작업을 수행 하는 중 확인 합니다. 이 이벤트 메모 전체 RID 증가 풀 2 기본 이상 크기<sup>30</sup>자동으로 이루어집니다 하지 해야만 관리 작업입니다.|  
  
|||  
|-|-|  
|이벤트 ID|16656|  
|원본|삼-디렉터리-서비스|  
|심각도|경고|  
|메시지|%1 계정-Rid (식별자)에 대 한 전 세계 최대 증가 되었습니다.|  
|노트 및 해결 방법|별도 작업이 필요 합니다. 계정 식별자 (RID) 풀은이 도메인 컨트롤러에 할당 되었습니다. 풀 값이 도메인 총 사용할 수 있는 계정-식별자의 많은 부분을 사용 했습니다.<br /><br />도메인 총 사용할 수 있는 계정-식별자 남은 다음 임계값에 도달 하면 보호 메커니즘을 정품 인증 됩니다. %1 합니다.  보호 메커니즘 수동으로 다시 설정한 후 계정 식별자 할당 RID 마스터 도메인 컨트롤러에서 계정을 만들 수 없게 됩니다.<br /><br />See https://go.microsoft.com/fwlink/?LinkId=228610 for more information.|  
  
|||  
|-|-|  
|이벤트 ID|16657|  
|원본|삼-디렉터리-서비스|  
|심각도|오류|  
|메시지|별도 작업이 필요 합니다. 이 도메인은 총 사용할 수 있는 계정-Rid (식별자)의 많은 부분을 사용 했습니다. 총 사용할 수 있는 계정-식별자 남은 보호 메커니즘 활성화 된 미만: X % [인공 최대 인수] 합니다.<br /><br />보호 메커니즘 수동으로 다시 설정한 후 계정 식별자 할당 RID 마스터 도메인 컨트롤러에서 계정을 만들을 수 없습니다.<br /><br />것은 매우 중요 특정 진단 계정이이 도메인 수 있도록 생성 비정상적 속도로 계정 식별자를 사용 하 고 하지 다시 사용 하기 전에 수행 됩니다. 한 문제 식별 계정 만들기를 다시 사용 하기 전에 해결 해야 합니다.<br /><br />이후에 계정 만들기가 영구적으로에서 해제할 수이 도메인 도메인에 있는 계정 식별자 소모 오류를 진단 하 고 계정 식별자 소비의 비정상적 속도 모든 기본 문제 해결 될 수 있습니다.<br /><br />See https://go.microsoft.com/fwlink/?LinkId=228610 for more information.|  
|노트 및 해결 방법|모든 도메인 관리자에 게 문의 하 고 알려 없이 추가 보안 사용자 보호이 기능을 재정의 때까지이 도메인에 만들 수 있습니다. 풀을 보호를 무시 하 고 전체 RID 가능 증가 하는 방법에 대 한 자세한 내용은 참조 하십시오 [글로벌 제거 공간 크기의 잠금을 해제](../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/../../ad-ds/manage/Managing-RID-Issuance.md#BKMK_GlobalRidSpaceUnlock)합니다.|  
  
|||  
|-|-|  
|이벤트 ID|16658|  
|원본|삼-디렉터리-서비스|  
|심각도|경고|  
|메시지|이 이벤트는 사용할 수 있는 계정-Rid (식별자)의 나머지 총 수량에 정기적으로 업데이트 합니다. 나머지 계정 식별자 수 약는: 1% 합니다.<br /><br />계정 식별자 계정을 만든 새 계정을 설정 하지 않고 도메인에 만들 수 소진은으로 사용 됩니다.<br /><br />See https://go.microsoft.com/fwlink/?LinkId=228745 for more information.|  
|노트 및 해결 방법|모든 도메인 관리자에 게 문의 하 고 RID 소비 주요 중요 시점; 알려주므로는 알려 이 정상적인된 동작 또는 하지 보안 트러스티 생성 패턴을 검토 하 여 확인 합니다. 적이 이벤트를 표시 되지 않는 매우 평소 해당 이상 ~ 100 백만 RID 할당 된 되었음을 의미 합니다.|  
  
## <a name="see-also"></a>참조 하십시오  
[Windows Server 2012에서에서 발급 RID 관리](http://blogs.technet.com/b/askds/archive/2012/08/10/managing-rid-issuance-in-windows-server-2012.aspx)  
  


