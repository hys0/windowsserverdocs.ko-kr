---
ms.assetid: 4d21d27d-5523-4993-ad4f-fbaa43df7576
title: "관리 센터 Active Directory (수준을 200)를 사용 하 여 고급 AD DS 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 19e83ce0123bd484c61d5a4522ebdd90cd40241e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="advanced-ad-ds-management-using-active-directory-administrative-center-level-200"></a>관리 센터 Active Directory (수준을 200)를 사용 하 여 고급 AD DS 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 자세히, 문제 해결 정보 및 아키텍처 예 일반적인 작업을 비롯 하 여 새 Active Directory 휴지통, 세분화 암호 정책 및 Windows PowerShell 기록 뷰어 업데이트 된 Active Directory 관리 센터에 설명 합니다. 대 한 소개 [Active Directory 관리 센터 향상 기능 및 #40; 소개 수준을 100 & #41; ](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md).  
  
-   [관리 센터 아키텍처 active Directory](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Arch)  
  
-   [관리 센터 Active Directory를 사용 하 여 휴지통을 활성화 하 고 Active Directory 관리](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_EnableRecycleBin)  
  
-   [구성 및 관리 센터 Active Directory를 사용 하 여 세밀 암호 정책을 관리](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_FGPP)  
  
-   [관리 센터 Windows PowerShell 기록 Active Directory 뷰어를 사용 하 여](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_HistoryViewer)  
  
-   [광고 DS 관리 문제 해결](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Tshoot)  
  
## <a name="BKMK_Arch"></a>관리 센터 아키텍처 active Directory  
  
### <a name="adprep-executables-dlls"></a>Dll ADPrep 실행 파일  
새 휴지통, FGPP, 및 기록 뷰어 기능이 모듈 및 기본 아키텍처 Active Directory 관리 센터의 변경 되지 않았습니다.  
  
-   Microsoft.ActiveDirectory.Management.UI.dll  
  
-   Microsoft.ActiveDirectory.Management.UI.resources.dll  
  
-   Microsoft.ActiveDirectory.Management.dll  
  
-   Microsoft.ActiveDirectory.Management.resources.dll  
  
-   ActiveDirectoryPowerShellResources.dll  
  
기본 Windows PowerShell 및 계층 휴지통의 새로운 기능에 대 한 작업을 하시 아래 나와 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/adds_adrestore.png)  
  
## <a name="BKMK_EnableRecycleBin"></a>관리 센터 Active Directory를 사용 하 여 휴지통을 활성화 하 고 Active Directory 관리  
  
### <a name="capabilities"></a>기능  
  
-   Windows Server 2012 Active Directory 관리 센터 구성 하 고 Active Directory 휴지통을 숲 속의 파티션의 도메인에 대 한 관리할 수 있습니다. 요구 사항을 Windows PowerShell 또는 Ldp.exe Active Directory 휴지통을 사용 하도록 설정 하거나 복원 도메인 파티션에서 개체를 사용 하는 더 이상 합니다.  
  
-   필터링 기준을 대상으로 복원 대규모 많은 의도적으로 삭제 개체 환경에서 더 쉽게 만드는, Active Directory 관리 센터 발전 했습니다.  
  
### <a name="limitations"></a>제한  
  
