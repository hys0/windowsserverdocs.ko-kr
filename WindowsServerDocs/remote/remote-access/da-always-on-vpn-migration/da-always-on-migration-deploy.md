---
title: DirectAccess에서 Always On VPN으로 마이그레이션
description: DirectAccess에서 Always On VPN으로 마이그레이션하려면 클라이언트를 마이그레이션하기 위한 특정 프로세스가 필요 하며,이를 통해 마이그레이션 단계를 수행 하는 동안 발생 하는 경합 상태를 최소화 하는 데 도움이 됩니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 06/07/2018
ms.openlocfilehash: 2bcbc7030d54e96b4ac120b943cc1adc0513feca
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822644"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Always On VPN 마이그레이션 및 DirectAccess 해제

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

&#171;[ **이전:** VPN 마이그레이션을 Always On DirectAccess 계획](da-always-on-migration-planning.md)<br>

DirectAccess에서 Always On VPN으로 마이그레이션하려면 클라이언트를 마이그레이션하기 위한 특정 프로세스가 필요 하며,이를 통해 마이그레이션 단계를 수행 하는 동안 발생 하는 경합 상태를 최소화 하는 데 도움이 됩니다. 높은 수준에서 마이그레이션 프로세스는 다음과 같은 4 가지 기본 단계로 구성 됩니다.

1.  **Side-by-side VPN 인프라를 배포 합니다.** 마이그레이션 단계와 배포에 포함할 기능을 결정 한 후에는 VPN 인프라를 기존 DirectAccess 인프라와 나란히 배포 합니다.  

2.  **인증서 및 구성을 클라이언트에 배포 합니다.**  VPN 인프라가 준비 되 면 필요한 인증서를 만들어 클라이언트에 게시 합니다. 클라이언트에서 인증서를 받은 경우 VPN_Profile. ps1 구성 스크립트를 배포 합니다. 또는 Intune을 사용 하 여 VPN 클라이언트를 구성할 수 있습니다. Microsoft Endpoint Configuration Manager 또는 Microsoft Intune를 사용 하 여 성공적인 VPN 구성 배포를 모니터링할 수 있습니다.

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

DirectAccess에서 Always On VPN으로 마이그레이션 프로세스를 시작 하기 전에 마이그레이션을 계획 해야 합니다.  마이그레이션을 계획 하지 않은 경우 [ALWAYS ON VPN 마이그레이션을 위한 DirectAccess 계획](da-always-on-migration-planning.md)을 참조 하세요.

>[!TIP] 
>이 섹션은 Always On VPN에 대 한 단계별 배포 가이드는 아니지만 [Windows Server 및 windows 10 용 Vpn 배포를 Always On](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) 보완 하 고 마이그레이션 관련 배포 지침을 제공 하기 위한 것입니다.

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>Side-by-side VPN 인프라 배포

VPN 인프라를 기존 DirectAccess 인프라와 나란히 배포 합니다.  단계별 세부 정보는 Always On VPN 인프라를 설치 하 고 구성 하는 [Windows Server 및 windows 10에 대 한 ALWAYS ON Vpn 배포](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) 를 참조 하세요. 

병렬 배포는 다음과 같은 개략적인 작업으로 구성 됩니다.

1.  VPN 사용자, VPN 서버 및 NPS 서버 그룹을 만듭니다.

2.  필요한 인증서 템플릿을 만들고 게시 합니다.

3.  서버 인증서를 등록 합니다.

4.  Always On VPN에 대 한 원격 액세스 서비스를 설치 하 고 구성 합니다.

5.  NPS를 설치 하 고 구성 합니다.

6.  Always On VPN에 대 한 DNS 및 방화벽 규칙을 구성 합니다.

다음 이미지는 DirectAccess에서 Always On VPN 마이그레이션을 통해 인프라 변경에 대 한 시각적 참조를 제공 합니다.

