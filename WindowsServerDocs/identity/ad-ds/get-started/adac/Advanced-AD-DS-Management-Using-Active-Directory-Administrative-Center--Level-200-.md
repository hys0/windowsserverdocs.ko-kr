---
ms.assetid: 4d21d27d-5523-4993-ad4f-fbaa43df7576
title: Advanced AD DS Management Using Active Directory Administrative Center (Level 200)
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc2aaa9f7c7c42b6e94995ff473a580ce560ed93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820004"
---
# <a name="advanced-ad-ds-management-using-active-directory-administrative-center-level-200"></a>Advanced AD DS Management Using Active Directory Administrative Center (Level 200)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 아키텍처, 일반 작업에 대한 예제 및 문제 해결 정보를 비롯하여 새로운 Active Directory 휴지통, 세분화된 암호 정책 및 Windows PowerShell 기록 뷰어 등의 기능과 함께 업데이트된 Active Directory 관리 센터에 대해 자세히 알아봅니다. 참조에 대 한 소개 [Active Directory 관리 센터 개선 사항 및 #40; 도입 수준 100 & #41;](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)합니다.  
  
- [Active Directory 관리 센터 아키텍처](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Arch)  
- [Active Directory 관리 센터를 사용 하 여 휴지통 사용 하도록 설정 하 고 Active Directory 관리](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_EnableRecycleBin)  
- [구성 하 고 Active Directory 관리 센터를 사용 하 여 세분화 된 암호 정책 관리](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_FGPP)  
- [Active Directory 관리 센터 Windows PowerShell 기록 뷰어를 사용 하 여](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_HistoryViewer)  
- [AD DS 관리 문제 해결](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Tshoot)  
  
## <a name="BKMK_Arch"></a>Active Directory 관리 센터 아키텍처  
  
### <a name="active-directory-administrative-center-executables-dlls"></a>Active Directory Administrative Center 실행 파일, Dll  

새 휴지통, FGPP 및 기록 뷰어 기능이 추가되었지만 Active Directory 관리 센터의 모듈 및 기본 아키텍처는 변경되지 않았습니다.  
  
- Microsoft.ActiveDirectory.Management.UI.dll  
- Microsoft.ActiveDirectory.Management.UI.resources.dll  
- Microsoft.ActiveDirectory.Management.dll  
- Microsoft.ActiveDirectory.Management.resources.dll  
- ActiveDirectoryPowerShellResources.dll  
  
기본 Windows PowerShell 및 새 휴지통 기능의 작업 계층이 아래 그림에 나와 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/adds_adrestore.png)  
  
## <a name="BKMK_EnableRecycleBin"></a>Active Directory 관리 센터를 사용 하 여 휴지통 사용 하도록 설정 하 고 Active Directory 관리  
  
### <a name="capabilities"></a>기능  
  
- Windows Server 2012 또는 최신 Active Directory 관리 센터를 구성 하 고 Active Directory 휴지통 포리스트의 모든 도메인 파티션에 대 한 관리 할 수 있습니다. 이제 Windows PowerShell 또는 Ldp.exe를 사용하여 Active Directory 휴지통을 활성화하거나 도메인 파티션에 개체를 복원하기 위한 요구 사항이 없습니다.
- Active Directory 관리 센터에서는 의도적으로 삭제된 개체가 많은 대규모 환경에서 특정 대상을 보다 쉽게 복원할 수 있는 고급 필터링 조건을 제공합니다.
  
### <a name="limitations"></a>제한 사항  
  
