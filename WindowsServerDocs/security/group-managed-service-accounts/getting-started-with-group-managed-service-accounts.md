---
title: 관리 서비스 계정 그룹 시작하기
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-gmsa
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 52456b8027196f20c4ca52a08bcd7f7bba92eb82
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856996"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>관리 서비스 계정 그룹 시작하기

>적용 대상: Windows Server(반기 채널), Windows Server 2016


이 가이드에서는 Windows Server 2012에서 그룹 관리 서비스 계정을 사용 하도록 설정 하 고 사용 하는 방법에 대 한 단계별 지침 및 배경 정보를 제공 합니다.

**이 문서의**

-   [필수 구성 요소](#BKMK_Prereqs)

-   [소개](#BKMK_Intro)

-   [새 서버 팜 배포](#BKMK_DeployNewFarm)

-   [기존 서버 팜에 구성원 호스트 추가](#BKMK_AddMemberHosts)

-   [그룹 관리 서비스 계정 속성 업데이트](#BKMK_Update_gMSA)

-   [기존 서버 팜에서 구성원 호스트 서비스 해제](#BKMK_DecommMemberHosts)


> [!NOTE]
> 이 항목에는 설명된 일부 절차를 자동화하는 데 사용할 수 있는 예제 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.

## <a name="prerequisites"></a><a name="BKMK_Prereqs"></a>사전
이 항목의 [그룹 관리 서비스 계정에 대한 요구 사항](#BKMK_gMSA_Req) 섹션을 참조하세요.

## <a name="introduction"></a><a name="BKMK_Intro"></a>간략하게
클라이언트 컴퓨터가 NLB(네트워크 부하 분산) 또는 모든 서버가 클라이언트에 동일한 서비스로 표시되는 다른 방법을 사용하여 서버 팜에서 호스트되는 서비스에 연결한 경우, 서비스의 모든 인스턴스에서 동일한 보안 주체를 사용하지 않는 한 Kerberos와 같은 상호 인증을 지원하는 인증 프로토콜을 사용할 수 없습니다. 이는 각 서비스에서 동일한 암호/키를 사용하여 ID를 증명해야 함을 의미합니다.

> [!NOTE]
> 장애 조치(failover) 클러스터는 gMSA를 지원하지 않습니다. 그러나 클러스터 서비스를 기반으로 실행되는 서비스가 Windows 서비스, 응용 프로그램 풀 또는 예약된 작업이거나 기본적으로 gMSA 또는 sMSA를 지원하는 경우에는 gMSA 또는 sMSA를 사용할 수 있습니다.

서비스에서 선택할 수 있는 보안 주체는 다음과 같으며, 각각 특정 제한 사항이 있습니다.

|보안 주체|범위|지원되는 서비스|암호 관리|
|-------|-----|-----------|------------|
|Windows 시스템의 컴퓨터 계정|도메인|도메인 가입 서버 하나로 제한|컴퓨터에서 관리|
|Windows 시스템이 없는 컴퓨터 계정|도메인|모든 도메인 가입 서버|없음|
|가상 계정|로컬|서버 하나로 제한|컴퓨터에서 관리|
|Windows 7 독립 실행형 관리 서비스 계정|도메인|도메인 가입 서버 하나로 제한|컴퓨터에서 관리|
|사용자 계정|도메인|모든 도메인 가입 서버|없음|
|그룹 관리 서비스 계정|도메인|모든 Windows Server 2012 도메인 가입 서버|도메인 컨트롤러에서 관리하고 호스트에서 검색|

Windows 컴퓨터 계정이나 Windows 7 sMSA(독립 실행형 관리 서비스 계정) 또는 가상 계정은 여러 시스템에서 공유할 수 없습니다. 서버 팜의 서비스에서 공유할 계정 하나를 구성하려면 Windows 시스템과 별개인 사용자 계정 또는 컴퓨터 계정을 선택해야 합니다. 그러나 이러한 계정에는 단일 제어 지점 암호 관리 기능이 없습니다. 따라서 각 조직에서 Active Directory의 서비스에 대한 키를 업데이트하는 고가의 솔루션을 만든 다음 이러한 서비스의 모든 인스턴스에 배포해야 하는 문제가 있습니다.

Windows Server 2012에서는 서비스 또는 서비스 관리자가 gMSA (그룹 관리 서비스 계정)를 사용할 때 서비스 인스턴스 간의 암호 동기화를 관리할 필요가 없습니다. AD에서 gMSA를 프로비전한 다음 관리 서비스 계정을 지원하는 서비스를 구성하면 됩니다. Active Directory 모듈의 일부인 *-ADServiceAccount cmdlet을 사용하여 gMSA를 프로비전할 수 있습니다. 호스트의 서비스 ID 구성은 다음에서 지원됩니다.

-   sMSA와 동일한 API(따라서 sMSA를 지원하는 제품은 gMSA를 지원함)

-   서비스 제어 관리자를 사용하여 로그온 ID를 구성하는 서비스

-   애플리케이션 풀에 IIS 관리자를 사용하여 ID를 구성하는 서비스

-   작업 스케줄러를 사용하는 작업

### <a name="requirements-for-group-managed-service-accounts"></a><a name="BKMK_gMSA_Req"></a>그룹 관리 서비스 계정에 대 한 요구 사항
다음 표에는 gMSA를 사용하는 서비스에서 Kerberos 인증을 사용하기 위한 운영 체제 요구 사항이 나와 있습니다. Active Directory 요구 사항은 이 표 다음에 설명되어 있습니다.

64비트 아키텍처에서는 그룹 관리 서비스 계정을 관리하는 데 사용되는 Windows PowerShell 명령을 실행해야 합니다.

**운영 체제 요구 사항**

|요소|요구 사항|운영 체제|
|------|--------|----------|
|클라이언트 응용 프로그램 호스트|RFC 호환 Kerberos 클라이언트|Windows XP 이상|
|사용자 계정의 도메인 Dc|RFC 호환 KDC|Windows Server 2003 이상|
|공유 서비스 구성원 호스트|| Windows Server 2012 |
|구성원 호스트의 도메인 Dc|RFC 호환 KDC|Windows Server 2003 이상|
|gMSA 계정의 도메인 Dc| 호스트에서 암호를 검색 하는 데 사용할 수 있는 Windows Server 2012 Dc|Windows server 2012 이전 버전의 시스템을 가질 수 있는 Windows Server 2012 도메인 |
|백 엔드 서비스 호스트|RFC 호환 Kerberos 애플리케이션 서버|Windows Server 2003 이상|
|백 엔드 서비스 계정의 도메인 Dc|RFC 호환 KDC|Windows Server 2003 이상|
|Active Directory용 Windows PowerShell|원격 관리 컴퓨터에서 64비트 아키텍처를 지원(예: 원격 서버 관리 도구 키트 사용)하는 컴퓨터에 로컬로 설치된 Active Directory용 Windows PowerShell| Windows Server 2012 |

**Active Directory 도메인 서비스 요구 사항**

-   GMSA를 만들려면 gMSA 도메인 포리스트의 Active Directory 스키마를 Windows Server 2012로 업데이트 해야 합니다.

    Windows server 2012를 실행 하는 도메인 컨트롤러를 설치 하거나 Windows Server 2012를 실행 하는 컴퓨터에서 버전의 adprep.exe를 실행 하 여 스키마를 업데이트할 수 있습니다. CN=Schema,CN=Configuration,DC=Contoso,DC=Com 개체의 object-version 특성 값은 52여야 합니다.

-   프로비전된 새 gMSA 계정

-   gMSA를 사용할 서비스 호스트 권한을 그룹별로 관리하는 경우 새 보안 그룹 또는 기존 보안 그룹

-   서비스 액세스 제어를 그룹별로 관리하는 경우 새 보안 그룹 또는 기존 보안 그룹

-   Active Directory의 첫 번째 마스터 루트 키가 도메인에 배포되지 않았거나 생성되지 않은 경우 이 키를 만듭니다. 만들기 결과는 KdsSvc 작업 로그에서 이벤트 ID 4004를 통해 확인할 수 있습니다.

키를 만드는 방법에 대 한 지침은 [키 배포 서비스 KDS 루트 키 만들기](create-the-key-distribution-services-kds-root-key.md)를 참조 하세요. Microsoft 키 배포 서비스(kdssvc.dll)는 AD용 루트 키입니다.

**주기**

gMSA 기능을 사용하는 서버 팜의 수명 주기에는 일반적으로 다음 작업이 포함됩니다.

-   새 서버 팜 배포

-   기존 서버 팜에 구성원 호스트 추가

-   기존 서버 팜에서 구성원 호스트 서비스 해제

-   기존 서버 팜 서비스 해제

-   필요한 경우 서버 팜에서 손상된 구성원 호스트 제거

## <a name="deploying-a-new-server-farm"></a><a name="BKMK_DeployNewFarm"></a>새 서버 팜 배포
새 서버 팜을 배포할 때는 서비스 관리자가 다음 사항을 결정해야 합니다.

-   서비스에서 gMSA 사용을 지원하는지 여부

-   서비스에 인바운드 또는 아웃바운드 인증된 연결이 필요한지 여부

-   gMSA를 사용하는 서비스에 대한 구성원 호스트의 컴퓨터 계정 이름

-   서비스의 NetBIOS 이름

-   서비스의 DNS 호스트 이름

-   서비스의 SPN(서비스 사용자 이름)

-   암호 변경 간격(기본값은 30일)

### <a name="step-1-provisioning-group-managed-service-accounts"></a><a name="BKMK_Step1"></a>1 단계: 그룹 관리 서비스 계정 프로 비전
포리스트 스키마가 Windows Server 2012로 업데이트 되 고 Active Directory의 마스터 루트 키가 배포 된 경우에만 gMSA를 만들 수 있으며, gMSA를 만들 도메인에 Windows Server 2012 DC가 하나 이상 있는 경우에만 만들 수 있습니다.

다음 절차를 완료하려면 최소한 **Domain Admins** 또는 **Account Operators**의 구성원이거나 msDS-GroupManagedServiceAccount 개체를 만들 수 있는 권한이 있어야 합니다.

> [!NOTE]
> -Name 매개 변수 값은-DNSHostName,-RestrictToSingleComputer 및-RestrictToOutboundAuthentication을 사용 하 여 세 가지 배포 시나리오에 대 한 보조 요구 사항으로 항상 필요 합니다 (-Name을 지정 했는지 여부에 관계 없이).    


#### <a name="to-create-a-gmsa-using-the-new-adserviceaccount-cmdlet"></a><a name="BKMK_CreateGMSA"></a>Uninstall-adserviceaccount cmdlet을 사용 하 여 gMSA를 만들려면

1.  Windows Server 2012 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다. Active Directory 모듈이 자동으로 로드됩니다.

    **Uninstall-adserviceaccount [-Name] &lt;string&gt;-DNSHostName &lt;string&gt; [-KerberosEncryptionType &lt;ADKerberosEncryptionType&gt;] [-ManagedPasswordIntervalInDays < Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >] [-SamAccountName &lt;string&gt;] [-ServicePrincipalNames < string [] >]**

    |매개 변수|String|예제|
    |-------|-----|------|
    |이름|계정 이름|ITFarm1|
    |DNSHostName|서비스의 DNS 호스트 이름|ITFarm1.contoso.com|
    |KerberosEncryptionType|호스트 서버에서 지원되는 모든 암호화 종류|None, RC4, AES128, AES256|
    |ManagedPasswordIntervalInDays|암호 변경 간격(지정하지 않을 경우 기본값은 30일)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트가 속해 있는 보안 그룹의 컴퓨터 계정|ITFarmHosts|
    |SamAccountName|서비스의 NetBIOS 이름(Name과 동일하지 않은 경우)|ITFarm1|
    |ServicePrincipalNames|서비스의 SPN(서비스 사용자 이름)|http/Itfarm1.contoso.com, http/Itfarm1.contoso.com/contoso, http/Itfarm1.contoso.com/contoso, http/Itfarm1.contoso.com/contoso, MSSQLSvc/Itfarm1.contoso.com: 1433:1433, MSSQLSvc/Itfarm1.contoso.com: INST01. m s c:|

    > [!IMPORTANT]
    > 암호 변경 간격은 만드는 동안에만 설정할 수 있습니다. 간격을 변경해야 하는 경우 새 gMSA를 만든 후 만들기 과정에서 이를 설정해야 합니다.
   
    **예제**

    서식 제약 조건으로 인해 명령이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 명령을 한 줄에 입력해야 합니다.

    ```Powershell
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts$ -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso
    ```

다음 절차를 완료하려면 최소한 **Domain Admins** 또는 **Account Operators**의 구성원이거나 msDS-GroupManagedServiceAccount 개체를 만들 수 있는 권한이 있어야 합니다. 적절한 계정과 그룹 구성원 사용에 대한 자세한 내용은 [로컬 및 도메인 기본 그룹](https://technet.microsoft.com/library/dd728026(WS.10).aspx)을 참조하세요.

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>New-ADServiceAccount cmdlet을 사용하여 아웃바운드 인증용으로만 gMSA를 만들려면

1.  Windows Server 2012 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **Uninstall-adserviceaccount [-Name] &lt;string&gt;-RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays < Nullable [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >]**

    |매개 변수|String|예제|
    |-------|-----|------|
    |이름|계정 이름|ITFarm1|
    |ManagedPasswordIntervalInDays|암호 변경 간격(지정하지 않을 경우 기본값은 30일)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트가 속해 있는 보안 그룹의 컴퓨터 계정|ITFarmHosts|

    > [!IMPORTANT]
    > 암호 변경 간격은 만드는 동안에만 설정할 수 있습니다. 간격을 변경해야 하는 경우 새 gMSA를 만든 후 만들기 과정에서 이를 설정해야 합니다.
    
  **예제**

```PowerShell
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts$
```

### <a name="step-2-configuring-service-identity-application-service"></a><a name="BKMK_ConfigureServiceIdentity"></a>2 단계: 서비스 id 응용 프로그램 서비스 구성
Windows Server 2012에서 서비스를 구성 하려면 다음 기능 설명서를 참조 하세요.

-   IIS 애플리케이션 풀

    자세한 내용은 [응용 프로그램 풀의 ID 지정(IIS 7)](https://technet.microsoft.com/library/cc771170(WS.10).aspx)을 참조하세요.

-   Windows 서비스

    자세한 내용은 [서비스](https://technet.microsoft.com/library/cc772408.aspx)를 참조하세요.

-   작업

    자세한 내용은 [작업 스케줄러 개요](https://technet.microsoft.com/library/cc721871.aspx)를 참조하세요.

다른 서비스에서도 gMSA를 지원할 수 있습니다. 이러한 서비스를 구성하는 방법에 대한 자세한 내용은 해당 제품 설명서를 참조하세요.

## <a name="adding-member-hosts-to-an-existing-server-farm"></a><a name="BKMK_AddMemberHosts"></a>기존 서버 팜에 구성원 호스트 추가
보안 그룹을 사용 하 여 구성원 호스트를 관리 하는 경우 다음 방법 중 하나를 사용 하 여 보안 그룹 (gMSA의 구성원 호스트가 속해 있는)에 새 구성원 호스트의 컴퓨터 계정을 추가 합니다.

다음 절차를 완료하려면 최소한 **Domain Admins**의 구성원이거나 보안 그룹 개체에 구성원을 추가할 수 있는 권한이 있어야 합니다.

-   방법 1: Active Directory 사용자 및 컴퓨터

    이 방법을 사용하는 절차는 Windows 인터페이스를 사용하여 [그룹에 컴퓨터 계정 추가](https://technet.microsoft.com/library/cc733097.aspx) 및 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)를 참조하세요.

-   방법 2: dsmod

    이 방법을 사용하는 절차는 명령줄을 사용하여 [그룹에 컴퓨터 계정 추가](https://technet.microsoft.com/library/cc733097.aspx) 를 참조하세요.

-   방법 3: Windows PowerShell Active Directory cmdlet Add-ADPrincipalGroupMembership

    이 방법을 사용하는 절차는 [Add-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx)(영문)을 참조하세요.

컴퓨터 계정을 사용하는 경우 기존 계정을 찾은 다음 새 컴퓨터 계정을 추가합니다.

다음 절차를 완료하려면 최소한 **Domain Admins** 또는 **Account Operators**의 구성원이거나 msDS-GroupManagedServiceAccount 개체를 관리할 수 있는 권한이 있어야 합니다. 적절한 계정과 그룹 구성원 사용에 대한 자세한 내용은 로컬 및 도메인 기본 그룹을 참조하세요.

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-ADServiceAccount cmdlet을 사용하여 구성원 호스트를 추가하려면

1.  Windows Server 2012 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **Uninstall-adserviceaccount [-Name] &lt;string&gt;-PrincipalsAllowedToRetrieveManagedPassword**

3.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **Uninstall-adserviceaccount [-Name] &lt;string&gt;-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|매개 변수|String|예제|
|-------|-----|------|
|이름|계정 이름|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트가 속해 있는 보안 그룹의 컴퓨터 계정|Host1, Host2, Host3|

**예제**

예를 들어 구성원 호스트를 추가하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

```PowerShell
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword
```

```PowerShell
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1$,Host2$,Host3$
```

## <a name="updating-the-group-managed-service-account-properties"></a><a name="BKMK_Update_gMSA"></a>그룹 관리 서비스 계정 속성 업데이트
다음 절차를 완료하려면 최소한 **Domain Admins** 또는 **Account Operators**의 구성원이거나 msDS-GroupManagedServiceAccount 개체를 쓸 수 있는 권한이 있어야 합니다.

Windows PowerShell Active Directory 모듈을 열고 Set-ADServiceAccount cmdlet을 사용하여 속성을 설정합니다.

이러한 속성을 설정하는 방법에 대한 자세한 내용은 TechNet 라이브러리에서 [Set-ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) 를 참조하세요. Windows PowerShell Active Directory 모듈 명령 프롬프트에서 **Get-Help Set-ADServiceAccount** 를 입력하고 Enter 키를 눌러 참조할 수도 있습니다.

## <a name="decommissioning-member-hosts-from-an-existing-server-farm"></a><a name="BKMK_DecommMemberHosts"></a>기존 서버 팜에서 구성원 호스트 서비스 해제
다음 절차를 완료하려면 최소한 **Domain Admins**의 구성원이거나 보안 그룹 개체에서 구성원을 제거할 수 있는 권한이 있어야 합니다.

### <a name="step-1-remove-member-host-from-gmsa"></a>1단계: gMSA에서 구성원 호스트 제거
보안 그룹을 사용 하 여 구성원 호스트를 관리 하는 경우 다음 방법 중 하나를 사용 하 여 gMSA의 구성원 호스트가 속해 있는 보안 그룹에서 서비스 해제 된 구성원 호스트의 컴퓨터 계정을 제거 합니다.

-   방법 1: Active Directory 사용자 및 컴퓨터

    이 방법을 사용하는 절차는 Windows 인터페이스를 사용하여 [컴퓨터 계정 삭제](https://technet.microsoft.com/library/cc754624.aspx) 및 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)를 참조하세요.

-   방법 2: drsm

    이 방법을 사용하는 절차는 명령줄을 사용하여 [컴퓨터 계정 삭제](https://technet.microsoft.com/library/cc754624.aspx) 를 참조하세요.

-   방법 3: Windows PowerShell Active Directory cmdlet Add-ADPrincipalGroupMembership

    이 작업을 수행하는 방법에 대한 자세한 내용은 TechNet 라이브러리에서  [Remove-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) 을 참조하세요. Windows PowerShell Active Directory 모듈 명령 프롬프트에서 **Get-Help Remove-ADPrincipalGroupMembership** 를 입력하고 Enter 키를 눌러 참조할 수도 있습니다.

컴퓨터 계정을 나열하는 경우 기존 계정을 검색한 다음 제거된 컴퓨터 계정을 제외하고 모든 컴퓨터 계정을 추가합니다.

다음 절차를 완료하려면 최소한 **Domain Admins** 또는 **Account Operators**의 구성원이거나 msDS-GroupManagedServiceAccount 개체를 관리할 수 있는 권한이 있어야 합니다. 적절한 계정과 그룹 구성원 사용에 대한 자세한 내용은 로컬 및 도메인 기본 그룹을 참조하세요.

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Set-ADServiceAccount cmdlet을 사용하여 구성원 호스트를 제거하려면

1.  Windows Server 2012 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **Uninstall-adserviceaccount [-Name] &lt;string&gt;-PrincipalsAllowedToRetrieveManagedPassword**

3.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **Uninstall-adserviceaccount [-Name] &lt;string&gt;-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|매개 변수|String|예제|
|-------|-----|------|
|이름|계정 이름|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트가 속해 있는 보안 그룹의 컴퓨터 계정|Host1, Host3|

**예제**

예를 들어 구성원 호스트를 제거하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

```PowerShell
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword
```

```PowerShell
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1$,Host3$
```

### <a name="step-2-removing-a-group-managed-service-account-from-the-system"></a><a name="BKMK_RemoveGMSA"></a>2 단계: 시스템에서 그룹 관리 서비스 계정 제거
호스트 시스템에서 Uninstall-ADServiceAccount 또는 NetRemoveServiceAccount API를 사용하여 캐시된 gMSA 자격 증명을 구성원 호스트에서 제거합니다.

이 절차를 완료하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>Uninstall-ADServiceAccount cmdlet을 사용하여 gMSA를 제거하려면

1.  Windows Server 2012 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **Uninstall-adserviceaccount &lt;Uninstall-adserviceaccount&gt;**

    **예제**

    예를 들어 ITFarm1이라는 gMSA의 캐시된 자격 증명을 제거하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```PowerShell
    Uninstall-ADServiceAccount ITFarm1
    ```

Uninstall-ADServiceAccount cmdlet에 대한 자세한 내용을 보려면 Windows PowerShell Active Directory 모듈 명령 프롬프트에서 **Get-Help Uninstall-ADServiceAccount**를 입력하고 Enter 키를 누르거나, TechNet 웹 [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx)를 참조하세요.



## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목

-   [그룹 관리 서비스 계정 개요](group-managed-service-accounts-overview.md)