![](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>클라이언트에 인증서 및 VPN 구성 스크립트 배포

[ALWAYS ON Vpn 배포](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md) 섹션에 있는 대부분의 vpn 클라이언트 구성에서는 DirectAccess에서 Always On VPN으로의 마이그레이션을 완료 하는 데 두 가지 추가 단계가 필요 합니다. 

VPN 클라이언트가 해당 인증서를 사용 하지 않고 연결을 시도 하지 않도록 인증서를 발급 _한 후_ 에 **VPN_Profile.** p s 1을 사용 하는지 확인 해야 합니다. 이렇게 하려면 인증서에 등록 된 사용자만 VPN 배포 준비 그룹에 추가 하는 스크립트를 실행 합니다 .이 그룹은 Always On VPN 구성을 배포 하는 데 사용 됩니다.

>[!NOTE] 
>사용자 마이그레이션 링에서이 프로세스를 수행 하기 전에이 프로세스를 테스트 하는 것이 좋습니다.

1.  **VPN 인증서를 만들어 게시 하 고 자동 등록 그룹 정책 개체 (GPO)를 사용 하도록 설정 합니다.** 기존의 인증서 기반 Windows 10 VPN 배포의 경우 연결을 인증할 수 있도록 장치 또는 사용자에 게 인증서가 발급 됩니다. 자동 등록을 위해 새 인증 인증서를 만들고 게시 하는 경우 VPN 사용자 그룹에 구성 된 자동 등록 설정을 사용 하 여 GPO를 만들고 배포 해야 합니다. 인증서 및 자동 등록을 구성 하는 단계는 [서버 인프라 구성](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)을 참조 하세요.

2.  **VPN 사용자 그룹에 사용자를 추가 합니다.** 마이그레이션할 사용자를 VPN 사용자 그룹에 추가 합니다. 이러한 사용자는 나중에 인증서 업데이트를 받을 수 있도록 마이그레이션한 후 해당 보안 그룹에 유지 됩니다. DirectAccess의 모든 사용자를 Always On VPN으로 이동할 때까지이 그룹에 사용자를 계속 추가 합니다. 

3.  **VPN 인증 인증서를 받은 사용자를 식별 합니다.** DirectAccess에서 마이그레이션하는 경우 클라이언트가 필요한 인증서를 수신 하 고 VPN 구성 정보를 받을 준비가 되었을 때를 식별 하는 메서드를 추가 해야 합니다. **Getusers Withcert.** p s 1을 실행 하 여 지정 된 템플릿 이름에서 현재 해지 되지 않은 인증서를 발급 한 사용자를 지정 된 AD DS 보안 그룹에 추가 합니다. 예를 들어 **Getusers Withcert.** p s 1 스크립트를 실행 한 후 Vpn 인증 인증서 템플릿에서 올바른 인증서를 발급 한 모든 사용자가 Vpn 배포 준비 그룹에 추가 됩니다.

    >[!NOTE] 
    >클라이언트에서 필요한 인증서를 받은 시기를 식별할 수 있는 방법이 없는 경우 인증서가 사용자에 게 발급 되기 전에 VPN 구성을 배포할 수 있습니다 .이로 인해 VPN 연결이 실패 합니다. 이러한 상황을 방지 하려면 인증 기관 또는 일정에 따라 **Getusers Withcert.** p s 1 스크립트를 실행 하 여 인증서를 받은 사용자를 VPN 배포 준비 그룹에 동기화 합니다. 그런 다음 해당 보안 그룹을 사용 하 여 Microsoft Endpoint Configuration Manager 또는 Intune에서 VPN 구성 배포를 대상으로 합니다. 그러면 관리 되는 클라이언트가 인증서를 받기 전에 VPN 구성을 받지 않게 됩니다.
    
    ### <a name="getuserswithcertps1"></a>Getusers Withcert. ps1
    
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

4. Always On VPN 구성을 배포 합니다. VPN 인증 인증서를 발급 하 고 **Getusers Withcert.** p s 1 스크립트를 실행 하면 사용자가 Vpn 배포 준비 보안 그룹에 추가 됩니다.


| 다음을 사용 하는 경우 ...  | 발생하는 결과 |
| ---- | ---- |
| Configuration Manager | 해당 보안 그룹의 멤버 자격을 기반으로 사용자 컬렉션을 만듭니다.<br><br>![](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)\!|
| Intune | 동기화 된 후에는 보안 그룹을 직접 대상으로 합니다. |
|
    
**Getusers Withcert. ps1** 구성 스크립트를 실행할 때마다 AD DS 검색 규칙을 실행 하 여 Configuration Manager의 보안 그룹 멤버 자격을 업데이트 해야 합니다. 또한 배포 컬렉션에 대 한 멤버 자격 업데이트가 충분히 자주 발생 하는지 확인 합니다 (스크립트 및 검색 규칙과 맞춤).

Configuration Manager 또는 Intune을 사용 하 여 Windows 클라이언트에 Always On VPN을 배포 하는 방법에 대 한 자세한 내용은 [Windows Server 및 windows 10 용 Vpn 배포 Always On](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)를 참조 하세요. 그러나 이러한 마이그레이션 관련 작업을 통합 해야 합니다.

>[!NOTE] 
>이러한 마이그레이션 관련 작업을 통합 하는 것은 간단한 Always On VPN 배포와 DirectAccess에서 Always On VPN으로의 마이그레이션 사이에 중요 한 차이점입니다. 배포 가이드에서 메서드를 사용 하는 대신 보안 그룹을 대상으로 하는 컬렉션을 올바르게 정의 해야 합니다.


## <a name="remove-devices-from-the-directaccess-security-group"></a>DirectAccess 보안 그룹에서 장치 제거

사용자가 인증 인증서와 **VPN_Profile.** p s 1 구성 스크립트를 수신 하면 Configuration Manager 또는 Intune에 해당 하는 성공적인 VPN 구성 스크립트 배포가 표시 됩니다. 각 배포 후에 directaccess 보안 그룹에서 해당 사용자의 장치를 제거 하 여 나중에 DirectAccess를 제거할 수 있도록 합니다. Intune 및 Configuration Manager에는 각 사용자의 장치를 결정 하는 데 도움이 되는 사용자 장치 할당 정보가 포함 되어 있습니다.

>[!NOTE] 
>컴퓨터 그룹이 아닌 Ou (조직 구성 단위)를 통해 DirectAccess Gpo를 적용 하는 경우 사용자의 컴퓨터 개체를 OU 외부로 이동 합니다.

## <a name="decommission-the-directaccess-infrastructure"></a>DirectAccess 인프라 서비스 해제

모든 DirectAccess 클라이언트를 Always On VPN으로 마이그레이션하는 작업이 완료 되 면 DirectAccess 인프라를 서비스 해제 하 고 그룹 정책에서 DirectAccess 설정을 제거할 수 있습니다. 환경에서 DirectAccess를 정상적으로 제거 하려면 다음 단계를 수행 하는 것이 좋습니다.

1.  [!INCLUDE [remove-config-settings-shortdesc-include](../includes/remove-config-settings-shortdesc-include.md)]

    ![](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

3.  **DNS를 정리 합니다.** 내부 DNS 서버 및 DirectAccess와 관련 된 공용 DNS 서버 (예: DA.contoso.com, DAGateway.contoso.com)의 모든 레코드를 제거 해야 합니다.

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

5.  **Active Directory 인증서 서비스에서 DirectAccess 인증서를 제거 합니다.** DirectAccess 구현에 컴퓨터 인증서를 사용한 경우 인증 기관 콘솔의 인증서 템플릿 폴더에서 게시 된 템플릿을 제거 합니다.

## <a name="next-step"></a>다음 단계
DirectAccess에서 Always On VPN으로 마이그레이션하는 작업을 완료 했습니다. 

---