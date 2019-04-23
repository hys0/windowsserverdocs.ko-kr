---
title: VPN에 항상 하는 DirectAccess에서 마이그레이션
description: DirectAccess에서 Always On VPN로 마이그레이션 발생 순서가 마이그레이션 단계를 수행 하는 경합을 최소화 하는 데 도움이 되는 클라이언트를 마이그레이션할 특정 프로세스에 필요 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 06/07/2018
ms.openlocfilehash: 94852b33936ece0b329614f428e845f2c7a2ac6a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854584"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Always On VPN 마이그레이션 및 DirectAccess 해제

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

&#171;[ **이전:** Always On VPN 마이그레이션에 대 한 DirectAccess 계획](da-always-on-migration-planning.md)<br>

DirectAccess에서 Always On VPN로 마이그레이션 발생 순서가 마이그레이션 단계를 수행 하는 경합을 최소화 하는 데 도움이 되는 클라이언트를 마이그레이션할 특정 프로세스에 필요 합니다. 마이그레이션 프로세스 높은 수준에서 이러한 네 가지 기본 단계로 구성 됩니다.

1.  **Side-by-side-VPN 인프라를 배포 합니다.** 배포에 포함 하려는 기능과 마이그레이션 단계에 확인 한 후에 기존 DirectAccess 인프라와 함께 VPN 인프라를 배포 합니다.  

2.  **클라이언트 인증서 및 구성을 배포 합니다.**  VPN 인프라 준비 되 면 만들고 클라이언트에 필요한 인증서를 게시 합니다. 클라이언트 인증서를 받은 경우 VPN_Profile.ps1 구성 스크립트를 배포 합니다. 또는 VPN 클라이언트를 구성 하려면 Intune을 사용할 수 있습니다. Microsoft System Center Configuration Manager 또는 Microsoft Intune을 사용 하 여 성공적인 VPN 구성 배포를 모니터링 합니다.

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

마이그레이션 프로세스를 DirectAccess에서 Always On VPN을 시작 하기 전에 마이그레이션을 계획 해야 합니다.  마이그레이션 계획 하지, 참조 [Always On VPN 마이그레이션에 대 한 DirectAccess 계획](da-always-on-migration-planning.md)합니다.

>[!TIP] 
>이 섹션에서는 Always On VPN에 대 한 단계별 배포 가이드 되지 않지만 보완 하기 위해 [Always On VPN 배포에 대 한 Windows Server 및 Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) 마이그레이션 관련 배포 지침을 제공 합니다.

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>Side-by-side-VPN 인프라를 배포 합니다.

기존 DirectAccess 인프라와 함께 VPN 인프라를 배포할 수 있습니다.  단계별 세부 정보를 참조 하세요 [Always On VPN 배포에 대 한 Windows Server 및 Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) 를 설치 하 여 Always On VPN 인프라를 구성 합니다. 

Side-by-side-배포는 다음과 같은 개략적인 작업 이루어져 있습니다.

1.  VPN 사용자, VPN 서버 및 NPS 서버 그룹을 만듭니다.

2.  페이지를 만들고 필요한 인증서 템플릿을 게시 합니다.

3.  서버 인증서를 등록 합니다.

4.  설치 하 고 Always On VPN에 대 한 원격 액세스 서비스를 구성 합니다.

5.  설치 하 고 NPS를 구성 합니다.

6.  Always On VPN에 대 한 DNS 및 방화벽 규칙을 구성 합니다.

다음 이미지는 DirectAccess-에-Always On VPN 마이그레이션 전체 인프라 변경에 대 한 시각적 참조를 제공합니다.