- Active Directory 관리 센터에서는 도메인 파티션만 관리할 수 있으므로 구성, 도메인 DNS 또는 포리스트 DNS 파티션에서 삭제된 개체를 복원할 수 없습니다(스키마 파티션에서 개체를 삭제할 수 없음). 도메인이 아닌 파티션에서 개체를 복원하려면 [Restore-ADObject](https://technet.microsoft.com/library/ee617262.aspx)를 사용하세요.  

- Active Directory 관리 센터에서는 단일 작업에서 개체의 하위 트리를 복원할 수 없습니다. 예를 들어 중첩된 OU, 사용자, 그룹 및 컴퓨터가 있는 OU를 삭제한 경우 기본 OU를 복원해도 자식 개체는 복원되지 않습니다.  
  
    > [!NOTE]  
    > Active Directory 관리 센터 일괄 복원 작업에서는 한 "최상의" 삭제 된 개체에 일종의 *만 선택 영역 내* 있으므로 부모 복원 목록에 대 한 자식 앞에 정렬 됩니다. 간단한 테스트 사례에서는 단일 작업으로 개체의 하위 트리를 복원할 수 있습니다. 하지만 부분 트리-누락 된 삭제 된 부모 노드 중 일부와 트리-를 포함 하는 선택과 같은 코너 케이스 또는 오류 것과 같은 경우 예상 대로 작동 하지 않을 수, 실패 하면 부모 복원 하는 경우 자식 개체를 건너뜁니다. 따라서 항상 부모 개체를 복원한 후 개체의 하위 트리를 별도 작업으로 복원해야 합니다.  
  
Active Directory 휴지통에 Windows Server 2008 R2 포리스트 기능 수준이 필요 하 고 Enterprise Admins 그룹의 멤버 여야 합니다. 활성화된 후에는 Active Directory 휴지통을 비활성화할 수 없습니다. Active Directory 휴지통은 포리스트의 모든 도메인 컨트롤러에서 Active Directory 데이터베이스(NTDS.DIT)의 크기를 증가시킵니다. 휴지통에 사용되는 디스크 공간은 개체 및 모든 특성 데이터를 유지하므로 시간이 지남에 따라 계속 증가합니다.  
  
### <a name="enabling-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory 관리 센터를 사용하여 Active Directory 휴지통 활성화

Active Directory 휴지통을 활성화하려면 **Active Directory 관리 센터** 를 열고 탐색 창에서 포리스트 이름을 클릭합니다. **작업** 창에서 **휴지통 사용**을 클릭합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBin.png)  
  
Active Directory 관리 센터에 **휴지통 사용 확인** 대화 상자가 표시됩니다. 이 대화 상자에는 휴지통을 활성화한 후 되돌릴 수 없음을 알리는 경고 메시지가 표시되어 있습니다. **확인**을 클릭하여 Active Directory 휴지통을 활성화합니다. Active Directory 관리 센터에는 모든 도메인 컨트롤러가 구성 변경 사항을 복제할 때까지 Active Directory 휴지통이 완전하게 작동하지 않음을 알리는 또 다른 대화 상자도 표시됩니다.  
  
> [!IMPORTANT]  
> 다음에 해당하는 경우 Active Directory 휴지통을 활성화하는 옵션을 사용할 수 없습니다.  
>
> - 포리스트 기능 수준이 Windows Server 2008 R2보다 낮은 경우  
> - 이미 활성화된 경우  

해당 Active Directory Windows PowerShell cmdlet은 다음과 같습니다.  

```powershell
Enable-ADOptionalFeature  
```

Windows PowerShell을 사용하여 Active Directory 휴지통을 활성화하는 방법에 대한 자세한 내용은 [Active Directory 휴지통 단계별 가이드](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-#active-directory-recycle-bin-step-by-step)를 참조하세요.  
  
### <a name="managing-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory 관리 센터를 사용하여 Active Directory 휴지통 관리

이 섹션에서는 **corp.contoso.com**이라는 기존 도메인 예를 사용합니다. 이 도메인은 **UserAccounts**라는 부모 OU에 사용자를 구성합니다. **UserAccounts** OU에는 부서별로 이름이 지정되고 각각 추가 OU, 사용자 및 그룹을 포함하는 세 개의 자식 OU가 포함되어 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBinExampleOU.png)  
  
#### <a name="storage-and-filtering"></a>저장소 및 필터링

Active Directory 휴지통은 포리스트에서 삭제된 모든 개체를 유지합니다. 기본적으로 포리스트의 **tombstoneLifetime** 특성과 일치하도록 설정된 **msDS-deletedObjectLifetime** 특성에 따라 이러한 개체를 저장합니다. Windows Server 2003 SP1 이상을 사용하여 만든 모든 포리스트에서 **tombstoneLifetime** 값은 기본적으로 180일로 설정됩니다. Windows 2000에서 업그레이드되거나 Windows Server 2003(서비스 팩 없음)과 함께 설치된 모든 포리스트에는 기본 tombstoneLifetime 특성이 설정되지 않으므로 Windows에서 내부 기본값인 60일을 사용합니다. 이 모든 값을 구성할 수 있습니다. Active Directory 관리 센터를 사용하여 포리스트의 도메인 파티션에서 삭제된 모든 개체를 복원할 수 있습니다. 다른 파티션에서 삭제된 개체(예: 구성)를 복원하려면 계속 **Restore-ADObject** cmdlet을 사용해야 합니다. Active Directory 휴지통을 활성화하면 Active Directory 관리 센터에서 모든 도메인 파티션 아래에 **삭제된 개체** 컨테이너가 표시됩니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_DeletedObjectsContainer.png)  
  
