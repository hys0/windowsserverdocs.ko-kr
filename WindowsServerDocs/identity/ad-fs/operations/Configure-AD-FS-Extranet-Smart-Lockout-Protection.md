---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS 엑스트라넷 잠금 보호 구성
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 05/20/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 843ed0b3ebf25d662d0b90c17f8fe23548829a7e
ms.sourcegitcommit: 371e59315db0cca5bdb713264a62b215ab43fd0f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82192607"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS 엑스트라넷 잠금 및 엑스트라넷 스마트 잠금

## <a name="overview"></a>개요

ESL (엑스트라넷 스마트 잠금)는 악의적인 활동에서 엑스트라넷 계정 잠금이 발생 하지 않도록 사용자를 보호 합니다.  

ESL를 사용 하면 사용자에 대 한 친숙 한 위치의 로그인 시도와 공격자의 로그인 시도를 구분할 수 AD FS 있습니다. 공격자는 유효한 사용자가 자신의 계정을 계속 사용할 수 있도록 하는 동시에 공격자를 잠글 수 AD FS. 이는 사용자에 대 한 서비스 거부 및 특정 클래스의 암호 스프레이 공격을 방지 하 고 보호 합니다. ESL는 Windows Server 2016에 AD FS 사용할 수 있으며 Windows Server 2019에서 AD FS에 기본 제공 됩니다.

