---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: Introduction to Active Directory Administrative Center Enhancements (Level 100)
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a3bd82feb3a0caf827091bd0cb10edf991921b3c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390618"
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Introduction to Active Directory Administrative Center Enhancements (Level 100)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server의 Active Directory 관리 센터에는 다음에 대 한 관리 기능이 포함 되어 있습니다.

- [Active Directory 휴지통](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)
- [세분화 되는 암호 정책](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)
- [Windows PowerShell 기록 뷰어](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Active Directory 휴지통

AD DS(Active Directory Domain Services) 및 AD LDS(Active Directory Lightweight Directory Services) 사용자는 실수로 Active Directory 개체를 삭제하는 경우가 종종 있습니다. 이전 버전의 Windows Server 2008 R2 이전 Windows Server를 복구할 수 Active Directory에서 실수로 삭제 된 개체 있었지만 해결 방법에 단점이 있습니다.

Windows Server 2008에서는 Windows Server 백업 기능 및 **ntdsutil** 정식 복원 명령을 사용하여 개체를 정식 복원 대상으로 표시함으로써 복원된 데이터가 도메인 전체에 복제되었는지 확인할 수 있습니다. 정식 복원 솔루션은 DSRM(디렉터리 서비스 복원 모드)에서 수행해야 한다는 단점이 있습니다. DSRM에서는 복원 중인 도메인 컨트롤러가 오프라인 상태를 유지해야 합니다. 따라서 클라이언트 요청을 처리할 수 없습니다.

Windows Server 2003 Active Directory 및 Windows Server 2008 AD DS에서는 삭제 표시 다시 애니메이션 명령을 통해 삭제된 Active Directory 개체를 복구할 수 있습니다. 하지만 물리적으로 제거된 다시 애니메이션된 개체의 연결된 값 특성(예: 사용자 계정의 그룹 구성원) 및 연결되어 있지 않아서 지워진 값 특성은 복구되지 않습니다. 따라서 삭제 표시 다시 애니메이션 명령은 실수로 삭제된 개체에 대한 궁극적인 해결 방안이 되지는 못합니다. 삭제 표식 다시 애니메이션에 대한 자세한 내용은 [Active Directory 삭제 표식 개체 다시 애니메이션](https://go.microsoft.com/fwlink/?LinkID=125452)을 참조하세요.

Windows Server 2008 R2부터 Active Directory 휴지통이 기존의 삭제 표시 다시 애니메이션 인프라에 구축되어 실수로 삭제된 Active Directory 개체를 유지하고 복구하는 기능이 개선됩니다.

Active Directory 휴지통을 사용할 경우 삭제된 Active Directory 개체의 모든 연결된 값 특성과 연결되지 않은 값 특성이 유지되고, 개체는 삭제 바로 전과 동일하게 일관된 논리적인 상태로 복원됩니다. 예를 들어 복원된 사용자 계정은 삭제 바로 전에 도메인에서 갖고 있었던 모든 그룹 구성원 자격과 해당하는 액세스 권한을 자동으로 다시 얻게 됩니다. Active Directory 휴지통은 AD DS 및 AD LDS 환경에서 모두 작동합니다. 참조에 대 한 자세한 설명은 Active Directory 휴지통, [는 AD DS의 새로운 기능: Active Directory 휴지통](https://technet.microsoft.com/library/dd391916(WS.10).aspx)합니다.

**새로운 기능** Windows Server 2012 이상 버전에서는 사용자가 삭제 된 개체를 관리 하 고 복원할 수 있는 새로운 그래픽 사용자 인터페이스를 사용 하 여 Active Directory 휴지통 기능이 향상 되었습니다. 이제 사용자는 삭제된 개체 목록을 시각적으로 찾아 원래 위치나 원하는 위치에 복원할 수 있습니다.

Windows Server에서 Active Directory 휴지통을 사용 하도록 설정 하려는 경우 다음 사항을 고려 하세요.

- 기본적으로 Active Directory 휴지통은 사용할 수 없도록 설정됩니다. 이 기능을 사용 하려면 먼저 AD DS 또는 AD LDS 환경의 포리스트 기능 수준을 Windows Server 2008 R2 이상으로 올려야 합니다. 이렇게 하려면 포리스트의 모든 도메인 컨트롤러 또는 AD LDS 구성 집합의 인스턴스를 호스트 하는 모든 서버에서 Windows Server 2008 R2 이상을 실행 해야 합니다.
- Active Directory 휴지통을 사용하도록 설정하는 프로세스는 되돌릴 수 없습니다. 즉, 사용자 환경에서 Active Directory 휴지통을 사용하도록 설정하고 나면 다시 사용하지 않도록 설정을 되돌릴 수 없습니다.
- 사용자 인터페이스를 통해 휴지통 기능을 관리 하려면 Windows Server 2012에 Active Directory 관리 센터 버전을 설치 해야 합니다.

    > [!NOTE]
    > **서버 관리자** 를 사용 하 원격 서버 관리 도구 (RSAT)를 설치 하 여 올바른 버전의 Active Directory 관리 센터를 사용 하 여 사용자 인터페이스를 통해 휴지통을 관리할 수 있습니다.
    >
    > RSAT를 설치 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)문서를 참조 하세요.

### <a name="active-directory-recycle-bin-step-by-step"></a>Active Directory 휴지통 단계별 가이드

다음 단계에서는 Windows Server 2012에서 다음과 같은 Active Directory 휴지통 작업을 수행 하려면 ADAC를 사용 합니다.

- [1 단계: 포리스트 기능 수준 올리기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)
- [2 단계: 휴지통 사용](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)
- [3 단계: 테스트 사용자, 그룹 및 조직 구성 단위 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)
- [4 단계: 삭제 된 개체 복원](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> 다음 단계를 수행하려면 Enterprise Admins 그룹의 구성원이거나 이와 동등한 권한이 있어야 합니다.

### <a name="bkmk_raise_ffl"></a>1 단계: 포리스트 기능 수준 올리기

이 단계에서는 포리스트 기능 수준을 올립니다. 먼저 Active Directory 휴지통을 활성화 하기 전에 최소한 Windows Server 2008 r 2를 대상 포리스트의 기능 수준을 올려야 합니다.

#### <a name="to-raise-the-functional-level-on-the-target-forest"></a>대상 포리스트의 기능 수준을 올리려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. 왼쪽 탐색 창에서 대상 도메인을 클릭하고 **작업** 창에서 **포리스트 기능 수준 올리기**를 클릭합니다. 이상의 포리스트 기능 수준 선택 Windows Server 2008 R2 이상 클릭 하 고 **확인**합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

**-Identity** 인수에 대해 정규화 된 DNS 도메인 이름을 지정 합니다.

### <a name="bkmk_enable_recycle_bin"></a>2 단계: 휴지통 사용

이 단계에서는 휴지통을 사용하도록 설정하여 AD DS에서 삭제된 개체를 복원합니다.

#### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>대상 도메인의 ADAC에서 Active Directory 휴지통을 사용하도록 설정하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. **작업** 창에서, **작업** 창의 **휴지통 사용...** 을 클릭하고 경고 메시지 상자에서 **확인**을 클릭한 후 다시 **확인**을 클릭하여 ADAC 메시지를 새로 고칩니다.

4. F5 키를 눌러 ADAC를 새로 고칩니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>3 단계: 테스트 사용자, 그룹 및 조직 구성 단위 만들기

다음 절차에서는 두 명의 테스트 사용자를 만듭니다. 그런 다음 테스트 그룹을 만들어 테스트 사용자를 이 그룹에 추가합니다. 또한 OU도 만듭니다.

#### <a name="to-create-test-users"></a>테스트 사용자를 만들려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. **작업** 창에서 **새로 만들기** 를 클릭한 다음, **사용자**를 클릭합니다.

    ![AD 관리 센터 소개 (영문)](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4. **계정**에 다음 정보를 입력한 후 [확인]을 클릭합니다.

   - 전체 이름: test1
   - 사용자 SamAccountName 로그온: test1
   - 암호: p@ssword1
   - 암호 확인: p@ssword1

5. 이전 단계를 반복하여 두 번째 사용자, test2를 만듭니다.

#### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>테스트 그룹을 만들어 사용자를 이 그룹에 추가하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.
2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.
3. **작업** 창에서 **새로 만들기**를 클릭한 다음, **그룹**을 클릭합니다.
4. **그룹**에 다음 정보를 입력한 후 **확인**을 클릭합니다.

    -   **그룹 이름: group1**

5. **group1**을 클릭하고 **작업** 창 아래에서 **속성**을 클릭합니다.
6. **구성원**을 클릭하고 **추가**를 클릭한 후 **test1;test2**를 입력하고 **확인**을 클릭합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Add-ADGroupMember -Identity group1 -Member test1
```

#### <a name="to-create-an-organizational-unit"></a>조직 구성 단위를 만들려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.
2. **관리**, **탐색 노드 추가** 를 차례로 클릭 하 고 **탐색 노드 추가** 대화 상자에서 적절 한 대상 도메인을 선택한 다음 * * 확인을 클릭 합니다.
3. **작업** 창에서 **새로 만들기** 를 클릭한 다음 **조직 구성 단위**를 클릭합니다.
4. **조직 구성 단위**에 다음 정보를 입력한 후 **확인**을 클릭합니다.

   - **NameOU1**

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"
```

### <a name="bkmk_restore_del_obj"></a>4 단계: 삭제 된 개체 복원

다음 절차에서는 삭제된 개체를 **Deleted Objects** 컨테이너에서 원래 위치 및 다른 위치로 복원합니다.

#### <a name="to-restore-deleted-objects-to-their-original-location"></a>삭제된 개체를 원래 위치로 복원하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. 사용자 **test1** 및 **test2**를 선택하고 **작업** 창에서 **삭제** 를 클릭한 후 **예** 를 클릭하여 삭제를 확인합니다.

    ![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

    다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

    ```powershell
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4. **Deleted Objects** 컨테이너로 이동한 후 **test2** , **test1** 을 선택하고 **작업** 창에서 **복원** 을 클릭합니다.

5. 개체가 원래 위치로 복원되었는지 확인하려면 대상 도메인으로 이동한 후 사용자 계정이 표시되는지 확인합니다.

    > [!NOTE]
    > 사용자 계정 **test1** , **test2** 의 **속성** 으로 이동한 후 **소속 그룹**을 클릭하면 해당 그룹의 구성원도 복원되었음을 확인할 수 있습니다.

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

#### <a name="to-restore-deleted-objects-to-a-different-location"></a>삭제된 개체를 다른 위치로 복원하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. 사용자 **test1** 및 **test2**를 선택하고 **작업** 창에서 **삭제** 를 클릭한 후 **예** 를 클릭하여 삭제를 확인합니다.

4. **Deleted Objects** 컨테이너로 이동한 후 **test2** , **test1** 을 선택하고 **작업** 창에서 **복원 위치** 를 클릭합니다.

5. **OU1**을 선택한 후 **확인**을 클릭합니다.

6. 개체가 **OU1**으로 복원되었는지 확인하려면 대상 도메인으로 이동한 후 **OU1**을 두 번 클릭하고 사용자 계정이 표시되는지 확인합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>세분화 되는 암호 정책

Windows Server 2008 운영 체제는 도메인의 각 사용자 집합에 대해 서로 다른 암호 및 계정 잠금 정책을 정의하는 방법을 조직에 제공합니다. Windows Server 2008 이전의 Active Directory 도메인에서는 하나의 암호 정책과 계정 잠금 정책만 도메인의 모든 사용자에 적용할 수 있었습니다. 이러한 정책은 도메인의 Default Domain Policy에서 지정되었습니다. 따라서 각 사용자 집합에 대해 다른 암호 및 계정 잠금 설정을 지정하려는 조직은 암호 필터를 만들거나 여러 도메인을 배포해야 했습니다. 두 옵션은 서로 다른 이유로 많은 비용이 필요합니다.

세분화된 암호 정책을 사용하여 단일 도메인 내 여러 암호 정책을 지정하고 도메인의 각 사용자 집합에 서로 다른 암호 및 계정 잠금 정책 제한을 적용할 수 있습니다. 예를 들어 더 엄격한 설정을 권한 있는 계정에 적용하고 덜 엄격한 설정을 다른 사용자 계정에 적용할 수 있습니다. 경우에 따라 암호가 다른 데이터 원본과 동기화되는 계정에 대해 특별한 암호 정책을 적용할 수도 있습니다. 참조에 대 한 자세한 설명은 세분화 된 암호 정책, [AD DS: 세분화 된 암호 정책](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**새로운 기능**

Windows Server 2012 이상에서 세분화 된 암호 정책 관리는 AD DS 관리자가 ADAC에서 관리 하는 데 사용할 수 있는 사용자 인터페이스를 제공 하 여 더 쉽고 시각적으로 이루어집니다. 관리자 수 이제 지정된 된 사용자의 정책 결과 보기 및 지정된 된 도메인 내에서 모든 암호 정책을 정렬할 고 보고 관리할 각 암호 정책을 시각적으로.

Windows Server 2012에서 세분화 된 암호 정책을 사용 하려는 경우 다음 사항을 고려 하세요.

- 세분화 된 암호 정책은 전역 보안 그룹 및 사용자 개체 (또는 사용자 개체 대신 사용 되는 경우 inetOrgPerson 개체)에만 적용 됩니다. 기본적으로 Domain Admins 그룹의 구성원만 세분화된 암호 정책을 설정할 수 있습니다. 그러나 이러한 정책을 설정하는 기능을 다른 사용자에게 위임할 수도 있습니다. 도메인 기능 수준은 Windows Server 2008 이상 버전이어야 합니다.

- 그래픽 사용자 인터페이스를 통해 세분화 된 암호 정책을 관리 하려면 Windows Server 2012 이상 버전의 Active Directory 관리 센터를 사용 해야 합니다.

    > [!NOTE]
    > **서버 관리자** 를 사용 하 원격 서버 관리 도구 (RSAT)를 설치 하 여 올바른 버전의 Active Directory 관리 센터를 사용 하 여 사용자 인터페이스를 통해 휴지통을 관리할 수 있습니다.
    >
    > RSAT를 설치 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)문서를 참조 하세요.

### <a name="fine-grained-password-policy-step-by-step"></a>세분화된 암호 정책 단계별 가이드

다음 단계에서는 ADAC를 사용하여 다음과 같은 세분화된 암호 정책 작업을 수행합니다.

- [1 단계: 도메인 기능 수준 올리기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)
- [2 단계: 테스트 사용자, 그룹 및 조직 구성 단위 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)
- [3 단계: 새 세분화 된 암호 정책 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)
- [4 단계: 사용자의 정책 결과 집합 보기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)
- [5 단계: 세분화 된 암호 정책 편집](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)
- [6 단계: 세분화 된 암호 정책 삭제](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> 다음 단계를 수행하려면 Domain Admins 그룹의 구성원이거나 이와 동등한 권한이 있어야 합니다.

#### <a name="bkmk_raise_dfl"></a>1 단계: 도메인 기능 수준 올리기

다음 절차에서는 Windows Server 2008로 또는 그 이상 대상 도메인의 도메인 기능 수준을 올립니다. 도메인 기능 수준은 Windows Server 2008 이상는 세분화 된 암호 정책을 사용 하도록 설정 해야 합니다.

##### <a name="to-raise-the-domain-functional-level"></a>도메인 기능 수준을 올리려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. 왼쪽 탐색 창에서 대상 도메인을 클릭하고 **작업** 창에서 **도메인 기능 수준 올리기**를 클릭합니다. 이상의 포리스트 기능 수준 선택 하 고 클릭 한 다음 Windows Server 2008 이상 **확인**합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>2 단계: 테스트 사용자, 그룹 및 조직 구성 단위 만들기

이 단계에 필요한 테스트 사용자 및 그룹을 만들려면 다음 단계를 따르세요. [3 단계: 테스트 사용자, 그룹 및 조직 구성 단위 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env) (세분화 된 암호 정책을 보여 주기 위해 OU를 만들 필요는 없음).

#### <a name="bkmk_create_fgpp"></a>3 단계: 새 세분화 된 암호 정책 만들기

다음 절차에서는 ADAC의 UI를 사용하여 새 세분화된 암호 정책을 만듭니다.

##### <a name="to-create-a-new-fine-grained-password-policy"></a>새 세분화된 암호 정책을 만들려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. ADAC 탐색 창에서 **System** 컨테이너를 연 후 **Password Settings Container**를 클릭합니다.

4. **작업** 창에서 **새로 만들기**를 클릭한 다음 **암호 설정**을 클릭합니다.

    속성 페이지의 필드에 내용을 입력하거나 필드를 편집하여 새 **암호 설정** 개체를 만듭니다. **이름** 및 **우선 순위** 필드는 필수입니다.

    ![AD 관리 센터 소개 (영문)](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5. 아래에서 **직접에 적용 됩니다.** , 클릭 **추가**, 형식 **group1**, 를 클릭 하 고 **확인**합니다.

    그러면 테스트 환경에 대해 만든 글로벌 그룹의 구성원과 암호 정책 개체가 연결됩니다.

6. **확인** 을 클릭하여 만든 세분화된 암호 정책을 제출합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>4 단계: 사용자의 정책 결과 집합 보기

다음 절차에서는 [Step 3: Create a new fine-grained password policy](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)에서 세분화된 암호 정책을 할당한 그룹 구성원인 사용자에 대한 결과 암호 설정을 봅니다.

##### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>사용자의 정책 결과 집합을 보려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. **3단계: 새 세분화된 암호 정책 만들기**에서 세분화된 암호 정책과 연결한 그룹 **group1**에 속한 사용자 [test1](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)을 선택합니다.

4. **작업** 창에서 **결과 암호 설정 보기**를 클릭합니다.

5. 암호 설정 정책을 확인한 후 **취소**를 클릭합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>5 단계: 세분화 된 암호 정책 편집

다음 절차에서는 [3단계: 새 세분화된 암호 정책 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)에서 만든 세분화된 암호 정책을 편집합니다.

##### <a name="to-edit-a-fine-grained-password-policy"></a>세분화된 암호 정책을 편집하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. ADAC **탐색 창**에서 **시스템** 을 확장한 후 **암호 설정 컨테이너**를 클릭합니다.

4. [Step 3: Create a new fine-grained password policy](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) 에서 만든 세분화된 암호 정책을 선택한 후 **작업** 창에서 **속성** 을 클릭합니다.

5. **최근 암호 기억**에서 **기억할 암호 수**의 값을 **30**으로 변경합니다.

6. **확인**을 클릭합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>6 단계: 세분화 된 암호 정책 삭제

##### <a name="to-delete-a-fine-grained-password-policy"></a>세분화된 암호 정책을 삭제하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. ADAC 탐색 창에서 **System** 을 확장한 후 **Password Settings Container**를 클릭합니다.

4. [3단계: 새 세분화된 암호 정책 만들기](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)에서 만든 세분환된 암호 정책을 선택한 후 **작업** 창에서 **속성**을 클릭합니다.

5. **실수로 삭제되지 않도록 보호** 확인란의을 선택을 취소하고 **확인**을 클릭합니다.

6. 세분화된 암호 정책을 선택한 후 **작업** 창에서 **삭제**를 클릭합니다.

7. 확인 대화 상자에서 **확인**을 클릭합니다.

![AD 관리 센터](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell 해당 명령</em> 소개***

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

```powershell
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Windows PowerShell 기록 뷰어

ADAC는 Windows PowerShell 위에 구축된 사용자 인터페이스 도구입니다. Windows Server 2012 이상에서 IT 관리자는 ADAC를 활용 하 여 Windows PowerShell 기록 뷰어를 통해 Active Directory cmdlet에 대 한 Windows PowerShell을 익힐 수 있습니다. 동작이 사용자 인터페이스에서 실행될 때 동일한 Windows PowerShell 명령이 Windows PowerShell 기록 뷰어의 사용자에게 표시됩니다. 따라서 관리자는 자동화된 스크립트를 만들고 반복 작업을 줄여 IT 생산성을 높일 수 있습니다. 또한이 기능은 Active Directory에 대 한 Windows PowerShell을 배울 시간이 줄어들고 자동화 스크립트의 정확성에 사용자의 신뢰도 늘어납니다.

Windows Server 2012 이상에서 Windows PowerShell 기록 뷰어를 사용 하는 경우 다음 사항을 고려 하세요.

- Windows PowerShell 스크립트 뷰어를 사용 하려면 Windows Server 2012 또는 최신 버전의 ADAC를 사용 해야 합니다.

    > [!NOTE]
    > **서버 관리자** 를 사용 하 원격 서버 관리 도구 (RSAT)를 설치 하 여 올바른 버전의 Active Directory 관리 센터를 사용 하 여 사용자 인터페이스를 통해 휴지통을 관리할 수 있습니다.
    >
    > RSAT를 설치 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)문서를 참조 하세요.

- Windows PowerShell에 대 한 기본적인 지식이 있어야 합니다. 예를 들어 Windows PowerShell의 파이프가 어떻게 작동하는지 알고 있어야 합니다. Windows PowerShell의 파이프에 대한 자세한 내용은 [Windows PowerShell의 파이프 및 파이프라인](https://technet.microsoft.com/library/ee176927.aspx)을 참조하세요.

### <a name="windows-powershell-history-viewer-step-by-step"></a>Windows PowerShell 기록 뷰어 단계별 가이드

다음 절차에서는 ADAC의 Windows PowerShell 기록 뷰어를 사용하여 Windows PowerShell 스크립트를 작성합니다.  이 절차를 시작하기 전에 그룹 **group1** 에서 사용자 **test1**을 제거합니다.

#### <a name="to-construct-a-script-using-powershell-history-viewer"></a>PowerShell 기록 뷰어를 사용하여 스크립트를 작성하려면

1. Windows PowerShell 아이콘을 마우스 오른쪽 단추로 클릭, 클릭 **관리자 권한으로 실행** 유형과 **dsac.exe** ADAC를 열려면 합니다.

2. **관리**, **탐색 노드 추가** 를 차례로 클릭하고 **탐색 노드 추가** 대화 상자에서 원하는 대상 도메인을 선택한 후 **확인**을 클릭합니다.

3. ADAC 화면 하단에서 **Windows PowerShell 기록** 창을 확장합니다.

4. 사용자 **test1**을 선택합니다.

5. 클릭 **그룹에 추가 …** 에 **작업** 창입니다.

6. **group1**로 이동한 후 대화 상자에서 **확인**을 클릭합니다.

7. **Windows PowerShell 기록** 창으로 이동한 후 방금 생성된 명령을 찾습니다.

8. 명령을 복사하여 원하는 편집기에 붙여넣어 스크립트를 작성합니다.

    예를 들어 명령을 수정하여 다른 사용자를 **group1**에 추가하거나 **test1**을 다른 그룹에 추가할 수 있습니다.

## <a name="see-also"></a>참고 항목

[Active Directory 관리 센터 &#40;수준 200을 사용한 고급 AD DS 관리&#41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)