-   Active Directory 관리 센터 도메인 파티션을 관리할 수 있습니다을 하기 때문에 (스키마 파티션에서 개체를 삭제할 수 없습니다.) 구성, DNS 도메인 또는 숲 DNS 파티션을에서 삭제 개체를 복원할 수 없습니다 것입니다. 개체 비 도메인 파티션을에서 복원 하려면 [복원 ADObject](https://technet.microsoft.com/library/ee617262.aspx)합니다.  
  
-   Active Directory 관리 센터에서 작업을 단일 개체 하위 밤나무 복원할 수 없습니다. 예를 들어 중첩 Ou, 사용자가, 그룹을 및 컴퓨터와 OU을 삭제 하면 기본 OU 복원 복원 되지 않습니다 자식 개체.  
  
    > [!NOTE]  
    > Active Directory 관리 센터 일괄 복원 작업 않습니다 "최선을 다" 삭제 개체 일종의 *만 선택 영역 내* 하므로 부모가 자녀 복원 목록에 대 한 하기 전에 정렬 됩니다. 간단 하 게 테스트 사례 단일 작업에서 개체의 하위 밤나무를 복원할 수 있습니다. 그러나 일부 밤나무-누락 삭제 부모 노드 중 일부 밤나무-포함 된 선택 항목이 등 코너 경우 나 부모 복원 실패, 예상 대로 작동 하지 않을 수 면 자녀 개체를 건너뛰는 것이 등의 오류 경우 합니다. 따라서 항상 복원 해야 개체의 하위 밤나무 별도 작업으로 부모 개체를 복원한 후 합니다.  
  
Active Directory 휴지통은 Windows Server 2008 R2 기능 수준 차지 하며 Enterprise 관리자 그룹의 회원 여야 합니다. 활성화 되 면 Active Directory 휴지통 비활성화할 수 없습니다. Active Directory 휴지통 Active Directory (NTDS 데이터베이스의 크기를 늘리는. DIT)는 숲 속의 모든 도메인 컨트롤러에 있습니다. 휴지통에 사용 된 디스크 공간 계속 개체와 모든 특성 데이터 보존 시간이 지남에 따라 증가 합니다.  
  
자세한 내용은 참조 [Active Directory 휴지통 Bin 단계별 가이드](https://technet.microsoft.com/library/dd392261(v=WS.10).aspx) 및 [(Active Directory 휴지통)에 대 한 하드웨어 요구 사항을 평가](https://technet.microsoft.com/library/cc753439(WS.10).aspx)합니다.  
  
수행할 수 있습니다 *낮은* 숲 및 도메인 기능 수준 Windows Server 2012에서 Windows Server 2008 R2, Active Directory 휴지통을 활성화 한 후에 있습니다. 사용 하 여이 위해서는 **설정 ADForestMode** 및 **설정 ADDomainMode** Active Directory cmdlet 합니다.  
  
예를 들어:  
  
```  
Set-AdForestMode -identity corp.contoso.com -server dc1.corp.contoso.com -forestmode Windows2008R2Forest  
Set-AdDomainMode -identity research.corp.contoso.com -server dc3.research.corp.contoso.com -domainmode Windows2008R2Domain  
  
```  
  
이 변경 하기 위해 Active Directory 관리 센터를 사용할 수 없는-기능 수준 에서만 발생 합니다.  
  
### <a name="enabling-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory 휴지통 Active Directory 관리 센터를 사용 하 여 활성화 합니다.  
열고 Active Directory 휴지통을 사용 하도록 설정 하는 **Active Directory 관리 센터** 탐색 창에서 숲 사용자 이름을 클릭 합니다. **작업** 창 클릭 **휴지통 활성화**합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBin.png)  
  
Active Directory 관리 센터 표시 되는 **Recycle Bin 확인 사용** 대화 합니다. 이 대화 상자 경고 메시지를 표시 하 고 휴지통을 활성화은 되돌릴 수 없습니다. 클릭 **확인** Active Directory 휴지통 수 있도록 합니다. Active Directory 관리 센터 모든 도메인 컨트롤러 복제 구성 변경 될 때까지 Active Directory 휴지통 완벽 하 게 작동 하지 않습니다 알려주는 다른 대화 상자를 표시 합니다.  
  
> [!IMPORTANT]  
> 사용 Active Directory 휴지통 옵션을 사용할 수 없는 경우 다음과 같습니다.  
>   
> -   숲 기능 수준을 미만인 Windows Server 2008 R2  
> -   이미 사용 가능  
  
해당 하는 Active Directory Windows PowerShell cmdlet 여전히는 다음과 같습니다.  
  
```  
Enable-ADOptionalFeature  
```  
  
Windows PowerShell를 사용 하 여 Active Directory 휴지통에 대 한 자세한 내용은 참조는 [Active Directory 휴지통 Bin 단계별 가이드](https://technet.microsoft.com/library/dd392261(v=WS.10).aspx)합니다.  
  
### <a name="managing-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory 휴지통 Active Directory 관리 센터를 사용 하 여 관리  
이 섹션의 기존 도메인 라는 예 사용 하 여 **corp.contoso.com**합니다. 이 도메인 부모 라는 OU로 사용자가 구성 **사용자 계정**합니다. **사용자 계정** OU 자녀 구성 단위 세 개 부서에서 이름을 포함 하는 각 추가로 Ou, 사용자 및 그룹에 포함 되어 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBinExampleOU.png)  
  
#### <a name="storage-and-filtering"></a>저장소 및 필터링  
Active Directory 휴지통 유지 모든 개체 숲에서 삭제 합니다. 에 따라 이러한 물체 저장는 **를 deletedObjectLifetime** 특성 기본적으로와 일치 하도록 설정 하는 **tombstoneLifetime** 특성 숲입니다. 모든 숲 속의 Windows Server 2003 s p 1을 사용 하 여 만든 이상 값 **tombstoneLifetime** 180 일에 기본적으로 설정 됩니다. 숲 속의 Windows 2000 업그레이드 되거나, Windows Server 2003 (서비스 팩 제외)과 함께 설치의 기본 tombstoneLifetime 특성 설정 되어 있지 않으면 하 고 Windows 60 일 내부 기본 따라서 사용 합니다. 이 모든를 구성할 수 있습니다. 숲 도메인 파티션을에서 삭제 개체를 복원 하려면 Active Directory 관리 센터를 사용할 수 있습니다. Cmdlet 사용 하 여 계속 합니다 **복원 ADObject** Configuration.Enabling Active Directory 휴지통에서는 같은 다른 파티션에서 삭제 복원 개체를는 **삭제 개체** 컨테이너 Active Directory 관리 센터에서 모든 도메인 파티션을 아래에서 볼 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_DeletedObjectsContainer.png)  
  