**삭제된 개체** 컨테이너에는 해당 도메인 파티션의 복구 가능한 모든 개체가 표시됩니다. **msDS-deletedObjectLifetime** 보다 오래된 삭제된 개체를 재활용된 개체라고 합니다. Active Directory 관리 센터에는 재활용된 개체가 표시되지 않으므로 Active Directory 관리 센터를 사용하여 이러한 개체를 복원할 수 없습니다.  
  
휴지통의 아키텍처 및 처리 규칙의 자세한 내용은 참조 하세요. [AD 휴지통: 이해, 구현, 모범 사례 및 문제 해결](http://blogs.technet.com/b/askds/archive/2009/08/27/the-ad-recycle-bin-understanding-implementing-best-practices-and-troubleshooting.aspx)합니다.  
  
Active Directory 관리 센터는 컨테이너에서 반환되는 기본 개체 수를 인위적으로 20,000개로 제한합니다. **관리** 메뉴를 클릭한 다음 **관리 목록 옵션**을 클릭하여 이 제한을 100,000개까지 늘릴 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_MgmtList.png)  
  
#### <a name="restoration"></a>복원  
  
##### <a name="filtering"></a>필터링

Active Directory 관리 센터에서는 강력한 조건 및 필터링 옵션을 제공합니다. 실제 복원에서 사용하기 전에 이러한 옵션을 잘 알고 있어야 합니다. 도메인에서는 수명이 다한 많은 개체를 의도적으로 삭제합니다. 삭제된 개체 수명이 180일이라고 하면, 사고가 발생하는 경우 개체 중 일부는 복원하지 못할 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_AddCriteria.png)  
  
복잡한 LDAP 필터를 쓰고 UTC 값을 날짜와 시간으로 변환하는 대신 기본 및 고급 **필터** 메뉴를 사용하여 관련 개체만 나열할 수 있습니다. 삭제한 날짜, 개체의 이름 또는 기타 주요 데이터를 알고 있는 경우 필터링할 때 이를 유용하게 활용할 수 있습니다. 검색 상자의 오른쪽에 있는 펼침 단추를 클릭하여 고급 필터 옵션을 전환합니다.  
  
복원 작업에는 다른 검색과 마찬가지로 모든 표준 필터 조건 옵션이 지원됩니다. 기본 제공 필터를 사용할 경우 개체 복원의 중요한 요소는 일반적으로 다음과 같습니다.  
  
- *ANR (모호한 이름 확인-메뉴에서 있지만에 입력할 때 사용 되는 것에 나열 되지 않은 합니다 * * * 필터 * * * 상자)*  
- 지정한 날짜 사이에 마지막으로 수정된 개체  
- 개체는 사용자/조직 구성원/컴퓨터/그룹/조직 구성 단위  
- 이름  
- 삭제된 날짜  
- 마지막으로 알려진 부모  
- 형식  
- 설명  
- City  
- 국가/지역  
- 부서  
- 직원 ID  
- 이름  
- 직함  
- 성  
- SAM 계정 이름  
- 시/도  
- 전화 번호  
- UPN  
- 우편 번호  

여러 조건을 추가할 수 있습니다. 예를 들어 일 일리노이 주 시카고에서에서 2012 년 9 월 24 일 관리자의 직함으로 삭제 된 모든 사용자 개체를 찾을 수 있습니다.
  
복구할 개체를 평가할 때 열 머리글을 추가, 수정 또는 다시 정렬하여 보다 자세한 정보를 제공할 수도 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ColumnHeaders.png)  
  
모호한 이름 확인에 대 한 자세한 내용은 참조 [ANR 특성](https://msdn.microsoft.com/library/ms675092(VS.85).aspx)합니다.  
  
##### <a name="single-object"></a>단일 개체

삭제된 개체를 복원하는 작업은 항상 단일 작업이었습니다.  Active Directory 관리 센터에서 이 작업을 보다 쉽게 수행할 수 있습니다. 단일 사용자와 같은 삭제된 개체를 복원하려면 다음을 수행합니다.  
  
1. Active Directory 관리 센터의 탐색 창에서 도메인 이름을 클릭합니다.  
2. 관리 목록에서 **삭제된 개체**를 두 번 클릭합니다.  
3. 개체를 마우스 오른쪽 단추로 클릭하고 **복원**을 클릭하거나, **작업** 창에서 **복원** 을 클릭합니다.  
  
개체가 원래 위치로 복원됩니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreSingle.gif)  
  
