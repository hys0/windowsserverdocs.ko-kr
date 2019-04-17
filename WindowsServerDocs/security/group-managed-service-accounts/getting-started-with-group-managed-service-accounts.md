---
title: "관리 서비스 계정 하는 그룹 시작"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: cd1e92f93701e5b430d1425fcf9a2f3590d1fe5d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="getting-started-with-group-managed-service-accounts"></a>관리 서비스 계정 하는 그룹 시작

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016


이 가이드 설정 및 Windows Server 2012에서 그룹 관리 서비스 계정 사용에 대 한 단계별 지침 및 배경 정보를 제공 합니다.

**이 문서에서**

-   [필수](#BKMK_Prereqs)

-   [소개](#BKMK_Intro)

-   [새 서버 농장 배포](#BKMK_DeployNewFarm)

-   [호스트 기존 서버 팜을 구성원 추가](#BKMK_AddMemberHosts)

-   [그룹 관리 서비스 계정 속성 업데이트](#BKMK_Update_gMSA)

-   [기존 서버 농장에서 구성원 호스트 해제](#BKMK_DecommMemberHosts)


> [!NOTE]
> 이 항목에 설명 된 절차 일부 자동화 데 사용할 수 있는 샘플 Windows PowerShell cmdlet 포함 되어 있습니다. 자세한 내용은 참조 [사용 하 여 Cmdlet](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.

## <a name="BKMK_Prereqs"></a>필수
이 항목의 섹션에 표시 [그룹 관리 서비스 계정에 대 한 요구](#BKMK_gMSA_Req)합니다.

## <a name="BKMK_Intro"></a>소개
클라이언트 컴퓨터에 있는 모든 서버 클라이언트로 같은 서비스 것 같지 네트워크 NLB (부하 분산) 또는 기타 방법을 사용 하 여 서버 팜 호스트 되는 서비스에 연결할 때 다음 인증 프로토콜 Kerberos 등 상호 인증을 지 원하는 사용할 수 없도록 서비스의 모든 인스턴스 동일한 주 사용 하지 않는 한 합니다. 각 서비스에 해당 id를 동일한 암호/키를 사용 하는 것을 의미 합니다.

> [!NOTE]
> 클러스터 장애 조치 gMSAs 지원 하지 않습니다. 그러나 Windows 서비스, 앱 풀, 예약된 된 작업 인지 gMSA 또는 sMSA 기본적으로 지원 경우는 gMSA 또는 sMSA 위에 클러스터 서비스가 실행 되는 서비스 사용할 수 있습니다.

서비스에는 다음과 같은 사용자를 선택할 수 있는 하며 각 특정 제한 됩니다.

|주체|범위|지원 되는 서비스|암호 관리|
|-------|-----|-----------|------------|
|Windows의 계정 컴퓨터|도메인|제한 된 도메인에 가입 서버|컴퓨터에서 관리|
|Windows 시스템 하지 않고 컴퓨터 계정|도메인|도메인 결합된 서버|없음|
|가상 계정|로컬|서버에 제한|컴퓨터에서 관리|
|Windows 7 독립 실행형 관리 서비스 계정|도메인|제한 된 도메인에 가입 서버|컴퓨터에서 관리|
|사용자 계정|도메인|도메인 결합된 서버|없음|
|그룹 관리 서비스 계정|도메인|Windows Server 2012 도메인에 가입 서버|도메인 컨트롤러 관리 하 고 호스트 검색|

Windows 컴퓨터 계정을 또는 Windows 7 독립 실행형 관리 서비스 계정 (sMSA) 또는 가상 계정 여러 시스템 공유할 수 없습니다. 하나의 계정 서비스에 대 한 서버 농장 공유에서 구성한 경우 사용자 계정이 나 Windows 시스템 외에도 컴퓨터 계정을 선택 것입니다. 두 방식 모두 이러한 계정은 없는 단일 지점을 제어 암호 관리 하는 기능이 합니다. 각 조직 비싼 솔루션 키 Active Directory에 서비스에 대 한 업데이트 한 다음 해당 서비스의 모든 경우에는 키를 배포을 만들기 해야 하는 문제를 만듭니다.

Windows Server 2012와 서비스를 또는 서비스 관리자 필요가 없습니다 간의 서비스 인스턴스 그룹 관리 서비스 계정 (gMSA)를 사용 하는 경우 암호 동기화를 관리 합니다. 광고는 gMSA 프로비저닝 하 고 관리 서비스 계정 지원 서비스를 구성 합니다. 사용 하 여 gMSA 제공할 수 있는 *-Active Directory 모듈의 일부인 ADServiceAccount cmdlet 합니다. 하 여 서비스 호스트 신원을 구성을 지원 됩니다.

-   제품을 지 원하는 sMSA는 gMSA 지원 되므로 sMSA로 같은 Api

-   서비스를 제어 관리자를 사용 하 여 로그온 id를 구성 하는 서비스

-   풀 응용 프로그램에 대 한 IIS 관리자를 사용 하 여 id를 구성 하는 서비스

-   작업 스케줄러를 사용 하 여 작업입니다.

### <a name="BKMK_gMSA_Req"></a>그룹 관리 서비스 계정에 대 한 요구 사항
다음 표에서 gMSA 사용 하는 서비스와 작동 하도록 Kerberos 인증의 운영 체제 요구 사항이 나열 됩니다. 표 Active Directory 요구 사항이 나열 됩니다.

64 비트 아키텍처 그룹 관리 서비스 계정 관리 하는 데 사용 하 여 Windows PowerShell 명령을 실행 해야 합니다.

**운영 체제 요구 사항**

|요소|요구 사항|운영 체제|
|------|--------|----------|
|클라이언트 응용 프로그램 호스트|RFC 규격 Kerberos 클라이언트|Windows XP 최소 at|
|사용자 계정의 도메인 Dc|호환 KDC RFC|At 최소 Windows Server 2003|
|공유 서비스 구성원 호스트|| Windows Server 2012 |
|회원 호스트 도메인 Dc|호환 KDC RFC|At 최소 Windows Server 2003|
|gMSA 계정의 도메인 Dc| Windows Server 2012 Dc 호스트 암호를 검색 하는 데 사용할 수 있는|시스템에 따라 Windows Server 2012 이전 가질 수 있는 Windows Server 2012와 도메인 |
|백 엔드 서비스 호스트|RFC 준수 Kerberos 응용 프로그램 서버|At 최소 Windows Server 2003|
|백 엔드 서비스 계정 도메인 Dc|호환 KDC RFC|At 최소 Windows Server 2003|
|Windows PowerShell Active Directory에 대 한|Windows PowerShell 로컬로 또는 (예: 원격 서버 관리 도구 키트를 사용 하 여) 관리 원격 컴퓨터에 64 비트 아키텍처 지원 컴퓨터에 설치 된 Active Directory에 대 한| Windows Server 2012 |

**Active Directory 도메인 서비스 요구 사항**

-   GMSA 도메인 숲 속의 Active Directory 스키마를 gMSA 만드는 Windows Server 2012 업데이트 해야 합니다.

    Windows Server 2012를 실행 하는 도메인 컨트롤러를 설치 하 여 또는 Windows Server 2012를 실행 하는 컴퓨터에서 adprep.exe 버전을 실행 하 여 스키마를 업데이트할 수 있습니다. 개체 CN 개체 버전 특성 값 CN 스키마 = = 구성 DC Contoso, DC = = Com 52 포함 되어 있어야 합니다.

-   새 gMSA 계정을 프로비저닝

-   GMSA 그룹에서 다음 새로운 기능이 나 기존 보안 그룹 하 여 사용 하 여 서비스 호스트 권한을 관리 하는 경우

-   서비스 액세스 제어 그룹에서 다음 새로운 기능이 나 기존 보안 그룹으로 관리 하는 경우

-   도메인에 배포 되지 않은 Active Directory에 대 한 첫 번째 마스터 루트 키를 만들지 않은 경우 다음 만듭니다. 이벤트 ID 4004 KdsSvc 운영 로그에서 만든 결과 확인할 수 있습니다.

지침에 대 한 참고 키를 만드는 방법 [키 배포 서비스 KDS 루트 키를 만들](create-the-key-distribution-services-kds-root-key.md)합니다. Microsoft 키 배포 서비스 (kdssvc.dll)에서 루트 키 광고 합니다.

**수명 주기**

일반적으로 gMSA 기능을 사용 하는 서버 농장의 수명 주기는 다음과 같은 작업이 포함 됩니다.

-   새 서버 농장 배포

-   호스트 기존 서버 팜을 구성원 추가

-   기존 서버 농장에서 구성원 호스트 해제

-   기존 서버 팜 해제

-   필요한 경우 손상 된 회원 호스트 농장 서버에서에서 제거 합니다.

## <a name="BKMK_DeployNewFarm"></a>새 서버 농장 배포
새 팜을 배포 하는 경우 서비스 관리자 확인 해야 합니다.

-   GMSAs를 사용 하 여 서비스를 지 원하는 경우

-   서비스 아웃 바운드 인증된 연결에 필요한 경우

-   사용 하 여 gMSA 서비스에 대 한 구성원 호스트에 대 한 컴퓨터 계정 이름

-   서비스에 대 한 NetBIOS 이름

-   서비스에 대 한 DNS 호스트 이름

-   서비스에 대 한 서비스 사용자 이름 (Spn)

-   암호 변경 간격이 (기본값은 30 일).

### <a name="BKMK_Step1"></a>1 단계: 프로비저닝 그룹 관리 서비스 계정
Windows Server 2012로 업데이트 되었으며이 숲 스키마, Active Directory에 대 한 마스터 루트 키를 배포한 후 뿐 이며 하나 이상의 Windows Server 2012 DC는 gMSA 만들 수는 도메인의 경우에는 gMSA 만들 수 있습니다.

회원 **도메인 관리자**, **계정 운영자** 를 GroupManagedServiceAccount 개체 만들 수는 다음 절차를 수행 하는 데 필요한 최소 또는 합니다.

#### <a name="BKMK_CreateGMSA"></a>새로 만들기 ADServiceAccount cmdlet 사용 하 여 gMSA 만들려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Windows PowerShell에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다. (Active Directory 모듈은 자동으로 로드 됩니다.)

    **새 ADServiceAccount [-이름] <string> -DNSHostName <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < Nullable [i n t 32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal >]-SamAccountName <string> -ServicePrincipalNames < 문자열 >**

    |매개|문자열|예제|
    |-------|-----|------|
    |이름|계정 이름|ITFarm1|
    |DNSHostName|DNS 서비스 호스트 이름|ITFarm1.contoso.com|
    |KerberosEncryptionType|호스트 서버에서 지 원하는 모든 암호화 유형|AES128, R C 4 AES256|
    |ManagedPasswordIntervalInDays|암호 변경 간격 일 동안 (기본은 30 일 동안 지정 하지 않은 경우)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트의 회원은 보안 그룹의 컴퓨터 계정|ITFarmHosts|
    |SamAccountName|그렇지 않은 경우 서비스에 대 한 NetBIOS 이름 이름이 같은|ITFarm1|
    |ServicePrincipalNames|서비스에 대 한 서비스 사용자 이름 (Spn)|http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso|

    > [!IMPORTANT]
    > 암호 변경 간격 생성 하는 동안만 설정할 수 있습니다. 간격을 변경 하려는 경우 새 gMSA 만들고를 만들 때 설정 해야 합니다.

    **예제**

    하지만 포맷 제한으로 인해 여러 줄 여기에서 단어 싸여 표시 될 수 있습니다 명령 한 줄에 입력 합니다.

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

회원 **도메인 관리자**, **계정 운영자**를 GroupManagedServiceAccount 개체 만들 수는이 절차를 수행 하는 데 필요한 최소 또는 합니다. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>새로 만들기 ADServiceAccount cmdlet 사용 하 여만 gMSA 아웃 바운드 인증에 대 한를 만들려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **새 ADServiceAccount [-이름] <string> -RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays < Nullable [i n t 32] >] [-< ADPrincipal > PrincipalsAllowedToRetrieveManagedPassword]**

    |매개|문자열|예제|
    |-------|-----|------|
    |이름|계정 이름|ITFarm1|
    |ManagedPasswordIntervalInDays|암호 변경 간격 일 동안 (기본은 30 일 동안 지정 하지 않은 경우)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트의 회원은 보안 그룹의 컴퓨터 계정|ITFarmHosts|

    > [!IMPORTANT]
    > 암호 변경 간격 생성 하는 동안만 설정할 수 있습니다. 간격을 변경 하려는 경우 새 gMSA 만들고를 만들 때 설정 해야 합니다.

**예제**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>2 단계: 구성 id 응용 프로그램 서비스를 서비스
서비스를 Windows Server 2012에서 구성 하려면 다음과 같은 기능 설명서를 참조 하세요.

-   응용 프로그램 풀

    자세한 내용은 참조 [응용 프로그램 (IIS 7) 풀에 대 한 Id 지정](https://technet.microsoft.com/library/cc771170(WS.10).aspx)합니다.

-   Windows 서비스

    자세한 내용은 참조 [서비스](https://technet.microsoft.com/library/cc772408.aspx)합니다.

-   작업

    자세한 내용은 참조는 [작업 스케줄러 개요](https://technet.microsoft.com/library/cc721871.aspx)합니다.

다른 서비스 gMSA 지원할 수 있습니다. 이러한 서비스를 구성 하는 방법에 대 한 자세한 내용은 해당 제품 설명서를 참조 하세요.

## <a name="BKMK_AddMemberHosts"></a>호스트 기존 서버 팜을 구성원 추가
컴퓨터 계정을 새 구성원 호스트 (되 고 gMSA 구성원 호스트 소속) 보안 그룹에 대 한 추가 보안 그룹 구성원 호스트 관리 하기 위한를 사용 하는 경우 다음 방법 중 하나를 사용 합니다.

회원 **도메인 관리자**, 보안 그룹 개체 구성원을 추가 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

-   방법 1: Active Directory 사용자와 컴퓨터

    절차 참조 하십시오이 방법을 사용 하는 방법을 [그룹에 계정을 추가](https://technet.microsoft.com/library/cc733097.aspx) 사용 하 여 Windows 인터페이스 및 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)합니다.

-   방법 2: dsmod

    절차 참조 하십시오이 방법을 사용 하는 방법을 [그룹에 계정을 추가](https://technet.microsoft.com/library/cc733097.aspx) 명령줄을 사용 하 여 합니다.

-   Windows Active Directory PowerShell cmdlet 추가 ADPrincipalGroupMembership 방법 3:

    절차 참조 하십시오이 방법을 사용 하는 방법을 [추가 ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx)합니다.

계정 컴퓨터를 사용 하 여 기존 계정을 찾아 다음 새 컴퓨터 계정을 추가 합니다.

회원 **도메인 관리자**, **계정 운영자**를 GroupManagedServiceAccount 개체를 관리 하는 기능에는이 절차를 수행 하는 데 필요한 최소 또는 합니다. 사용 하 여 해당 계정 및 그룹 구성원에 대 한 자세한 내용은 지역 및 도메인 기본 그룹을 참조 하십시오.

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>사용 하 여 설정 ADServiceAccount cmdlet 구성원 호스트 추가 하려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **Get ADServiceAccount [-이름] <string> -PrincipalsAllowedToRetrieveManagedPassword**

3.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **설정 ADServiceAccount [-이름] <string> -PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal >**

|매개|문자열|예제|
|-------|-----|------|
|이름|계정 이름|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트의 회원은 보안 그룹의 컴퓨터 계정|호스트 2, Host1 Host3|

**예제**

예를 들어, 구성원을 추가 하려면 호스트 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1 Host2 Host3

```

## <a name="BKMK_Update_gMSA"></a>그룹 관리 서비스 계정 속성 업데이트
회원 **도메인 관리자**, **계정 운영자**,이 절차를 수행 하는 데 필요한 최소를 GroupManagedServiceAccount 개체에 쓸 수 있는 기능은 또는 합니다.

Active Directory 모듈에 대 한 Windows PowerShell를 열고 설정 ADServiceAccount cmdlet 사용 하 여 속성을 설정 합니다.

에 대 한 자세한 정보를 참조 하세요 이러한 속성을 설정 하는 방법을 [설정 ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) TechNet 라이브러리 또는 입력 하 여 **도움말 얻기 설정 ADServiceAccount** 명령 프롬프트 및 눌러서 ENTER의 Active Directory Windows PowerShell 모듈에 있습니다.

## <a name="BKMK_DecommMemberHosts"></a>기존 서버 농장에서 구성원 호스트 해제
회원 **도메인 관리자**, 보안 그룹 개체의 구성원을 제거 하는 기능에는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

### <a name="step-1-remove-member-host-from-gmsa"></a>1 단계: 회원 호스트 gMSA에서 제거
보안 그룹 구성원 호스트 관리 하기 위한를 사용 하는 경우 컴퓨터 계정을 해지 구성원 호스트 gMSA의 회원 호스트의 다음 방법 중 하나를 사용 하는 보안 그룹에서 제거 합니다.

-   방법 1: Active Directory 사용자와 컴퓨터

    절차 참조 하십시오이 방법을 사용 하는 방법을 [컴퓨터 계정을 삭제](https://technet.microsoft.com/library/cc754624.aspx) 사용 하 여 Windows 인터페이스 및 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)합니다.

-   방법 2: drsm

    절차 참조 하십시오이 방법을 사용 하는 방법을 [컴퓨터 계정을 삭제](https://technet.microsoft.com/library/cc754624.aspx) 명령줄을 사용 하 여 합니다.

-   방법 3: Active Directory Windows PowerShell cmdlet ADPrincipalGroupMembership 제거

    에 대 한 자세한 정보를 참조 하십시오이 작업을 수행 하는 방법을 [제거 ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) TechNet 라이브러리 또는 입력 하 여 **도움말 얻기 제거 ADPrincipalGroupMembership** 명령 프롬프트 및 눌러서 ENTER의 Active Directory Windows PowerShell 모듈에 있습니다.

컴퓨터 계정 나열 기존 계정 검색 하 고 제거 컴퓨터 계정을 제외한 모든 추가 합니다.

회원 **도메인 관리자**, **계정 운영자**를 GroupManagedServiceAccount 개체를 관리 하는 기능에는이 절차를 수행 하는 데 필요한 최소 또는 합니다. 사용 하 여 해당 계정 및 그룹 구성원에 대 한 자세한 내용은 지역 및 도메인 기본 그룹을 참조 하십시오.

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>사용 하 여 설정 ADServiceAccount cmdlet 구성원 호스트 제거 하려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **Get ADServiceAccount [-이름] <string> -PrincipalsAllowedToRetrieveManagedPassword**

3.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **설정 ADServiceAccount [-이름] <string> -PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal >**

|매개|문자열|예제|
|-------|-----|------|
|이름|계정 이름|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|구성원 호스트 또는 구성원 호스트의 회원은 보안 그룹의 컴퓨터 계정|Host3 Host1|

**예제**

예를 들어, 제거 하려면 회원 호스트 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1 Host3

```

### <a name="BKMK_RemoveGMSA"></a>2 단계: 시스템에서 그룹 관리 서비스 계정 제거
캐시 된 gMSA 자격 증명 호스트 시스템에서 제거 ADServiceAccount 또는 NetRemoveServiceAccount API를 사용 하 여 회원 호스트에서 제거 합니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>사용 하 여 제거 ADServiceAccount cmdlet gMSA 제거 하려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **제거 ADServiceAccount < ADServiceAccount >**

    **예제**

    예를 들어,는 gMSA에 대 한 캐시 된 자격 증명을 제거 하려면 명명된 ITFarm1 다음 명령을 입력 하 고 enter:

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

Windows PowerShell 명령 프롬프트에 대 한 Active Directory 모듈에서 제거 ADServiceAccount cmdlet에 대 한 자세한 내용을 보려면 입력 **도움말 얻기 제거 ADServiceAccount**, 다음 enter 키를 하거나 TechNet 웹 사이트에서 정보를 참조 하십시오 [제거 ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx)합니다.



## <a name="BKMK_Links"></a>참조 하십시오

-   [그룹 관리 서비스 계정 개요](group-managed-service-accounts-overview.md)