**삭제 개체** 컨테이너 표시 모든 복원할 개체 도메인 부의 합니다. 삭제 된 보다 오래 된 개체 **를 deletedObjectLifetime** 재활용된 개체도 알려져 있습니다. 이러한 물체 Active Directory 관리 센터를 사용 하 여 복원할 수 없습니다 및 Active Directory 관리 센터 재활용된 개체 표시 되지 않습니다.  
  
휴지통의 아키텍처와 처리 규칙 자세히 설명 참조 [광고 휴지통: 이해를 구현, 모범 사례 및 문제 해결](http://blogs.technet.com/b/askds/archive/2009/08/27/the-ad-recycle-bin-understanding-implementing-best-practices-and-troubleshooting.aspx)합니다.  
  
인공적 Active Directory 관리 센터 20, 000 개체 컨테이너에서 반환 되는 개체 기본 수를 제한 합니다. 클릭 하 여 100, 000 개체로 높은이 제한을 발생 시킬 수는 **관리** 메뉴, 다음 **관리 목록 옵션**합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_MgmtList.png)  
  
#### <a name="restoration"></a>복원  
  
##### <a name="filtering"></a>필터링  
Active Directory 관리 센터는 강력한 조건 및 잘 알고 있어야와 실제 복원을 사용 하 여 해야 하기 전에 필터링 옵션을 제공 합니다. 도메인 수명 주기를 통해 많은 개체를 의도적으로 삭제합니다. 180 일 가능성이 삭제 개체 기간을으로 복원할 수 없습니다 간단 하 게 모든 개체 사고 발생 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_AddCriteria.png)  
  
LDAP 복잡 한 필터 위에서 필기 하 고 날짜 및 시간 UTC 값을 변환을 대신 사용 하 여 기본 및 고급 **필터** 메뉴 관련 개체만를 나열 합니다. 삭제 날짜를 알고 있으면 개체, 이름 또는 기타 주요 데이터를 사용 하는 활용할 필터링 할 때입니다. 오른쪽에 있는 검색 상자에 펼침 단추를 클릭 하 여 필터 고급 옵션을 전환 합니다.  
  
다른 검색와 동일 모든 표준 필터 조건 옵션을 복원 작업을 지원합니다. 기본 제공 필터 개체 복원 하는 데 중요 한 항목은 일반적으로 다음과 같습니다.  
  
-   *ANR (메뉴 하지만에 입력할 때 사용 되는 것에 나열 되지 않은-모호한 이름 해상도 * * * 필터 * * * 상자)*  
  
-   마지막 제공 되는 날짜 사이 수정  
  
-   개체는 사용자/inetorgperson/컴퓨터/group/조직 장치  
  
-   이름  
  
-   삭제  
  
-   마지막으로 알려진된 부모  
  
-   입력  
  
-   설명  
  
-   도시  
  
-   국가/지역  
  
-   성  
  
-   사  
  
-   이름  
  
-   직함  
  
-   성  
  
-   SAMaccountname  
  
-   시/도  
  
-   전화 번호  
  
-   UPN  
  
-   우편 번호  
  
여러 조건 추가할 수 있습니다. 예를 들어, 모든 사용자 개체 년 9 월 24에서 삭제를 찾을 수 있습니다<sup>번째로</sup> 관리자의 직함와 시카고, Illinois에서 2012 합니다.  
  
추가 하 하거나 수정 복구 하기는 개체를 확인할 때 추가 세부 정보를 제공 하기 위해 열 머리글을 다시 정렬할 수도 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ColumnHeaders.png)  
  
모호한 이름을 확인에 대 한 자세한 내용은 참조 [ANR 특성](https://msdn.microsoft.com/library/ms675092(VS.85).aspx)합니다.  
  
##### <a name="single-object"></a>단일 개체  
삭제 된 개체 복원 작업을 단일 항상 했습니다.  Active Directory 관리 센터를 쉽게 작업을 합니다. 삭제 된 개체 명의 사용자와 같은 복원 하려면:  
  
1.  Active Directory 관리 센터의 탐색 창에서 도메인 이름을 클릭 합니다.  
  
2.  두 번 클릭 **삭제 개체** 관리 목록에서입니다.  
  
3.  개체 마우스 오른쪽 단추로 클릭 한 다음 **복원**, 키를 누르거나 **복원** 에서 **작업** 창 합니다.  
  
개체 원래 위치로 복원합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreSingle.gif)  
  
클릭 **복원... ** 복원 위치를 변경 합니다. 부모 컨테이너 삭제 개체의 삭제도 된 하지만 부모 복원 하려는 경우 유용 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreToSingle.gif)  
  
