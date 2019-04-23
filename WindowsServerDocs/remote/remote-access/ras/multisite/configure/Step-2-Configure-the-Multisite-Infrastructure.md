---
title: 멀티 사이트 인프라를 구성 하는 2 단계
description: 이 가이드의 일부인이 항목에서는 여러 원격 액세스 서버 배포 Windows Server 2016에서 멀티 사이트 배포에서 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: faec70ac-88c0-4b0a-85c7-f0fe21e28257
ms.author: pashort
author: shortpatti
ms.openlocfilehash: beecef692b2ac01e6cb6c36892fec16e55b08209
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835174"
---
# <a name="step-2-configure-the-multisite-infrastructure"></a>멀티 사이트 인프라를 구성 하는 2 단계

>적용 대상: Windows Server 2012 R2, Windows Server 2012

멀티 사이트 배포를 구성 하는 다양 한 네트워크 인프라 설정을 포함 하 여 수정 하는 데 필요한 단계: 사이트 및 도메인 컨트롤러, 추가 보안 그룹을 자동으로 사용 하지 않는 경우 그룹 정책 개체 (Gpo)를 구성 및 Gpo 구성 추가 Active Directory를 구성 합니다.  
  
|태스크|설명|  
|----|--------|  
|2.1. 추가 Active Directory 사이트 구성|배포에 대 한 추가 Active Directory 사이트를 구성 합니다.|  
|2.2. 추가 도메인 컨트롤러 구성|필요에 따라 추가 Active Directory 도메인 컨트롤러를 구성 합니다.|  
|2.3. 보안 그룹 구성|Windows 7 클라이언트 컴퓨터에 대 한 보안 그룹을 구성 합니다.|  
|2.4. GPO 구성|필요에 따라 추가 그룹 정책 개체를 구성 합니다.|  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_ConfigAD"></a>2.1. 추가 Active Directory 사이트 구성  
모든 진입점은 단일 Active Directory 사이트에 있을 수 있습니다. 따라서 하나 이상의 Active Directory 사이트에이 멀티 사이트 구성에 원격 액세스 서버 구현의 필요 합니다. 첫 번째 Active Directory 사이트를 만들어야 하는 경우 또는 멀티 사이트 배포에 대 한 추가 Active Directory 사이트를 사용 하려는 경우이 절차를 따르십시오. Active Directory 사이트 및 서비스 스냅인을 사용 하 여 새 사이트를 만들 조직의 "s 네트워크입니다.  

멤버는 **Enterprise Admins** 포리스트의 그룹 또는 **Domain Admins** 포리스트 루트 도메인 또는 최소한 해당 그룹의 그룹은이 절차를 완료 해야 합니다. 적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.  

