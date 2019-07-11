---
ms.assetid: d2429185-9720-4a04-ad94-e89a9350cdba
title: 클라우드 폴더 배포
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dongill
ms.author: jgerend
ms.date: 6/24/2017
description: 서버 역할을 설치하고 동기화 공유를 만들고 DNS 레코드를 만드는 방법을 포함하여 클라우드 폴더를 배포하는 방법을 설명합니다.
ms.openlocfilehash: d2ba117a021cfc7361c0f7c8df2ed9f3c4bc9d94
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792336"
---
# <a name="deploying-work-folders"></a>클라우드 폴더 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

이 항목에서는 클라우드 폴더를 배포할 때 거쳐야 할 단계적 절차에 대해 설명하며, 독자가 [클라우드 폴더 배포 계획](plan-work-folders.md)을 이미 읽어본 것으로 가정합니다.  
  
 여러 서버와 기술을 포함할 수 있는 클라우드 폴더를 배포하려면 다음 단계를 사용하세요.  
  
> [!TIP]
>  가장 간단한 클라우드 폴더 배포는 인터넷을 통한 동기화를 지원하지 않는 단일 파일 서버(종종 동기화 서버라고도 함)이며, 테스트 랩이나 도메인에 가입된 클라이언트 컴퓨터의 동기화 솔루션으로 유용한 배포일 수 있습니다. 단순 배포를 만들기 위해 따라야 하는 최소 단계는 다음과 같습니다. 
>  -   1단계: SSL 인증서 가져오기  
>  -   2단계: DNS 레코드 만들기 
>  -   3단계: 파일 서버에 클라우드 폴더 설치  
>  -   4단계: 동기화 서버에서 SSL 인증서 바인딩
>  -   5단계: 클라우드 폴더에 대한 보안 그룹 만들기  
>  -   7단계: 사용자 데이터에 대한 동기화 공유 만들기  
  
## <a name="step-1-obtain-ssl-certificates"></a>1단계: SSL 인증서 가져오기  
 클라우드 폴더는 HTTPS를 사용하여 클라우드 폴더 클라이언트와 클라우드 폴더 서버 간에 안전하게 파일을 동기화합니다. 클라우드 폴더에서 사용되는 SSL 인증서에 대한 요구 사항은 다음과 같습니다.  
  
- 신뢰할 수 있는 인증 기관에서 발급한 인증서여야 합니다. 대부분의 클라우드 폴더 구현에서는 도메인에 가입되지 않은 인터넷 기반 장치에서 인증서를 사용하므로 공개적으로 신뢰할 수 있는 CA가 권장됩니다.  
  
- 인증서가 유효해야 합니다.  
  
- 여러 서버에 인증서를 설치해야 하므로 인증서의 프라이빗 키를 내보낼 수 있어야 합니다.  
  
- 인증서의 주체 이름에 인터넷에서 클라우드 폴더 서비스를 검색하는 데 사용되는 공용 클라우드 폴더 URL이 포함되어 있어야 합니다(`workfolders.` *<domain_name>* 형식이어야 함).  
  
