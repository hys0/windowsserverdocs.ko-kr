---
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: "Windows PowerShell (수준을 100)를 사용 하 여 토폴로지 관리 및 Active Directory 복제 소개"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 006179bb3220f7bccfc7510e1b8ef69678321074
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Windows PowerShell (수준을 100)를 사용 하 여 토폴로지 관리 및 Active Directory 복제 소개

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows PowerShell Active Directory에 대 한 복제, 사이트, 도메인 및 숲, 도메인 컨트롤러 및 파티션을 관리 하는 기능을 포함 합니다. 이전 관리 도구 Active Directory 사이트 및 서비스와 같은 사용자에 게 스냅인 및 repadmin.exe 비슷한 기능에 대 한 Active Directory 상황에 맞는 Windows PowerShell에서 사용할 수 있는 이제 인지 알 수 있습니다. 또한 cmdlet의 기존 Windows PowerShell cmdlet, Active Directory에 대 한 간소화 된 환경을 만들고 고객 자동화 스크립트 쉽게 만들 수 있게 되므로와 호환 됩니다.

> [!NOTE]
> Windows PowerShell Active Directory 복제 및 토폴로지 cmdlet에 대 한 다음 환경에서 사용할 수 있습니다.
> 
> -    Windows Server 2012 도메인 컨트롤러
> -    Windows Server 2012 AD DS 및 광고 LDS에 대 한 원격 서버 관리 도구를 설치 합니다.
> -   Windows&reg; AD DS 및 광고 LDS 설치에 대 한 원격 서버 관리 도구와 8 합니다.

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Windows PowerShell에 대 한 Active Directory 모듈 설치
Windows Server 2012를 실행 하는 서버에 AD DS 서버 역할을 설치할 때 Windows PowerShell에 대 한 Active Directory 모듈 기본적으로 설치 됩니다. 없이 추가 단계는 이외의 서버 역할을 추가 합니다. 원격 서버 관리 도구를 설치 하 여 Windows Server 2012를 실행 하는 서버에 Active Directory 모듈 설치할 수도 있습니다와 Active Directory 모듈 다운로드 및 설치 하 여 Windows 8을 실행 하는 컴퓨터에서 설치할 수 있는 [관리 도구 RSAT (원격 서버)](https://www.microsoft.com/download/details.aspx?id=28972)합니다. 참조 [지침](https://www.microsoft.com/download/details.aspx?id=28972)설치 단계에 있습니다.

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Windows PowerShell Active Directory 복제 및 토폴로지 관리 cmdlet에 대 한 테스트용 시나리오
다음과 같은 경우 새로운 관리 cmdlet 파악할 관리자 위한 다음과 같습니다.

-   모든 도메인 컨트롤러 및 해당 광고주 사이트의 목록을 보려면

-   복제 토폴로지 관리

-   복제 상태 보기 및 정보

## <a name="lab-requirements"></a>랩 요구 사항

-   두 명의 Windows Server 2012 도메인 컨트롤러: **d c 1** 및 **d c 2** contoso.com 도메인에 속한 하 고 그 도메인 회사 사이트에 있는 합니다.

## <a name="view-domain-controllers-and-their-sites"></a>도메인 컨트롤러 및 광고주 사이트 보기
이 단계에서 Windows PowerShell에 대 한 Active Directory 모듈 기존 도메인 컨트롤러 및 복제 토폴로지 도메인을 볼 수 사용 합니다.

다음 절차에 나와 있는 단계를 완료 하려면 관리자 도메인 그룹 구성원 하거나 권한이 동일 해야 합니다.

#### <a name="to-view-all-active-directory-sites"></a>모든 Active Directory 사이트를 보려면

1.  **d c 1**, 클릭 **Windows PowerShell** 작업 표시줄에서 합니다.

2.  다음 명령을 입력.

    `Get-ADReplicationSite -Filter *`

    각 사이트에 대 한 자세한 정보를 반환합니다. `Filter`반환 목록을 제한 Active Directory PowerShell cmdlet 전체 매개 변수를 사용 합니다. 이 경우 별표 (*) 모든 사이트 개체를 의미 합니다.

    > [!TIP]
    > Tab 키 명령 자동 완성를 Windows PowerShell에서 사용할 수 있습니다.
    > 
    > 예: 입력 `Get-ADRep`Tab 키를 눌러 여러 번 될 때까지 일치 하는 명령 이동 하 고 `Get-ADReplicationSite`합니다. 자동 완성에 대해서도 작동 매개 이름와 같은 `Filter`합니다.

    출력을 포맷 하려면는 `Get-ADReplicationSite`표로 명령을 하 고 디스플레이 제한 하 고 특정 필드에 출력 파이프 수는 `Format-Table`명령 (또는 "`ft`" 간단히):

    `Get-ADReplicationSite -Filter * | ft Name`

    이 짧은 이름 필드만 포함 한 사이트 목록 버전을 반환 합니다.

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>모든 도메인 컨트롤러의 표 생성 하기 위해

-   다음 명령을 입력 하 고 **Windows PowerShell 모듈 Active Directory** 프롬프트:

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    이 명령의 이름을 뿐만 아니라 해당 사이트 연결 개최 된 도메인 컨트롤러를 반환 합니다.

## <a name="manage-replication-topology"></a>복제 토폴로지 관리
명령을 실행 한 후 이전 단계에서 `Get-ADDomainController -Filter * | ft Hostname,Site`, **d c 2** 의 일환으로 나열 된는 **회사** 사이트 합니다. 아래 절차에 새로운 지점 사이트, 만들어집니다 **분기 1**만들고 새로운 사이트 링크 사이트 링크 비용과 복제 빈도 설정 하 고 다음 이동 **d c 2** 에 **분기 1**합니다.

다음 절차에 나와 있는 단계를 완료 하려면 관리자 도메인 그룹 구성원 하거나 권한이 동일 해야 합니다.

#### <a name="to-create-a-new-site"></a>새 사이트를 만들려면

-   다음 명령을 입력 하 고 **Windows PowerShell 모듈 Active Directory** 프롬프트:

    `New-ADReplicationSite BRANCH1`

    이 명령을 새로운 지점 사이트, 분기 1 만듭니다.

#### <a name="to-create-a-new-site-link"></a>새 사이트 링크를 만들려면

-   다음 명령을 입력 하 고 **Windows PowerShell 모듈 Active Directory** 프롬프트:

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    이 명령을 사이트 링크를 만든 **분기 1** 및 변경 알림 프로세스 켜져 있습니다.

    > [!TIP]
    > 탭 사용 하 여 자동 완성 매개 이름에와 같은 `-SitesIncluded`및 `-OtherAttributes`수동으로 입력 하는 대신 합니다.

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>사이트 링크 비용과 복제 빈도 설정 하려면

-   다음 명령을 입력 하 고 **Windows PowerShell 모듈 Active Directory** 프롬프트:

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    사이트 링크 비용 설정 **분기 1** 에 **100** 복제 하는 사이트와 빈도 설정 하 고 **15 분**합니다.

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>도메인 컨트롤러 다른 사이트를 이동 하려면

-   다음 명령을 입력 하 고 **Windows PowerShell 모듈 Active Directory** 프롬프트:

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    이 명령을 이동 도메인 컨트롤러 **d c 2** 하는 **분기 1** 사이트 합니다.

### <a name="verification"></a>확인

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>사이트 만들고 새 사이트 링크, 비용과 복제 주파수를 확인 하려면

-   클릭 **서버 관리자**, 클릭 **도구** 차례로 클릭 하 고 **Active Directory 사이트 및 서비스** 다음을 확인 하 고 있습니다.

    확인 하는 **분기 1** 사이트에서 Windows PowerShell 명령 올바르지 값 모두 포함 합니다.

    확인는 **회사 분기 1** 사이트 링크 만들고 연결는 **분기 1** 및 **회사** 사이트 합니다.

    확인 **d c 2** 이제는 **분기 1** 사이트 합니다. 열 수 있습니다의 **Active Directory Windows PowerShell 모듈** 확인 하려면 다음 명령을 입력 하 고 **d c 2** 에서 이제은 **분기 1** 사이트: `Get-ADDomainController -Filter * | ft Hostname,Site`합니다.

## <a name="view-replication-status-information"></a>복제 상태 정보 보기
다음 절차에는 중 하나를 사용할 Windows PowerShell Active Directory 복제 및 관리 cmdlet에 대 한 `Get-ADReplicationUpToDatenessVectorTable DC1`, 각 도메인 컨트롤러에서 관리 최신 vector 표를 사용 하는 간단한 복제 보고서를 생성 합니다. 최신 vector 다음 표는 추적 하 고 숲 속의 각 도메인 컨트롤러에서 본 높은 원래 쓰기 USN 합니다.

다음 절차에 나와 있는 단계를 완료 하려면 관리자 도메인 그룹 구성원 하거나 권한이 동일 해야 합니다.

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>단일 도메인 컨트롤러에 대 한 최신 vector 표를 보려면

1.  다음 명령을 입력 하 고 **Windows PowerShell 모듈 Active Directory** 프롬프트:

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    있을 때 보면 최고 Usn 목록이 표시 **d c 1** 숲 모든 도메인 컨트롤러에 대 한 합니다. **서버** 값이 경우에 테이블 유지 하는 서버 참조 **d c 1**합니다. **파트너** 값 변경 사항이 복제 파트너 (직접 또는 간접)에 게 말합니다. UsnFilter 값이 표시 높은 USN **d c 1** 파트너 로부터 합니다. 새 도메인 컨트롤러를 숲에 추가 되지에 표시 됩니다 **d c 1**까지 표의 **d c 1** 새 도메인에서 수집한 변경 받습니다.

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>도메인에 있는 모든 도메인 컨트롤러에 대 한 최신 vector 표를 보려면

1.  Windows PowerShell 프롬프트에 대 한 Active Directory 모듈에서 다음 명령을 입력.

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    이 명령을 대체 **d c 1** 으로 `*`, 따라서 모든 도메인 컨트롤러에서 최신 vector 표 데이터를 수집 합니다. 데이터도 정렬 **파트너** 및 **서버** 테이블에 표시 합니다.

    정렬 쉽게 비교 마지막 USN 지정된 복제 파트너에 대 한 각 도메인 컨트롤러에서 볼 수 있습니다. 귀하의 환경에서 복제 되는지 확인 하는 빠른 방법입니다. 복제 제대로 작동 하는 경우 특정된 복제 파트너에 대 한 보고 UsnFilter 값 있어야 비슷함 전체 도메인 컨트롤러 합니다.

## <a name="see-also"></a>참조 하십시오
[향상 된 Active Directory 복제 및 Windows PowerShell 및 #40;를 사용 하 여 토폴로지 관리 200 수준 & #41;](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


