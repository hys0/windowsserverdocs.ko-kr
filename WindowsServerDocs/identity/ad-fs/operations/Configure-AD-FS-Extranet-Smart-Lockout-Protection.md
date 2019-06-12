---
ms.assetid: 777aab65-c9c7-4dc9-a807-9ab73fac87b8
title: AD FS 엑스트라넷 잠금 보호를 구성 합니다.
description: ''
author: billmath
ms.author: billmath
manager: mtilman
ms.date: 05/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7a4ad8c0199f0f62d7cd69a43897cb4608ddb365
ms.sourcegitcommit: ccc802338b163abdad2e53b55f39addcfea04603
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66687364"
---
# <a name="ad-fs-extranet-lockout-and-extranet-smart-lockout"></a>AD FS 엑스트라넷 잠금 및 엑스트라넷 잠금

## <a name="overview"></a>개요

엑스트라넷 스마트 잠금 (ESL)를 악의적인 활동 으로부터 엑스트라넷 계정 잠금 경험에서 사용자를 보호 합니다.  

ESL AD FS를 사용자에 대 한 친숙 한 위치에서 로그인 시도 공격자 수에서 로그인 시도 구분할 수 있습니다. AD FS 유효한 사용자가 해당 계정을 사용 하 여 계속 하도록 허용 하는 동안 공격자를 잠글 수 있습니다. 이렇게 하면 수 없으며 서비스 거부 및 특정 부류의 사용자에 대 한 암호 스프레이 공격 으로부터 보호 합니다. ESL은 Windows Server 2016에서 AD FS에 대해 사용할 수 있으며 Windows Server 2019에서 AD FS에 빌드됩니다.