![](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>인증서 및 VPN 구성 스크립트를 클라이언트에 배포

있지만의 VPN 클라이언트 구성의 대부분을 [배포 Always On VPN](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md) 섹션을 두 개의 추가 DirectAccess에서 Always On VPN로의 마이그레이션을 완료 하는 데 필요한 단계입니다. 

되도록 해야 합니다는 **VPN_Profile.ps1** 제공 됩니다 _후_ VPN 클라이언트 하지 않고 연결을 시도 하지 않습니다 있도록 인증서가 발급 되었습니다. 이렇게 하려면 인증서에서 Always On VPN 구성을 배포 하는 데 사용할 수 있는 VPN 배포 준비 그룹으로 등록 하는 사용자를 추가 하는 스크립트를 실행할 수 있습니다.

>[!NOTE] 
>이 프로세스에 사용자 마이그레이션 링 중 하나에서 수행 하기 전에 테스트 하는 것이 좋습니다.

1.  **게시 VPN 인증서를 만들고 자동 등록 그룹 정책 개체 (GPO)를 사용 하도록 설정 합니다.** 기존의 인증서 기반 Windows 10 VPN 배포에 대 한 인증서는 연결을 인증할 수 있도록 사용자 또는 장치에 발급 됩니다. 새 인증서를 만들고 자동 등록에 대 한 게시를 만들고 해야 VPN 사용자 그룹에 구성 된 자동 등록 설정을 사용 하 여 GPO를 배포 합니다. 인증서 및 자동 등록을 구성 하는 단계를 참조 하세요 [서버 인프라 구성](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)합니다.

2.  **VPN 사용자 그룹에 사용자를 추가 합니다.** VPN 사용자 그룹에 마이그레이션한 어떤 사용자를 추가 합니다. 마이그레이션한 후 해당 인증서 업데이트 나중에 받을 수 있도록 해당 사용자가 해당 보안 그룹에 남아 있습니다. 계속 모든 사용자를 DirectAccess에서 Always On VPN 이동할 수 있을 때까지이 그룹에 사용자를 추가 합니다. 

3.  **VPN 인증 인증서를 받은 사용자를 식별 합니다.** 클라이언트에 필요한 인증서를 받은 VPN 구성 정보를 받을 준비가 될 때를 식별 하기 위한 메서드를 추가 해야 하므로 DirectAccess에서 마이그레이션하는 합니다. 실행 된 **GetUsersWithCert.ps1** 현재 발급 된 지정 된 AD DS 보안 그룹에 지정 된 템플릿 이름에서 시작 된 nonrevoked 인증서는 사용자를 추가 하는 스크립트입니다. 예를 들어, 실행 후 합니다 **GetUsersWithCert.ps1** 스크립트를 사용자에서에서 발급 된 유효한 인증서가 VPN 인증 인증서 템플릿 VPN 배포 준비 그룹에 추가 됩니다.

    >[!NOTE] 
    >클라이언트에 필요한 인증서를 받을 때 식별 하는 방법을 없는 경우 VPN 연결이 실패를 일으키는 사용자에 게 인증서가 발급 되기 전에 VPN 구성을 배포할 수 있습니다. 이 상황을 방지 하려면 다음을 실행 합니다 **GetUsersWithCert.ps1** 인증 기관에서 또는 VPN 배포 준비 그룹에 인증서를 받은 사용자를 동기화 할 일정에 따라 스크립트 합니다. 다음 System Center Configuration Manager 또는 관리 되는 클라이언트 인증서를 받기 전에 VPN 구성을 수신 하지 않습니다을 보장 하는 Intune에서 VPN 구성 배포를 대상으로 해당 보안 그룹을 사용 합니다.
    
    ### <a name="getuserswithcertps1"></a>GetUsersWithCert.ps1
    
    ```powershell
    Import-module ActiveDirectory
    Import-Module AdcsAdministration
    
    $TemplateName = 'VPNUserAuthentication'##Certificate Template Name (not the friendly name)
    $GroupName = 'VPN Deployment Ready' ##Group you will add the users to
    $CSServerName = 'localhost\corp-dc-ca' ##CA Server Information
    
    $users= @()
    $TemplateID = (get-CATemplate | Where-Object {$_.Name -like $TemplateName} | Select-Object oid).oid
    $View = New-Object -ComObject CertificateAuthority.View
    $NULL = $View.OpenConnection($CSServerName)
    $View.SetResultColumnCount(3)
    $i1 = $View.GetColumnIndex($false, "User Principal Name")
    $i2 = $View.GetColumnIndex($false, "Certificate Template")
    $i3 = $View.GetColumnIndex($false, "Revocation Date")
    $i1, $i2, $i3 | %{$View.SetResultColumn($_) }
    $Row= $View.OpenView()
    
    while ($Row.Next() -ne -1){
    $Cert = New-Object PsObject
    $Col = $Row.EnumCertViewColumn()
    [void]$Col.Next()
    do {
    $Cert | Add-Member -MemberType NoteProperty $($Col.GetDisplayName()) -Value $($Col.GetValue(1)) -Force
          }
    until ($Col.Next() -eq -1)
    $col = ''
    
    if($cert."Certificate Template" -eq $TemplateID -and $cert."Revocation Date" -eq $NULL){
       $users= $users+= $cert."User Principal Name"
    $temp = $cert."User Principal Name"
    $user = get-aduser -Filter {UserPrincipalName -eq $temp} –Property UserPrincipalName
    Add-ADGroupMember $GroupName $user
       }
      }
    ```

4. Always On VPN 구성을 배포 합니다. VPN으로 인증 인증서를 발급을 실행 하는 **GetUsersWithCert.ps1** 스크립트 사용자 VPN 배포 준비 보안 그룹에 추가 됩니다.


| 사용 중인 경우...  | 발생하는 결과 |
| ---- | ---- |
| System Center Configuration Manager | 해당 보안 그룹의 멤버 자격에 따라 사용자 컬렉션을 만듭니다.<br><br>![](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)\!|
| Intune | 이 동기화 되 면 보안 그룹을 직접 대상 하기만 하면 됩니다. |
|
    
실행할 때마다 합니다 **GetUsersWithCert.ps1** 구성 스크립트를 실행 해야 System Center Configuration Manager의 보안 그룹 구성원을 업데이트 하는 AD DS 검색 규칙입니다. 또한 발생 하는지 확인 된 배포 컬렉션 멤버 자격 업데이트 자주 충분히 (스크립트 및 검색 규칙을 사용 하 여 정렬).

System Center Configuration Manager 또는 Intune을 사용 하 여 Always On VPN 클라이언트를 배포 하려면 Windows에 대 한 자세한 내용은 참조 하세요. [Always On VPN 배포에 대 한 Windows Server 및 Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)합니다. 그러나 해야, 이러한 마이그레이션 관련 작업을 통합 합니다.

>[!NOTE] 
>이러한 마이그레이션 관련 작업을 통합 DirectAccess에서 Always On VPN로 마이그레이션하는 간단한 Always On VPN 배포와 중요 한 차이가 합니다. 제대로 배포 가이드에서 메서드를 사용 하는 대신 보안 그룹을 대상으로 컬렉션을 정의 해야 합니다.


## <a name="remove-devices-from-the-directaccess-security-group"></a>DirectAccess 보안 그룹에서 장치 제거

사용자가 인증 인증서를 수신 하며 **VPN_Profile.ps1** 구성 스크립트 표시 System Center Configuration Manager 또는 Intune에서 VPN 구성 스크립트 배포 성공에 해당 합니다. 각 배포 후 DirectAccess를 나중에 제거할 수 있도록 해당 사용자의 장치 DirectAccess 보안 그룹에서 제거 합니다. Intune 및 System Center Configuration Manager는 각 사용자의 장치를 확인할 수 있도록 사용자 장치 할당 정보를 포함 합니다.

>[!NOTE] 
>적용 하는 경우 DirectAccess Gpo 조직 구성 단위 (Ou)를 통해 컴퓨터 그룹 대신 OU에서 사용자의 컴퓨터 개체를 이동 합니다.

## <a name="decommission-the-directaccess-infrastructure"></a>DirectAccess 인프라를 서비스 해제

Always On VPN 모든 DirectAccess 클라이언트 마이그레이션 했으면 DirectAccess 인프라를 서비스 해제할 수 있으며 DirectAccess 설정을 그룹 정책에서 제거할 수 있습니다. 사용자 환경에서 DirectAccess를 정상적으로 제거 하려면 다음 단계를 수행 하는 것이 좋습니다.

1.  [!INCLUDE [remove-config-settings-shortdesc-include](../includes/remove-config-settings-shortdesc-include.md)]

    ![](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

3.  **DNS를 정리 합니다.** 내부 DNS 서버에서 모든 레코드를 제거 해야 및 공용 DNS 서버 관련 DirectAccess를 사용 하면 예를 들어 DA.contoso.com, DAGateway.contoso.com.

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

5.  **Active Directory 인증서 서비스에서 모든 DirectAccess 인증서를 제거 합니다.** 컴퓨터 인증서를 사용 하는 DirectAccess 구현에 대 한 경우 인증 기관 콘솔에서 인증서 템플릿 폴더에서 게시 된 템플릿을 제거 합니다.

## <a name="next-step"></a>다음 단계
완료 하면 DirectAccess에서 Always On VPN로 마이그레이션. 

---