##### <a name="multiple-peer-objects"></a>여러 개의 피어 개체  
모든 사용자에에서 등의 여러 수준 피어 개체 복원할 수 있습니다. CTRL 키를 누른 복원 하나 이상의 삭제 개체를 클릭 합니다. 클릭 **복원** 작업 창에서 합니다. Ctrl 키와 키를 누른 채 표시 된 모든 개체 선택할 수도 있습니다 또는 shift 키를 사용 하 고 클릭 개체의 범위.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestorePeers.png)  
  
##### <a name="multiple-parent-and-child-objects"></a>부모 및 자녀 개체 여러  
것이 중요 하며, 이해 복원 프로세스 복원 하는 parent-자녀에 대 한 Active Directory 관리 센터를 한 동작으로 삭제 개체의 중첩된 밤나무 복원할 수 없습니다.  
  
1.  나무의 최상위 삭제 개체를 복원 합니다.  
  
2.  부모 개체의 즉각적인 아동을 복원 합니다.  
  
3.  이러한 부모 개체의 즉각적인 아동을 복원 합니다.  
  
4.  필요에 따라 모든 개체 복원 될 때까지 반복 합니다.  
  
부모 복원 하기 전에 자녀가 개체를 복원할 수 없습니다. 이 복원을 시도 반환 다음과 같은 오류가 발생을 합니다.  
  
**부모는 개체 되었으므로 또는 삭제 하기 때문에 작업을 수행할 수 없습니다.**  
  
**마지막 알려진 부모** 특성 각 개체의 상위 관계를 보여 줍니다. **마지막 알려진 부모** 특성으로 변경 삭제 된 위치에서 복원 된 위치 부모 복원한 후 Active Directory 관리 센터를 새로 고칩니다. 따라서 위치 부모 개체의 삭제 개체 컨테이너의 고유 이름을 더 이상 표시 되 면 해당 자녀 개체를 복원할 수 없습니다.  
  
자녀가 Ou 및 사용자가 포함 된 영업 OU에 관리자 실수로 삭제 시나리오를 고려 합니다.  
  
먼저 값을 관찰는 **마지막 알려진 부모** 삭제 된 모든 사용자에 대 한 특성과 읽는 방법을 * *OU Sales\0ADEL =:*< guid + 삭제 개체 컨테이너 구분 이름 >** *:  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParent.gif)  
  
삭제 된 OU 다음 복원 하는 반환 하는 모호한 이름 판매 필터링 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSales.png)  
  
삭제 된 사용자 개체의 마지막 알려진 부모 속성 복원된 판매 OU 고유 이름 변경 보려면 Active Directory 관리 센터를 새로 고칩니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesRestored.gif)  
  
모든 판매 사용자를 필터링 합니다. 삭제 모든 판매 사용자가 선택 하려면 ctrl 키와 A 키를 누른 합니다. 클릭 **복원** 개체를 이동 하 고 **삭제 개체** 그룹 구성원와 특성 그대로 판매를 컨테이너 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesUndelete.png)  
  
하는 경우는 **판매** OU 포함 자체의 다음 자녀를 복원 하기 전에 먼저 자녀가 Ou 복원 하는 방식입니다.  
  
삭제 된 부모 컨테이너 지정 하 여 중첩 된 모든 삭제 개체를 복원 하려면 참조 [부록 b: 복원 여러, 삭제 된 Active Directory 개체 (샘플 스크립트)](https://technet.microsoft.com/library/dd379504(WS.10).aspx)합니다.  
  
삭제 된 개체를 복원 하는 것에 대 한 Active Directory Windows PowerShell cmdlet는 다음과 같습니다.  
  
```  
Restore-adobject  
  
```  
  
**복원 ADObject** cmdlet 기능 Windows Server 2008 R2 및 Windows Server 2012 간에 바뀌지 않았습니다.  
  
##### <a name="server-side-filtering"></a>서버 쪽 필터링  
시간이 지남에 따라 삭제 개체 컨테이너는 중간 및 대기업에서 20 개, 000 (또는 100, 000) 개체 누적을 모든 개체를 표시 하는 데 문제가 있을 것 같습니다. Active Directory 관리 센터에서 필터 장치 클라이언트 측 필터링에 의존, 이러한 추가 개체를 표시할 수 없습니다. 이 문제를 해결 하려면 다음 단계를 사용 하 여 서버 쪽 검색을 수행 하려면:  
  
1.  마우스 오른쪽 단추로 클릭는 **삭제 개체** 컨테이너 및 클릭 **이 노드에서 검색**합니다.  
  
2.  노출 펼침 단추를 클릭는 **조건을 추가 +** 메뉴를 선택 하 고 추가 **마지막 제공 되는 날짜 사이 수정**합니다. 지난 수정 시간 (의 **whenChanged** 특성) 삭제 시간, 가장 근접 대부분의 환경에서 자녀가 동일합니다. 이 쿼리 서버 쪽 검색을 수행합니다.  
  
3.  디스플레이 필터링, 결과에서 등 정렬 더 이상 사용 하 여 복원할 수 삭제 개체 찾은 다음 일반적으로 복원 합니다.  
  
## <a name="BKMK_FGPP"></a>구성 및 관리 센터 Active Directory를 사용 하 여 세밀 암호 정책을 관리  
  
### <a name="configuring-fine-grained-password-policies"></a>정교한 암호 정책을 구성  
Active Directory 관리 센터 만들고 fgpp (세분화 암호 정책 세분화) 개체를 관리할 수 있습니다. Windows Server 2012에 대 한 첫 번째 그래픽 관리 인터페이스는 하지만 Windows Server 2008 FGPP 기능을 소개 합니다. Windows Server 2003에 필요한 단일 도메인 암호 재정의 수 있으며 도메인 수준 세분화 암호 정책이 적용 됩니다. 다른 FGPP 다른 설정이 함께 작성 하 여 개별 사용자 또는 그룹 로그인 서로 다른 암호 정책을 도메인.  
  
세분화 암호 정책에 대 한 내용은 [광고 DS 세분화 암호와 잠금 정책 단계별 가이드 계정 (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)합니다.  
  
탐색 창에서 밤나무 보기, 도메인 클릭, 클릭 **시스템**, 클릭 **암호 설정 컨테이너**, 작업 창에서 클릭 하 고 **새로** 및 **암호 설정**합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_PasswordSettings.png)  
  
### <a name="managing-fine-grained-password-policies"></a>정교한 암호 정책을 관리  
새 FGPP 만들기 또는 편집 기존 나타납니다는 **암호 설정** 편집기 합니다. 여기에서 회사 편집기도 지금 Windows Server 2008 또는 Windows Server 2008 R2에 있는 것 처럼 모든 원하는 암호 정책, 구성 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_CreatePasswordSettings.png)  
  
