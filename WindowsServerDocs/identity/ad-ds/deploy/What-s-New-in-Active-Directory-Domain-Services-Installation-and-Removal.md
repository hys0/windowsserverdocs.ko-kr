---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: "작업 & #39, Active Directory 도메인에 새로 s 서비스 설치 및 제거"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 814a6f1af9144db28e81163b21cb5da4b6e51b3b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="what39s-new-in-active-directory-domain-services-installation-and-removal"></a>작업 & #39, Active Directory 도메인에 새로 s 서비스 설치 및 제거

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에 설명 합니다.  
  
-   [도메인 서비스 구성 Active Directory 마법사](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_ADConfigurationWizard)  
  
-   [Adprep.exe 통합](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep)  
  
-   [광고 DS 설치 필수 유효성 검사](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_PrereqCheck)  
  
-   [시스템 요구 사항](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_SystemReqs)  
  
-   [알려진된 문제](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)  
  
Windows Server 2012에서 active Directory DS (도메인 서비스 AD) 배포 더 간단 하 고 이전 버전의 Windows Server 보다 더 빠릅니다. 광고 DS 설치 과정 이제 Windows PowerShell에 기본 제공 하 고 서버 관리자와 통합 되어 있습니다. 기존 Active Directory 환경에 도메인 컨트롤러를 소개 하는 데 필요한 단계 횟수가 줄어듭니다 됩니다. 이렇게 하면를 간단 하 고 더 효율적으로 새 Active Directory 환경을 만드는 과정 있습니다. 그렇지 않으면 차단 설치 하는 오류를 소모할 가능성이 최소화 하는 새로운 광고 DS 배포 프로세스입니다.  
  
또한 동시에 여러 서버의 (즉, AD DS 서버 역할) 광고 DS 서버 역할 바이너리를 설치할 수 있습니다. 개별 서버에 원격으로 AD DS 설치 마법사를 실행할 수도 있습니다. 이러한 개선이 특히 배포용 대규모, 전 세계 여러 도메인 컨트롤러 다양 한 지역에서 사무실에 배포 해야 하는 Windows Server 2012를 실행 하는 도메인 컨트롤러 배포를 위해 더 많은 유연성을 제공 합니다.  
  
광고 DS 설치 다음과 같은 기능이 포함 됩니다.  
  
-   **Adprep.exe DS AD 설치 프로세스에 통합 됩니다.** 다양 한 다른 자격 증명을 사용 하 여 Adprep.exe 파일을 복사 하거나 특정 도메인 컨트롤러에 로그온 할 필요가 같은 기존 Active Directory를 준비 하는 데 필요한 번거롭게 단계 간체는 모두 하거나 자동으로 수행 합니다. 이 광고 DS 설치 하는 데 걸리는 시간은 감소 도메인 컨트롤러 프로 모션 차단 그렇지 않은 경우 될 수 오류에 대 한 높입니다.  
  
    새 도메인 컨트롤러 설치 하기 전에 adprep.exe 명령을 실행 하는 것이 좋습니다 하는 환경에 대 한 여전히에서 실행할 수 있습니다 adprep.exe 명령을 별도로 AD DS 설치 합니다. Windows Server 2012 버전의 adprep.exe 나중에 또는 Windows Server 2008 64 비트 버전을 실행 하는 서버에서 모든 필요한 명령을 실행할 수 있도록 원격으로 실행 됩니다.  
  
-   **새로운 광고 DS 설치에서 Windows PowerShell 빌드되어 원격으로 호출할 수 있습니다.** 동일한 인터페이스 AD DS 다른 서버 역할을 설치할 때 사용 하는 설치에 사용할 수 있도록 새로운 광고 DS 설치 서버 관리자 통합 되어 있습니다. Windows PowerShell 사용자를 위해 광고 DS 배포 cmdlet 향상 된 기능 및 유연성을 제공합니다. 명령줄 간에 기능 패리티가 및 GUI 설치 옵션 합니다.  
  