ESL 사용자 이름에 사용할 수 있는 전용 이며 웹 응용 프로그램 프록시를 사용 하 여 또는 타사 엑스트라넷을 통해 제공 되는 암호 인증 요청 파티 프록시입니다. 와 같은 웹 응용 프로그램 프록시를 대신 사용할 MS ADFSPIP 프로토콜을 지원 해야 하는 모든 타사 파티 프록시 [F5 BIG-IP Access Policy Manager](https://devcentral.f5.com/s/articles/ad-fs-proxy-replacement-on-f5-big-ip-30191)합니다. 프록시 MS ADFSPIP 프로토콜을 지원 하는지 확인 하는 타사 파티 프록시 설명서를 참조 하세요.   

## <a name="additional-features-in-ad-fs-2019"></a>2019 AD FS에서 추가 기능
AD FS 2019에서에서 엑스트라넷 잠금 추가 AD FS 2016에 비해 다음과 같은 이점이 있습니다.
- 알려진된 적절 한 위치에 사용자가 주의 대상 위치에서 요청 보다 오류에 대 한 더 많은 공간을 그려볼 수 있도록 친숙 하 고 알 수 없는 위치에 대 한 독립적인 잠금 임계값을 설정 합니다.
- 이전 소프트 잠금 동작을 적용 하면서 스마트 잠금에 대 한 감사 모드를 사용 합니다. 이 옵션을 사용 하면 사용자 친숙 한 위치에 대해 알아보고 여전히 AD FS 2012 r2에서 제공 되는 엑스트라넷 잠금 기능으로 보호 될 수 있습니다.  

## <a name="how-it-works"></a>작동 방법
### <a name="configuration-information"></a>구성 정보
ESL을 사용 하는 AdfsArtifactStore.AccountActivity, 아티팩트 데이터베이스에 새 테이블을 만들고 "사용자 활동" 마스터와 AD FS 팜에 노드를 선택 합니다. WID 구성에서이 노드는 항상 주 노드. SQL 구성에서 노드 하나를 사용자 작업 마스터가 되도록 선택 됩니다.  

선택한 사용자 작업 마스터 노드를 표시 합니다. Get-AdfsFarmInformation.FarmRoles

모든 보조 노드에 잘못 된 암호 수의 최신 값 및 새 익숙한 위치 값을 포트 80을 통해 새로운 각 로그인에 마스터 노드를 문의 하 고 로그인이 처리 된 후 해당 노드를 업데이트 됩니다.

![구성](media/configure-ad-fs-extranet-smart-lockout-protection/esl1.png)

 보조 노드에서 마스터에 연결할 수 없는 경우 AD FS 관리자 로그에 오류 이벤트를 기록 합니다. 인증 처리를 계속 하지만 AD FS 업데이트 상태를 로컬로 기록만 합니다. AD FS 마스터 10 분 마다 연결 다시 시도 하 고 마스터 마스터를 사용할 수 있으면 다시 전환 됩니다.

### <a name="terminology"></a>용어
- **FamiliarLocation**: 인증 요청을 하는 동안 ESL Ip를 제공 하는 모든 확인 합니다. 이러한 Ip 네트워크 IP를 IP 전달 및 선택적 x-전달 기능에 대 한 IP 조합 됩니다. Ip의 모든 요청이 성공 하면 "친숙 한 ip" 계정 활동 테이블에 추가 됩니다. 요청에 있는 경우 "친숙 한 Ip"에 있는 모든 Ip를 요청 "익숙한" 위치로 간주 됩니다.
- **UnknownLocation**: 요청에서 제공 되는 기존 "FamiliarLocation" 목록에 없는 하나 이상의 IP가 요청을 "Unknown" 위치로 처리 됩니다. 이 Exchange Online 주소 성공 및 실패 한 요청을 처리 하는 위치에 Exchange Online 레거시 인증과 같은 프록시 시나리오를 처리 하는 것입니다.  
- **badPwdCount**: 인증 및 잘못 된 암호를 전송 된 횟수를 나타내는 값을 실패 했습니다. 각 사용자에 대해 별도 카운터는 친숙 한 위치 및 알 수 없는 위치에 대해 유지 됩니다.
- **UnknownLockout**: 알 수 없는 위치에서 액세스 하지 못하도록 사용자 잠겨 있으면 사용자별 부울 값입니다. 이 값은 badPwdCountUnfamiliar 및 ExtranetLockoutThreshold 값에 따라 계산 됩니다.
- **ExtranetLockoutThreshold**: 이 값이 잘못 된 암호 시도의 최대 수를 결정합니다. 임계값에 도달 하면 ADFS 관찰 창 경과할 때까지 엑스트라넷의 요청을 거부 합니다.
- **ExtranetObservationWindow**: 이 값이 알 수 없는 위치에서 사용자 이름 및 암호 요청이 잠겨 있는 기간을 결정 합니다. 창에 전달 되는 경우 ADFS는 알 수 없는 위치에서 사용자 이름 및 암호 인증을 다시 수행 하기 시작 합니다.
- **ExtranetLockoutRequirePDC**: 사용 하도록 설정 하면 엑스트라넷 잠금 주 도메인 컨트롤러 (PDC) 필요 합니다. 사용 하지 않도록 설정, 엑스트라넷 잠금 PDC를 사용할 수 없는 경우 다른 도메인 컨트롤러에 대체가 됩니다.  
- **ExtranetLockoutMode**: 컨트롤의 스마트 엑스트라넷 잠금 적용 하는 vs 모드만 로그
    - **ADFSSmartLockoutLogOnly**: 엑스트라넷 잠금 활성화 되어 있지만 AD FS는만 관리 하 고 감사 이벤트를 쓰지만 거부 인증 요청 하지 것입니다. 이 모드는 처음에 사용할 수 있도록 FamiliarLocation 'ADFSSmartLockoutEnforce'를 사용 하기 전에 채워질 것입니다.
    - **ADFSSmartLockoutEnforce**: 임계값에 도달 하면 알 수 없는 인증 요청을 차단 하는 것에 대 한 전체 지원 합니다.

IPv4 및 IPv6 주소가 지원 됩니다.

### <a name="anatomy-of-a-transaction"></a>트랜잭션의 분석
- **사전 인증 검사**: 인증 요청을 하는 동안 ESL Ip를 제공 하는 모든 확인 합니다. 이러한 Ip 네트워크 IP를 IP 전달 및 선택적 x-전달 기능에 대 한 IP 조합 됩니다. 감사 로그에 이러한 Ip에 나열 되는 <IpAddress> x-ms-전달-클라이언트-ip, x-전달 기능에 대 한 순서 대로 x-ms-프록시-클라이언트-ip 필드입니다.

  이러한 Ip에 따라 ADFS 결정 하는 경우 또는 요청 친숙 한 또는 알 수 없는 위치에서 이며 그런 다음 해당 badPwdCount 임계값 제한 설정 보다 작은 경우를 확인 하는 경우 마지막 **실패 한** 시도 발생 한 이상는 관찰 창 시간 프레임입니다. 이러한 조건 중 하나가 true 인 경우 ADFS 추가 처리를 위해이 트랜잭션이 있으며 유효성 검사를 자격 증명입니다. 두 조건을 모두 false 인 경우 계정은 이미 잠긴 상태의 관찰 창 전달 될 때 까지입니다. 관찰 창에 통과 한 후 사용자 인증을 시도한을 허용 됩니다. 2019에서 ADFS를 기반으로 하는 적절 한 임계값 제한에 대해 IP 주소와 일치 하는지 확인 익숙한 위치 여부 note 합니다.
- **로그인이 성공한**: 로그인에 성공 하면 요청에서 Ip는 사용자의 친숙 한 위치 IP 목록에 추가 됩니다.  
- **로그인 하지 못했습니다.** : 로그인 실패를 badPwdCount 경우 증가 합니다. 공격자가 더 이상 잘못 된 암호 시스템에 허용 된 임계값 보다 전송 하는 경우 사용자는 잠금 상태로 전환 됩니다. (badPwdCount > ExtranetLockoutThreshold)  

![구성](media/configure-ad-fs-extranet-smart-lockout-protection/esl2.png)

계정이 잠겨 때로 "UnknownLockout" 값은 같습니다. 이 사용자의 badPwdCount 임을 의미를 통해 임계값 보다 즉, 누군가가 시스템에서 허용 된 것 보다 더 많은 암호를 시도 합니다. 이 상태는 유효한 사용자가 로그인 할 수는 2 가지가 있습니다.
- 사용자 ObservationWindow 시간 경과를 기다려야 합니다. 또는
- 잠금 상태를 다시 설정 하기 위해는 badPwdCount ' 재설정 ADFSAccountLockout'를 사용 하 여 0으로 다시 설정 합니다.

없는 재설정 발생 하는 경우 각 관찰 창에 대 한 AD에 대해 단일 암호 시도 하는 계정이 허용 됩니다. 계정 이후에 잠긴된 상태를 관찰 창과 시도 다시 시작을 반환 합니다. BadPwdCount 값 성공적인 암호 로그인 한 후 자동으로 다시 설정만 됩니다.

### <a name="log-only-mode-versus-enforce-mode"></a>'적용' 모드 및 로그 전용 모드
AccountActivity 테이블은 모두 ' 로그 전용 ' 모드 및 '적용' 모드 중에 채워집니다. ' 로그 전용 ' 모드를 생략 하 고 ESL 권장 되는 유예 기간이 없는 모드 '적용'으로 직접 이동 하는 경우 사용자의 친숙 한 Ip ADFS에 알 수 없게 됩니다. 이 경우 잠재적으로 사용자 계정이 active 무차별 공격을 받고 합법적인 사용자 트래픽을 차단 'ADBadPasswordCounter' 같은 ESL 작동 합니다. ' 로그 전용 ' 모드를 시행 하지 않으며 상태 "UnknownLockout"를 사용 하 여 사용자가 잠긴 경우 = TRUE 및 로그인 수 없습니다 "익숙한" IP 목록에 없는 IP에서 적절 한 암호 로그인을 시도 합니다. 이 시나리오를 방지 하려면 3 ~ 7 일 동안 로그 전용 모드 것이 좋습니다. 계정이 있으면 적극적으로 공격을 받고, 최소 24 ' 로그 전용 ' 모드의 경우 합법적인 사용자가 잠금을 방지 하는 데 필요한  

## <a name="extranet-smart-lockout-configuration"></a>엑스트라넷 잠금 구성  

### <a name="prerequisites-for-ad-fs-2016"></a>AD FS 2016에 대 한 필수 구성 요소

1. **팜의 모든 노드에서 업데이트를 설치 합니다.**

   먼저, 2018 년 6 월 Windows 업데이트를 기준으로 최신 상태입니다. 모든 Windows Server 2016 AD FS 서버 및 AD FS 2016 팜 2016 팜 동작 수준에서 실행 되 고 있는지 확인 합니다.
1. **권한 확인**

   엑스트라넷 잠금에는 모든 AD FS 서버에서 Windows 원격 관리를 사용할 필요 합니다.
3. **아티팩트 데이터베이스 권한을 업데이트합니다**

   엑스트라넷 잠금에는 AD FS 서비스 계정을 AD FS 아티팩트 데이터베이스에 새 테이블을 만들 수 있는 권한이 필요 합니다. AD FS 관리자의 경우 AD FS 서버에 로그인 하 고 PowerShell 명령 프롬프트 창에서 다음 명령을 실행 하 여이 권한을 부여 합니다.

   ``` powershell
   PS C:\>$cred = Get-Credential
   PS C:\>Update-AdfsArtifactDatabasePermission -Credential $cred
   ```
   >[!NOTE]
   >$Cred 자리 표시자는 AD FS 관리자 권한이 있는 계정입니다. 이 테이블을 만들 수 있는 쓰기 권한을 제공 해야 합니다.

   위의 명령을 AD FS 팜의 SQL Server를 사용 하는 위에 제공 된 자격 증명을 SQL server에서 관리자 권한이 없는 것 이므로 충분 한 사용 권한 부족으로 인해 실패할 수 있습니다. 이 경우 구성할 수 있습니다 데이터베이스 사용 권한을 수동으로 SQL Server 데이터베이스의 AdfsArtifactStore 데이터베이스에 연결 되 면 다음 명령을 실행 하 여.
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

### <a name="ensure-ad-fs-security-audit-logging-is-enabled"></a>AD FS 보안 감사 로깅을 사용 하도록 설정 확인
이 기능을 사용 하면 모든 AD FS 서버의 로컬 정책을 비롯 하 여 AD FS에 따라서 감사 로그를 사용할 수 있어야 합니다 보안 감사를 사용 합니다.

### <a name="configuration-instructions"></a>구성 지침
ADFS 속성을 사용 하는 엑스트라넷 스마트 잠금 **ExtranetLockoutEnabled**합니다. 이 속성 컨트롤 "엑스트라넷 소프트 잠금" Server 2012R2에 이전에 사용 되었습니다. 실행의 현재 속성 구성을 보려면 엑스트라넷 소프트 잠금 활성화 된 경우 ` Get-AdfsProperties` 합니다.

### <a name="configuration-recommendations"></a>구성 권장 사항
엑스트라넷 잠금을 구성할 때 임계값을 설정 하는 것에 대 한 모범 사례를 따릅니다.  

`ExtranetObservationWindow (new-timespan -Minutes 30)`

`ExtranetLockoutThreshold: – 2x AD Threshold Value`

AD 값: 20, ExtranetLockoutThreshold: 10

Active Directory 잠금 독립적으로 작동에서 엑스트라넷 잠금. 그러나 Active Directory 잠금 사용 하는 경우, AD FS에서 ExtranetLockoutThreshold < AD의 계정 잠금 임계값

`ExtranetLockoutRequirePDC - $false`

사용 하도록 설정 하면 엑스트라넷 잠금 주 도메인 컨트롤러 (PDC) 필요 합니다. 사용 하지 않도록 설정 하 고 false로 구성 하면 엑스트라넷 잠금 PDC를 사용할 수 없는 경우 다른 도메인 컨트롤러에 대체가 됩니다.

실행 하는이 속성을 설정 합니다.

``` powershell
Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow (new-timespan -Minutes 30) -ExtranetLockoutRequirePDC $false
```
### <a name="enable-log-only-mode"></a>로그 전용 모드를 사용 하도록 설정

로그 전용 모드에서 AD FS 보안 감사 이벤트를 기록 하며 모든 요청을 차단 하지 않습니다 사용자 친숙 한 위치 정보를 채웁니다. 이 모드는 스마트 잠금 실행 되 고 AD를 사용 하도록 설정 하려면 사용자에 대 한 친숙 한 위치를 사용 하도록 설정 하기 전에 "알아보려면" FS "강제 적용" 모드는 유효성 검사에 사용 됩니다. AD FS 학습 하는 대로 저장 사용자별 로그인 작업 (로그 전용 모드에서 든 또는 강제 적용 모드).
다음 commandlet을 실행 함으로써만 기록할 잠금 동작을 설정 합니다.  

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartlockoutLogOnly`

로그 전용 모드는 임시 상태 시스템의 스마트 잠금 동작을 사용 하 여 잠금 적용을 소개 하기 전에 로그인 동작을 알 수 있도록 할 것입니다. 로그 전용 모드에 대 한 권장 되는 기간에는 3 ~ 7 일입니다. 계정이 있으면 적극적으로 공격을 받고, 24 시간 동안 최소 로그 전용 모드를 실행 해야 합니다.

AD FS 2016에서 엑스트라넷 잠금 사용 하기 전에 2012R2 ' 엑스트라넷 소프트 잠금 ' 동작을 사용 하는 경우 로그 전용 모드는 사용 안 함 ' 엑스트라넷 소프트 잠금 ' 동작 AD FS에 대 한 스마트 잠금 로그 전용 모드의 사용자를 잠그지 않음. 그러나 온-프레미스 AD AD 구성에 따라 사용자를 잠글 수 있습니다. 자세한 AD 잠금 정책을 검토 하세요 어떻게 온-프레미스 AD 잠금 사용자 수 있습니다.

AD FS 2019에 추가 점으로 손꼽을 하는 것을 계속 사용 하 여 이전 소프트 잠금 동작을 적용 하는 동안 스마트 잠금에 대 한 로그 전용 모드를 사용 하도록 설정할 수는 아래 Powershell.

`Set-AdfsProperties -ExtranetLockoutMode 3`

적용 하려면 새 모드에서는 팜의 모든 노드에서 AD FS 서비스를 다시 시작

`Restart-service adfssrv`

EnableExtranetLockout 매개 변수를 사용 하 여 스마트 잠금 모드를 구성 되 면 설정할 수 있습니다.

`Set-AdfsProperties -EnableExtranetLockout $true`

### <a name="enable-enforce-mode"></a>강제 적용 모드 사용

잠금 임계값 및 관찰 창에 익숙해지면 후 ESL 모드를 다음 PSH cmdlet을 사용 하 여 "적용" 이동할 수 있습니다.

`Set-AdfsProperties -ExtranetLockoutMode AdfsSmartLockoutEnforce`

적용 하려면 새 모드의 경우 다음 명령을 사용 하 여 팜의 모든 노드에서 AD FS 서비스를 다시 시작 합니다.

`Restart-service adfssrv`

## <a name="manage-user-account-activity"></a>사용자 계정 활동 관리
AD FS 계정 활동 데이터를 관리 하기 위한 세 가지 cmdlet을 제공 합니다. 이러한 cmdlet 마스터 역할을 보유 하는 노드에 자동으로 연결 합니다.
>[!NOTE]
>계정 잠금 다시 설정 하려면 AD FS commandlet 위임할 관리 JEA (just Enough)를 사용할 수 있습니다. 예를 들어 헬프 데스크 직원 ESL commandlet을 사용 하는 위임 된 권한을 수 있습니다. 이러한 cmdlet을 사용 하 여에 대 한 권한을 위임에 대 한 내용은 참조 [대리자 AD FS Powershell Commandlet에 대 한 액세스 비관리자 사용자](delegate-ad-fs-pshell-access.md)

전달 하 여이 동작을 재정의할 수 있습니다-Server 매개 변수입니다.

- Get-ADFSAccountActivity -UserPrincipalName

  사용자 계정에 대 한 현재 계정 활동을 읽습니다. Cmdlet는 항상 자동으로 계정 활동 REST 끝점을 사용 하 여 팜 마스터에 연결 합니다. 따라서 모든 데이터 항상 일치 해야 합니다.

`Get-ADFSAccountActivity user@contoso.com`

  속성:
    - BadPwdCountFamiliar: 알려진된 위치에서 인증을 성공적으로 증가 합니다.
    - BadPwdCountUnknown: 알 수 없는 위치에서 인증을 성공적으로 수행 되지 때 증가 합니다.
    - LastFailedAuthFamiliar: LastFailedAuthUnknown 실패 한 인증의 시간으로 설정 되어 친숙 한 위치에서 인증 성공 하지 못한 경우
    - LastFailedAuthUnknown: 알 수 없는 위치에서 인증에 성공 하지 LastFailedAuthUnknown 실패 한 인증의 시간으로 설정 됩니다.
    - FamiliarLockout: 됩니다 "True"를 부울 값 "BadPwdCountFamiliar" > ExtranetLockoutThreshold
    - UnknownLockout: 됩니다 "True"를 부울 값 "BadPwdCountUnknown" > ExtranetLockoutThreshold  
    - FamiliarIPs: 최대 20 개 Ip는 사용자에 대해 잘 알고 있습니다. 이 값을 초과 하는 경우 가장 오래 된 IP 목록에서 제거 됩니다.
-    Set-ADFSAccountActivity

     새 친숙 한 위치를 추가합니다. 친숙 한 IP 목록에 최대 20 개의 항목의이 값을 초과 하는 경우 가장 오래 된 IP 목록에서 제거 됩니다.

`Set-ADFSAccountActivity user@contoso.com -AdditionalFamiliarIps “1.2.3.4”`

- Reset-ADFSAccountLockout

  사용자 계정에 대 한 각 친숙 한 위치 (badPwdCountFamiliar) 잠금 또는 알 수 없는 위치 카운터 (badPwdCountUnfamiliar)를 다시 설정합니다. 카운터를 다시 설정 하 여 "FamiliarLockout" 또는 "UnfamiliarLockout" 값을 업데이트 됩니다, 재설정 카운터 임계값 보다 작아야 합니다.  

`Reset-ADFSAccountLockout user@contoso.com -Location Familiar`
`Reset-ADFSAccountLockout user@contoso.com -Location Unknown`

## <a name="event-logging--user-activity-information-for-ad-fs-extranet-lockout"></a>이벤트 로깅 및 AD FS 엑스트라넷 잠금에 대 한 사용자 작업 정보

### <a name="connect-health"></a>Connect Health
Connect Health를 통해 사용자 계정 작업을 모니터링 하는 방법이 권장된 됩니다. 연결 상태 위험한 Ip에 대 한 다운로드 가능한 보고를 생성 하 고 잘못 된 암호 시도 합니다. 위험한 IP 보고서의 각 항목에는 실패 한 AD FS 로그인 활동이 지정 된 임계값을 초과 하는 방법에 대 한 집계 정보가 표시 됩니다. 전자 메일 알림은 사용자 지정 가능한 이메일 설정을 사용 하 여 발생 하는 즉시 관리자에 게 경고를 설정할 수 있습니다. 추가 정보 및 설치 지침을 방문 합니다 [Connect Health 설명서](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-health-adfs)합니다.

### <a name="ad-fs-extranet-smart-lockout-events"></a>AD FS 엑스트라넷 잠금 이벤트입니다.
기록할 엑스트라넷 잠금 이벤트에 대 한 ESL '적용' 또는 ' 로그 전용 ' 모드에서 활성화 해야 하며 ADFS 보안 감사를 사용할 수 있습니다.
AD FS 엑스트라넷 잠금 이벤트는 보안 감사 로그에 작성 합니다.
- 사용자가 차단 하는 경우 아웃 (실패 한 로그인 시도 대 한 잠금 임계값에 도달)
- AD FS 잠금 상태에서 이미 사용자에 대 한 로그인 시도 수신 하는 경우

로그 전용 모드에서 작업 하는 동안 잠금 이벤트에 대 한 보안 감사 로그를 확인할 수 있습니다. 찾을 수 있는 이벤트에 대 한 잠금이 발생 한 경우 두 번 확인 하는 친숙 한 또는 알 수 없는 IP 주소에서 해당 사용자에 대 한 친숙 한 IP 주소 목록을 결정할 ADFSAccountActivity Get cmdlet을 사용 하 여 사용자 상태를 확인할 수 있습니다.


|이벤트 ID|설명|
|-----|-----|
|1203|잘못 된 암호를 시도할 때마다이 이벤트가 기록 됩니다. badPwdCount ExtranetLockoutThreshold 지정 된 값에 도달 하면 즉시 계정이 잠깁니다 ADFS에서 ExtranetObservationWindow에 지정 된 기간에 대 한 합니다.</br>작업 ID: %1</br>XML: %2|
|1201|이 이벤트는 사용자 때마다 잠겨 기록 됩니다. </br>작업 ID: %1</br>XML: %2|
|557 (ADFS 2019)| 노드 %1에 계정 저장소 rest 서비스와 통신 하는 동안 오류가 발생 했습니다. WID 팜의 경우 주 노드가 오프 라인일 수 있습니다. 이 경우 ADFS SQL 팜 사용자 저장소 마스터 역할을 호스트에 새 노드를 자동으로 선택 됩니다.|
|562 (ADFS 2019)|오류가 발생 했습니다. 계정 사용 하 여 communcating %1 서버의 끝점을 저장 하는 경우.</br>예외 메시지: %2|
|563 (ADFS 2019)|엑스트라넷 잠금 상태를 계산 하는 동안 오류가 발생 했습니다. 이 사용자에 대해 허용 됩니다 인증 설정 %1 값 하 고 토큰 발급 계속 됩니다. WID 팜의 경우 주 노드가 오프 라인일 수 있습니다. 이 경우 ADFS SQL 팜 사용자 저장소 마스터 역할을 호스트에 새 노드를 자동으로 선택 됩니다.</br>계정 저장소 서버 이름: %2</br>사용자 Id: %3</br>예외 메시지: %4|
|512|다음 사용자의 계정이 잠겼습니다. 로그인 시도 사용 하는 시스템 구성 했기 때문에 허용 됩니다.</br>작업 ID: %1 </br>사용자: %2 </br>클라이언트 IP: %3 </br>잘못 된 암호 수: %4  </br>잘못 된 암호 시도가 마지막: %5|
|515|잠긴된 상태 였던 사용자 계정 및 올바른 암호를 제공한 것입니다. 이 계정이 손상 될 수 있습니다.</br>추가 데이터 </br>작업 ID: %1 </br>사용자: %2 </br>클라이언트 IP: %3 |
|516|사용자 계정으로 잘못 된 암호로 너무 많이 시도 하면 인해 잠 궜 습니다.</br>작업 ID: %1  </br>사용자: %2  </br>클라이언트 IP: %3  </br>잘못 된 암호 수: %4  </br>잘못 된 암호 시도가 마지막: %5|

## <a name="esl-frequently-asked-questions"></a>ESL에 대 한 질문과 대답

**엑스트라넷 잠금에 사용 하 여 ADFS 팜 모드 적용 악의적인 사용자가 잠금을 확인할 수 있습니까?** 

A: 경우 ADFS에 대 한 잠금 정보는 표시 되지 것입니다 (brute force) 또는 서비스 거부가 잠겨 합법적인 사용자의 계정이 다음 모드를 '적용'으로 설정 됩니다. 악의적인 계정 잠금에 사용자가 로그인 하지 못할 수 있습니다 하는 유일한 방법은 되었거나 경우 악의적 행위자 사용자 암호가 해당 사용자에 대 한 알려진된 좋은 (친숙 한) IP 주소에서 요청을 보낼 수 있습니다. 

**ESL가 활성화 되어 있고 잘못 된 행위자 사용자 암호를 어떻게 되나요?** 

A: 무차별 공격 시나리오의 일반적인 목표는 암호를 추측 하 고 성공적으로 로그인 하는 것입니다.  사용자가 피싱 또는 암호를 추측 된 경우 다음 ESL 기능을 차단 하지 않습니다 액세스 이후 로그인에는 올바른 암호와 새 IP "성공" 조건을 충족 됩니다. 믿지 못할 자 IP는 다음 "익숙한"으로 표시 됩니다. 이 시나리오에서 가장 좋은 완화에는 ad FS의 사용자 활동의 선택을 취소 하 고 사용자에 대 한 다단계 인증을 요구 하도록입니다. 시스템으로 추측할 수 있는 암호를 얻지 못하는 보장 하는 AAD 암호 보호를 설치 하는 것이 좋습니다.

**내 사용자가 되지 성공적으로 로그인 ip에서 하 고 다음 잘못 된 암호를 사용 하 여 시도 몇 번 경우 될 로그인 할 마지막 입력 암호가 잘못 되 면?** 

A: 사용자 (즉, 합법적인 방식으로 입력 잘못) 여러 개의 잘못 된 암호를 제출 하는 경우에 다음 시도가 잘못 된 암호를 가져옵니다 하 고 사용자 로그인을 즉시 성공 합니다.  잘못 된 암호 수를 지우고 추가 FamiliarIPs 목록에 해당 IP입니다.  그러나 알 수 없는 위치에서 로그인 실패 임계값 이동, 잠금 상태로 입력할 것 및 과거 관찰 창 및 로그인 올바른 암호로 기다리거나 해당 계정을 다시 설정 하려면 관리자가 개입 해야 하는 데 필요한 됩니다.  

**ESL 작동 인트라넷에 너무?**   
A: 클라이언트 웹 응용 프로그램 프록시 서버 통해서가 아닌 ADFS 서버에 직접 연결 하는 경우 ESL 동작이 적용 되지 않습니다. 

**클라이언트 IP 필드에 Microsoft IP 주소를 표시 합니다. 않습니다 ESL 블록 EXO 프록시 무차별 암호 대입 공격?**  

A: ESL은 Exchange Online 또는 다른 레거시 인증 무차별 공격 시나리오를 방지 하는 잘 작동 합니다. 레거시 인증 00000000-0000-0000-0000-000000000000 "활동 ID"가 있습니다. 이러한 공격에서는 잘못 된 행위자 클라이언트 IP 주소 하나를 Microsoft로 표시 되도록 Exchange Online 기본 인증 (레거시 인증이 라고도 함)를 활용 하 고는 합니다. 클라우드 프록시 인증 확인 하는 Outlook 클라이언트를 대신 하 여 Exchange online 서버. 이러한 시나리오에서는 악의적인 제출자의 IP 주소 x-ms-전달-클라이언트-ip 및 IP ms 클라이언트 ip x 값에 포함 될 Microsoft Exchange Online 서버 됩니다.
엑스트라넷 잠금 Ip의 x-전달-클라이언트-IP 및 ms 클라이언트 ip x 값을 전달 하는 네트워크 Ip 확인 합니다. 요청이 성공 하면 모든 Ip는 친숙 한 목록에 추가 됩니다. 요청이 들어오면 및 제공 된 Ip의 모든 친숙 한 목록에 없는 경우 다음 요청이 표시 됩니다으로 알 수 없는 합니다. 친숙 한 사용자는 알 수 없는 위치에서 요청을 차단할지 동안 성공적으로 로그인 할 수 됩니다.  


## <a name="additional-references"></a>추가 참조  
[Active Directory Federation Services 보안에 대 한 모범 사례](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-AdfsProperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