필요한 모든 (빨간색 별표) 필드와 선택 필드를 입력 하 고 클릭 한 다음 **추가** 사용자 또는 그룹을 받는이 정책을 설정 합니다. FGPP 이러한 지정된 보안 사용자에 대 한 기본 도메인 정책 설정을 재정의합니다. 위의 그림 매우 제한적 정책은 손상을 방지 하기 위해 기본 관리자 계정에만 적용 됩니다. 정책은 너무 표준 사용자를 위해 준수, 복잡 한 이지만 IT 전문가 사용 하는 위험 계정에 적합 합니다.  
  
또한 우선 순위를 설정 하 고 있는 사용자 및 그룹 정책을 해당된 도메인에 적용 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_Precedence.png)  
  
세분화 암호 정책에 대 한 Active Directory Windows PowerShell cmdlet는 다음과 같습니다.  
  
```  
Add-ADFineGrainedPasswordPolicySubject  
Get-ADFineGrainedPasswordPolicy  
Get-ADFineGrainedPasswordPolicySubject  
New-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicySubject  
Set-ADFineGrainedPasswordPolicy  
  
```  
  
Windows Server 2008 R2 및 Windows Server 2012 간에 암호 정책 cmdlet 기능 세부적으로 변경 되지 않았습니다. 다음 그림을의 편의 cmdlet에 대 한 관련 된 인수를 보여 줍니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPP.gif)  
  
Active Directory 관리 센터를 사용 하면 특정 사용자를 위한 적용된 FGPP 집합이 결과 찾을 수 있습니다. 모든 사용자를 마우스 오른쪽 단추로 클릭 하 고 클릭 **결과 암호 설정 보기... ** 열려면는 *암호 설정* 암시적 또는 명시적 할당을 통해 해당 사용자에 게 적용 되는 페이지:  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RSOP.png)  
  
검사는 **속성** 프로그램의 모든 사용자 또는 그룹의 **암호 설정 직접 관련 된**, 할당 된 명시적으로 FGPPs 되는:  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPPSettings.gif)  
  
암묵적인 FGPP 할당 여기; 표시 되지 않습니다. 그에 대 한 사용 해야 하는 **결과 암호 설정 보기... ** 옵션이 있습니다.  
  
## <a name="BKMK_HistoryViewer"></a>관리 센터 Windows PowerShell 기록 Active Directory 뷰어를 사용 하 여  
관리 Windows의 미래 Windows PowerShell입니다. 작업 자동화 프레임 워크 맨 위에 표시 되는 층 그래픽 도구에서 가장 복잡 한 분산된 시스템의 관리 일관 되 고 효율적 됩니다. 모든 가능성 연락 하 고 컴퓨팅 투자 극대화 하기 위해 Windows PowerShell 작동 하는 방법을 파악 해야 합니다.  
  
이제 Active Directory 관리 센터 실행 모든 Windows PowerShell cmdlet 인수 및 값 전체 기록을 제공 합니다. 다른 위치에 대 한 연구 수정 및 사용 하 여 다시 cmdlet 역사를 복사할 수 있습니다. Windows PowerShell로 인해 명령을 어떤 사용자 Active Directory 관리 센터를 분리 지원 하기 위해 작업 메모 만들 수 있습니다. 찾을 안내 하 고 기록을 필터링 할 수 있습니다.  
  