ESL는 엑스트라넷을 통해 웹 응용 프로그램 프록시 또는 타사 프록시와 함께 제공 되는 사용자 이름 및 암호 인증 요청에만 사용할 수 있습니다. 모든 타사 프록시는 웹 응용 프로그램 프록시 대신 사용 되는 웹 응용 프로그램 프록시 (예: [F5 빅 IP 액세스 정책 관리자)](https://devcentral.f5.com/s/articles/ad-fs-proxy-replacement-on-f5-big-ip-30191)에서 사용할 MS ADFSPIP 프로토콜을 지원 해야 합니다. 프록시가 MS ADFSPIP 프로토콜을 지원 하는지 확인 하려면 타사 프록시 설명서를 참조 하세요.   

## <a name="additional-features-in-ad-fs-2019"></a>AD FS 2019의 추가 기능
AD FS 2019의 엑스트라넷 스마트 잠금은 AD FS 2016에 비해 다음과 같은 이점을 추가 합니다.
- 알려진 적절 한 위치의 사용자가 주의 대상의 요청 보다 오류에 대 한 공간을 더 확보할 수 있도록 친숙 하 고 잘 모르는 위치에 대해 독립적인 잠금 임계값을 설정 합니다.
- 이전 소프트 잠금 동작을 계속 적용 하면서 스마트 잠금에 대해 감사 모드를 사용 하도록 설정 합니다. 이를 통해 사용자에 게 친숙 한 위치에 대해 배우고 AD FS 2012R2 2에서 제공 되는 엑스트라넷 잠금 기능으로 계속 보호할 수 있습니다.  

## <a name="how-it-works"></a>작동 방법
### <a name="configuration-information"></a>구성 정보
ESL를 사용 하는 경우 아티팩트 데이터베이스 AdfsArtifactStore의 새 테이블이 만들어지고 AD FS 팜에서 "사용자 활동" 마스터로 노드가 선택 됩니다. WID 구성에서이 노드는 항상 주 노드입니다. SQL 구성에서는 하나의 노드가 사용자 활동 마스터로 선택 됩니다.  

사용자 활동 마스터로 선택 된 노드를 봅니다. (AdfsFarmInformation). FarmRoles

모든 보조 노드는 포트 80을 통해 새로 로그인 할 때마다 마스터 노드에 연결 하 여 잘못 된 암호 수와 친숙 한 새 위치 값의 최신 값을 알아보고 로그인이 처리 된 후 해당 노드를 업데이트 합니다.

![구성](media/configure-ad-fs-extranet-smart-lockout-protection/esl1.png)

 보조 노드가 마스터에 연결할 수 없는 경우 오류 이벤트를 AD FS 관리자 로그에 기록 합니다. 인증은 계속 처리 되지만 AD FS는 업데이트 된 상태만 로컬로 기록 됩니다. AD FS는 10 분 마다 마스터에 연결을 다시 시도 하 고 마스터를 사용할 수 있게 되 면 다시 마스터로 전환 합니다.

### <a name="terminology"></a>용어
- **FamiliarLocation**: 인증 요청 중 ESL은 표시 된 모든 ip를 확인 합니다. 이러한 ip는 네트워크 IP, 전달 된 IP 및 선택적인 x 전달-IP의 조합입니다. 요청에 성공 하면 모든 Ip가 계정 활동 테이블에 "친숙 한 Ip"로 추가 됩니다. 요청에 "친숙 한 Ip"에 있는 모든 Ip가 있는 경우 요청은 "친숙 한" 위치로 처리 됩니다.
- **UnknownLocation**:에 제공 된 요청에 기존 "FamiliarLocation" 목록에 없는 IP가 하나 이상 있는 경우 해당 요청은 "알 수 없음" 위치로 처리 됩니다. Exchange online 주소는 성공한 요청과 실패 한 요청을 모두 처리 하는 Exchange Online 레거시 인증과 같은 프록시 시나리오를 처리 하기 위한 것입니다.  
- **badPwdCount**: 잘못 된 암호를 제출 하 고 인증에 실패 한 횟수를 나타내는 값입니다. 각 사용자에 대해 친숙 한 위치와 알 수 없는 위치에 대 한 별도의 카운터가 유지 됩니다.
- **UnknownLockout**: 사용자가 잠긴 위치에서 액세스할 수 없는 경우 사용자 당 부울 값입니다. 이 값은 badPwdCountUnfamiliar 및 ExtranetLockoutThreshold 값을 기준으로 계산 됩니다.
- **ExtranetLockoutThreshold**:이 값은 잘못 된 암호 시도의 최대 수를 결정 합니다. 임계값에 도달 하면 ADFS는 관찰 창이 통과 될 때까지 엑스트라넷의 요청을 거부 합니다.
- **ExtranetObservationWindow**:이 값은 알 수 없는 위치의 사용자 이름 및 암호 요청이 잠기는 기간을 결정 합니다. 창이 전달 되 면 ADFS는 알 수 없는 위치에서 사용자 이름 및 암호 인증을 다시 수행 하기 시작 합니다.
- **ExtranetLockoutRequirePDC**: 사용 하도록 설정 하면 엑스트라넷 잠금에 주 도메인 컨트롤러 (PDC)가 필요 합니다. 사용 하지 않도록 설정 되 면 PDC를 사용할 수 없는 경우 엑스트라넷 잠금이 다른 도메인 컨트롤러에 대체 됩니다.  
- **ExtranetLockoutMode**: 엑스트라넷 스마트 잠금의 로그 전용 및 적용 모드를 제어 합니다.
    - **ADFSSmartLockoutLogOnly**: 엑스트라넷 스마트 잠금이 사용 하도록 설정 되어 있지만 AD FS는 관리자 및 감사 이벤트만 작성 하지만 인증 요청을 거부 하지는 않습니다. 이 모드는 처음에는 ' ADFSSmartLockoutEnforce '를 사용 하도록 설정 하기 전에 FamiliarLocation를 채우도록 설정 되어 있습니다.
    - **ADFSSmartLockoutEnforce**: 임계값에 도달 했을 때 익숙하지 않은 인증 요청 차단에 대 한 완전 한 지원입니다.

IPv4 및 IPv6 주소가 지원 됩니다.

### <a name="anatomy-of-a-transaction"></a>트랜잭션 분석
- **사전 인증 확인**: 인증 요청 중에 ESL은 표시 된 모든 ip를 확인 합니다. 이러한 ip는 네트워크 IP, 전달 된 IP 및 선택적인 x 전달-IP의 조합입니다. 감사 로그에서 이러한 Ip는 x-m-전달 <IpAddress> -클라이언트-ip, x--------------ip의 순서로 필드에 나열 됩니다.

  ADFS는 이러한 Ip를 기반으로 요청이 친숙 한 위치 또는 익숙하지 않은 위치에서 온 것인지를 확인 한 다음 각 badPwdCount가 설정 된 임계값 제한 보다 작음을 확인 하거나 마지막으로 **실패** 한 시도가 관찰 창 시간 프레임 보다 오래 발생 했는지 확인 합니다. 이러한 조건 중 하나가 true 이면 ADFS는 추가 처리 및 자격 증명 유효성 검사를 위해이 트랜잭션을 허용 합니다. 두 조건이 모두 false 이면 관찰 창이 통과할 때까지 계정이 이미 잠긴 상태입니다. 관찰 창이 전달 된 후에는 사용자가 인증을 시도할 수 있습니다. 2019에서 ADFS는 IP 주소가 친숙 한 위치와 일치 하는지 여부에 따라 적절 한 임계값 제한을 확인 합니다.
- **성공한 로그인**: 로그인이 성공 하면 요청의 ip가 사용자의 친숙 한 위치 IP 목록에 추가 됩니다.  
- **실패 한 로그인**: 로그인이 실패 하면 badPwdCount가 증가 합니다. 공격자가 임계값이 허용 하는 것 보다 더 많은 암호를 시스템에 전송할 경우 사용자는 잠금 상태로 전환 됩니다. (badPwdCount > ExtranetLockoutThreshold)  

![구성](media/configure-ad-fs-extranet-smart-lockout-protection/esl2.png)

계정이 잠겨 있는 경우 "UnknownLockout" 값은 true와 같습니다. 즉, 사용자의 badPwdCount가 임계값을 초과 합니다. 즉, 누군가가 시스템에서 허용 된 것 보다 많은 암호를 시도한 경우 이 상태에서는 유효한 사용자가 로그인 할 수 있는 두 가지 방법이 있습니다.
- 사용자는 ObservationWindow 시간이 경과할 때까지 기다려야 합니다.
- 잠금 상태를 다시 설정 하려면 ' Reset-ADFSAccountLockout '를 사용 하 여 badPwdCount을 다시 0으로 설정 합니다.

재설정이 발생 하지 않으면 각 관찰 기간 동안 AD에 대해 단일 암호 시도를 허용 하는 계정입니다. 해당 시도 후에는 계정이 잠긴 상태로 돌아가서 관찰 창이 다시 시작 됩니다. BadPwdCount 값은 암호 로그인이 성공한 후에만 자동으로 다시 설정 됩니다.

### <a name="log-only-mode-versus-enforce-mode"></a>로그 전용 모드와 ' 강제 ' 모드 비교
AccountActivity 테이블은 ' 로그 전용 ' 모드 및 ' 적용 ' 모드로 채워집니다. ' 로그 전용 ' 모드를 무시 하 고 권장 되는 대기 기간 없이 ESL를 ' 강제 ' 모드로 직접 이동 하면 사용자의 친숙 한 Ip가 ADFS에 알려지지 않습니다. 이 경우 ESL는 ' ADBadPasswordCounter ' 처럼 동작 하므로 사용자 계정이 활성 무차별 암호 대입 공격을 받는 경우에도 합법적인 사용자 트래픽을 차단할 수 있습니다. ' 로그 전용 ' 모드가 무시 되 고 사용자가 "UnknownLockout" = TRUE를 사용 하 여 잠긴 상태를 입력 하 고 "친숙 한" IP 목록에 없는 IP의 올바른 암호를 사용 하 여 로그인 하려고 하면 로그인 할 수 없게 됩니다. 이 시나리오를 방지 하기 위해 3-7 일 동안에는 로그 전용 모드를 사용 하는 것이 좋습니다. 계정이 적극적으로 공격을 받고 있는 경우 합법적인 사용자에 대 한 잠금을 방지 하기 위해 최소 24 시간의 ' 로그 전용 ' 모드가 필요 합니다.  

## <a name="extranet-smart-lockout-configuration"></a>엑스트라넷 스마트 잠금 구성  

### <a name="prerequisites-for-ad-fs-2016"></a>AD FS 2016에 대 한 필수 구성 요소

1. **팜의 모든 노드에 업데이트 설치**

   먼저 모든 Windows Server 2016 AD FS 서버가 6 월 2018 Windows 업데이트를 기준으로 최신 상태 인지 확인 하 고 AD FS 2016 팜이 2016 팜 동작 수준에서 실행 중인지 확인 합니다.
1. **권한 확인**

   엑스트라넷 스마트 잠금에서는 모든 AD FS 서버에서 Windows 원격 관리를 사용 하도록 설정 해야 합니다.
3. **아티팩트 데이터베이스 사용 권한 업데이트**

   엑스트라넷 스마트 잠금 AD FS 서비스 계정에 AD FS 아티팩트 데이터베이스에 새 테이블을 만들 수 있는 권한이 있어야 합니다. AD FS 서버에 AD FS 관리자로 로그인 한 후 PowerShell 명령 프롬프트 창에서 다음 명령을 실행 하 여이 사용 권한을 부여 합니다.

   ``` powershell
   PS C:\>$cred = Get-Credential
   PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
   ```
   >[!NOTE]
   >$Cred 자리 표시자는 AD FS 관리자 권한이 있는 계정입니다. 이렇게 하면 테이블을 만들기 위한 쓰기 권한이 제공 됩니다.

   AD FS 팜이 SQL Server를 사용 하 고 있으며 위에서 제공한 자격 증명에는 SQL Server에 대 한 관리자 권한이 없기 때문에 위의 명령은 충분 한 권한이 없어 실패할 수 있습니다. 이 경우 AdfsArtifactStore 데이터베이스에 연결 되어 있을 때 다음 명령을 실행 하 여 SQL Server Database에서 데이터베이스 권한을 수동으로 구성할 수 있습니다.
    ```  
    # when prompted with “Are you sure you want to perform this action?”, enter Y.

    [CmdletBinding(SupportsShouldProcess=$true,ConfirmImpact = 'High')]
    Param()

    $fileLocation = "$env:windir\ADFS\Microsoft.IdentityServer.Servicehost.exe.config"

    if (-not [System.IO.File]::Exists($fileLocation))
    {
    write-error "Unable to open ADFS configuration file."
    return
    }

    $doc = new-object Xml
    $doc.Load($fileLocation)
    $connString = $doc.configuration.'microsoft.identityServer.service'.policystore.connectionString
    $connString = $connString -replace "Initial Catalog=AdfsConfigurationV[0-9]*", "Initial Catalog=AdfsArtifactStore"

    if ($PSCmdlet.ShouldProcess($connString, "Executing SQL command sp_addrolemember 'db_owner', 'db_genevaservice' "))
    {
    $cli = new-object System.Data.SqlClient.SqlConnection
    $cli.ConnectionString = $connString
    $cli.Open()

    try
    {     

    $cmd = new-object System.Data.SqlClient.SqlCommand
    $cmd.CommandText = "sp_addrolemember 'db_owner', 'db_genevaservice'"
    $cmd.Connection = $cli
    $rowsAffected = $cmd.ExecuteNonQuery()  
    if ( -1 -eq $rowsAffected )
    {
    write-host "Success"
    }
    }
    finally
    {
    $cli.CLose()
    }
    }
    ```

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS 보안 감사 로깅을 사용할 수 있는지 확인
이 기능을 사용 하면 보안 감사 로그가 사용 되므로 AD FS에서 감사를 사용 하도록 설정 하 고 모든 AD FS 서버의 로컬 정책에 대해 감사를 사용 하도록 설정 해야 합니다.

### <a name="configuration-instructions"></a>구성 지침
엑스트라넷 스마트 잠금은 ADFS 속성 **ExtranetLockoutEnabled**를 사용 합니다. 이 속성은 이전에 Server 2012R2 2의 "엑스트라넷 소프트 잠금"을 제어 하는 데 사용 되었습니다. 엑스트라넷 소프트 잠금이 사용 하도록 설정 된 경우 현재 속성 구성을 보려면를 실행 ` Get-AdfsProperties` 합니다.

### <a name="configuration-recommendations"></a>구성 권장 사항
엑스트라넷 스마트 잠금을 구성할 때 임계값 설정에 대 한 모범 사례를 따릅니다.  

`ExtranetObservationWindow (new-timespan -Minutes 30)`

`ExtranetLockoutThreshold: – 2x AD Threshold Value`

AD 값: 20, ExtranetLockoutThreshold: 10

Active Directory 잠금은 엑스트라넷 스마트 잠금과 독립적으로 작동 합니다. 그러나 Active Directory 잠금이 설정 된 경우 AD에서 계정 잠금 임계값을 AD FS < ExtranetLockoutThreshold

`ExtranetLockoutRequirePDC - $false`

사용 하도록 설정 하는 경우 엑스트라넷 잠금에는 주 도메인 컨트롤러 (PDC)가 필요 합니다. 사용 하지 않도록 설정 되 고 false로 구성 된 경우에는 PDC를 사용할 수 없는 경우 엑스트라넷 잠금이 다른 도메인 컨트롤러에 대체 됩니다.

이 속성을 설정 하려면 다음을 실행 합니다.

``` powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```
### <a name="enable-log-only-mode"></a>로그 전용 모드 사용

로그 전용 모드에서 AD FS는 사용자에 게 친숙 한 위치 정보를 채우고 보안 감사 이벤트를 작성 하지만 모든 요청을 차단 하지는 않습니다. 이 모드는 스마트 잠금이 실행 중인지 확인 하 고 "적용" 모드를 사용 하도록 설정 하기 전에 사용자에 게 친숙 한 위치를 "학습" AD FS 수 있도록 하는 데 사용 됩니다. AD FS 학습 하는 것 처럼 사용자 마다 로그인 활동 (로그 전용 모드 또는 강제 모드)을 저장 합니다.
다음을 실행 하 여 잠금 동작을 로그만으로 설정 합니다.  

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly`

로그 전용 모드는 시스템에서 스마트 잠금 동작에 대 한 잠금 적용을 도입 하기 전에 로그인 동작을 학습할 수 있도록 임시 상태를 유지 하기 위한 것입니다. 로그 전용 모드의 권장 기간은 3-7 일입니다. 계정이 적극적으로 공격을 받고 있는 경우 최소 24 시간 동안 로그 전용 모드를 실행 해야 합니다.

AD FS 2016에서 엑스트라넷 스마트 잠금을 사용 하도록 설정 하기 전에 2012R2 ' 엑스트라넷 소프트 잠금 ' 동작을 사용 하도록 설정 하면 로그 전용 모드에서 ' 엑스트라넷 소프트 잠금 ' 동작을 사용 하지 않도록 설정 합니다. AD FS 스마트 잠금은 로그 전용 모드에서 사용자를 잠그지 않습니다. 그러나 온-프레미스 AD는 AD 구성에 따라 사용자를 잠글 수 있습니다. 온-프레미스 AD가 사용자를 어떻게 잠금 할 수 있는지 알아보려면 AD 잠금 정책을 검토 하세요.

AD FS 2019에서 추가 이점은 다음 Powershell을 사용 하 여 이전 소프트 잠금 동작을 계속 적용 하면서 스마트 잠금에 대 한 로그 전용 모드를 사용 하도록 설정할 수 있다는 것입니다.

`Set-AdfsProperties -ExtranetLockoutMode 3`

새 모드를 적용 하려면 팜의 모든 노드에서 AD FS 서비스를 다시 시작 합니다.

`Restart-service adfssrv`

모드가 구성 된 후에는 EnableExtranetLockout 매개 변수를 사용 하 여 스마트 잠금을 사용 하도록 설정할 수 있습니다.

`Set-AdfsProperties -EnableExtranetLockout $true`

### <a name="enable-enforce-mode"></a>적용 모드 사용

잠금 임계값 및 관찰 창에 익숙해지면 다음 PSH cmdlet을 사용 하 여 ESL를 "적용" 모드로 이동할 수 있습니다.

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce`

새 모드를 적용 하려면 다음 명령을 사용 하 여 팜의 모든 노드에서 AD FS 서비스를 다시 시작 합니다.

`Restart-service adfssrv`

## <a name="manage-user-account-activity"></a>사용자 계정 작업 관리
AD FS는 계정 활동 데이터를 관리 하는 세 가지 cmdlet을 제공 합니다. 이러한 cmdlet은 마스터 역할을 보유 하는 팜의 노드에 자동으로 연결 됩니다.
>[!NOTE]
>충분 한 관리 (jea)를 사용 하 여 계정 잠금을 다시 설정 하 AD FS commandlet을 위임할 수 있습니다. 예를 들어 지원 센터 직원은 ESL commandlets 사용 권한을 위임할 수 있습니다. 이러한 cmdlet 사용 권한을 위임 하는 방법에 대 한 자세한 내용은 [관리자가 아닌 사용자에 대 한 AD FS Powershell 이상 액세스 위임](delegate-ad-fs-pshell-access.md)

-Server 매개 변수를 전달 하 여이 동작을 재정의할 수 있습니다.

- ADFSAccountActivity-UserPrincipalName

  사용자 계정에 대 한 현재 계정 작업을 읽습니다. 이 cmdlet은 항상 계정 작업 REST 끝점을 사용 하 여 팜 마스터에 자동으로 연결 합니다. 따라서 모든 데이터가 항상 일치 해야 합니다.

`Get-ADFSAccountActivity user@contoso.com`

  속성:
    - BadPwdCountFamiliar: 알려진 위치에서 인증에 성공 하면 증가 합니다.
    - BadPwdCountUnknown: 알 수 없는 위치에서 인증에 실패 하면 증가 합니다.
    - LastFailedAuthFamiliar: 익숙한 위치에서 인증에 실패 한 경우 Lastfailedauthfamiliar이 실패 한 인증의 시간으로 설정 됩니다.
    - LastFailedAuthUnknown: 알 수 없는 위치에서 인증에 실패 한 경우 LastFailedAuthUnknown이 실패 한 인증의 시간으로 설정 됩니다.
    - FamiliarLockout: "BadPwdCountFamiliar" > ExtranetLockoutThreshold 경우 "True"가 되는 부울 값입니다.
    - UnknownLockout: "BadPwdCountUnknown" > ExtranetLockoutThreshold 인 경우 "True"가 되는 부울 값입니다.  
    - FamiliarIPs: 사용자에 게 친숙 한 최대 20 개의 Ip입니다. 이를 초과 하면 목록에서 가장 오래 된 IP가 제거 됩니다.
-    ADFSAccountActivity

     익숙한 새 위치를 추가 합니다. 친숙 한 IP 목록에는 최대 20 개의 항목이 있습니다 .이를 초과 하면 목록에서 가장 오래 된 IP가 제거 됩니다.

`Set-ADFSAccountActivity user@contoso.com -AdditionalFamiliarIps “1.2.3.4”`

- ADFSAccountLockout

  친숙 한 각 위치의 사용자 계정에 대 한 잠금 카운터를 다시 설정 합니다 (badPwdCountFamiliar) 또는 익숙하지 않은 위치 카운터 (badPwdCountUnfamiliar). 카운터를 다시 설정 하면 reset 카운터가 임계값 보다 작으므로 "FamiliarLockout" 또는 "UnfamiliarLockout" 값이 업데이트 됩니다.  

`Reset-ADFSAccountLockout user@contoso.com -Location Familiar`
`Reset-ADFSAccountLockout user@contoso.com -Location Unknown`

## <a name="event-logging--user-activity-information-for-ad-fs-extranet-lockout"></a>AD FS 엑스트라넷 잠금에 대 한 사용자 활동 정보를 & 이벤트 로깅

### <a name="connect-health"></a>Connect Health
사용자 계정 작업을 모니터링 하는 데 권장 되는 방법은 Connect Health를 사용 하는 것입니다. Connect Health는 위험한 Ip에 대 한 다운로드 가능한 보고와 잘못 된 암호 시도를 생성 합니다. 위험한 IP 보고서의 각 항목에는 지정된 임계값을 초과하는 실패한 AD FS 로그인 활동에 대한 집계 정보가 표시됩니다. 사용자 지정 가능한 메일 설정에서이 문제가 발생 하는 즉시 경고 관리자에 게 전자 메일 알림을 설정할 수 있습니다. 추가 정보 및 설정 지침은 [Connect Health 설명서](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)를 참조 하세요.

### <a name="ad-fs-extranet-smart-lockout-events"></a>엑스트라넷 스마트 잠금 이벤트를 AD FS 합니다.

>[!NOTE]
> [AD FS 지원 엑스트라넷 잠금 문제 해결 가이드](https://adfshelp.microsoft.com/TroubleshootingGuides/Workflow/a73d5843-9939-4c03-80a1-adcbbf3ccec8) 를 사용 하 여 엑스트라넷 스마트 잠금 문제 해결

엑스트라넷 스마트 잠금 이벤트를 작성 하려면 ' 로그 전용 ' 또는 ' 강제 적용 ' 모드에서 ESL를 사용 하도록 설정 하 고 ADFS 보안 감사를 사용 하도록 설정 해야 합니다.
AD FS는 보안 감사 로그에 엑스트라넷 잠금 이벤트를 기록 합니다.
- 사용자가 잠겨 있는 경우 (실패 한 로그인 시도에 대 한 잠금 임계값에 도달)
- 이미 잠금 상태에 있는 사용자에 대 한 로그인 시도를 수신 하 AD FS 경우

로그 전용 모드에서는 잠금 이벤트에 대 한 보안 감사 로그를 확인할 수 있습니다. 발견 된 모든 이벤트에 대해 ADFSAccountActivity cmdlet을 사용 하 여 사용자 상태를 확인 하 여 친숙 한 IP 주소나 익숙하지 않은 IP 주소에서 잠금이 발생 했는지 확인 하 고 해당 사용자에 대 한 친숙 한 IP 주소 목록을 다시 확인할 수 있습니다.


|이벤트 ID|설명|
|-----|-----|
|1203|이 이벤트는 잘못 된 암호 시도에 대해 기록 됩니다. BadPwdCount이 ExtranetLockoutThreshold에 지정 된 값에 도달 하는 즉시, ExtranetObservationWindow에 지정 된 기간 동안 ADFS에서 계정이 잠깁니다.</br>작업 ID: %1</br>XML: %2|
|1201|이 이벤트는 사용자가 잠길 때마다 기록 됩니다. </br>작업 ID: %1</br>XML: %2|
|557 (ADFS 2019)| %1 노드의 계정 저장소 rest 서비스와 통신 하는 동안 오류가 발생 했습니다. WID 팜이 면 주 노드가 오프 라인 상태일 수 있습니다. SQL 팜 인 경우 ADFS가 자동으로 새 노드를 선택 하 여 사용자 저장소 마스터 역할을 호스팅합니다.|
|562 (ADFS 2019)|서버 %1의 계정 저장소 끝점과 communcating 하는 동안 오류가 발생 했습니다.</br>예외 메시지: %2|
|563 (ADFS 2019)|엑스트라넷 잠금 상태를 계산 하는 동안 오류가 발생 했습니다. %1의 값으로 인해이 사용자에 대 한 인증 설정이 허용 되 고 토큰 발급이 계속 됩니다. WID 팜이 면 주 노드가 오프 라인 상태일 수 있습니다. SQL 팜 인 경우 ADFS가 자동으로 새 노드를 선택 하 여 사용자 저장소 마스터 역할을 호스팅합니다.</br>계정 저장소 서버 이름: %2</br>사용자 Id: %3</br>예외 메시지: %4|
|512|다음 사용자에 대 한 계정이 잠겼습니다. 시스템 구성으로 인해 로그인 시도가 허용 됩니다.</br>작업 ID: %1 </br>사용자: %2 </br>클라이언트 IP: %3 </br>잘못 된 암호 수: %4  </br>마지막 잘못 된 암호 시도: %5|
|515|다음 사용자 계정이 잠긴 상태 이며 올바른 암호를 제공 했습니다. 이 계정은 손상 될 수 있습니다.</br>추가 데이터 </br>작업 ID: %1 </br>사용자: %2 </br>클라이언트 IP: %3 |
|516|잘못 된 암호 시도 횟수가 너무 많기 때문에 다음 사용자 계정이 잠겼습니다.</br>작업 ID: %1  </br>사용자: %2  </br>클라이언트 IP: %3  </br>잘못 된 암호 수: %4  </br>마지막 잘못 된 암호 시도: %5|

## <a name="esl-frequently-asked-questions"></a>ESL 질문과 대답

**적용 모드에서 엑스트라넷 스마트 잠금을 사용 하는 ADFS 팜에서 악의적인 사용자 잠금이 표시 되나요?** 

A: ADFS 스마트 잠금이 ' 강제 적용 ' 모드로 설정 되어 있으면 합법적인 사용자 계정이 무차별 암호 대입 또는 서비스 거부에 의해 잠긴 것을 볼 수 없습니다. 악의적인 계정 잠금은 사용자 로그인을 방해할 수 있는 유일한 방법입니다. 잘못 된 행위자가 사용자 암호를가지고 있거나 해당 사용자에 대해 알려진 양호 (친숙 한) IP 주소에서 요청을 보낼 수 있는 경우입니다. 

**ESL가 사용 하도록 설정 되 고 잘못 된 행위자에 사용자 암호가 있나요?** 

A: 무차별 암호 대입 공격 시나리오의 일반적인 목표는 암호를 추측 하 고 성공적으로 로그인 하는 것입니다.사용자가 피싱 하거나 암호를 추측 하는 경우 로그인이 올바른 암호와 새 IP의 "성공" 조건을 충족 하기 때문에 ESL 기능은 액세스를 차단 하지 않습니다. 그러면 잘못 된 행위자 IP가 "친숙 한" 것으로 나타납니다.이 시나리오에서 가장 좋은 완화 방법은 ADFS의 사용자 활동을 지우고 사용자에 대해 Multi-factor Authentication을 요구 하는 것입니다. 추측할 암호가 시스템에 표시 되지 않도록 하는 AAD 암호 보호를 설치 하는 것이 좋습니다.

**사용자가 IP에서 성공적으로 로그인 한 적이 없는 경우 잘못 된 암호를 사용 하 여 마지막으로 암호를 올바르게 입력 하면 로그인 할 수 있나요?** 

A: 사용자가 잘못 된 암호를 여러 개 제출 하는 경우 (즉, 합법적인 mis를 입력 하는 경우) 다음 시도에서 암호를 올바르게 입력 하면 사용자는 즉시 로그인이 성공 합니다. 그러면 잘못 된 암호 수가 삭제 되 고 해당 IP가 FamiliarIPs 목록에 추가 됩니다.그러나 알 수 없는 위치에서 실패 한 로그인의 임계값을 초과 하는 경우 잠금 상태로 전환 되며 관찰 창에서 대기 하 고 유효한 암호로 로그인 하거나 관리자의 개입이 있어야만 계정을 다시 설정할 수 있습니다.  
 
**ESL도 인트라넷에서 작동 하나요?**

A: 클라이언트가 ADFS 서버에 직접 연결 하 고 웹 응용 프로그램 프록시 서버를 통해 연결 하지 않는 경우 ESL 동작이 적용 되지 않습니다.  

**클라이언트 IP 필드에 Microsoft IP 주소가 표시 됩니다. ESL에서 프록시 무차별 암호 대입 공격을 차단 하나요?**  

A: ESL는 Exchange Online 또는 기타 레거시 인증 무작위 공격 시나리오를 방지 하는 데 효과적입니다. 레거시 인증에는 00000000-0000-0000-0000-000000000000의 "작업 ID"가 있습니다.이러한 공격에서 잘못 된 행위자는 Exchange Online 기본 인증 (레거시 인증이 라고도 함)을 활용 하 여 클라이언트 IP 주소가 Microsoft 하나로 표시 되도록 합니다. 클라우드의 Exchange online 서버는 Outlook 클라이언트를 대신 하 여 인증 확인을 합니다. 이러한 시나리오에서 악의적인 제출자의 IP 주소는 x-ms로 전달 된-클라이언트 ip에 있고 Microsoft Exchange Online server IP는 x-m-클라이언트 ip 값에 있습니다.
엑스트라넷 스마트 잠금은 네트워크 ip, 전달 된 ip, x로 전달 된 클라이언트 IP 및 x-m-클라이언트 ip 값을 확인 합니다. 요청에 성공 하면 모든 Ip가 친숙 한 목록에 추가 됩니다. 요청이 표시 되 고 제공 된 Ip가 친숙 한 목록에 없는 경우 요청은 익숙하지 않은 것으로 표시 됩니다. 친숙 한 사용자는 잘 로그인 할 수 있지만, 익숙하지 않은 위치의 요청은 차단 됩니다.  

* * Q: ESL를 사용 하기 전에 ADFSArtifactStore 크기를 예측할 수 있나요?

A: ESL를 사용 하도록 설정 하면 ADFSArtifactStore 데이터베이스의 사용자에 대 한 계정 작업 및 알려진 위치를 추적 AD FS 합니다. 이 데이터베이스는 추적된 사용자 및 알려진 위치의 수를 기준으로 크기를 조정합니다. ESL을 사용하도록 계획하는 경우 ADFSArtifactStore 데이터베이스의 크기가 사용자 100,000명당 최대 1GB의 속도로 확장한다고 예측할 수 있습니다. AD FS 팜이 WID (Windows 내부 데이터베이스)를 사용 하는 경우 데이터베이스 파일의 기본 위치는 C:\Windows\WID\Data\.입니다. 이 드라이브를 채우지 않도록 방지하려면 ESL을 사용하도록 설정하기 전에 최소 5GB의 사용 가능한 스토리지가 있어야 합니다. 디스크 스토리지 외에도 500,000명 이하의 사용자 인구에 대해 최대 1GB의 RAM을 추가하여 ESL을 사용하도록 설정한 후 총 프로세스 메모리를 늘리도록 계획합니다.


## <a name="additional-references"></a>추가 참조  
[Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