클릭 **복원 대상...** 복원 위치를 변경 합니다. 삭제 된 개체의 부모 컨테이너도 삭제 되었지만 부모를 복원 하지 않을 경우에 유용 합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreToSingle.gif)  
  
##### <a name="multiple-peer-objects"></a>여러 개의 피어 개체

OU의 모든 사용자와 같은 피어 수준의 여러 개체를 복원할 수 있습니다. Ctrl 키를 누른 채 복원할 삭제된 개체를 하나 이상 클릭합니다. 작업 창에서 **복원**을 클릭합니다. Ctrl 키와 A 키를 눌러 표시된 모든 개체를 선택하거나, Shift 키를 누르고 클릭하여 개체 범위를 선택할 수도 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestorePeers.png)  
  
##### <a name="multiple-parent-and-child-objects"></a>여러 부모 및 자식 개체

Active Directory 관리 센터에서는 삭제된 개체의 중첩된 트리를 단일 작업으로 복원할 수 없기 때문에 여러 부모/자식 복원에 대한 복원 프로세스를 이해해야 합니다.  
  
1. 트리의 맨 위에 있는 삭제된 개체를 복원합니다.  
2. 해당 부모 개체의 직계 자식을 복원합니다.  
3. 이러한 부모 개체의 직계 자식을 복원합니다.  
4. 필요에 따라 모든 개체가 복원될 때까지 반복합니다.  
  
부모를 복원하기 전에 자식 개체를 복원할 수 없습니다. 이 복원을 시도하면 다음 오류가 반환됩니다.  
  
**해당 개체의 부모가 설치되지 않거나 삭제되었으므로 작업을 실행할 수 없습니다.**  
  
**마지막으로 알려진 부모** 특성에 각 개체의 부모 관계가 표시됩니다. 부모를 복원한 후 Active Directory 관리 센터를 새로 고치면 **마지막으로 알려진 부모** 특성이 삭제된 위치에서 복원된 위치로 변경됩니다. 따라서 부모 개체의 위치에는 더 이상 삭제 된 개체 컨테이너의 고유 이름을 표시 하는 경우 해당 자식 개체를 복원할 수 없습니다.  
  
자식 OU 및 사용자가 포함된 Sales OU를 관리자가 실수로 삭제한 시나리오를 예로 들어 보겠습니다.  
  
첫째,의 값을 관찰 합니다 **마지막으로 알려진 부모** 삭제 된 모든 사용자에 대 한 특성을 읽는 방법을 **OU = Sales\0ADEL:*< guid + 삭제 된 개체 컨테이너 고유 이름 > * * *:  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParent.gif)  
  
모호한 이름 Sales를 필터링하여 삭제된 OU가 반환되면 복원합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSales.png)  
  
복원 된 Sales OU 고유 이름으로 변경 하는 삭제 된 사용자 개체의 마지막으로 알려진 부모 특성을 보려면 Active Directory 관리 센터를 새로 고칩니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesRestored.gif)  
  
모든 Sales 사용자를 필터링합니다. Ctrl 키와 A 키를 눌러 삭제된 모든 Sales 사용자를 선택합니다. **복원** 을 클릭하여 **삭제된 개체** 컨테이너의 개체를 그룹 구성원 자격 및 특성을 그대로 유지한 채 Sales OU로 이동합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesUndelete.png)  
  
**Sales** OU에 자식 OU가 포함된 경우 먼저 이 자식 OU를 복원한 다음 해당 자식을 차례로 복원할 수 있습니다.  
  
