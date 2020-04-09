---
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: Windows PowerShell을 사용한 Active Directory 복제 및 토폴로지 관리 소개(수준 100)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 63ecad01ec6d4b4d72b7aaff315b74541cb0fadc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822986"
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Windows PowerShell을 사용한 Active Directory 복제 및 토폴로지 관리 소개(수준 100)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory용 Windows PowerShell에는 복제, 사이트, 도메인/포리스트, 도메인 컨트롤러 및 파티션 관리 기능이 포함되어 있습니다. Active Directory 사이트, 서비스 스냅인 및 repadmin.exe와 같은 이전 관리 도구 사용자는 이제 Active Directory용 Windows PowerShell 컨텍스트 내에서 유사한 기능이 제공됨을 확인할 수 있습니다. 또한 cmdlet은 기존의 Active Directory용 Windows PowerShell cmdlet과 호환되므로 편리한 환경이 생성되며 고객이 자동화 스크립트를 쉽게 만들 수 있습니다.

> [!NOTE]
> Active Directory용 Windows PowerShell 복제 및 토폴로지 cmdlet은 다음 환경에서 사용할 수 있습니다.
> 
> -    Windows Server 2012 도메인 컨트롤러
> -    Windows Server 2012 AD DS 및 AD LDS 용 원격 서버 관리 도구와 함께 설치 합니다.
> -   Windows&reg; 8 AD DS 및 AD LDS 설치에 대 한 원격 서버 관리 도구를 사용 합니다.

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Windows PowerShell용 Active Directory 모듈 설치
Active Directory 모듈에 대 한 Windows PowerShell은 Windows Server 2012를 실행 하는 서버에 AD DS 서버 역할을 설치할 때 기본적으로 설치 됩니다. 서버 역할 추가 외에 다른 추가 단계는 필요하지 않습니다. 원격 서버 관리 도구를 설치 하 여 Windows Server 2012를 실행 하는 서버에서 Active Directory 모듈을 설치할 수도 있습니다와 다운로드 및 설치 하 여 Windows 8을 실행 하는 컴퓨터에서 Active Directory 모듈을 설치할 수는 [원격 서버 관리 도구 (RSAT)](https://www.microsoft.com/download/details.aspx?id=28972)합니다. 설치 단계는 [지침](https://www.microsoft.com/download/details.aspx?id=28972)을 참조하세요.

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Windows PowerShell에서 Active Directory 복제 및 토폴로지 관리 cmdlet을 테스트하는 시나리오
관리자는 다음 시나리오를 통해 새로운 관리 cmdlet을 파악할 수 있습니다.

-   모든 도메인 컨트롤러 및 해당 사이트 목록 가져오기

-   복제 토폴로지 관리

-   복제 상태 및 정보 확인

## <a name="lab-requirements"></a>랩 요구 사항

-   두 명의 Windows Server 2012 도메인 컨트롤러: **d c 1** 및 **DC2** contoso.com 도메인의 일부가 되 고 해당 도메인 내의 CORPORATE 사이트에 상주 합니다.

## <a name="view-domain-controllers-and-their-sites"></a>도메인 컨트롤러 및 해당 사이트 확인
이 단계에서는 Windows PowerShell용 Active Directory 모듈을 사용하여 기존 도메인 컨트롤러 및 도메인의 복제 토폴로지를 확인합니다.

다음 절차의 단계를 완료하려면 Domain Admins 그룹의 구성원이거나 해당하는 사용 권한이 있어야 합니다.

#### <a name="to-view-all-active-directory-sites"></a>모든 Active Directory 사이트를 확인하려면

1.  **DC1**의 작업 표시줄에서 **Windows PowerShell**을 클릭합니다.

2.  다음 명령을 입력합니다:

    `Get-ADReplicationSite -Filter *`

    그러면 각 사이트에 대한 자세한 정보가 반환됩니다. `Filter` 매개 변수는 Active Directory PowerShell cmdlet 전체에서 반환되는 개체 목록을 제한하는 데 사용됩니다. 여기서 별표(*)는 모든 사이트 개체를 나타냅니다.

    > [!TIP]
    > Tab 키를 사용하여 Windows PowerShell에서 명령을 자동 완성할 수 있습니다.
    > 
    > 예: `Get-ADRep` 를 입력하고 Tab 키를 여러 번 눌러 `Get-ADReplicationSite`에 도달할 때까지 일치하는 명령을 건너뜁니다. 자동 완성은 `Filter` 등의 매개 변수 이름에 대해서도 작동합니다.

    출력의 서식을 지정 하는 `Get-ADReplicationSite` 테이블로 표시를 제한 한 특정 필드에는 출력을 파이프할 수 있습니다는 `Format-Table` 명령 (또는 "`ft`" 줄여서):

    `Get-ADReplicationSite -Filter * | ft Name`

    그러면 이름 필드만 포함된 사이트 목록의 짧은 버전이 반환됩니다.

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>모든 도메인 컨트롤러의 표를 생성하려면

-   **Windows PowerShell용 Active Directory 모듈** 프롬프트에 다음 명령을 입력합니다.

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    이 명령은 도메인 컨트롤러 호스트 이름과 해당 사이트 연결을 반환합니다.

## <a name="manage-replication-topology"></a>복제 토폴로지 관리
이전 단계에서 `Get-ADDomainController -Filter * | ft Hostname,Site`명령을 실행하고 나면 **DC2** 가 **CORPORATE** 사이트의 일부분으로 나열됩니다. 아래 절차에서는 새 지점 사이트 **BRANCH1**을 만들고 새 사이트 링크를 만든 다음, 사이트 링크 비용 및 복제 빈도를 설정하고 나서 **DC2**를 **BRANCH1**로 이동합니다.

다음 절차의 단계를 완료하려면 Domain Admins 그룹의 구성원이거나 해당하는 사용 권한이 있어야 합니다.

#### <a name="to-create-a-new-site"></a>새 사이트를 만들려면

-   **Windows PowerShell용 Active Directory 모듈** 프롬프트에 다음 명령을 입력합니다.

    `New-ADReplicationSite BRANCH1`

    이 명령은 새 지점 사이트인 branch1을 만듭니다.

#### <a name="to-create-a-new-site-link"></a>새 로그 파일을 만들려면

-   **Windows PowerShell용 Active Directory 모듈** 프롬프트에 다음 명령을 입력합니다.

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    이 명령은 **BRANCH1**에 대한 사이트 링크를 만들고 변경 알림 프로세스를 설정합니다.

    > [!TIP]
    > Tab 키를 사용하여 `-SitesIncluded` 및 `-OtherAttributes` 등의 매개 변수 이름을 수동으로 입력하는 대신 자동 완성할 수 있습니다.

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>사이트 링크 비용 및 복제 빈도를 설정하려면

-   **Windows PowerShell용 Active Directory 모듈** 프롬프트에 다음 명령을 입력합니다.

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    이 명령은 **BRANCH1** 에 대한 사이트 링크 비용을 **100** 으로 설정하고 사이트 복제 빈도를 **15분**으로 설정합니다.

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>도메인 컨트롤러를 다른 사이트로 이동하려면

-   **Windows PowerShell용 Active Directory 모듈** 프롬프트에 다음 명령을 입력합니다.

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    이 명령은 도메인 컨트롤러 **DC2** 를 **BRANCH1** 사이트로 이동합니다.

### <a name="verification"></a>확인

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>사이트 만들기, 새 사이트 링크 및 비용과 복제 빈도를 확인하려면

-   **서버 관리자**, **도구** , **Active Directory 사이트 및 서비스** 를 차례로 클릭하고 다음을 확인합니다.

    **BRANCH1** 사이트에 Windows PowerShell 명령의 올바른 값이 모두 포함되어 있는지 확인합니다.

    **CORPORATE-BRANCH1** 사이트 링크가 작성되었으며 **BRANCH1** 및 **CORPORATE** 사이트에 연결되는지 확인합니다.

    **DC2** 가 현재 **BRANCH1** 사이트에 있는지 확인합니다. 또한 **Windows PowerShell용 Active Directory 모듈**을 열고 다음 명령을 입력하여 **DC2**가 현재 **BRANCH1** 사이트에 있는지 확인할 수도 있습니다. `Get-ADDomainController -Filter * | ft Hostname,Site`.

## <a name="view-replication-status-information"></a>복제 상태 정보 확인
다음 절차에서는 Active Directory용 Windows PowerShell 복제 및 관리 cmdlet 중 하나인 `Get-ADReplicationUpToDatenessVectorTable DC1`을 사용하여 간단한 복제 보고서(각 도메인 컨트롤러가 유지 관리하는 최신 벡터 테이블 사용)를 생성합니다. 이 최신 벡터 테이블은 포리스트의 각 도메인 컨트롤러에 표시되는 최고 원래 쓰기 USN을 추적합니다.

다음 절차의 단계를 완료하려면 Domain Admins 그룹의 구성원이거나 해당하는 사용 권한이 있어야 합니다.

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>단일 도메인 컨트롤러에 대한 최신 벡터 테이블을 확인하려면

1.  **Windows PowerShell용 Active Directory 모듈** 프롬프트에 다음 명령을 입력합니다.

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    그러면 포리스트의 모든 도메인 컨트롤러에 대해 **DC1**에서 확인되는 최고 USN 목록이 표시됩니다. **Server** 값은 테이블을 유지 관리하는 서버(여기서는 **DC1**)를 나타냅니다. **Partner** 값은 변경된 복제 파트너(직접 또는 간접)를 나타냅니다. UsnFilter 값은 Partner에서 **DC1** 에서 확인되는 최고 USN입니다. 새 도메인 컨트롤러를 포리스트에 추가 되는 경우에 나타나지 것입니다 **d c 1**될 때까지 테이블의 **d c 1** 새 도메인에서 시작 하는 변경 받습니다.

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>도메인의 모든 도메인 컨트롤러에 대한 최신 벡터 테이블을 확인하려면

1.  Windows PowerShell용 Active Directory 모듈 프롬프트에 다음 명령을 입력합니다.

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    이 명령은 **DC1** 을 `*`로 바꿔 모든 도메인 컨트롤러에서 최신 벡터 테이블 데이터를 수집합니다. 데이터는 **Partner** 및 **Server** 를 기준으로 정렬된 다음 테이블에 표시됩니다.

    이처럼 데이터가 정렬되므로 지정된 복제 파트너에 대해 각 도메인 컨트롤러가 마지막으로 표시한 USN을 쉽게 비교할 수 있습니다. 이러한 방법으로 환경 전체에서 수행되는 복제를 빠르게 확인할 수 있습니다. 복제가 정상적으로 작동하면 지정된 복제 파트너에 대해 보고되는 UsnFilter 값은 모든 도메인 컨트롤러에서 비슷해야 합니다.

## <a name="see-also"></a>관련 항목
[Windows PowerShell &#40;수준 200을 사용한 고급 Active Directory 복제 및 토폴로지 관리&#41;](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


