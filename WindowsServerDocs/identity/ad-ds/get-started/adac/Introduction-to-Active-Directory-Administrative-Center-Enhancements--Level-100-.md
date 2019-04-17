---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: "Active Directory (수준을 100) 관리 센터 향상 된 기능을 소개"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7f52b22ec74ba12c383952e68b412f871a56474c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Active Directory (수준을 100) 관리 센터 향상 된 기능을 소개

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2012에서 ADAC 다음 관리 기능이 포함 됩니다.

-   [Active Directory 휴지통](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)

-   [정교한 암호 정책](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)

-   [Windows PowerShell 기록 뷰어](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Active Directory 휴지통
실수로 Active Directory 개체의 삭제 되는 사용자의 Active Directory Domain Services (AD DS) 및 Active Directory 경량 디렉터리 서비스 (AD LDS)에 대 한 일반적인 발생 합니다. 이전 버전의 Windows Server, Windows Server 2008 R2, 이전 하나 수 복구할 실수로 삭제 된 Active Directory 개체 있지만 해결 방법을 자신의 단점 했습니다.

Windows Server 2008, Windows Server 백업 기능을 사용할 수 있습니다 및 **ntdsutil** 정식 복원 명령을 표시 하려면 개체 복원 된 데이터는 도메인 전체 복제 된 되도록 같이 신뢰할 수 있습니다. 신뢰할 수 있는 복원 솔루션을 단점은에서 DSRM 디렉터리 서비스 복원 모드 () 수행 해야 것 이었습니다. 복원 하는 도메인 컨트롤러 DSRM, 동안 오프 라인 상태를 유지 했습니다. 따라서 요청을 처리 하는 클라이언트 수 없습니다.

Windows Server 2003에 대 한 Active Directory 및 Windows Server 2008 AD DS 삭제 애니메이션 통해 삭제 된 Active Directory 개체를 복구할 수 있습니다. 그러나 개체의 연결 되는 특성 (예를 들어, 사용자 계정의 그룹 구성원)은 제거 물리적으로 다시 애니메이션 및 비 링크 반환 특성을 삭제 된 복구 되지 않은 합니다. 따라서 관리자 수 개체의 삭제 실수로 ultimate 솔루션으로 삭제 애니메이션에 의존 하지 합니다. 애니메이션 삭제 기록에 대 한 자세한 내용은 참조 [Active Directory 삭제 개체 다시 애니메이션](https://go.microsoft.com/fwlink/?LinkID=125452)합니다.

Active Directory 휴지통, Windows Server 2008 R2에서 시작 기존 삭제 애니메이션 인프라 빌드하고 보존 실수로 삭제 된 Active Directory 개체를 복구 하는 기능을 개선 합니다.

때 Active Directory 휴지통을 모두 링크 반환 사용 하도록 설정 하 고 삭제 된 Active Directory 개체의 특성 비 링크 값은 그대로 유지 고 개체와 같은 상태로 일관 되 게 논리를 삭제 하기 전에 바로에 있었던 전체적으로 복원 됩니다. 예를 들어, 사용자 복원 된 계정 모든 그룹 구성원 및 전과 바로 삭제, 도메인 및 내에서 해당 액세스 권한을 자동으로 다시. AD DS 및 광고 LDS 환경에 대 한 active Directory 휴지통 작동합니다. Active Directory 휴지통의 자세한 내용은 참조 [AD DS의 새로운: Active Directory 휴지통](https://technet.microsoft.com/library/dd391916(WS.10).aspx)합니다.

**새 소식** Windows Server 2012에서 관리 및 삭제 개체 복원 하는 사용자를 위한 그래픽 사용자 인터페이스를 새로 된 Active Directory 휴지통 기능이 향상 되었습니다. 사용자가 수 이제 시각 목록을 삭제 개체의 찾아서 또는 원하는 원래 위치로 복원 합니다.

Active Directory 휴지통 Windows Server 2012에서 사용 하려는 경우 다음을 고려 합니다.

-   기본적으로 Active Directory 휴지통 사용할 수 없습니다. 을 사용 하려면 먼저 Windows Server 2008 R2 이상 AD DS 또는 광고 LDS 환경을 숲 기능 수준의 올린 해야 합니다. 이 요구가 있는 숲 속의 모든 도메인 컨트롤러 나 광고 LDS 구성 집합 인스턴스 개최 된 모든 서버 되는 Windows Server 2008 R2 실행 이상 합니다.

-   Active Directory 휴지통을 활성화 하는 과정은 되돌릴 수 없습니다. 사용자 환경에서 Active Directory 휴지통을 설정한 후에 비활성화할 수 없습니다.

-   휴지통 사용자 인터페이스를 통해이 기능을 관리 하려면 Windows Server 2012에서 Active Directory 관리 센터의 버전을 설치 해야 합니다.

    > [!NOTE]
    > 사용할 수 있는 **서버 관리자** 원격 서버 관리 도구 RSAT ()을 사용 하는 올바른 버전 Active Directory 관리 센터의 관리 휴지통 사용자 인터페이스를 통해 Windows Server 2012 컴퓨터에 설치 해야 합니다.
    > 
    > 사용할 수 있는 [RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) windows&reg; 8 컴퓨터를 사용 하 여 올바른 버전 Active Directory 관리 센터의 사용자 인터페이스를 통해 휴지통을 관리 합니다.

### <a name="active-directory-recycle-bin-step-by-step"></a>Active Directory 휴지통 단계별
다음 단계를 Windows Server 2012에서 다음과 같은 Active Directory 휴지통 작업을 수행 ADAC를 사용 합니다.

-   [1 단계: 숲 기능 수준 높이기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)

-   [2 단계: 사용 휴지통](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)

-   [3 단계: 테스트 사용자, 그룹과 조직 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)

-   [4 단계: 복원 개체 삭제](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> 엔터프라이즈 관리자 그룹 또는 해당 사용 권한을 구성원은 다음 단계를 수행 해야 합니다.

### <a name="bkmk_raise_ffl"></a>1 단계: 숲 기능 수준 높이기
이 단계에서 숲 기능 수준을 발생 합니다. 먼저 Active Directory 휴지통을 사용 하기 전에 Windows Server 2008 R2 최소한 되도록 대상 숲 속의 기능 수준을 올린 해야 합니다.

##### <a name="to-raise-the-functional-level-on-the-target-forest"></a>대상 숲 속의 기능 수준을 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  왼쪽된 탐색 창와 대상 도메인 클릭는 **작업** 창 클릭 **숲 기능 수준을**합니다. 최소 숲 기능 수준을 선택 Windows Server 2008 R2 이상 차례로 클릭 하 고 **확인**합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

에 대 한는 **-신원을** 인수 정식된 DNS 이름을 지정 합니다.

### <a name="bkmk_enable_recycle_bin"></a>2 단계: 사용 휴지통
이 단계를 삭제 복원 개체 AD DS에 휴지통에 수 있게 합니다.

##### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>Active Directory 휴지통 ADAC 대상 도메인에에서 사용 하도록 설정 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  에 **작업** 창 클릭 **휴지통 활성화... **에 **작업** 창 클릭 **확인** 클릭 경고 메시지 상자에서 **확인** 새로 고침 ADAC 메시지에 있습니다.

4.  F5 ADAC 새로 고침을 합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>3 단계: 테스트 사용자, 그룹과 조직 만들기
다음 절차에서는 두 개의 테스트 사용자 만듭니다. 그런 다음 테스트 그룹을 만들 하 고 테스트 사용자 그룹에 추가 됩니다. OU 만들어집니다.

##### <a name="to-create-test-users"></a>테스트 사용자를 만들려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  에 **작업** 창 클릭 **새로** 차례로 클릭 하 고 **사용자**합니다.

    ![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4.  아래에서 다음 정보를 입력 **계정** 한 다음 확인을 클릭 합니다.

    -   전체 이름: test1

    -   사용자 SamAccountName 로그온: test1

    -   암호:p@ssword1

    -   암호를 확인 합니다.p@ssword1

5.  두 번째 사용자 test2 만드는 데 위 단계를 반복 합니다.

##### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>테스트 그룹을 만들고 그룹에 사용자를 추가 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  에 **작업** 창 클릭 **새로** 차례로 클릭 하 고 **그룹**합니다.

4.  아래에서 다음 정보를 입력 **그룹** 차례로 클릭 하 고 **확인**:

    -   **그룹 이름: 그룹 1**

5.  클릭 **그룹 1**를 선택한 다음는 **작업** 창 클릭 **속성**합니다.

6.  클릭 **회원**, 클릭 **추가**, 입력 **test1; test2**을 차례로 클릭 하 고 **확인**합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Add-ADGroupMember -Identity group1 -Member test1
```

##### <a name="to-create-an-organizational-unit"></a>조직 만들려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  에 **작업** 창 클릭 **새로** 차례로 클릭 하 고 **조직**합니다.

4.  아래에서 다음 정보를 입력 **조직** 차례로 클릭 하 고 **확인**:

    -   **NameOU1**

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"

```

### <a name="bkmk_restore_del_obj"></a>4 단계: 복원 개체 삭제
다음 절차에서는 삭제 개체 복원 됩니다는 **삭제 개체** 컨테이너 원래 위치에와 다른 위치에 있습니다.

##### <a name="to-restore-deleted-objects-to-their-original-location"></a>삭제 된 개체 원래 위치에 복원 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  사용자가 선택 **test1** 및 **test2**, 클릭 **삭제** 에 **작업** 창과 클릭 **예** 삭제할지 합니다.

    ![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

    다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

    ```
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4.  로 이동는 **삭제 개체** 컨테이너, **test2** 및 **test1** 차례로 클릭 하 고 **복원** 에 **작업** 창 합니다.

5.  원래 위치로 복원 된 개체를 확인 하려면 대상 도메인으로 이동 하 고 사용자 계정이 나열 되어 확인 합니다.

    > [!NOTE]
    > 으로 이동 하는 경우는 **속성** 의 사용자 계정 **test1** 및 **test2** 차례로 클릭 하 고 **소속**, 그룹 구성원 복원도 표시 됩니다.

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

##### <a name="to-restore-deleted-objects-to-a-different-location"></a>삭제 된 개체 다른 위치에 복원 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  사용자가 선택 **test1** 및 **test2**, 클릭 **삭제** 에 **작업** 창과 클릭 **예** 삭제할지 합니다.

4.  로 이동는 **삭제 개체** 컨테이너, **test2** 및 **test1** 차례로 클릭 하 고 **복원** 에 **작업** 창 합니다.

5.  선택 **o u 1** 차례로 클릭 하 고 **확인**합니다.

6.  개체 것인지를 복원 된 **o u 1**대상 도메인 탐색을 두 번 클릭, **o u 1** 사용자 계정이 나열 되어 있는지 확인 합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>정교한 암호 정책
Windows Server 2008 운영 체제에는 조직 도메인의 서로 다른 암호 및 사용자의 다른 세트에 대 한 계정 잠금 정책을 정의 하는 방법 제공 합니다. Windows Server 2008 전에 Active Directory 도메인 하나만 암호 정책 및 계정 잠금 정책 수 도메인에 있는 모든 사용자에 게 적용 됩니다. 이 정책 도메인에 대 한 기본 도메인 정책에 지정 된 합니다. 결과적으로, 사용자의 다른 세트에 대 한 다른 암호 및 계정 잠금 설정 원하는 조직 암호 필터 만들기 또는 여러 도메인 배포 했습니다. 모두 비용이 옵션입니다.

정교한 암호 정책을 단일 도메인에서 암호 정책을 여러 지정 하 고 계정 및 암호 잠금 정책에 대 한 다른 제한 도메인에 있는 사용자의 다른 세트에 적용를 사용할 수 있습니다. 예를 들어, 엄격한 권한이 있는 계정 설정 및 덜 무과실 설정 다른 사용자 계정에 적용할 수 있습니다. 그 외의 경우 암호는 다른 데이터 소스와 동기화 되므로 계정에 대 한 특수 암호 정책을 적용 좋습니다. 세분화 암호 정책에 대 한 자세한 내용은, 참조 [AD DS: 세분화 암호 정책](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**새 소식** Windows Server 2012에서 세밀 암호 정책 관리 제조 쉽고 더 스마트 AD DS 관리자 ADAC에 관리 하는 사용자 인터페이스를 제공 하 여 합니다. 관리자 수 이제 정책 결과 특정된 사용자의, 보기 및 특정된 도메인에서 암호 정책을 모든 정렬 및 관리 개별 암호 정책을 시각 합니다.

Windows Server 2012에서 세밀 암호 정책을 사용 하려는 경우 다음 고려해 야 합니다.

-   정교한 암호 정책이 적용만 글로벌 보안 그룹 하 고 사용자 개체 (또는 inetOrgPerson 개체 사용자 개체 대신 사용 하는 경우). 기본적으로 도메인 관리자 그룹의 회원만 세밀 암호 정책을 설정할 수 있습니다. 그러나 이러한 정책을 다른 사용자에 게 설정 하는 기능을 위임 수도 있습니다. 도메인 기능 수준 Windows Server 2008 이상 이어야 합니다.

-   그래픽 사용자 인터페이스를 통해 정책 세부적으로 암호를 관리할 수의 Active Directory 관리 센터 Windows Server 2012 버전을 사용 해야 합니다.

    > [!NOTE]
    > 사용할 수 있는 **서버 관리자** 원격 서버 관리 도구 RSAT ()을 사용 하는 올바른 버전 Active Directory 관리 센터의 관리 휴지통 사용자 인터페이스를 통해 Windows Server 2012 컴퓨터에 설치 해야 합니다.
    > 
    > 사용할 수 있는 [RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) windows&reg; 8 컴퓨터를 사용 하 여 올바른 버전 Active Directory 관리 센터의 사용자 인터페이스를 통해 휴지통을 관리 합니다.

### <a name="fine-grained-password-policy-step-by-step"></a>단계별 세밀 암호 정책
다음 단계에 다음 세밀 암호 정책 작업을 수행할 ADAC 사용 합니다.

-   [1 단계: 도메인 기능 수준 높이기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)

-   [2 단계: 테스트 사용자, 그룹과 조직 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)

-   [3 단계: 세밀 암호 정책을 새로 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

-   [4 단계: 사용자에 대 한 정책 집합을 결과 보기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)

-   [5 단계: 세밀 암호 정책을 편집합니다](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)

-   [6 단계: 세밀 암호 정책 삭제](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> 해당 사용 권한을 도메인 관리자 하나 또는 여러 개의의 회원은 다음 단계를 수행 해야 합니다.

#### <a name="bkmk_raise_dfl"></a>1 단계: 도메인 기능 수준 높이기
다음 절차에 Windows Server 2008 이상 대상 도메인 기능 도메인 수준을 발생 합니다. 정교한 암호 정책을 사용 하도록 도메인 기능 수준 Windows Server 2008 이상이 필요 합니다.

###### <a name="to-raise-the-domain-functional-level"></a>도메인 기능 수준을 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  왼쪽된 탐색 창와 대상 도메인 클릭는 **작업** 창 클릭 **도메인 기능 수준을**합니다. 최소 숲 기능 수준을 선택 클릭 하 고 Windows Server 2008 이상의 **확인**합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>2 단계: 테스트 사용자, 그룹과 조직 만들기
테스트 사용자를 만들고이 단계에 대 한 필요성을 그룹화 하 이곳에 절차에 따라: [3 단계: 테스트 사용자, 그룹 조직 만들](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env) (하면 필요 하지 않은 세밀 암호 정책을 설명 하기 위해 OU 만드는).

#### <a name="bkmk_create_fgpp"></a>3 단계: 세밀 암호 정책을 새로 만들기
다음 절차에 새 세밀 암호 정책을 ADAC에서 UI를 사용 하 여 만들어집니다.

###### <a name="to-create-a-new-fine-grained-password-policy"></a>새 미세한 암호 정책을 만들려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  ADAC 탐색 창에서 엽니다는 **시스템** 컨테이너 및 클릭 **암호 설정 컨테이너**합니다.

4.  에 **작업** 창 클릭 **새로**을 차례로 클릭 하 고 **암호 설정**합니다.

    입력 하거나 속성 페이지를 새로 만드는 내 필드 편집 **암호 설정** 개체 합니다. **이름** 및 **우선 순위** 필드는 필요 합니다.

    ![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5.  아래에서 **직접에 적용 됩니다.**, 클릭 **추가**, 입력 **그룹 1**을 차례로 클릭 하 고 **확인**합니다.

    이 암호 정책 개체 테스트 환경에 대 한 만든 글로벌 그룹의 회원 들과 연결 됩니다.

6.  클릭 **확인** 를 전송 합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>4 단계: 사용자에 대 한 정책 집합을 결과 보기
다음 절차에 미세한 암호 정책 할당 그룹 구성원 사용자에 대 한 결과 암호 설정 볼 [3 단계: 세밀 암호 정책 새로 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)합니다.

###### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>결과 사용자에 대 한 정책 집합을 보려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  사용자를 선택 **test1** 그룹에 속하는 **그룹 1** 내 세밀 암호 정책 연결한 [3 단계: 세밀 암호 정책 새로 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)합니다.

4.  클릭 **결과 암호 설정 보기** 에 **작업** 창 합니다.

5.  암호 설정 정책을 검토 하 고 클릭 한 다음 **취소**합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>5 단계: 세밀 암호 정책을 편집합니다
다음 절차에에서 만든 미세한 암호 정책을 편집는 [3 단계: 세밀 암호 정책 새로 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

###### <a name="to-edit-a-fine-grained-password-policy"></a>정교한 암호 정책을 편집 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  에 ADAC **탐색 창**, 확장 **시스템** 차례로 클릭 하 고 **암호 설정 컨테이너**합니다.

4.  만든 미세한 암호 정책을 선택 [3 단계: 세밀 암호 정책 새로 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) 클릭 **속성** 에 **작업** 창 합니다.

5.  아래에서 **최근 암호 기억**을 변경 하는 가치에 **암호를 기억할 수** 에 **30**합니다.

6.  클릭 **확인**합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>6 단계: 세밀 암호 정책 삭제

###### <a name="to-delete-a-fine-grained-password-policy"></a>정교한 암호 정책을 삭제 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  ADAC 탐색 창에서 확장 **시스템** 차례로 클릭 하 고 **암호 설정 컨테이너**합니다.

4.  만든 미세한 암호 정책을 선택 [3 단계: 세밀 암호 정책 새로 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) 의 **작업** 창 클릭 **속성**합니다.

5.  지우기는 **실수로 삭제 되지 않도록에서 보호** 확인란을 클릭 하 고 **확인**합니다.

6.  선택 미세한 암호 정책을는 **작업** 창 클릭 **삭제**합니다.

7.  클릭 **확인** 확인 대화 합니다.

![광고 관리 센터를 소개](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 또는 cmdlet 이전 절차와 같은 기능을 수행 합니다. 하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 각 cmdlet 한 줄에 입력 합니다.

```
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Windows PowerShell 기록 뷰어
ADAC는 Windows PowerShell를 기반으로 빌드된 사용자 인터페이스 도구입니다.  IT 관리자는 Windows Server 2012에서 Windows PowerShell 기록 뷰어를 사용 하 여 Windows PowerShell cmdlet Active Directory에 대 한 자세한 내용은 ADAC 활용할 수 있습니다. 작업이 실행 사용자 인터페이스에서 Windows PowerShell 기록 뷰어에서 사용자에 게 해당 하는 Windows PowerShell 명령 표시 됩니다. 관리자를 자동화 된 스크립트 만들고 따라서 IT 생산성 향상 반복 되는 작업을 줄일 수 있습니다.  또한,이 기능은 Windows PowerShell Active Directory에 대 한 자세한 내용은 시간을 줄입니다 하 고 자녀가 자동화 스크립트 정확성에서 사용자의 향상 합니다.

Windows Server 2012에서 Windows PowerShell 기록 뷰어를 사용 하는 경우 다음을 고려 합니다.

-   ADAC의 Windows Server 2012 버전을 사용 해야 Windows PowerShell 스크립트 뷰어를 사용 하려면

    > [!NOTE]
    > 사용할 수 있는 **서버 관리자** 원격 서버 관리 도구 RSAT ()을 사용 하는 올바른 버전 Active Directory 관리 센터의 관리 휴지통 사용자 인터페이스를 통해 Windows Server 2012 컴퓨터에 설치 해야 합니다.
    > 
    > 사용할 수 있는 [RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) windows&reg; 8 컴퓨터를 사용 하 여 올바른 버전 Active Directory 관리 센터의 사용자 인터페이스를 통해 휴지통을 관리 합니다.

-   일부 기본적인 Windows PowerShell 기술을 했습니다. 예를 들어,에서 Windows PowerShell 파이핑 모드가 작동 하는지 해야 할 수도 있습니다. Windows PowerShell 파이핑에 대 한 자세한 내용은 참조 [파이핑 및에서 Windows PowerShell 파이프라인](https://technet.microsoft.com/library/ee176927.aspx)합니다.

### <a name="windows-powershell-history-viewer-step-by-step"></a>Windows PowerShell 단계별 기록 뷰어
다음 절차에 ADAC Windows PowerShell 기록 뷰어를 사용 하 여 Windows PowerShell 스크립트를 생성 하는 합니다.  이 절차를 시작 하기 전에 사용자, 제거 **test1** 그룹에서 **그룹 1**합니다.

##### <a name="to-construct-a-script-using-powershell-history-viewer"></a>PowerShell 기록 뷰어를 사용 하 여 스크립트 생성 하려면

1.  마우스 오른쪽 단추로 클릭 Windows PowerShell 아이콘을 클릭 **관리자 권한으로 실행** 입력 **dsac.exe** 를 ADAC 엽니다.

2.  클릭 **관리**, 클릭 **탐색 노드 추가** 에서 적절 한 목표 도메인을 선택 하 고 있는 **탐색 노드 추가** 대화 상자를 클릭 한 다음 **확인**합니다.

3.  확장은 **Windows PowerShell 기록** 창 ADAC 화면 맨 아래에 있습니다.

4.  선택 하 고 사용자 **test1**합니다.

5.  클릭 **그룹에 추가... **에 **작업** 창 합니다.

6.  로 이동 **그룹 1** 클릭 **확인** 대화 상자에서 합니다.

7.  로 이동는 **Windows PowerShell 기록** 창 생성 하면 명령 찾습니다.

8.  명령 복사한 스크립트 생성 하 여 원하는 편집기에 붙여 넣습니다.

    예를 들어, 명령에 다른 사용자 추가를 수정할 수 있습니다 **그룹 1**, 추가 또는 **test1** 다른 그룹입니다.

## <a name="see-also"></a>참조 하십시오
[관리 센터 Active Directory & #40;를 사용 하 여 고급 AD DS 관리 200 수준 & #41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)