삭제 된 부모 컨테이너를 지정 하 여 중첩 된 모든 삭제 된 개체를 복원 하려면 참조 [부록 b: 여러 복원할 삭제 된 Active Directory 개체 (예제 스크립트)](https://technet.microsoft.com/library/dd379504(WS.10).aspx)합니다.  
  
삭제된 개체를 복원하는 Active Directory Windows PowerShell cmdlet은 다음과 같습니다.  

```powershell
Restore-adobject  
```

**Restore-ADObject** cmdlet 기능은 Windows Server 2008 R2와 Windows Server 2012 간에 변경되지 않았습니다.  
  
##### <a name="server-side-filtering"></a>서버 쪽 필터링

중간 규모 및 대규모 기업의 경우 시간이 지남에 따라 삭제된 개체 컨테이너에 20,000개(또는 심지어 100,000개)가 넘는 개체가 누적되어 모든 개체를 표시하기가 어려워집니다. Active Directory 관리 센터의 필터 메커니즘은 클라이언트 쪽 필터링을 기반으로 하므로 이러한 추가 개체를 표시할 수 없습니다. 이 제한을 해결하려면 다음 단계를 사용하여 서버 쪽 검색을 수행하세요.  
  
1. **삭제된 개체** 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **이 노드에서 검색**을 클릭합니다.  
2. 펼침 단추를 클릭하여 **+조건 추가** 메뉴를 표시하고 **지정한 날짜 사이에 마지막으로 수정된 개체**를 선택하여 추가합니다. 마지막 수정 시간(**whenChanged** 특성)은 삭제 시간의 근사치이며, 대부분의 환경에서 동일합니다. 이 쿼리는 서버 쪽 검색을 수행합니다.  
3. 결과에서 추가 표시 필터링, 정렬 등을 사용하여 복원할 삭제된 개체를 찾은 후 정상적으로 복원합니다.  
  
## <a name="BKMK_FGPP"></a>구성 하 고 Active Directory 관리 센터를 사용 하 여 세분화 된 암호 정책 관리  
  
### <a name="configuring-fine-grained-password-policies"></a>세분화된 암호 정책 구성

Active Directory 관리 센터에서 FGPP(세분화된 암호 정책) 개체를 만들고 관리할 수 있습니다. Windows Server 2008에서 FGPP 기능이 도입되었지만 이 기능을 위한 그래픽 관리 인터페이스는 Windows Server 2012에서 처음 제공되었습니다. 도메인 수준에서 세분화된 암호 정책을 적용하여 Windows Server 2003에 필요한 단일 도메인 암호를 재정의할 수 있습니다. 서로 다른 설정으로 여러 FGPP를 만들어 도메인의 개별 사용자 또는 그룹에 서로 다른 암호 정책을 적용할 수 있습니다.  
  
세분화된 암호 정책에 대한 자세한 내용은 [AD DS 세분화된 암호 및 계정 잠금 정책 단계별 가이드(Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)를 참조하세요.  
  
탐색 창에서 트리 보기와 도메인을 차례로 클릭하고, **시스템**, **암호 설정 컨테이너**를 클릭한 다음, 작업 창에서 **새로 만들기** 및 **암호 설정**을 클릭합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_PasswordSettings.png)  
  
### <a name="managing-fine-grained-password-policies"></a>세분화된 암호 정책 관리

새 FGPP를 만들거나 기존 FGPP를 편집할 경우 **암호 설정** 편집기가 나타납니다. 이제 이 특정 용도의 편집기로 Windows Server 2008 또는 Windows Server 2008 R2에서처럼 원하는 모든 암호 정책을 구성할 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_CreatePasswordSettings.png)  
  
모든 필수(빨간색 별표) 필드 및 선택적 필드를 입력한 다음 **추가** 를 클릭하여 이 정책을 받을 사용자 또는 그룹을 설정합니다. FGPP는 이러한 지정된 보안 주체에 대한 기본 도메인 정책 설정을 재정의합니다. 위 그림에서는 손상을 방지하기 위해 매우 제한적인 정책이 기본 제공 관리자 계정에만 적용됩니다. 이 정책은 표준 사용자가 준수하기에는 너무 복잡하지만 IT 전문가만 사용하는 높은 위험 수준의 계정에는 완벽합니다.  
  
또한 지정된 도메인 내에서 정책이 적용되는 사용자 및 그룹과 우선 순위를 설정할 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_Precedence.png)  
  
세분화된 암호 정책에 대한 Active Directory Windows PowerShell cmdlet은 다음과 같습니다.  
  
```powershell
Add-ADFineGrainedPasswordPolicySubject  
Get-ADFineGrainedPasswordPolicy  
Get-ADFineGrainedPasswordPolicySubject  
New-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicySubject  
Set-ADFineGrainedPasswordPolicy  
```

세분화된 암호 정책 cmdlet 기능은 Windows Server 2008 R2와 Windows Server 2012 간에 변경되지 않았습니다. 편의를 위해 다음 다이어그램에서는 cmdlet의 관련 인수를 보여 줍니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPP.gif)  
  
Active Directory 관리 센터를 사용하여 특정 사용자에 대해 적용된 FGPP의 결과 집합을 찾을 수도 있습니다. 모든 사용자를 마우스 오른쪽 단추로 클릭 하 고 클릭 **결과 암호 설정... 볼** 열려는 *암호 설정* 암시적 또는 명시적 할당을 통해 해당 사용자에 게 적용 되는 페이지:  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RSOP.png)  
  
사용자 또는 그룹의 **속성** 을 살펴보면 **직접 연결된 암호 설정**이 표시되는데, 이는 명시적으로 할당된 FGPP입니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPPSettings.gif)  
  