-   **새 광고 DS 설치 필수 유효성 검사에 포함 됩니다.** 설치를 시작 하기 전에 잠재적 오류가 표시 됩니다. 모든 업그레이드를 완료 부분적으로에서 발생 한 문제를 않고도 발생 하기 전에 오류 조건이 수정할 수 있습니다. 예를 들어 adprep /domainprep을 실행 하는 경우 설치 마법사 사용자가 작업을 실행할 수 있는 권한이 있는지 확인 합니다.  
  
-   **가장 일반적인 프로 모션 옵션 마법사 페이지 더 적은 수의 그룹화 관련 옵션이 요구 사항을 반영 순서로 구성 페이지 그룹화 되어 있습니다.** 더 나은 상황에 맞는 설치 옵션을 제공 합니다.  
  
-   **그래픽 설치 중에 지정 된 모든 옵션이 포함 된 Windows PowerShell 스크립트를 내보낼 수 있습니다.** 설치 또는 제거 끝 설정을 같은 작업을 자동화 된 사용에 대 한 Windows PowerShell 스크립트를 내보낼 수 있습니다.  
  
-   **다시 부팅 되기 전에 중요 복제가 에서만 발생합니다.** 다시 부팅 되기 전에 중요 한 데이터를 복제 수 있도록 새로운 전환 하세요. 자세한 내용은 참조 [ADDSDeployment cmdlet 인수](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)합니다.  
  
### <a name="BKMK_ADConfigurationWizard"></a>도메인 서비스 구성 Active Directory 마법사  
Windows Server 2012부터, Active Directory 도메인 서비스 구성 마법사 도메인 컨트롤러를 설치할 때 설정을 지정 하려면 사용자 인터페이스 옵션으로는 레거시 Active Directory 도메인 Services 설치 마법사를 대체 합니다. Active Directory 도메인 서비스 구성 마법사 역할 추가 마법사가 완료 된 후에 시작 됩니다.  
  
> [!WARNING]  
> 레거시 Active Directory 도메인 서비스 설치 마법사 (dcpromo.exe)는 일부 터 Windows Server 2012와 사용 되지 않습니다.  
  