Active Directory 관리 센터 Windows PowerShell 기록 뷰어의 목적은 실제 경험을 통해 자세한 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_HistoryViewer.gif)  
  
Windows PowerShell 기록 뷰어 표시 펼침 단추 (화살표)를 클릭 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RaiseViewer.png)  
  
그런 다음 사용자 또는 그룹의 회원 수정 합니다. 인수 지정 된 Active Directory 관리 센터를 실행 하는 각 cmdlet에 대 한 축소 뷰를 기록 뷰어 지속적으로 업데이트 합니다.  
  
Cmdlet의 인수에 제공 되는 모든 값을 확인 하는 관심 있는 품목을 확장 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ViewArgs.png)  
  
클릭는 **작업 시작** 메뉴를 만들 수정 또는 삭제 개체 Active Directory 관리 센터를 사용 하기 전에 수동 표기법 만들 수 있습니다. 수행 중인 작업에 입력 합니다.  변경 내용에 따라 완료 되 면 **작업 끝내기**합니다. 이러한 작업은 모두 더 잘 이해를 위한 사용할 수 있는 축소할 수 있는 노트에 수행할 작업 노트 그룹입니다.  
  
예를 들어, 사용자의 암호를 변경 하 고 그룹에서 저를 제거 하는 데 사용 하 여 Windows PowerShell 명령을 보려면:  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RemoveUser.gif)  
  
확인란을 선택 하 여 모두 표시 표시 다운로드-* 동사만 데이터를 검색 하는 Windows PowerShell cmdlet 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ShowAll.png)  
  
기록 뷰어 명령 Active Directory 관리 센터에서 실행 하 고 불필요 하 게 실행 하도록 일부 cmdlet 표시 되는 참고 수 리터럴 표시 됩니다. 예를 들어,를 새 사용자를 만들 수 있습니다.  
  
```  
new-aduser   
```  
  
및 사용 하 여 필요가 없습니다.  
  
```  
set-adaccountpassword  
enable-adaccount  
set-aduser  
  
```  
  
Active Directory 관리 센터 디자인 최소 코드 사용 및 모듈 필요합니다. 따라서 기능 만든 새 사용자, 사용자가 기존 수정 하는 다른 세트 것 최소한 각 기능 하 고을 cmdlet 함께 연결 합니다. Active Directory Windows PowerShell 들 배우고 때이 점에 유의 해야 합니다. 또한으로 사용할 수 있습니다 있는 학습 기술 나타나는 한 작업을 완료 하려면 Windows PowerShell 어떻게 간단 하 게 사용할 수 있습니다.  
  
## <a name="BKMK_Tshoot"></a>광고 DS 관리 문제 해결  
  
### <a name="introduction-to-troubleshooting"></a>문제 해결 소개  
최신 기능은 상대 및 기존 고객 환경에서 사용 부족으로 인해 Active Directory 관리 센터 문제 해결 옵션 제한 됩니다.  
  
### <a name="troubleshooting-options"></a>문제 해결 옵션  
  
#### <a name="logging-options"></a>로그인 옵션  
이제 Active Directory 관리 센터 추적 구성 파일의 일환으로 Windows Server 2012에서 기본 제공 로깅 포함 됩니다. 만들기/수정 dsac.exe와 동일한 폴더에 파일:  
  
**dsac.exe.config**  
  
다음과 같은 콘텐츠를 만듭니다.  
  
```  
<appSettings>  
  <add key="DsacLogLevel" value="Verbose" />  
</appSettings>  
<system.diagnostics>   
 <trace autoflush="false" indentsize="4">   
  <listeners>   
   <add name="myListener"   
    type="System.Diagnostics.TextWriterTraceListener"   
    initializeData="dsac.trace.log" />   
   <remove name="Default" />   
  </listeners>   
 </trace>   
</system.diagnostics>  
  
```  
  
에 대 한의 세부 정보 표시 수준 **DsacLogLevel** 는 **없음**, **오류**, **경고**, **정보**, 및 **자세히**합니다. 출력 파일 이름 구성할 수 및 dsac.exe와 동일한 폴더를 기록 합니다. 출력 사용자에 대해 더 ADAC의 작동 방식 도메인 컨트롤러 것 연락처에 연락한를 Windows PowerShell 명령을 실행, 응답의가 및 더 자세히 알 수 있습니다.  
  
예를 들어 정보 수준을 사용 하는 동안 추적 수준의 세부 정보 표시 수준 제외한 모든 결과가 반환 하는 다음과 같습니다.  
  
-   DSAC.exe 시작  
  
-   로깅 시작  
  
-   도메인 컨트롤러 초기 도메인 정보를 반환 요청  
  
    ```  
    [12:42:49][TID 3][Info] Command Id, Action, Command, Time, Elapsed Time ms (output), Number objects (output)  
    [12:42:49][TID 3][Info] 1, Invoke, Get-ADDomainController, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADDomainController-Discover:$null-DomainName:"CORP"-ForceDiscover:$null-Service:ADWS-Writable:$null  
    ```  
  