암시적 FGPP 할당 여기서 표시 되지 않습니다. 사용 해야 하는 **결과 암호 설정... 볼** 옵션입니다.  
  
## <a name="BKMK_HistoryViewer"></a>Active Directory 관리 센터 Windows PowerShell 기록 뷰어를 사용 하 여

Windows 관리의 미래는 Windows PowerShell입니다. 그래픽 도구의 계층을 작업 자동화 프레임워크 위에 두면 아무리 복잡한 분산 시스템도 일관성 있게 효율적으로 관리할 수 있습니다. 잠재력을 최대한 실현하고 컴퓨팅 투자를 극대화하려면 Windows PowerShell의 작동 방식을 이해해야 합니다.  
  
이제 Active Directory 관리 센터에서는 실행하는 모든 Windows PowerShell cmdlet과 해당 인수 및 값에 대한 전체 기록을 제공합니다. 어디에서든 cmdlet 기록을 복사하여 검토하거나 수정하고 재사용할 수 있습니다. Active Directory 관리 센터 명령에 따른 Windows PowerShell 결과를 격리하는 데 도움이 되도록 작업 메모를 만들 수 있습니다. 또한 기록을 필터링하여 관심 지점을 찾을 수 있습니다.  
  
Active Directory 관리 센터 Windows PowerShell 기록 뷰어의 용도는 실제 경험을 통해 학습할 수 있는 환경을 제공하는 것입니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_HistoryViewer.gif)  
  
펼침 단추(화살표)를 클릭하여 Windows PowerShell 기록 뷰어를 표시합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RaiseViewer.png)  
  
그런 다음 사용자를 만들거나 그룹의 구성원 자격을 수정합니다. 기록 뷰어는 Active Directory 관리 센터에서 지정된 인수와 함께 실행한 각 cmdlet의 축소된 보기로 지속적으로 업데이트됩니다.  
  
확인하려는 행 항목을 모두 확장하여 cmdlet의 인수에 제공된 모든 값을 표시합니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ViewArgs.png)  
  
Active Directory 관리 센터를 사용하여 개체를 생성, 수정 또는 삭제하기 전에 **작업 시작** 메뉴를 클릭하여 수동 표기법을 만듭니다. 수행하려는 작업을 입력합니다.  변경 작업이 완료되면 **작업 끝내기**를 선택합니다. 작업 메모는 수행한 모든 작업을 축소 가능한 메모로 그룹화하며, 이를 통해 보다 쉽게 이해할 수 있습니다.  
  
예를 들어 사용자의 암호를 변경하고 해당 사용자를 그룹에서 제거하는 데 사용된 Windows PowerShell 명령을 확인하기 위해 작업 메모를 축소할 수 있습니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RemoveUser.gif)  
  
또한 모두 표시 확인란을 선택하면 데이터 검색만 수행하는 Get-* verb Windows PowerShell cmdlet이 표시됩니다.  
  
![고급 AD DS 관리](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ShowAll.png)  
  
기록 뷰어에는 Active Directory 관리 센터에서 실행된 리터럴 명령이 표시되는데, 이를 보면 일부 cmdlet이 불필요하게 실행된 것처럼 보일 수 있습니다. 예를 들어 다음을 사용하여 새 사용자를 만들 수 있습니다.  

```powershell
new-aduser
```

하지만 다음 명령은 사용할 필요가 없습니다.  

```powershell
set-adaccountpassword  
enable-adaccount  
set-aduser  
```

Active Directory 관리 센터는 필요한 코드 사용 및 모듈을 최소화하도록 디자인되었습니다. 따라서 새 사용자를 만들고 기존 사용자를 수정하는 데 서로 다른 함수 집합을 사용하는 대신 각 함수를 최소한으로 실행한 다음 cmdlet을 사용하여 서로 연결합니다. Active Directory Windows PowerShell을 학습할 때 이 점을 염두에 두어야 합니다. 또한 이를 하나의 학습 기법으로 활용하여 Windows PowerShell을 통해 단일 작업을 완료하는 것이 얼마나 간단한지 확인할 수 있습니다.  
  
## <a name="BKMK_Tshoot"></a>AD DS 관리 문제 해결  
  
### <a name="introduction-to-troubleshooting"></a>문제 해결 소개

비교적 새로운 요소가 도입되고 기존 고객 환경에서 사용된 요소가 없어졌기 때문에 Active Directory 관리 센터에는 제한된 문제 해결 옵션이 있습니다.  
  
### <a name="troubleshooting-options"></a>문제 해결 옵션  
  