자세한 내용은 참조 [포리스트에 사이트 추가](https://technet.microsoft.com/library/cc732761.aspx)합니다.  

### <a name="to-configure-additional-active-directory-sites"></a>추가 Active Directory 사이트를 구성 하려면  
  
1.  주 도메인 컨트롤러에서 **시작**, 를 클릭 하 고 **Active Directory 사이트 및 서비스**합니다.  
  
2.  Active Directory 사이트 및 서비스 콘솔의 콘솔 트리에서 마우스 오른쪽 단추로 클릭 **사이트**, 를 클릭 하 고 **새 사이트**합니다.  
  
3.  에 **새 개체-사이트** 대화 상자는 **이름** 상자에 새 사이트의 이름을 입력 합니다.  
  
4.  **링크 이름**, 사이트 링크 개체를 클릭 하 고 클릭 한 다음 **확인** 두 번입니다.  
  
5.  콘솔 트리에서 확장 **사이트**, 를 마우스 오른쪽 단추로 클릭 **서브넷**, 를 클릭 하 고 **새 서브넷**합니다.  
  
6.  에 **새 개체-서브넷** 대화 상자의 **접두사**, 에 IPv4 또는 IPv6 서브넷 접두사를 입력의 **이 접두사에 대 한 사이트 개체를 선택** 목록에서이 서브넷과 연결을 클릭 한 다음 사이트를 클릭 **확인**합니다.  
  
7.  배포에 필요한 모든 서브넷을 만든까지 5-6 단계를 반복 합니다.  
  
8.  Active Directory 사이트 및 서비스를 닫습니다.  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
설치 하려면 "Windows PowerShell 용 Active Directory 모듈" Windows 기능:  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
또는 "Active Directory PowerShell 스냅인" OptionalFeatures를 통해 추가 합니다.  
  
Windows 7"또는 Windows Server 2008 r 2에서 다음 cmdlet을 실행 하는 경우에 Active Directory PowerShell 모듈을 가져올 수 있어야 합니다.  
  
```  
Import-Module ActiveDirectory  
```  
  
Active Directory 사이트를 구성 하려면 "두 번째-사이트 라는" 기본 제공 DEFAULTIPSITELINK를 사용 하 여:  
  
```  
New-ADReplicationSite -Name "Second-Site"  
Set-ADReplicationSiteLink -Identity "DEFAULTIPSITELINK" -sitesIncluded @{Add="Second-Site"}  
```  
  
두 번째 사이트에 대 한 IPv4 및 IPv6 서브넷을 구성 합니다.  
  
```  
New-ADReplicationSubnet -Name "10.2.0.0/24" -Site "Second-Site"  
New-ADReplicationSubnet -Name "2001:db8:2::/64" -Site "Second-Site"  
```  
  
## <a name="BKMK_AddDC"></a>2.2. 추가 도메인 컨트롤러 구성  
단일 도메인에서 멀티 사이트 배포를 구성 하려면 배포에서 각 사이트에 대 한 쓰기 가능한 도메인 컨트롤러가 하나 이상 있는지이 좋습니다.  
  
도메인 컨트롤러 설치 되 고 도메인의 Domain Admins 그룹의 구성원 이어야 하는 최소한이 절차를 수행 합니다.  
  
자세한 내용은 참조 [추가 도메인 컨트롤러 설치](https://technet.microsoft.com/library/cc733027.aspx)합니다.
  
### <a name="to-configure-additional-domain-controllers"></a>추가 도메인 컨트롤러를 구성 하려면  
  
1.  도메인 컨트롤러의 역할은 서버에서 **서버 관리자**, 에 **대시보드**, 클릭 **역할 및 기능 추가**합니다.  
  
2.  클릭 **다음** 하 여 서버 역할 선택 화면을 세 번  
  
3.  에 **서버 역할 선택** 페이지에서 선택 **Active Directory 도메인 서비스**합니다. 클릭 **기능 추가** 메시지가 표시 되 고 클릭 **다음** 3 번입니다.  
  
4.  **확인** 페이지에서 **설치**를 클릭합니다.  
  
5.  설치가 성공적으로 완료 되 면 클릭 **이 서버를 도메인 컨트롤러로 승격**합니다.  
  
6.  에 Active Directory 도메인 서비스 구성 마법사에 **배포 구성** 페이지에서 클릭 **기존 도메인에 도메인 컨트롤러 추가**합니다.  
  
7.  **도메인**, 도메인을 입력 이름, 예를 들어 corp.contoso.com입니다.  
  
8.  아래에서 **이 작업을 수행 하는 자격 증명**, 클릭 **변경**합니다. 에 **Windows 보안** 대화 상자에서 추가 도메인 컨트롤러를 설치할 수 있는 계정의 사용자 이름 및 암호를 제공 합니다. 추가 도메인 컨트롤러를 설치하려면 Enterprise Admins 그룹 또는 Domain Admins 그룹의 구성원이어야 합니다. 자격 증명을 제공했으면 **다음**을 클릭합니다.  
  
9. 에 **도메인 컨트롤러 옵션** 페이지에서 다음을 수행 합니다.  
  
    1.  다음과 같은 선택을 합니다.  
  
        -   **도메인 이름 시스템 (DNS) 서버**"이이 옵션은 도메인 컨트롤러를 도메인 이름 시스템 (DNS) 서버로 작동할 수 있도록 기본적으로 선택 됩니다. 도메인 컨트롤러를 DNS 서버로 사용하지 않으려면 이 옵션을 선택 취소합니다.  
  
            포리스트 루트 도메인의 주 도메인 컨트롤러 (PDC) 에뮬레이터에서 DNS 서버 역할 설치 되어 있지 않으면, 추가 도메인 컨트롤러에 DNS 서버 설치 옵션은 사용할 수 없습니다. 이 상황에서이 문제를 해결 하기 전에 또는 AD DS 설치 후 DNS 서버 역할을 설치할 수 있습니다.  
  
            > [!NOTE]  
            > DNS 서버를 설치 하는 옵션을 선택 하면 DNS 서버에 대 한 DNS 위임을 만들 수 없습니다 및 DNS 서버를 신뢰할 수 있는 이름 확인에 DNS 위임을 수동으로 만들어야 되었음을 나타내는 메시지가 나타날 수 있습니다. 포리스트 루트 도메인 또는 트리 루트 도메인에서 추가 도메인 컨트롤러를 설치 하는 경우 DNS 위임을 만들 필요가 없습니다. 이 경우 클릭 **예** 메시지는 무시 합니다.  
  
        -   **글로벌 카탈로그 (GC)**"이이 옵션이 기본적으로 선택 됩니다. 글로벌 카탈로그, 읽기 전용 디렉터리 파티션을 도메인 컨트롤러에 추가하고 글로벌 카탈로그 검색 기능을 사용하도록 설정합니다.  
  
        -   **읽기 전용 도메인 컨트롤러 (RODC)**"이이 옵션은 기본적으로 선택 되지 않습니다. 읽기 전용 이면 추가 도메인 컨트롤러를 사용 하면 즉, 도메인 컨트롤러는 RODC 수 있습니다.  
  
    2.  **사이트 이름**, 를 목록에서 사이트를 선택 합니다.  
  
    3.  아래에서 **디렉터리 서비스 복원 모드 (DSRM) 암호를 입력**,  **암호** 및 **암호 확인**, 를 입력 한 강력한 암호를 두 번 클릭 한 다음 **다음**합니다. DSRM에서 오프 라인으로 수행 해야 하는 작업에 대 한 AD DS를 시작 하려면이 암호를 사용 해야 합니다.  
  
10. 에 **DNS 옵션** 페이지는 **업데이트 DNS 위임** 역할 설치 중에 DNS 위임 업데이트 한 다음 클릭 하려면 확인란 **다음**.  
  
11. 에 **추가 옵션** 페이지 입력 하거나 데이터베이스 파일, 디렉터리 서비스 로그 파일 및 시스템 볼륨 (SYSVOL) 파일에 대 한 볼륨 및 폴더 위치를 찾습니다. 필요에 따라 복제 옵션을 지정 하 고 클릭 한 다음 **다음**합니다.  
  
12. 에 **옵션 검토** 페이지, 설치 옵션을 검토 한 다음 클릭 **다음**합니다.  
  
13. 에 **필수 구성 요소 확인** 페이지에서 필수 구성 요소가 확인 되 면 클릭 **설치**합니다.  
  
14. 마법사가 구성을 완료 될 때까지 기다린 다음 클릭 **닫기**합니다.  
  
15. 자동으로 시작 되지 않은 경우 컴퓨터를 다시 시작 합니다.  
  
## <a name="BKMK_ConfigSG"></a>2.3. 보안 그룹 구성  
멀티 사이트 배포는 Windows 7 클라이언트 컴퓨터에 액세스할 수 있는 배포의 모든 진입점에 대 한 Windows 7 클라이언트 컴퓨터에 대 한 추가 보안 그룹을 필요 합니다. Windows 7 클라이언트 컴퓨터를 포함 하는 여러 도메인에 있는 동일한 진입점에 대 한 각 도메인에서 보안 그룹을 만드는 권장 됩니다. 또는 두 도메인 모두에서 클라이언트 컴퓨터를 포함 하는 하나의 유니버설 보안 그룹을 사용할 수 있습니다. 예를 들어 두 도메인이 있는 환경에서 항목에 없지만 1과 3 이며 진입점에 Windows 7 클라이언트 컴퓨터에 대 한 액세스를 허용 하려는 경우 2, 다음 각 도메인의 각 진입점에 대 한 Windows 7 클라이언트 컴퓨터를 포함 하도록 두 개의 새 보안 그룹을 만들 합니다.  
  
### <a name="to-configure-additional-security-groups"></a>추가 보안 그룹을 구성 하려면  
  
1.  주 도메인 컨트롤러에서 **시작**, 를 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다.  
  
2.  콘솔 트리에서 corp.contoso.com/Users 예를 들어, 새 그룹을 추가 하려는 폴더를 마우스 오른쪽 단추로 클릭 합니다. 가리킨 **새로**, 를 클릭 하 고 **그룹**합니다.  
  
3.  에 **새 개체-그룹** 대화 상자의 **그룹 이름**, 예를 들어 Win7_Clients_Entrypoint1 새 그룹의 이름을 입력 합니다.  
  
4.  아래에서 **그룹 범위**, 클릭 **범용**, 아래에서 **그룹 종류**, 클릭 **보안**, 를 클릭 하 고 **확인**합니다.  
  
5.  컴퓨터에 새 보안 그룹을 추가 하려면 보안 그룹을 두 번 클릭 및는 **< o u p _ > 속성** 대화 상자를 클릭 하는 **멤버** 탭 합니다.  
  
6.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
7.  이 보안 그룹에 추가 하 고 클릭 한 다음 Windows 7 컴퓨터 선택 **확인**합니다.  
  
8.  필요에 따라 모든 진입점에 대 한 보안 그룹을 만들기 위해이 절차를 반복 합니다.  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
설치 하려면 "Windows PowerShell 용 Active Directory 모듈" Windows 기능:  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
또는 "Active Directory PowerShell 스냅인" OptionalFeatures를 통해 추가 합니다.  
  
Windows 7"또는 Windows Server 2008 r 2에서 다음 cmdlet을 실행 하는 경우에 Active Directory PowerShell 모듈을 가져올 수 있어야 합니다.  
  
```  
Import-Module ActiveDirectory  
```  
  
Win7_Clients_Entrypoint1 라는 보안 그룹을 구성 하 고 CLIENT2 라는 클라이언트 컴퓨터를 추가 하려면:  
  
```  
New-ADGroup -GroupScope universal -Name Win7_Clients_Entrypoint1  
Add-ADGroupMember -Identity Win7_Clients_Entrypoint1 -Members CLIENT2$  
```  
  
## <a name="ConfigGPOs"></a>2.4. GPO 구성  
멀티 사이트 원격 액세스 배포에는 다음 그룹 정책 개체 사항이 필요합니다.  
  
-   원격 액세스 서버에 대 한 모든 진입점에 대 한 GPO 합니다.  
  
-   각 도메인에 대 한 모든 Windows 8 클라이언트 컴퓨터에 대 한 GPO입니다.  
  
-   Windows 7 클라이언트 컴퓨터에서 각 진입점에 대 한 포함 된 각 도메인에서 GPO 클라이언트를 Windows 7을 지원 하도록 구성 합니다.  
  
    > [!NOTE]  
    > Windows 7 클라이언트 컴퓨터를 하지 않은 경우 Gpo에 대 한 Windows 7 컴퓨터를 만들 필요가 없습니다.  
  
원격 액세스를 구성할 때 자동으로 만들어집니다 필요한 그룹 정책 개체 "t 이미 존재 않으면 합니다. 그룹 정책 개체를 만드는 데 필요한 권한이 없는 경우 원격 액세스를 구성 하기 전에 생성 되어야 합니다. DirectAccess 관리자는 Gpo에 대 한 모든 권한을 갖고 있어야 (편집 + 보안 수정 + 삭제).  
  
> [!IMPORTANT]  
> 원격 액세스 Gpo를 수동으로 만든 후 Active Directory 및 원격 액세스 서버와 연결 된 Active Directory 사이트에 도메인 컨트롤러에 DFS 복제에 대 한 충분 한 시간을 허용 해야 합니다. 원격 액세스에서 자동으로 그룹 정책 개체를 만든 경우 대기 시간이 없는 필요 합니다.  
  
그룹 정책 개체를 만들려면 참조 [만들고 그룹 정책 개체 편집](https://technet.microsoft.com/library/cc754740.aspx)합니다.  
  
### <a name="DCMaintandDowntime"></a>도메인 컨트롤러가 유지 관리 및 가동 중지 시간  
PDC 에뮬레이터 역할을 실행 하는 도메인 컨트롤러 또는 서버 Gpo를 관리 하는 도메인 컨트롤러는 가동 중지 시간을 발생 하는 경우 로드 하거나 원격 액세스 구성을 수정 하는 것이 불가능 합니다. 다른 도메인 컨트롤러를 사용할 수 있는 경우 클라이언트 연결 되지 영향이 수 있습니다.  
  
을 로드 하거나 원격 액세스 구성을 수정 하려면 클라이언트 또는 응용 프로그램 서버 Gpo;에 대 한 다른 도메인 컨트롤러에 PDC 에뮬레이터 역할을 전송할 수 있습니다. 서버 Gpo에 대 한 서버 Gpo를 관리 하는 도메인 컨트롤러를 변경 합니다.  
  
> [!IMPORTANT]  
> 도메인 관리자가만이 작업을 수행할 수 있습니다. 주 도메인 컨트롤러 변경에 따른 결과 원격 액세스를 제한 되지 않습니다. 따라서 PDC 에뮬레이터 역할을 전송 하는 경우 주의 해야 합니다.  
  
> [!NOTE]  
> 도메인 컨트롤러 연결을 수정 하기 전에 모든 원격 액세스 배포에서 Gpo의 모든 도메인의 도메인 컨트롤러에 복제 되었는지 확인 합니다. GPO 동기화 되지 않으면 최근 구성 변경 내용을 손실 될 구성이 손상 시킬 수 있는 도메인 컨트롤러 연결을 수정한 후 합니다. GPO 동기화를 확인 하려면 참조 [그룹 정책 인프라 상태 확인](https://technet.microsoft.com/library/jj134176.aspx)합니다.  
  
#### <a name="TransferPDC"></a>PDC 에뮬레이터 역할을 전송 하려면  
  
1.  에 **시작** 화면에서 입력**dsa.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  Active Directory 사용자 및 컴퓨터 콘솔의 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **Active Directory 사용자 및 컴퓨터**, 를 클릭 하 고 **도메인 컨트롤러 변경**합니다. 디렉터리 서버 변경 대화 상자에서 클릭 **이 도메인 컨트롤러 또는 AD LDS 인스턴스**, 의 목록에 새 역할 소유자를 클릭 한 다음 도메인 컨트롤러를 클릭 합니다. **확인**합니다.  
  
    > [!NOTE]  
    > 역할을 전송 하려면 도메인 컨트롤러에 없는 경우이 단계를 수행 해야 합니다. 역할을 전송 하려면 도메인 컨트롤러에 이미 연결한 경우에이 단계를 수행 하지 마십시오.  
  
3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **Active Directory 사용자 및 컴퓨터**, 가리킨 **모든 작업**, 를 클릭 하 고 **작업 마스터**합니다.  
  
4.  작업 마스터 대화 상자에서 클릭 된 **PDC** 탭을 클릭 한 후 **변경**합니다.  
  
5.  클릭 **예** 하는 역할을 전송 하 고 클릭 한 다음 확인을 **닫기**합니다.  
  
#### <a name="ChangeDC"></a>서버 Gpo를 관리 하는 도메인 컨트롤러를 변경 하려면  
  
-   Windows PowerShell cmdlet을 실행  `HYPERLINK "https://technet.microsoft.com/library/hh918412.aspx" Set-DAEntryPointDC` 원격 액세스 서버에 연결할 수 없는 도메인 컨트롤러의 이름을 지정 하 고는 *ExistingDC* 매개 변수입니다. 이 명령은 해당 도메인 컨트롤러에서 현재 관리 되는 진입점의 서버 Gpo에 대 한 도메인 컨트롤러 연결을 수정 합니다.  
  
    -   도메인 컨트롤러 "dc2.corp.contoso.com"와 "dc1.corp.contoso.com" 연결할 수 없는 도메인 컨트롤러를 바꾸려면 다음을 수행 합니다.  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "NewDC 'dc2.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
    -   연결할 수 없는 도메인 컨트롤러 "dc1.corp.contoso.com"와 "DA1.corp.contoso.com" 원격 액세스 서버에 가장 가까운 Active Directory 사이트에 도메인 컨트롤러를 바꾸려면 다음을 수행 합니다.  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
### <a name="ChangeTwoDCs"></a>서버 Gpo를 관리 하는 두 개 이상의 도메인 컨트롤러를 변경 합니다.  
사례 수가 최소 서버 Gpo를 관리 하는 도메인 컨트롤러 두 개 이상 제공 되지 않습니다. 이 경우 서버 Gpo에 대 한 도메인 컨트롤러 연결을 변경 하려면 더 많은 단계가 필요한 합니다.  
  
원격 액세스 서버의 레지스트리에 모든 서버 Gpo에서 도메인 컨트롤러 연결 정보가 저장 됩니다. 다음 예제에서 두 명의 원격 액세스 서버를 "DA1" 인 두 개의 진입점에 있는 "1" 및 "d a 2"의 진입점 "진입점 2"입니다. "진입점 1"의 서버 GPO의 서버 GPO 하는 동안 도메인 컨트롤러 "d c 1"에서 관리 하는 "진입점 2"는 "DC2" 도메인 컨트롤러에서 관리 합니다. "D c 1" 및 "d c 2"을 모두 사용할 수 있습니다. 세 번째 도메인 컨트롤러 "DC3" 도메인에서 이용할 수 있으며 "DC1" 및 "d c 2"에서 데이터를 이미 "DC3"에 복제 됩니다.  
  
![멀티 사이트 인프라 구성](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc1.png)  
  
##### <a name="to-change-two-or-more-domain-controllers-that-manage-server-gpos"></a>서버 Gpo를 관리 하는 두 개 이상의 도메인 컨트롤러를 변경 하려면  
  
1.  도메인 컨트롤러 "DC3"와 "d c 2"에서 사용할 수 없는 도메인 컨트롤러를 바꾸려면 다음 명령을 입력 합니다.  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    이 명령은 도메인 컨트롤러에 대 한 연결 "진입점 2" 서버 GPO 레지스트리에 "진입점 2" 서버 GPO 자체 및 d a 2의 업데이트 그러나 업데이트 되지 않습니다 "진입점 1" 서버 GPO를 통해 관리 하는 도메인 컨트롤러를 사용할 수 없기 때문입니다.  
  
    > [!TIP]  
    > 이 명령은 계속 값을 사용 하 여는 *ErrorAction* "진입점 1" 서버 GPO를 업데이트 하려면 실패 해도 "진입점 2" 서버 GPO를 업데이트 하는 매개 변수입니다.  
  
    결과적인 구성이 아래 다이어그램에 표시 됩니다.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc2.png)  
  
2.  도메인 컨트롤러 "DC3"와 "d c 1"에서 사용할 수 없는 도메인 컨트롤러를 바꾸려면 다음 명령을 입력 합니다.  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC1' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    이 명령은 "진입점 1" 및 "진입점 1" 및 "진입점 2" DA1의 레지스트리에 서버 GPO 서버 Gpo에 대 한 도메인 컨트롤러 연결을 업데이트합니다. 결과적인 구성이 아래 다이어그램에 표시 됩니다.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc3.png)  
  
3.  GPO "DC3"와 "d c 2"을 대체 하 고 해당 서버가 GPO 동기화 되지 않으므로,이 경우 원격 액세스 서버를 지정 하는 명령을 실행 하는 "진입점 1" 서버에서 "진입점 2" 서버 GPO에 대 한 도메인 컨트롤러 연결을 동기화 하려면 "DA1"에 대 한는 *ComputerName* 매개 변수입니다.  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA1' "ErrorAction Continue  
    ```  
  
    최종 구성은 다음 다이어그램에 표시 됩니다.  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssocFinal.png)  
  
### <a name="ConfigDistOptimization"></a>구성 배포의 최적화  
구성 변경 작업을 수행 하는 경우 서버 Gpo 원격 액세스 서버에 전파 된 후에 변경 내용이 적용 됩니다. 구성 배포 시간을 줄이기 위해 원격 액세스를 자동으로 선택 하이퍼링크는 쓰기 가능한 도메인 컨트롤러 "https://technet.microsoft.com/library/cc978016.aspx" 해당 서버 GPO를 만들 때 원격 액세스 서버에 가장 가까운 합니다.  
  
일부 시나리오에서는 해야 구성 배포 시간을 최적화 하기 위해 서버 GPO를 관리 하는 도메인 컨트롤러를 수동으로 수정 해야 합니다.  
  
-   진입점으로 추가 시 원격 액세스 서버의 Active Directory 사이트에 쓰기 가능한 도메인 컨트롤러가 없는 했습니다. 쓰기 가능한 도메인 컨트롤러는 이제 원격 액세스 서버의 Active Directory 사이트에 추가 되 고 있습니다.  
  
-   IP 주소 변경, 또는 Active Directory 사이트 및 서브넷 변경 될 수 있습니다 다른 Active Directory 사이트도 원격 액세스 서버를 전환 했습니다.  
  
-   도메인 컨트롤러가 다시 온라인 상태가 되는 이제 하 진입점에 대 한 도메인 컨트롤러 연결 수동으로 도메인 컨트롤러에서 유지 관리 작업으로 인해 수정 합니다.  
  
이러한 시나리오에서는 PowerShell cmdlet을 실행 `Set-DAEntryPointDC` 원격 액세스 서버에서 매개 변수를 사용 하 여 최적화 하려면 진입점의 이름을 지정 하 고 *EntryPointName*합니다. 현재 GPO를 이미 완전히 원하는 새 도메인 컨트롤러에 복제 하는 서버를 저장 하는 도메인 컨트롤러에서 GPO 데이터 후에 수행 해야 있습니다.  
  
> [!NOTE]  
> 도메인 컨트롤러 연결을 수정 하기 전에 모든 원격 액세스 배포에서 Gpo의 모든 도메인의 도메인 컨트롤러에 복제 되었는지 확인 합니다. GPO 동기화 되지 않으면 최근 구성 변경 내용을 손실 될 구성이 손상 시킬 수 있는 도메인 컨트롤러 연결을 수정한 후 합니다. GPO 동기화를 확인 하려면 참조 [그룹 정책 인프라 상태 확인](https://technet.microsoft.com/library/jj134176.aspx)합니다.  
  
구성 배포 시간을 최적화 하려면 다음 중 하나를 수행 합니다.  
  
-   서버를 관리 하려면 GPO 항목의 서버를 가리키도록 "진입점 1" 가장 가까운 Active Directory 사이트에 도메인 컨트롤러에 원격 액세스 "DA1.corp.contoso.com" 다음 명령을 실행 합니다.  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
-   서버를 관리 하려면 GPO 항목의 "진입점 1"에서 가리킨는 도메인 컨트롤러 "dc2.corp.contoso.com", 다음 명령을 실행:  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "NewDC 'dc2.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
    > [!NOTE]  
    > 에 대 한 해당 진입점의 구성원 인 원격 액세스 서버를 지정 해야 특정 진입점과 연결 된 도메인 컨트롤러를 수정할 때는 *ComputerName* 매개 변수입니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [3 단계: 멀티 사이트 배포를 구성 합니다.](Step-3-Configure-the-Multisite-Deployment.md)  
-   [1단계: 단일 서버 원격 액세스 배포 구현](Step-1-Implement-a-Single-Server-Remote-Access-Deployment.md)  