[Active Directory 도메인 서비스 & #40; 설치 수준을 100 & #41; ](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md), UI 절차 AD DS 서버를 설치 하려면 역할 추가 마법사를 시작 하는 방법을 역할 바이너리 표시 한 다음 실행 Active Directory 도메인 서비스 구성 마법사 도메인 컨트롤러 설치를 완료 합니다. Windows PowerShell 예제 AD DS 배포 cmdlet 사용 하 여 두 단계를 완료 하는 방법을 보여 줍니다.  
  
### <a name="BKMK_NewAdprep"></a>Adprep.exe 통합  
Adprep.exe의 하나만 버전은 Windows Server 2012 부터는 (32 비트 버전이 adprep32.exe). Adprep 명령은 기존 Active Directory 도메인 또는 숲 Windows Server 2012를 실행 하는 도메인 컨트롤러를 설치할 때 필요할 때 자동으로 실행 됩니다.  
  
Adprep 작업은 자동으로 실행 되지만 별도로 Adprep.exe을 실행할 수 있습니다. 예를 들어, 광고 DS 설치 하는 사용자의 Adprep /forestprep 실행 하는 데 필요한 엔터프라이즈 관리자 그룹 구성원 없는 경우 다음 해야 별도로 명령을 실행 합니다. 그러나 실행 adprep.exe 계획 업그레이드 하는 경우 먼저 Windows Server 2012 도메인 컨트롤러 해야 (즉, 하려는 위치에서 업그레이드 Windows Server 2012를 실행 하는 도메인 컨트롤러의 운영 체제).  
  
Adprep.exe는 \support\adprep 폴더는 Windows Server 2012 설치 디스크에 있습니다. Adprep Windows Server 2012 버전이 원격으로 실행할 수 있습니다.  
  
나중에 또는 Windows Server 2008 64 비트 버전을 실행 하는 모든 서버 Windows Server 2012 버전 adprep.exe 실행할 수 있습니다. 서버 숲와 도메인 컨트롤러를 추가 하려면는 도메인의 infrastructure 마스터 스키마 마스터 네트워크 연결이 필요 합니다. Windows Server 2003을 실행 하는 서버에 호스트 중 한 가지 역할을 한 adprep 원격으로 실행 해야 합니다. 도메인 컨트롤러를 adprep 실행 하는 서버 필요가 없습니다. 결합 또는 작업 그룹 도메인 수 있습니다.  
  
> [!NOTE]  
> Windows Server 2003을 실행 하는 서버에 adprep.exe의 Windows Server 2012 버전을 실행 하려는 경우 다음과 같은 오류가 나타납니다.  
>   
> Adprep.exe 올바른 Win32 응용 프로그램이 않습니다.  
  
![새로운 기능](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)  
  
Adprep.exe에서 반환 된 다른 오류 해결에 대 한 정보를 참조 하세요. [알려진 문제](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)합니다.  
  
#### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Windows Server 2003 마스터 역할 작업에 대해 그룹 구성원 검사  
각 명령에 대해 (/ forestprep, /domainprep, 또는 /rodcprep), Adprep 지정된 자격 증명 나타내는지 특정 그룹에서 계정을 확인 하는 그룹 구성원 검사를 수행 합니다. 이 검사를 수행 하려면 Adprep 작업 마스터 역할 소유자에 접속 합니다. 작업 마스터 Windows Server 2003을 실행 중인 경우 Adprep.exe 그룹 구성원 검사는 항상에서 수행를 실행 하는 경우 사용자 및 /userdomain 명령줄 매개 변수를 지정 해야 합니다.  
  
사용자와 /userdomain Adprep.exe Windows Server 2012에 대 한 새로운 매개 됩니다. 이러한 매개 지정 사용자 계정 이름 및 사용자 도메인 각각 adprep 명령을 실행 하는 사용자의 합니다. Adprep.exe 명령줄 유틸리티 차단 /userdomain 및 사용자는 다른 생략 중 하나를 지정 합니다.  
  
그러나 Windows PowerShell 또는 서버 관리자를 사용 하 여 광고 DS 설치의 일부로 Adprep 작업 실행할 수 수도 있습니다. 이러한 경험 adprep.exe와 같은 기본 구현 (adprep.dll)를 공유합니다. Windows PowerShell 및 서버 관리자 환경을 입력 하 고, 동일한 요구 adprep.exe 기준으로 따르면 하는 별도 자격 증명 합니다. Windows PowerShell 또는 서버 관리자를 사용 하는 사용자 하지만 /userdomain 하지에 대 한 값 adprep.dll를 전달할 수 사용자 지정 하는 경우 /userdomain 지정 하지 않은 로컬 컴퓨터 도메인 확인을 수행 하는 데 사용 됩니다. 컴퓨터가 도메인에 가입 그룹 구성원을 확인할 수 없습니다.  
  
그룹 구성원을 확인할 수 없습니다 Adprep adprep 로그 파일에 경고 메시지를 표시 하 고 계속:  
  
```  
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.  
```  
  
사용자와 /userdomain 매개 변수를 지정 하지 않고 Adprep.exe 실행 작업 마스터 Windows Server 2003을 실행 중인 경우 Adprep.exe 현재 로그온 한 사용자의 도메인에 있는 도메인 컨트롤러에 접속 합니다. 현재 로그온 사용자 도메인 계정인 경우 Adprep.exe 그룹 구성원 검사를 수행할 수 없습니다. Adprep.exe도 수 없는 검사를 수행할 그룹 구성원 스마트 카드 자격 증명을 사용 하는 경우 사용자 및 /userdomain 지정 수행 하는 경우에 있습니다.  
  
Adprep 성공적으로 완료 되 면 인지 작업이 필요 하지 않습니다. 액세스 오류로 인해 실행 하는 동안 오류가 발생 하면 Adprep 계정을 올바른 멤버 자격으로 제공 합니다. 자세한 내용은 참조 [Adprep.exe 실행 하 고 Active Directory 도메인 서비스 설치 요구 사항이 자격 증명](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)합니다.  
  
#### <a name="syntax-for-adprep-in-windows-server-2012"></a>Windows Server 2012에서에서 Adprep 구문  
다음 구문을 별도로 실행 하 adprep AD DS 설치 사용:  
  
```  
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *  
```  
  
더 자세한 로그를 생성 하려면 /logdsid 명령에 사용 합니다. adprep.log %windir%\System32\Debug\Adprep\Logs 있습니다.  
  
#### <a name="running-adprep-using-smartcard"></a>스마트 카드를 사용 하 여 adprep 실행  
Windows Server 2012 버전의 adprep.exe 스마트 카드를 사용 하 여 자격 증명으로 작동 하지만 명령줄 스마트 카드 자격 증명을 지정 쉽게 방법은 없습니다. 이렇게 하는 방법은 PowerShell cmdlet Get 자격 증명을 통해 스마트 카드 자격 증명을 얻을 수 있습니다. 다음으로 표시 되는 반환된 PSCredential 개체의 사용자 이름을 사용 하 여 `@@...`합니다. 암호가 스마트 카드의 PIN 합니다.  
  
사용자 지정 된 Adprep.exe /userdomain이 필요 합니다. 스마트 카드 자격 증명은 /userdomain 스마트 카드도 표현 하는 기본 사용자 계정의 도메인 되어야 합니다.  
  
#### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>Adprep /domainprep /gpprep 명령은 자동으로 실행 되지 않는 경우  
광고 DS 설치의 일부로 adprep /domainprep /gpprep 명령을 실행 되지 않습니다. 이 설정에 대 한 결과 설정의 정책 (RSOP) 필요한 권한 모드 기능 계획 합니다. 이 명령에 대 한 자세한 내용은 참조 [Microsoft 기술 자료 문서 324392](https://support.microsoft.com/kb/324392)합니다. 명령 Active Directory 도메인에 실행 하는 경우 광고 DS 설치에서 별도로 실행할 수 있습니다. Windows Server 2003 s p 1을 실행 하는 도메인 컨트롤러 배포 준비에서 명령 이미 실행 경우 나중에 다시 실행 하는 명령 필요 하지 않습니다.  
  
안전 하 게 실행 adprep 하십시오를 않고도 기존 도메인 Windows Server 2012를 실행 하는 도메인 컨트롤러 추가할 수는 있지만 RSOP 계획 모드 제대로 작동 하지 않습니다.  
  
### <a name="BKMK_PrereqCheck"></a>광고 DS 설치 필수 유효성 검사  
광고 DS 설치 마법사에서 설치를 시작 하기 전에 다음과 같은 사항을 충족 확인 합니다. 이 설치 차단 될 수 있는 문제를 해결 하는 기회를 제공 합니다.  
  
예를 들어 Adprep 관련 필수 다음과 같습니다.  
  
-   자격 증명 검증 Adprep: 설치 마법사는 사용자에 게 필요한 Adprep 작업을 실행할 수 있는 권한이 있는지 확인 adprep을 실행 하는 경우입니다.  
  
-   스키마 마스터 가용성 검사: 확인 스키마 마스터 온라인 한 실패 그렇지 않은 경우 설치 마법사에서 해당 adprep /forestprep 실행 해야으로 결정 합니다.  
  
-   Infrastructure 마스터 가용성 확인: 인프라 마스터 온라인가 고 그렇지 않은 경우 실패 확인 설치 마법사에서 해당 adprep /domainprep 실행 해야으로 결정 합니다.  
  
앞으로 레거시 Active Directory 설치 마법사에서 (dcpromo.exe) 수행 되는 다른 필수 검사 다음과 같습니다.  
  
-   이름 인증 포리스트: 숲 이름 유효 하 고 현재 없거나 설치할 수 있도록 보장 합니다.  
  
-   NetBIOS 인증 이름: NetBIOS 유효 이름과 충돌 하지 기존 이름을 함께 제공 되는 검사 합니다.  
  
-   구성 요소 경로 확인: Active Directory 데이터베이스, 로그 및 SYSVOL 경로가 올바른지 확인 하 고에 사용할 수 있는 충분 한 디스크 공간이 있는지 확인 합니다.  
  
-   자녀 도메인 이름 확인: 블 부모 및 자녀 도메인 이름 새로운 유효한 지 기존 도메인으로 충돌 하지 않습니다.  
  
-   나무 도메인 이름 확인: 밤나무 지정 된 이름이 올바른지는 현재 없는 블 합니다.  
  
## <a name="BKMK_SystemReqs"></a>시스템 요구 사항  
Windows Server 2012 시스템 요구 사항을 Windows Server 2008 R2에서 변경 되지 않습니다. 자세한 내용은 참조 [Windows Server 2008 R2 s p 1 시스템 요구 사항을 만족](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx) (https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx).  
  
일부 기능 추가 요구 사항이 있을 수 있습니다. 예를 들어, 가상 도메인 컨트롤러 복제 기능 해야 하는 PDC 에뮬레이터 Hyper-v 역할이 설치와 Windows Server 2012를 실행 하는 컴퓨터 및 Windows Server 2012를 실행 합니다.  
  
## <a name="BKMK_KnownIssues"></a>알려진된 문제  
이 섹션에는 몇 가지 알려진된 문제 Windows Server 2012에서 광고 DS 설치에 영향을 주는 나열 됩니다. 추가 알려진된 문제에 대 한 참고 [문제 해결 도메인 컨트롤러 배포](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)합니다.  
  
-   WMI 스키마 마스터에 대 한 액세스 adprep /forestprep 원격으로 실행 하는 경우 Windows 방화벽에서 차단 되어, 다음과 같은 오류 %systemroot%\system32\debug\adprep adprep 로그에 기록 됩니다.  
  
    ```  
    Adprep encountered a Win32 error.   
    Error code: 0x6ba Error message: The RPC server is unavailable.  
    ```  
  
    이 경우 해결할 수 있습니다 오류 실행 중 adprep /forestprep 하 여 스키마 마스터에 직접 또는 Windows 방화벽을 통해 WMI 교통 수 있도록 뒤 다음 명령을 중 하나를 실행할 수 있습니다.  
  
    Windows Server 2008 용 이상:  
  
    ```  
    netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=yes  
    ```  
  
    Windows Server 2003에 대 한  
  
    ```  
    netsh firewall set service RemoteAdmin enable  
    ```  
  
    Adprep 완료 한 후 다시 WMI 교통 차단 뒤 다음 명령을 중 하나를 실행할 수 있습니다.  
  
    ```  
    netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=no  
    ```  
  
    ```  
    netsh firewall set service remoteadmin disable  
    ```  
  
-   Ctrl + C 설치 ADDSForest cmdlet 취소 하려면 입력할 수 있습니다. 취소 설치 멈추고 서버 상태에 대 한 모든 변경 내용이 사라집니다. 그러나 취소 명령을 실행 한 후 제어 Windows PowerShell에 반환 되지 cmdlet 무기한으로 응답 하지 수 있습니다.  
  
-   **대상 서버가 설치 하기 전에 도메인에 가입 하지는 스마트 카드 자격 증명을 사용 하 여 추가 도메인 컨트롤러의 설치가 실패 합니다.**  
  
    이 경우 반환 하는 오류 메시지는 다음과 같습니다.  
  
    복제 소스 도메인 컨트롤러에 연결할 수 없습니다 *소스 도메인 컨트롤러의 이름을*합니다. (예외: Logonfailure: 알 수 없는 사용자 이름 이거나 잘못 된 암호)  
  
    대상 서버 도메인에 가입 하 고 다음을 수행 스마트 카드를 사용 하 여 설치 하는 경우 설치 성공 합니다.  
  
-   **ADDSDeployment 모듈 32 비트 프로세스에서 작동 하지 않습니다.** 배포 하 고 구성 하 고 기본 64 비트 프로세스를 지원 하지 않는 기타 cmdlet ADDSDeployment cmdlet 포함 된 스크립트를 사용 하 여 Windows Server 2012 자동화 하는 경우 스크립트 ADDSDeployment cmdlet를 찾을 수를 나타내는 오류가 실패할 수 있습니다.  
  
    이 경우 별도로 실행 하는 ADDSDeployment cmdlet 기본 64 비트 프로세스를 지원 하지 않는 cmdlet 해야 합니다.  
  
-   새 파일 시스템을 복원 파일 시스템 라는 Windows Server 2012에 있습니다. (ReFS) 복원 파일 시스템으로 포맷 데이터 볼륨 Active Directory 데이터베이스, 로그 파일 또는 SYSVOL 저장 하지 않습니다. ReFS에 대 한 자세한 내용은 참조 [Windows에 대 한 다음 세대 파일 시스템을 구축: ReFS](http://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx)합니다.  
  
-   서버 관리자에서 서버 Core 설치에서 광고 DS 또는 다른 서버 역할을 실행 하 고 Windows Server 2012로 업그레이드 하는 서버 예상 대로 이벤트 및 상태가 수집 되는 경우에 서버 역할 빨간색 상태로 나타날 수 있습니다. Windows Server 2012 영향을 미칠 수 있는 예비 릴리스의 서버 Core 설치를 실행 하는 서버 합니다.  
  
### <a name="active-directory-domain-services-installation-hangs-if-an-error-prevents-critical-replication"></a>Active Directory 도메인 서비스 설치가 중단 오류가 중요 한 복제 수 없는 경우  
광고 DS 설치 중요 한 복제 단계 중 오류가 발생 하는 경우 설치 무한 중지 될 수 있습니다. 예를 들어, 네트워킹 오류로 인해를 완료 중요 한 복제, 설치 진행 되지 않습니다.  
  
를 설치 하는 서버 관리자를 사용 하 여 설치 진행률 페이지 열려 하지만 화면에서 보고 오류가 없는 및 진행 15 분 정도 변경할 필요가 없습니다 표시 될 수 있습니다. Windows PowerShell를 사용 하는 경우 Windows PowerShell 창에 표시 된 진행 15 분 이상 변경 되지 않습니다.  
  
이 문제가 발생 하는 경우 대상 서버의 %systemroot%\debug 폴더의 나타나면 dcpromo.log 파일을 확인 합니다. 일반적으로 로그 파일 복제할 오류가 반복된 나타납니다. 이 문제에 대 한 몇 가지 알려진된 원인은 다음과 같습니다.  
  
-   네트워킹 문제로 인해 올렸습니다 대상 서버 복제가 원본 도메인 컨트롤러와 복제 중요 합니다.  
  
    예를 들어 있는 나타나면 dcpromo.log 보여 줍니다.  
  
    ```  
  
      05/02/2012 14:16:46 [INFO] EVENTLOG (Error): NTDS Replication / DS RPC Client : 1963  
      Internal event: The following local directory service received an exception from a remote procedure call (RPC) connection. Extensive RPC information was requested. This is intermediate information and might not contain a possible cause.  
    Process ID:   
    500  
    Reported error information:  
    Error value:   
    Could not find the domain controller for this domain. (1908)  
    directory service:   
    <domain>.com  
    Extensive error information:  
    Error value:   
    A security package specific error occurred. 1825  
    directory service:   
    <DC Name>  
    ```  
  
    설치 프로세스를 중요 복제 무기한 다시 시도 하기 때문에 기본 네트워크 문제 확인 하는 도메인 컨트롤러 설치 진행 됩니다. 필요에 따라 ipconfig, nslookup, 네트워크 모니터 등 도구를 사용 하 여 네트워킹 문제를 조사 하는 합니다. 홍보는 도메인 컨트롤러 간의 연결이 있는지 확인 하 고 복제 파트너 AD DS 설치 중에 선택 합니다. 또한 이름 확인 작동 하는지 확인 합니다.  
  
    설치를 시작 하기 전에 필수 확인 하는 동안 네트워크 연결 및 이름을 확인을 위해 광고 DS 설치 요구 사항은 확인 됩니다. 하지만 일부 오류 조건을 필수 유효성 검사가 수행 하 고 설치를 완료 하기 전에 등 복제 파트너 사용할 수 없게 되 설치 하는 동안 후 시간 내에 발생할 수 있습니다.  
  
-   복제본 도메인 컨트롤러 설치 하는 동안 대상 서버 로컬 관리자 계정을 설치 자격 증명을 지정 되 고 로컬 관리자 계정 암호 관리자 도메인 계정 암호를 찾습니다. 이 경우 설치 마법사를 완료 하 고 "액세스 거부" 오류 발생 하기 전에 설치를 시작할 수 있습니다.  
  
    예를 들어 있는 나타나면 dcpromo.log 보여 줍니다.  
  
    ```  
  
    03/30/2012 11:36:51 [INFO] Creating the NTDS Settings object for this Active Directory Domain Controller on the remote AD DC DC2.contoso.com...  
    03/30/2012 11:36:51 [INFO] EVENTLOG (Error): NTDS Replication / DS RPC Client : 1963Internal event: The following local directory service received an exception from a remote procedure call (RPC) connection. Extensive RPC information was requested. This is intermediate information and might not contain a possible cause.  
    Process ID:   
    508  
    Reported error information:  
    Error value:   
    Access is denied. (5)  
    directory service:   
    DC2.contoso.com  
  
    ```  
  
    운영 체제를 다시 설치 하면 복구 하기 위해 필요한 로컬 관리자 계정 및 암호를 지정 하 여 오류가 발생 하는 경우 [메타 데이터를 정리할](https://technet.microsoft.com/library/cc816907(WS.10).aspx) 설치를 완료 하 고 다시 도메인 관리자 자격 증명을 사용 하 여 광고 DS 설치에 실패 하는 도메인 컨트롤러의 계정을 합니다. 서버를 다시 시작는 서버가 설치를 완료 하지 않은 경우에 광고 DS 설치 되어 있는지 알려줍니다 때문에이 오류 문제를 해결 하지 않습니다.  
  
### <a name="BKMK_nonnormalDNSNameWarning"></a>비 표준화 DNS 이름을 지정 active Directory 도메인 서비스 구성 마법사 경고가 표시  
새 도메인 만들거나 숲 및 사용자 지정 표준화 됩니다 국제 문자를 포함 하 여 DNS 도메인 이름, Active Directory 도메인 서비스 구성 마법사 DNS 쿼리에 이름에 실패할 수 있는 경고를 표시 합니다. DNS 도메인 이름 배포 구성 페이지에 지정 된, 있지만 경고 마법사에서 나중에 필수 확인 페이지에 나타납니다.  
  
DNS 도메인 이름 füßball.com 또는 'ΣΤ'.com 같은 없다고 표준화 이름을 사용 하 여 지정 하는 경우 (표준화 버전은: füssball.com 및 βστα.com), WinHTTP와에 액세스 하려고 하는 클라이언트 응용 프로그램의 이름을 이름 확인 Api 취해도 표준화 합니다. 일부 대화 상자에서 "'ΣΤ'.com"를 입력 하 고 "βστα.com" DNS 서버가 일치 하는 것 "'ΣΤ'.com"에 대 한 리소스 기록으로 DNS 쿼리에 전송 됩니다. 사용자 이름 확인할 수 없습니다.  
  
이때 하나 표준화 하지는 IDN 이름을 사용 하는 경우 발생할 수 있는 문제를 설명 합니다.  
  
1.  비 표준화 이름을 사용 하는 도메인 만들고 dns 서버에 등록: füßball.com  
  
2.  기계 "nps"가 도메인에 가입 하 고 등록 이름 가져옵니다: nps.füßball.com  
  
3.  서버 nps.füßball.com에 연결 하려고 하는 클라이언트 응용 프로그램  
  
4.  클라이언트 응용 프로그램 이름을 nps.füßball.com 이름 확인 Api 통화를 확인 하려고 합니다.  
  
5.  표준화, 인해 nps.füssball.com 변환 이름과 nps.füßball.com로 유선 쿼리  
  
6.  클라이언트 응용 프로그램의 등록 된 이름은 nps.füßball.com 이후 이름을 확인할 수 없으면  
  
경고 Active Directory 도메인 서비스 구성 마법사에서 필수 확인 페이지에 표시 되 면, 배포 구성 페이지로 돌아와 표준화 DNS 도메인 이름 지정 합니다. 새 도메인 Windows PowerShell를 사용 하 여 설치 하는 경우-도메인 이름 옵션에 대 한 표준화 DNS 이름을 지정 합니다.  
  
Idn에 대 한 자세한 내용은 참조 [다국어 도메인 이름 처리 (Idn)](https://msdn.microsoft.com/library/windows/desktop/dd318142(v=vs.85).aspx)합니다.  
  