#### <a name="logging-options"></a>로깅 옵션

Active Directory 관리 센터는 이제 기본 제공 로깅, 추적 구성 파일의 일부로 포함 됩니다. dsac.exe와 동일한 폴더에서 다음 파일을 만들고 수정합니다.  
  
**dsac.exe.config**
  
다음 콘텐츠를 만듭니다.  
  
```xml
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

**DsacLogLevel** 의 자세한 표시 수준은 **None**, **Error**, **Warning**, **Info**및 **Verbose**입니다. 출력 파일 이름은 구성 가능하며 dsac.exe와 동일한 폴더에 기록됩니다. ADAC의 작동 방식, ADAC에서 연결한 도메인 컨트롤러, Windows PowerShell 명령에서 실행한 작업, 응답 등에 대한 자세한 정보를 출력 파일에서 확인할 수 있습니다.  

예를 들어 INFO 수준을 사용할 경우 추적 수준의 자세한 표시 수준을 제외하고 모든 결과가 반환됩니다.  
  
- DSAC.exe 시작  
- 로깅 시작  
- 도메인 컨트롤러에서 초기 도메인 정보를 반환하도록 요청  

   ```
   [12:42:49][TID 3][Info] Command Id, Action, Command, Time, Elapsed Time ms (output), Number objects (output)  
   [12:42:49][TID 3][Info] 1, Invoke, Get-ADDomainController, 2012-04-16T12:42:49  
   [12:42:49][TID 3][Info] Get-ADDomainController-Discover:$null-DomainName:"CORP"-ForceDiscover:$null-Service:ADWS-Writable:$null  
   ```

- Corp 도메인에서 도메인 컨트롤러 DC1 반환  
- PS AD 가상 드라이브 로드  

   ```
   [12:42:49][TID 3][Info] 1, Output, Get-ADDomainController, 2012-04-16T12:42:49, 1  
   [12:42:49][TID 3][Info] Found the domain controller 'DC1' in the domain 'CORP'.  
   [12:42:49][TID 3][Info] 2, Invoke, New-PSDrive, 2012-04-16T12:42:49  
   [12:42:49][TID 3][Info] New-PSDrive-Name:"ADDrive0"-PSProvider:"ActiveDirectory"-Root:""-Server:"dc1.corp.contoso.com"  
   [12:42:49][TID 3][Info] 2, Output, New-PSDrive, 2012-04-16T12:42:49, 1  
   [12:42:49][TID 3][Info] 3, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
   ```
  
- 도메인 루트 DSE 정보 가져오기  

   ```
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"  
   [12:42:49][TID 3][Info] 3, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
   [12:42:49][TID 3][Info] 4, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
   ```

- 도메인 AD 휴지통 정보 가져오기  

   ```
   [12:42:49][TID 3][Info] Get-ADOptionalFeature -LDAPFilter:"(msDS-OptionalFeatureFlags=1)" -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 4, Output, Get-ADOptionalFeature, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 5, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 5, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 6, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 6, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 7, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADOptionalFeature -LDAPFilter:"(msDS-OptionalFeatureFlags=1)" -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 7, Output, Get-ADOptionalFeature, 2012-04-16T12:42:50, 1
   [12:42:50][TID 3][Info] 8, Invoke, Get-ADForest, 2012-04-16T12:42:50
   ```

- AD 포리스트 가져오기  

   ```  
   [12:42:50][TID 3][Info] Get-ADForest -Identity:"corp.contoso.com" -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 8, Output, Get-ADForest, 2012-04-16T12:42:50, 1  
   [12:42:50][TID 3][Info] 9, Invoke, Get-ADObject, 2012-04-16T12:42:50  
   ```

- 지원되는 암호화 종류에 대한 스키마 정보, FGPP 및 특정 사용자 정보 가져오기  

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

- 도메인 헤드를 클릭한 관리자에게 표시할 도메인 개체에 대한 모든 정보 가져오기  

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

또한 Verbose 수준을 설정하면 각 함수에 대한 .NET 스택이 표시되지만 Dsac.exe의 액세스 위반 또는 크래시 문제를 해결할 때 외에는 특별히 유용한 데이터는 포함되지 않습니다. 이 문제의 가능한 원인에는 다음 두 가지가 있습니다.
  
- ADWS 서비스가 액세스 가능한 도메인 컨트롤러에서 실행되고 있지 않습니다.
- 네트워크 통신 ADWS 서비스에 Active Directory 관리 센터를 실행 하는 컴퓨터에서 차단 됩니다.

> [!IMPORTANT]  
> Windows Server 2008 SP2 및 Windows Server 2003 SP2에서 실행되는 [Active Directory 관리 게이트웨이](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=2852)라는 대역 외 버전의 서비스도 있습니다.
>

사용 가능한 Active Directory 웹 서비스 인스턴스가 없는 경우에 표시되는 오류는 다음과 같습니다.  
  
|Error|연산|
| --- | --- |  
|"도메인에 연결할 수 없습니다. 연결되면 새로 고치거나 다시 시도해 보세요."|Active Directory 관리 센터 응용 프로그램을 시작할 때 표시됩니다.|
|"에서 사용 가능한 서버를 찾을 수 없습니다는 *<NetBIOS domain name>* 는 웹 서비스 ADWS (Active Directory)를 실행 중인 도메인"|Active Directory 관리 센터 응용 프로그램에서 도메인 노드를 선택하려고 할 때 표시됩니다.|
  
이 문제를 해결하려면 다음 단계를 사용합니다.  
  
1. ADWS(Active Directory 웹 서비스) 서비스가 도메인에 있는 하나 이상의 도메인 컨트롤러(및 가급적 포리스트의 모든 도메인 컨트롤러)에서 시작되었는지 확인합니다. 모든 도메인 컨트롤러에서 자동으로 시작되도록 설정되어 있는지도 확인합니다.
2. Active Directory 관리 센터를 실행하는 컴퓨터에서 다음 NLTest.exe 명령을 실행하여 ADWS를 실행하는 서버를 찾을 수 있는지 확인합니다.  

   ```
   nltest /dsgetdc:<domain NetBIOS name> /ws /force
   nltest /dsgetdc:<domain fully qualified DNS name> /ws /force
   ```

   ADWS 서비스가 실행 중인 경우에도 이러한 테스트에 실패하면 ADWS 또는 Active Directory 관리 센터가 아니라 이름 확인 또는 LDAP에 문제가 있는 것입니다. ADWS가 도메인 컨트롤러에서 실행되고 있지 않은 경우에도 "1355 0x54B ERROR_NO_SUCH_DOMAIN" 오류와 함께 이 테스트에 실패하므로 결론을 내리기 전에 다시 한 번 확인해야 합니다.  
  
3. NLTest에서 반환된 도메인 컨트롤러에서 다음 명령을 사용하여 수신 대기 포트 목록을 덤프합니다.  

   ```
   Netstat -anob > ports.txt  
   ```

   ports.txt 파일을 검사하여 ADWS 서비스가 포트 9389에서 수신 대기 중인지 확인합니다. 예:  

   ```
   TCP    0.0.0.0:9389    0.0.0.0:0    LISTENING    1828  
   [Microsoft.ActiveDirectory.WebServices.exe]  

   TCP    [::]:9389       [::]:0       LISTENING    1828  
   [Microsoft.ActiveDirectory.WebServices.exe]  
   ```

   수신 대기 중이면 Windows 방화벽 규칙의 유효성을 검사하고 9389 TCP 인바운드를 허용하는지 확인합니다. 기본적으로 도메인 컨트롤러는 "Active Directory 웹 서비스(TCP-In)" 방화벽 규칙을 사용합니다. 수신 대기 중이지 않으면 서비스가 이 서버에서 실행되고 있는지 다시 확인한 후 서비스를 다시 시작합니다. 다른 프로세스가 포트 9389에서 이미 수신 대기 중인지 확인합니다.  
  
4. Active Directory 관리 센터를 실행하는 컴퓨터와 NLTEST에서 반환된 도메인 컨트롤러에 NetMon 또는 다른 네트워크 캡처 유틸리티를 설치합니다. 두 컴퓨터 모두에서 동시 네트워크 캡처를 수집합니다. 이때 Active Directory 관리 센터를 시작하여 캡처를 중지하기 전에 오류를 확인합니다. 클라이언트가 TCP 포트 9389를 통해 도메인 컨트롤러와 데이터를 주고받을 수 있는지 확인합니다. 패킷이 전송되었지만 수신되지 않거나, 패킷이 수신되어 도메인 컨트롤러에서 응답했지만 클라이언트에 응답이 수신되지 않는 경우 네트워크의 컴퓨터 사이에 해당 포트의 패킷을 삭제하는 방화벽이 있을 수 있습니다. 이 방화벽은 소프트웨어 또는 하드웨어일 수 있으며, 타사 끝점 보호(바이러스 백신) 소프트웨어의 일부일 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목

[AD 휴지통, 세분화 된 암호 정책을 PowerShell 기록](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)  