-   도메인 회사에서 반환 된 도메인 컨트롤러 d c 1  
  
-   광고 가상 드라이브 로드 PS  
  
    ```  
    [12:42:49][TID 3][Info] 1, Output, Get-ADDomainController, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] Found the domain controller 'DC1' in the domain 'CORP'.  
    [12:42:49][TID 3][Info] 2, Invoke, New-PSDrive, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] New-PSDrive-Name:"ADDrive0"-PSProvider:"ActiveDirectory"-Root:""-Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 2, Output, New-PSDrive, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 3, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
  
    ```  
  
-   도메인 루트 DSE 정보 가져오기  
  
    ```  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 3, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 4, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
  
    ```  
  
-   도메인 광고 휴지통 bin 정보 얻기  
  
    ```  
    [12:42:49][TID 3][Info] Get-ADOptionalFeature  
    -LDAPFilter:"(msDS-OptionalFeatureFlags=1)"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 4, Output, Get-ADOptionalFeature, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 5, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 5, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 6, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 6, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 7, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADOptionalFeature  
    -LDAPFilter:"(msDS-OptionalFeatureFlags=1)"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 7, Output, Get-ADOptionalFeature, 2012-04-16T12:42:50, 1  
    [12:42:50][TID 3][Info] 8, Invoke, Get-ADForest, 2012-04-16T12:42:50  
  
    ```  
  
-   광고 숲 받기  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADForest  
    -Identity:"corp.contoso.com"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 8, Output, Get-ADForest, 2012-04-16T12:42:50, 1  
    [12:42:50][TID 3][Info] 9, Invoke, Get-ADObject, 2012-04-16T12:42:50  
  
    ```  
  
-   지원 되는 암호화 유형, FGPP, 특정 사용자 정보 스키마 정보를 가져오기  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADObject  
    -LDAPFilter:"(|(ldapdisplayname=msDS-PhoneticDisplayName)(ldapdisplayname=msDS-PhoneticCompanyName)(ldapdisplayname=msDS-PhoneticDepartment)(ldapdisplayname=msDS-PhoneticFirstName)(ldapdisplayname=msDS-PhoneticLastName)(ldapdisplayname=msDS-SupportedEncryptionTypes)(ldapdisplayname=msDS-PasswordSettingsPrecedence))"  
    -Properties:lDAPDisplayName  
    -ResultPageSize:"100"  
    -ResultSetSize:$null  
    -SearchBase:"CN=Schema,CN=Configuration,DC=corp,DC=contoso,DC=com"  
    -SearchScope:"OneLevel"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 9, Output, Get-ADObject, 2012-04-16T12:42:50, 7  
    [12:42:50][TID 3][Info] 10, Invoke, Get-ADObject, 2012-04-16T12:42:50  
  
    ```  
  