- 사용 중인 각 동기화 서버의 서버 이름이 나열된 인증서에 SAN(주체 대체 이름)이 있어야 합니다.

  클라우드 폴더 인증서 관리 [블로그](https://blogs.technet.microsoft.com/filecab/2013/08/09/work-folders-certificate-management/)는 클라우드 폴더에 인증서를 사용하는 방법에 대한 추가 정보를 제공합니다.
  
## <a name="step-2-create-dns-records"></a>2단계: DNS 레코드 만들기  
 사용자가 인터넷을 통해 동기화하도록 허용하려면 인터넷 클라이언트에서 클라우드 폴더 URL을 확인할 수 있도록 공용 DNS에 호스트(A) 레코드를 만들어야 합니다. 이 DNS 레코드는 역방향 프록시 서버의 외부 인터페이스로 확인되어야 합니다.  
  
 내부 네트워크에서, DNS에 클라우드 폴더 서버의 FDQN을 확인하는 workfolders라는 이름의 CNAME 레코드를 만듭니다 작업 폴더 클라이언트가 자동 검색을 사용 하는 경우 클라우드 폴더 서버를 검색 하는 데 사용 하는 URL은 https:\//workfolders.domain.com 합니다. 자동 검색을 사용하려면 DNS에 workfolders CNAME 레코드가 있어야 합니다.  
  
## <a name="step-3-install-work-folders-on-file-servers"></a>3단계: 파일 서버에 클라우드 폴더 설치  
 서버 관리자를 사용하거나 로컬 또는 네트워크에서 원격으로 Windows PowerShell을 사용하여 도메인에 가입된 서버에 클라우드 폴더를 설치할 수 있습니다. 이는 네트워크에서 여러 동기화 서버를 구성하는 경우에 유용합니다.  
  
서버 관리자에서 역할을 배포하려면 다음을 수행합니다.  
  
1.  **역할 및 기능 추가 기능 마법사**를 시작합니다.  
  
2.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 배포**를 선택합니다.  
  
3.  **대상 서버 선택** 페이지에서 클라우드 폴더를 설치할 서버를 선택합니다.  
  
4.  **서버 역할 선택** 페이지에서 **File and Storage Services**를 확장하고 **파일 및 iSCSI 서비스**를 확장한 다음 **클라우드 폴더**를 선택합니다.  
  
5.  **IIS 호스팅 가능한 웹 코어**를 설치할 것인지 묻는 메시지가 나타나면 **확인**을 클릭하여 클라우드 폴더에 필요한 최소 버전의 IIS(인터넷 정보 서비스)를 설치합니다.  
  
6.  마법사를 완료할 때까지 **다음**을 클릭합니다.

Windows PowerShell을 사용하여 역할을 배포하려면 다음 cmdlet을 사용합니다.
  
```powershell  
Add-WindowsFeature FS-SyncShareService  
```

## <a name="step-4-binding-the-ssl-certificate-on-the-sync-servers"></a>4단계: 동기화 서버에서 SSL 인증서 바인딩
 클라우드 폴더는 IIS를 전체 설치하지 않고도 웹 서비스를 사용할 수 있도록 설계된 IIS 구성 요소인 IIS 호스팅 가능한 웹 코어를 설치합니다. IIS 호스팅 가능한 웹 코어를 설치한 후에는 서버의 SSL 인증서를 파일 서버의 기본 웹 사이트에 바인딩해야 합니다. 그러나 IIS 호스팅 가능한 웹 코어는 IIS 관리 콘솔을 설치하지 않습니다.

 인증서를 기본 웹 인터페이스에 바인딩하는 옵션에는 두 가지가 있습니다. 두 옵션 중 하나를 사용하려면 컴퓨터의 개인 저장소에 인증서의 개인 키를 설치해야 합니다.

- 서버에 설치된 IIS 관리 콘솔을 사용합니다. 콘솔 내에서 관리할 파일 서버에 연결한 다음 해당 서버의 기본 웹 사이트를 선택합니다. 기본 웹 사이트는 사용되지 않는 것으로 표시되지만 사이트의 바인딩을 편집하고 인증서를 선택하여 해당 웹 사이트에 바인딩할 수 있습니다.

- netsh 명령을 사용하여 인증서를 기본 웹 사이트 https 인터페이스에 바인딩합니다. 명령은 다음과 같습니다.

    ```
    netsh http add sslcert ipport=<IP address>:443 certhash=<Cert thumbprint> appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY
    ```

## <a name="step-5-create-security-groups-for-work-folders"></a>5단계: 클라우드 폴더에 대한 보안 그룹 만들기
 동기화 공유를 만들기 전에 Domain Admins 또는 Enterprise Admins 그룹의 구성원이 AD DS(Active Directory Domain Services)에 클라우드 폴더에 대한 몇 가지 보안 그룹을 만들어야 합니다(6단계에 설명된 대로 일부 제어 권한을 위임할 수도 있음). 필요한 그룹은 다음과 같습니다.

- 동기화 공유당 하나의 그룹 - 동기화 공유와 동기화할 수 있는 사용자 지정

- 모든 클라우드 폴더 관리자를 위한 하나의 그룹 - 클라우드 폴더 관리자가 사용자를 올바른 동기화 서버로 연결(여러 동기화 서버를 사용하는 경우)하는 각 사용자 개체에 대한 특성을 편집할 수 있음

  그룹은 표준 명명 규칙을 따라야 하며, 다른 보안 요구 사항과의 잠재적 충돌을 피하기 위해 클라우드 폴더에만 사용해야 합니다.

  적절한 보안 그룹을 만들려면 각 동기화 공유에 대해 다음 절차를 수행하고, 필요한 경우 파일 서버 관리자 그룹을 만들 때 다음 절차를 수행합니다.

#### <a name="to-create-security-groups-for-work-folders"></a>클라우드 폴더에 대한 보안 그룹을 만들려면

1. Active Directory 관리 센터가 설치된 Windows Server 2012 R2 또는 Windows Server 2016 컴퓨터에서 서버 관리자를 엽니다.

2.  **도구** 메뉴에서 **Active Directory 관리 센터**를 클릭합니다. Active Directory 관리 센터가 표시됩니다.

3.  새 그룹을 만들 컨테이너(예: 적절한 도메인 또는 OU의 사용자 컨테이너)를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **그룹**을 클릭합니다.

4.  **그룹 만들기** 창의 **그룹** 섹션에서 다음 설정을 지정합니다.

    -   **그룹 이름**에 보안 그룹의 이름(예: **HR Sync Share Users** 또는 **Work Folders Administrators**)을 입력합니다.  
  
    -   **그룹 범위**에서 **보안**을 클릭한 다음 **전역**을 클릭합니다.  
  
5.  **구성원** 섹션에서 **추가**를 클릭합니다. 사용자, 연락처, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 나타납니다.  
  
6.  특정 동기화 공유에 대한 액세스 권한을 부여할 사용자 또는 그룹의 이름(그룹을 만들어 동기화 공유에 대한 액세스를 제어하려는 경우)을 입력하거나, 클라우드 폴더 관리자의 이름(적절한 동기화 서버를 자동으로 검색하도록 사용자 계정을 구성하려는 경우)을 입력하고 **확인**을 클릭한 다음 **확인**을 다시 클릭합니다.

Windows PowerShell을 사용하여 보안 그룹을 만들려면 다음 cmdlet을 사용합니다.

```powershell  
$GroupName = "Work Folders Administrators"  
$DC = "DC1.contoso.com"  
$ADGroupPath = "CN=Users,DC=contoso,DC=com"  
$Members = "CN=Maya Bender,CN=Users,DC=contoso,DC=com","CN=Irwin Hume,CN=Users,DC=contoso,DC=com"  
  
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:$GroupName -Path:$ADGroupPath -SamAccountName:$GroupName -Server:$DC  
Set-ADGroup -Add:@{'Member'=$Members} -Identity:$GroupName -Server:$DC
```

## <a name="step-6-optionally-delegate-user-attribute-control-to-work-folders-administrators"></a>6단계: 클라우드 폴더 관리자에게 사용자 특성 제어 권한 위임(선택 사항)  
 여러 동기화 서버를 배포하고 사용자를 올바른 동기화 서버로 자동 연결하려면 AD DS에서 각 사용자 계정에 대한 특성을 업데이트해야 합니다. 그러나 이렇게 하려면 일반적으로 Domain Admins 또는 Enterprise Admins 그룹의 구성원에게 특성을 업데이트하게 해야 하므로 사용자를 자주 추가하거나 동기화 서버 간에 이동해야 하는 경우 번거로운 작업이 될 수 있습니다.  
  
 따라서 Domain Admins 또는 Enterprise Admins 그룹의 구성원은 다음 절차에 설명된 대로 5단계에서 만든 Work Folders Administrators 그룹에 사용자 개체의 msDS-SyncServerURL 속성을 수정할 수 있는 권한을 위임할 수 있습니다.  
  
#### <a name="delegate-the-ability-to-edit-the-msds-syncserverurl-property-on-user-objects-in-ad-ds"></a>AD DS에서 사용자 개체에 대한 msDS-SyncServerURL 속성을 편집할 수 있는 권한 위임  
  
1.  Active Directory 사용자 및 컴퓨터가 설치된 Windows Server 2012 R2 또는 Windows Server 2016 컴퓨터에서 서버 관리자를 엽니다.  
  
2.  **도구** 메뉴에서 **Active Directory 사용자 및 컴퓨터**를 클릭합니다. Active Directory 사용자 및 컴퓨터가 표시됩니다.  
  
3.  클라우드 폴더에 대한 모든 사용자 개체가 있는 OU(사용자가 여러 OU 또는 도메인에 저장된 경우 모든 사용자에게 공통적인 컨테이너)를 마우스 오른쪽 단추로 클릭한 다음 **제어 위임...** 을 클릭합니다. 제어 위임 마법사가 나타납니다.  
  
4.  **사용자 또는 그룹** 페이지에서 **추가…** 를 클릭합니다. 를 클릭한 다음 클라우드 폴더 관리자에 대해 만든 그룹(예: **Work Folders Administrators**)을 지정합니다.  
  
5.  **위임할 작업** 페이지에서 **위임할 사용자 지정 작업 만들기**를 클릭합니다.  
  
6.  **Active Directory 개체 형식** 페이지에서 **폴더에 있는 다음 개체만**을 클릭한 다음 **사용자 개체** 확인란을 선택합니다.  
  
7.  **사용 권한** 페이지에서 **일반** 확인란의 선택을 취소하고 **속성별** 확인란을 선택한 다음 **msDS-SyncServerUrl 읽기** 및 **msDS-SyncServerUrl 쓰기** 확인란을 선택합니다.

Windows PowerShell을 사용하여 사용자 개체에 대한 msDS-SyncServerURL 속성을 편집할 수 있는 권한을 위임하려면 DsAcls 명령을 사용하는 다음 예제 스크립트를 사용하세요.
  
```powershell  
$GroupName = "Contoso\Work Folders Administrators"  
$ADGroupPath = "CN=Users,dc=contoso,dc=com"  
  
DsAcls $ADGroupPath /I:S /G ""$GroupName":RPWP;msDS-SyncServerUrl;user"  
```  
  
> [!NOTE]
>  사용자 수가 많은 도메인에서 위임 작업을 실행할 경우 약간의 시간이 걸릴 수 있습니다.  
  
## <a name="step-7-create-sync-shares-for-user-data"></a>7단계: 사용자 데이터에 대한 동기화 공유 만들기  
 이제 동기화 서버에서 사용자 파일을 저장할 폴더를 지정할 준비가 완료되었습니다. 이 폴더를 동기화 공유라고 하며, 다음 절차를 사용하여 만들 수 있습니다.  
  
1. 동기화 공유 폴더와 그 안에 들어갈 사용자 파일을 저장할 여유 공간을 가진 NTFS 볼륨이 없는 경우에는 새 볼륨을 만들고 NTFS 파일 시스템으로 포맷합니다.  
  
2. 서버 관리자에서 **파일 및 저장소 서비스**를 클릭한 다음 **클라우드 폴더**를 클릭합니다.  
  
3. 기존 동기화 공유 목록이 세부 정보 창의 위쪽에 표시됩니다. 새 동기화 공유를 만들려면 **작업** 메뉴에서 **새 동기화 공유...** 를 선택합니다. 새 동기화 공유 마법사가 나타납니다.  
  
4. **서버 및 경로 선택** 페이지에서 동기화 공유를 저장할 위치를 지정합니다. 이 사용자 데이터용으로 만들어진 파일 공유가 이미 있는 경우 해당 공유를 선택해도 됩니다. 또는 새 폴더를 만들 수 있습니다.  
  
   > [!NOTE]
   >  기본적으로 동기화 공유에는 기존 파일 공유를 선택한 경우 외에는 파일 공유를 통해 직접 액세스할 수 없습니다. 파일 공유를 통해 동기화 공유에 액세스할 수 있도록 하려면 서버 관리자의 **공유** 타일 또는 [New-SmbShare](https://technet.microsoft.com/library/jj635722.aspx) cmdlet을 사용하여 파일 공유를 만드세요. 이때 액세스 기반 열거를 사용하는 것이 좋습니다.  
  
5. **사용자 폴더의 구조 지정** 페이지에서 동기화 공유 내 사용자 폴더에 대한 명명 규칙을 선택합니다. 사용 가능한 두 가지 옵션이 있습니다.  
  
   - **사용자 별칭** - 도메인 이름을 포함하지 않는 사용자 폴더를 만듭니다. 폴더 리디렉션 또는 다른 사용자 데이터 솔루션에서 이미 사용 중인 파일 공유를 사용하려면 이 명명 규칙을 선택합니다. 필요한 경우 **다음 하위 폴더만 동기화** 확인란을 선택하여 문서 폴더와 같은 특정 하위 폴더만 동기화할 수 있습니다.  
  
   - <strong>사용자 alias@domain</strong> - 도메인 이름을 포함하는 사용자 폴더를 만듭니다. 폴더 리디렉션 또는 다른 사용자 데이터 솔루션에서 이미 사용 중인 파일 공유를 사용하지 않으려면 이 명명 규칙을 선택하여 공유의 여러 사용자에게 동일한 별칭이 있는 경우에 발생할 수 있는 폴더 이름 지정 충돌(사용자가 여러 도메인에 속한 경우에 발생할 수 있음)을 방지합니다.  
  
6. **동기화 공유 이름 입력** 페이지에서 파일 공유의 이름과 설명을 지정합니다. 이는 네트워크에 보급되는 것이 아니라 동기화 공유를 쉽게 구분할 수 있도록 서버 관리자 및 Windows Powershell에 표시됩니다.  
  
7. **그룹에 동기화 액세스 부여** 페이지에서 이 동기화 공유를 사용하도록 허용된 사용자를 나열할 그룹을 지정합니다.  
  
   > [!IMPORTANT]
   >  성능 및 보안을 향상시키려면 개별 사용자 대신 그룹에 액세스 권한을 부여하고 Authenticated Users 및 Domain Users와 같은 일반적인 그룹이 아니라 가능한 한 특정 그룹을 지정하십시오. 사용자 수가 많은 그룹에 액세스 권한을 부여하면 클라우드 폴더에서 AD DS를 쿼리하는 데 걸리는 시간이 증가합니다. 사용자 수가 많은 경우 여러 동기화 공유를 만들어 부하를 분산시킬 수 있습니다.  
  
8. **장치 정책 지정** 페이지에서 클라이언트 PC와 장치에 대한 보안 제한을 요청할지 지정합니다. 개별적으로 선택할 수 있는 장치 정책에는 다음 두 가지가 있습니다.  
  
   -   **클라우드 폴더 암호화** 클라이언트 PC와 장치에서 클라우드 폴더를 암호화하도록 요청합니다.  
  
   -   **자동으로 화면 잠금 및 암호 설정** 클라이언트 PC와 장치에서 15분 후에 해당 화면을 자동으로 잠그도록 요청합니다. 화면 잠금을 해제하려면 6자 이상의 암호가 필요하며, 재시도에 10번 실패한 후에는 장치 잠금 모드가 활성화됩니다.  
  
       > [!IMPORTANT]
       >  Windows 7 PC에 그리고 도메인에 가입된 PC의 관리자가 아닌 사용자에 대해 암호 정책을 적용하려면 컴퓨터 도메인에 대한 그룹 정책 암호 정책을 사용하고 이러한 도메인을 클라우드 폴더 암호 정책에서 제외합니다. 동기화 공유를 만든 후 [Set-Syncshare -PasswordAutoExcludeDomain](https://technet.microsoft.com/library/dn296649\(v=wps.630\).aspx) cmdlet을 사용하여 도메인을 제외할 수 있습니다. 그룹 정책 암호 정책을 설정하는 방법에 대한 자세한 내용은 [암호 정책](https://technet.microsoft.com/library/hh994572(v=ws.11).aspx)을 참조하세요.  
  
9. 선택 항목을 검토하고 마법사를 완료하여 동기화 공유를 만듭니다.

[New-SyncShare](https://technet.microsoft.com/library/dn296635.aspx) cmdlet을 사용하여 Windows PowerShell에서 동기화 공유를 만들 수 있습니다. 다음은 이 방법의 예입니다.  
  
```powershell  
New-SyncShare "HR Sync Share" K:\Share-1 –User "HR Sync Share Users"  
```  
  
위 예에서는 이름이 *Share01*이고 경로가 *K:\Share-1*이며, *HR Sync Share Users* 그룹에 대한 액세스 권한이 부여된 새 동기화 공유를 만듭니다.  
  
> [!TIP]
>  동기화 공유를 만든 후에는 파일 서버 리소스 관리자 기능을 사용하여 공유의 데이터를 관리할 수 있습니다. 예를 들어 서버 관리자의 클라우드 폴더 페이지에 있는 **할당량** 타일을 사용하여 사용자 폴더에 대한 할당량을 설정할 수 있습니다. 또한 [파일 차단 관리](https://technet.microsoft.com/library/cc732074.aspx)를 사용하여 클라우드 폴더에서 동기화할 파일 형식을 제어하거나, [동적 액세스 제어](https://technet.microsoft.com/windows-server-docs/identity/solution-guides/dynamic-access-control--scenario-overview)에 설명된 시나리오를 사용하여 보다 정교한 파일 분류 작업을 수행할 수 있습니다.  
  
## <a name="step-8-optionally-specify-a-tech-support-email-address"></a>8단계: 필요에 따라 기술 지원 메일 주소를 지정   
 파일 서버에 클라우드 폴더를 설치한 후, 서버에 대한 관리 담당자 전자 메일 주소를 지정하고 싶을 것입니다. 전자 메일 주소를 추가하려면 다음 절차를 수행합니다.  
  
#### <a name="specifying-an-administrative-contact-email"></a>관리 담당자 전자 메일 지정 
  
1.  서버 관리자에서 **File and Storage Services**를 클릭한 다음 **서버**를 클릭합니다.  
  
2.  동기화 서버를 마우스 오른쪽 단추로 클릭한 다음 **클라우드 폴더 설정**을 클릭합니다. 클라우드 폴더 설정 창이 나타납니다.  
  
3.  탐색 창에서 **지원 전자 메일**을 클릭한 다음 사용자가 클라우드 폴더에 대한 도움을 요청하는 전자 메일을 보낼 때 사용해야 하는 전자 메일 주소를 입력합니다. 마치면 **확인**을 클릭합니다.  
  
     클라우드 폴더 사용자는 클라우드 폴더 제어판 항목의 링크를 클릭하여 클라이언트 PC에 대한 진단 정보가 포함된 메일을 여기에서 지정한 주소로 보낼 수 있습니다.  
  
## <a name="step-9-optionally-set-up-server-automatic-discovery"></a>9단계: 서버 자동 검색 설정(선택 사항)  
 환경에서 여러 동기화 서버를 호스팅하는 경우 AD DS에서 사용자 계정에 대한 **msDS-SyncServerURL** 속성을 채워 서버 자동 검색을 구성해야 합니다.  
  
>[!NOTE]
>Active Directory의 msDS-SyncServerURL 속성은 웹 응용 프로그램 프록시 또는 Azure AD 응용 프로그램 프록시와 같은 역방향 프록시 솔루션을 통해 클라우드 폴더에 액세스하는 원격 사용자에 대해서는 정의되어서는 안 됩니다. msDS-SyncServerURL 속성이 정의되면, 클라우드 폴더 클라이언트는 역방향 프록시 솔루션을 통해서는 액세스할 수 없는 내부 URL에 액세스하려 시도합니다. 웹 응용 프로그램 프록시 또는 Azure AD 응용 프로그램 프록시를 사용하는 경우, 각 클라우드 폴더 서버에 대한 고유 프록시 응용 프로그램을 만들어야 합니다. 자세한 내용은 참조 하세요. [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 개요](deploy-work-folders-adfs-overview.md) 나 [Azure AD 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)합니다.


 이렇게 하려면 먼저 Windows Server 2012 R2 도메인 컨트롤러를 설치하거나 `Adprep /forestprep` 및 `Adprep /domainprep` 명령을 사용하여 포리스트 및 도메인 스키마를 업데이트해야 합니다. 이러한 명령을 안전하게 실행하는 방법에 대한 자세한 내용은 [Adprep 실행](https://technet.microsoft.com/library/dd464018.aspx)을 참조하세요.  
  
 또한 5단계와 6단계에 설명된 대로 파일 서버 관리자에 대한 보안 그룹을 만들어 이 특정 사용자 특성을 수정할 수 있는 권한을 위임할 수도 있습니다. 이러한 단계를 수행하지 않으면 Domain Admins 또는 Enterprise Admins 그룹의 구성원에게 각 사용자에 대한 자동 검색을 구성하게 해야 합니다.  
  
#### <a name="to-specify-the-sync-server-for-users"></a>사용자에 대한 동기화 서버를 지정하려면  
  
1.  Active Directory 관리 도구가 설치된 컴퓨터에서 서버 관리자를 엽니다.  
  
2.  **도구** 메뉴에서 **Active Directory 관리 센터**를 클릭합니다. Active Directory 관리 센터가 표시됩니다.  
  
3.  해당 도메인의 **사용자** 컨테이너로 이동하여 동기화 공유에 할당할 사용자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  탐색 창에서 **확장**을 클릭합니다.  
  
5.  **특성 편집기** 탭을 클릭하고 **msDS-SyncServerUrl** 을 선택한 다음 **편집**을 클릭합니다. 다중값 문자열 편집기 대화 상자가 나타납니다.  
  
6.  **추가할 값** 상자에 이 사용자를 동기화할 동기화 서버의 URL을 입력하고 **추가**, **확인**을 차례로 클릭한 다음 **확인**을 다시 클릭합니다.  
  
    > [!NOTE]
    >  동기화 서버 URL은 `https://` 또는 `http://`(보안 연결이 필요한지 여부에 따라 결정됨) 뒤에 동기화 서버의 정규화된 도메인 이름이 오는 예를 들어 **https:\//sync1.contoso.com**합니다.

여러 사용자에 대한 특성을 채우려면 Active Directory PowerShell을 사용합니다. 다음은 5단계에서 설명한 *HR Sync Share Users* 그룹의 모든 구성원에 대한 특성을 채우는 예입니다.
  
```powershell  
$SyncServerURL = "https://sync1.contoso.com"  
$GroupName = "HR Sync Share Users"  
  
Get-ADGroupMember -Identity $GroupName |  
Set-ADUser –Add @{"msDS-SyncServerURL"=$SyncServerURL}  
  
```  
  
## <a name="step-10-optionally-configure-web-application-proxy-azure-ad-application-proxy-or-another-reverse-proxy"></a>10단계: 필요에 따라 웹 응용 프로그램 프록시, Azure AD 응용 프로그램 프록시 또는 다른 역방향 프록시 구성  

원격 사용자가 자신의 파일에 액세스할 수 있도록 하려면, 역방향 프록시를 통해 클라우드 폴더 서버를 게시하여 외부에서 인터넷을 통해 클라우드 폴더를 사용할 수 있도록 해야 합니다. 웹 응용 프로그램 프록시, Azure Active Directory 응용 프로그램 프록시 또는 다른 역방향 프록시 솔루션을 사용할 수 있습니다.  
  
AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 액세스를 구성하려면 [AD FS 및 WAP(웹 응용 프로그램 프록시)를 사용하여 클라우드 폴더 배포](deploy-work-folders-adfs-overview.md)를 참조하세요. 웹 응용 프로그램 프록시에 대한 배경 정보는 [Web Application Proxy in Windows Server 2016(Windows Server 2016의 웹 응용 프로그램 프록시)](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server)를 참조하세요. 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 같은 응용 프로그램을 인터넷에 게시하는 방법은 [Publishing Applications using AD FS Preauthentication(AD FS 사전 인증을 사용하여 응용 프로그램 게시)](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/publishing-applications-using-ad-fs-preauthentication)을 참조하세요.
 
Azure Active Directory 응용 프로그램 프록시를 사용하여 클라우드 폴더 액세스를 구성하려면 [Azure Active Directory 응용 프로그램 프록시를 사용하여 클라우드 폴더에 대한 원격 액세스를 사용하도록 설정](https://blogs.technet.microsoft.com/filecab/?p=7945)을 참조하세요. 
  
## <a name="step-11-optionally-use-group-policy-to-configure-domain-joined-pcs"></a>11단계: 그룹 정책을 사용하여 도메인에 가입된 PC 구성(선택 사항)  

클라우드 폴더를 배포할 도메인에 가입된 PC가 많은 경우 그룹 정책을 사용하여 다음과 같은 클라이언트 PC 구성 작업을 수행할 수 있습니다.  
  
- 사용자를 동기화할 동기화 서버 지정  
  
- 기본 설정을 사용하여 클라우드 폴더를 강제로 자동으로 설정(이 작업을 수행하기 전에 [클라우드 폴더 구현 디자인](plan-work-folders.md)에 설명된 그룹 정책 검토)  
  
  이러한 설정을 제어하려면 클라우드 폴더에 대한 새 GPO(그룹 정책 개체)를 만든 후 다음과 같은 그룹 정책 설정을 적절히 구성합니다.  
  
- 사용자 구성\정책\관리 템플릿\Windows 구성 요소\WorkFolders에서 Specify Work Folders settings(작업 폴더 설정 지정) 정책 설정  
  
- Computer Configuration\Policies\Administrative Templates\Windows Components\WorkFolders에서 Force automatic setup for all users(모든 사용자에 대한 자동 설정 강제) 정책 설정  
  
> [!NOTE]
>  이러한 정책 설정은 Windows 8.1 또는 Windows Server 2012 R2 이상의 그룹 정책 관리를 실행하는 컴퓨터에서 그룹 정책을 편집할 때만 사용할 수 있습니다. 이전 운영 체제의 그룹 정책 관리 버전에서는 이 설정을 사용할 수 없습니다. 이러한 정책 설정은 [Windows 7용 클라우드 폴더](http://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) 앱이 설치된 Windows 7 PC에 적용됩니다.  
  
##  <a name="BKMK_LINKS"></a> 참고 항목  
 자세한 내용은 다음 리소스를 참조하십시오.  
  
|콘텐츠 형식|참조|  
|------------------|----------------|  
|**이해**|-   [작업 폴더](work-folders-overview.md)|  
|**계획**|-   [클라우드 폴더 구현 디자인](plan-work-folders.md)|
|**배포**|-   [AD FS 및 WAP (웹 응용 프로그램 프록시)를 사용 하 여 클라우드 폴더 배포](deploy-work-folders-adfs-overview.md)<br />-   [클라우드 폴더 테스트 랩 배포](http://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) (블로그 게시물)<br />-   [클라우드 폴더 서버 Url에 대 한 새 사용자 특성](http://blogs.technet.com/b/filecab/archive/2013/10/09/a-new-user-attribute-for-work-folders-server-url.aspx) (블로그 게시물)|  
|**기술 참조**|-   [대화형 로그온: 컴퓨터 계정 잠금 임계값](https://technet.microsoft.com/library/jj966264(v=ws.11).aspx)<br />-   [동기화 공유 Cmdlet](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)|