-   도메인 헤드 클릭 관리자에 게 표시 하는 도메인 개체에 대 한 모든 정보를 알아보세요.  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADObject  
    -IncludeDeletedObjects:$false  
    -LDAPFilter:"(objectClass=*)"  
    -Properties:allowedChildClassesEffective,allowedChildClasses,lastKnownParent,sAMAccountType,systemFlags,userAccountControl,displayName,description,whenChanged,location,managedBy,memberOf,primaryGroupID,objectSid,msDS-User-Account-Control-Computed,sAMAccountName,lastLogonTimestamp,lastLogoff,mail,accountExpires,msDS-PhoneticCompanyName,msDS-PhoneticDepartment,msDS-PhoneticDisplayName,msDS-PhoneticFirstName,msDS-PhoneticLastName,pwdLastSet,operatingSystem,operatingSystemServicePack,operatingSystemVersion,telephoneNumber,physicalDeliveryOfficeName,department,company,manager,dNSHostName,groupType,c,l,employeeID,givenName,sn,title,st,postalCode,managedBy,userPrincipalName,isDeleted,msDS-PasswordSettingsPrecedence  
    -ResultPageSize:"100"  
    -ResultSetSize:"20201"  
    -SearchBase:"DC=corp,DC=contoso,DC=com"  
    -SearchScope:"Base"  
    -Server:"dc1.corp.contoso.com"  
  
    ```  
  
각 기능에 대 한.NET 스택도 표시의 자세한 정보 표시 수준 설정 하지만 이러한 제외 하 고 문제 해결 액세스 위반 나 크래시 감수 Dsac.exe 때 특히 유용 하 게 충분 한 데이터가 포함 되지 않습니다.  
  
> [!IMPORTANT]  
> 대역의 버전의 라는 서비스는 또한는 [Active Directory 관리 게이트웨이](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=2852), Windows Server 2008 SP2 및 Windows Server 2003 s p 2를 실행 합니다.  
  
이 문제의 원인이 두 가지는 다음과 같습니다.  
  
-   ADWS 서비스에서 액세스할 수 있는 도메인 컨트롤러 실행 되지 않습니다.  
  
-   네트워크 통신 ADWS 서비스 Active Directory 관리 센터를 실행 하는 컴퓨터에서 차단  
  
Active Directory 웹 서비스 인스턴스가 사용할 수 있는 경우 표시 되는 오류는 다음과 같습니다.  
  
|||  
|-|-|  
|오류|작업|  
|"모든 도메인에 연결할 수 없습니다. 새로 고침 또는 연결을 사용할 수 다시 시도해 보십시오 "|Active Directory 관리 센터 응용 프로그램의 시작 부분에 표시|  
|"에서 사용할 수 있는 서버를 찾을 수 없는 * <NetBIOS domain name> * Active Directory 웹 서비스 (ADWS)를 실행 하는 도메인"|도메인 노드 Active Directory 관리 센터 응용 프로그램에서 선택 하려고 할 때 표시|  
  
이 문제를 해결 하려면 다음이 단계를 사용 하 여 다음과 같습니다.  
  
1.  도메인에서 하나 이상의 도메인 컨트롤러 (와 숲 속의 가능 모든 도메인 컨트롤러)에서 시작 Active Directory 웹 서비스의 유효성을 검사 합니다. 모든 도메인 컨트롤러에 자동으로 시작 되도록 설정 되어 있는지 확인 합니다.  
  
2.  Active Directory 관리 센터를 실행 하는 컴퓨터에서의 유효성을 검사 ADWS NLTest.exe 명령을 실행 하 여 실행 하는 서버를 찾을 수 있습니다.  
  
    ```  
    nltest /dsgetdc:<domain NetBIOS name> /ws /force   
    nltest /dsgetdc:<domain fully qualified DNS name> /ws /force  
  
    ```  
  
    ADWS 서비스가 실행 중인 경우에 해당 테스트가 된다면 문제 이름 확인 하거나 LDAP ADWS 나 아니라 Active Directory 관리 센터입니다. 이 테스트 오류와 함께 실패 "1355 0x54B ERROR_NO_SUCH_DOMAIN" ADWS 하지만 도메인 컨트롤러에서 실행 되지 않으면, 모든 결론에 도달 하기 전에 지금 확인 합니다.  
  
3.  NLTest에서 반환 되는 도메인 컨트롤러에서 덤프할 명령 사용 하 여 듣기 포트 목록.  
  
    ```  
    Netstat -anob > ports.txt  
  
    ```  
  
    Ports.txt 파일을 검사 하 고 9389 포트에서 ADWS 서비스가 명령을 듣고 확인 합니다. 예:  
  
    ```  
    TCP    0.0.0.0:9389    0.0.0.0:0    LISTENING    1828  
    [Microsoft.ActiveDirectory.WebServices.exe]  
  
    TCP    [::]:9389       [::]:0       LISTENING    1828  
    [Microsoft.ActiveDirectory.WebServices.exe]  
  
    ```  
  
    명령을 듣고 있는 경우 Windows 방화벽 규칙의 유효성을 검사 하 고 9389 TCP 수 있는지 확인 인바인드 합니다. 기본적으로 도메인 컨트롤러 방화벽 규칙 "Active Directory 웹 서비스 (TCP in)"를 사용 합니다. 수신 되지 않을 경우 서비스가이 서버에서 실행 되 고 있는지 다시 확인 하 고 다시 시작 합니다. 다른 프로세스는 9389 포트에서 이미 수신 대기을 확인 합니다.  
  
4.  와 NLTEST에서 반환 되는 도메인 컨트롤러 Active Directory 관리 센터를 실행 하는 컴퓨터에서 네트워크 모니터 또는 다른 네트워크 캡처 유틸리티를 설치 합니다. 동시 네트워크 Active Directory 관리 센터를 시작 하 고 캡처를 중지 하기 전에 오류가 표시 두 컴퓨터에서 캡처를 수집 합니다. 클라이언트를 보내고 받는 포트 TCP 9389 도메인 컨트롤러에서 할 수 있는지 확인 합니다. 패킷 전송 있지만 도착 하지 또는 도착 고 클라이언트 도달할 도메인 컨트롤러 회신 있지만, 않기 가능성이 컴퓨터에 그 포트 패킷을 삭제 하는 네트워크에 사이 방화벽 합니다. 이 방화벽 소프트웨어 또는 하드웨어를 수 있으며 (바이러스 백신) 소프트웨어를 방지 제 3 자 끝점 될 수 있습니다.  
  
#### <a name="knownlikely-issues-and-support-scenarios"></a>가능성이/알려진 문제 및 지원 시나리오  
만 가능성이 문제가 Active Directory 관리 센터에 연결 하 고 Active Directory 웹 서비스 (ADWS) Windows Server 2012 또는 Windows Server 2008 R2 도메인 컨트롤러에서 실행 되지입니다.  
  
## <a name="see-also"></a>참조 하십시오  
[관리 센터 향상 된 Active Directory & #40; 소개 수준을 100 & #41;](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)  
  

