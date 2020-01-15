---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: Active Directory Domain Services 설치 및 제거의 새로운 기능
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 1f24615491391d932609d7f80549985818ced8c1
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947901"
---
# <a name="whats-new-in-active-directory-domain-services-installation-and-removal"></a>Active Directory Domain Services 설치 및 제거의 새로운 기능

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2012의 Active Directory Domain Services (AD DS) 배포는 이전 버전의 Windows Server 보다 간단 하 고 빠릅니다. 이제 AD DS 설치 프로세스는 Windows PowerShell에서 구축되며 서버 관리자와 통합됩니다. 따라서 도메인 컨트롤러를 기존의 Active Directory 환경에 추가하는 데 필요한 단계 수가 줄어들었으며, 이를 통해 새 Active Directory 환경을 만드는 프로세스가 보다 간편해지고 효율성이 개선되었습니다. 새 AD DS 배포 프로세스는 설치를 방해하는 오류 가능성을 최소화합니다.  
  
또한 여러 서버에 동시에 AD DS 서버 역할인 AD DS 서버 역할 바이너리를 설치할 수 있으며, 개별 서버에서 원격으로 AD DS 설치 마법사를 실행할 수도 있습니다. 이러한 향상 된 기능을 통해 Windows Server 2012를 실행 하는 도메인 컨트롤러를 보다 유연 하 게 배포할 수 있습니다. 특히 많은 도메인 컨트롤러를 여러 지역에 배포 해야 하는 대규모 글로벌 배포의 경우 더욱 유연 합니다.  
  
AD DS 설치에는 다음 기능이 포함됩니다.  
  
- **AD DS 설치 프로세스에 Adprep.exe 통합** 여러 개의 서로 다른 자격 증명을 사용하거나 Adprep.exe 파일을 복사하거나 특정 도메인 컨트롤러에 로그온해야 하는 등 Active Directory를 준비하는 데 필요했던 기존의 여러 가지 복잡한 단계가 모두 간소화되거나 자동으로 수행됩니다. 따라서 AD DS 를 설치하는 데 소요되는 시간이 단축되며 도메인 컨트롤러의 수준을 올리는 데 방해될 수 있는 오류 가능성이 줄어듭니다.  

   새 도메인 컨트롤러를 설치하는 데 앞서 adprep.exe 명령을 실행해야 하는 환경의 경우 AD DS 설치와 별도로 adprep.exe 명령을 계속해서 실행할 수 있습니다. Adprep.exe의 Windows Server 2012 버전은 원격으로 실행 되므로 64 비트 버전의 Windows Server 2008 이상을 실행 하는 서버에서 필요한 모든 명령을 실행할 수 있습니다.  

- **새 AD DS 설치가 Windows PowerShell에 구축되며 원격으로 호출할 수 있습니다.** 새 AD DS 설치가 서버 관리자와 통합되어 다른 서버 역할 설치 시 사용하는 것과 동일한 인터페이스를 사용하여 AD DS를 설치할 수 있습니다. Windows PowerShell 사용자의 경우 AD DS 배포 cmdlet은 보다 많은 기능 및 향상된 유연성을 제공합니다. 명령줄 및 GUI 설치 옵션 간 기능 패리티가 유지됩니다.  
- **새로운 AD DS 설치에 필수 유효성 검사가 포함됩니다.** 설치를 시작하기 전에 잠재적인 오류가 식별됩니다. 업그레이드 부분 완료와 관련한 우려 없이 오류가 발생하기 전에 오류 상태를 수정할 수 있습니다. 예를 들어 adprep /domainprep을 실행해야 하는 경우 설치 마법사에서 사용자에게 이 작업을 실행하는 데 필요한 권한이 있는지 확인합니다.  
- **구성 페이지가 가장 일반적인 프로모션 옵션의 요구 사항을 반영하는 순서로 그룹화되고 관련 옵션이 줄어든 마법사 페이지에서 그룹화됩니다.** 이를 통해 설치 옵션을 더 간단히 선택할 수 있습니다.  
- **그래픽 설치 중 지정된 모든 옵션이 포함되어 있는 Windows PowerShell 스크립트를 내보낼 수 있습니다.** 같은 작업을 자동화하는 데 사용할 수 있도록 설치 또는 제거 프로세스의 마지막에 Windows PowerShell 스크립트로 설정을 내보낼 수 있습니다.  
- **다시 부팅하기 전에 중요한 복제만 발생합니다.** 다시 부팅하기 전에 중요하지 않은 데이터의 복제를 허용하려면 새 스위치를 사용합니다. 자세한 내용은 참조 [ADDSDeployment cmdlet 인수](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)합니다.  

## <a name="BKMK_ADConfigurationWizard"></a>Active Directory Domain Services 구성 마법사

Windows Server 2012 부터는 Active Directory 도메인 서비스 구성 마법사는 도메인 컨트롤러를 설치할 때 설정을 지정 하는 사용자 인터페이스 (UI) 옵션으로는 레거시 Active Directory 도메인 서비스 설치 마법사를 대체 합니다. Active Directory Domain Services 구성 마법사는 역할 추가 마법사가 완료되면 시작됩니다.  

> [!WARNING]  
> 레거시 Active Directory Domain Services 설치 마법사 (dcpromo.exe)는 Windows Server 2012부터 더 이상 사용 되지 않습니다.  

[#40; 및 Active Directory 도메인 서비스 설치 수준 100 & #41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md), UI 프로시저 AD DS 서버를 설치 하려면 역할 추가 마법사를 시작 하는 방법을 보여 줍니다 역할 이진 파일 및 다음 도메인 컨트롤러 설치를 완료 하는 Active Directory 도메인 서비스 구성 마법사를 실행 합니다. Windows PowerShell 예제에는 AD DS 배포 cmdlet을 사용하여 두 단계를 모두 완료하는 방법을 보여 줍니다.  
  
## <a name="BKMK_NewAdprep"></a>Adprep.exe 통합

Windows Server 2012 부터는 Adprep.exe 버전이 하나 뿐입니다 (32 비트 버전인 adprep32.exe는 없음). Adprep 명령은 Windows Server 2012를 실행 하는 도메인 컨트롤러를 기존 Active Directory 도메인 또는 포리스트에 설치할 때 필요에 따라 자동으로 실행 됩니다.  
  
adprep 작업이 자동으로 실행되더라도 Adprep.exe를 별도로 실행할 수 있습니다. 예를 들어 AD DS를 설치하는 사용자가 Adprep /forestprep을 실행하는 데 필요한 Enterprise Admins 그룹의 구성원이 아닌 경우 이 명령을 별도로 실행해야 할 수 있습니다. 하지만 첫 번째 Windows Server 2012 도메인 컨트롤러를 전체 업그레이드 하려는 경우 (즉, Windows Server 2012를 실행 하는 도메인 컨트롤러의 운영 체제를 전체 업그레이드 하려면) adprep.exe만 실행 하면 됩니다.  
  
Adprep.exe는 Windows Server 2012 설치 디스크의 \support\adprep 폴더에 있습니다. Windows Server 2012 버전의 adprep은 원격으로 실행할 수 있습니다.  
  
Windows server 2012 버전의 adprep.exe는 64 비트 버전의 Windows Server 2008 이상을 실행 하는 모든 서버에서 실행할 수 있습니다. 이 경우 서버에는 도메인 컨트롤러를 추가할 도메인의 인프라 마스터 및 포리스트의 스키마 마스터에 대한 네트워크 연결이 설정되어 있어야 합니다. 이러한 역할 중 하나가 Windows Server 2003을 실행하는 서버에서 호스트된 경우 adprep을 원격으로 실행해야 합니다. adprep을 실행하는 서버는 도메인 컨트롤러일 필요는 없습니다. 서버를 도메인에 가입시키거나 작업 그룹에 포함할 수 있습니다.  

> [!NOTE]  
> Windows server 2003를 실행 하는 서버에서 Windows Server 2012 버전의 adprep.exe를 실행 하려고 하면 다음과 같은 오류가 나타납니다.  
>   
> Adprep.exe가 올바른 Win32 애플리케이션이 아닙니다.  

![새로운 기능](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)  

Adprep.exe에서 반환되는 기타 오류를 해결하는 방법에 대한 자세한 내용은 [Known issues](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)를 참조하십시오.  

### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Windows Server 2003 작업 마스터 역할에 대한 그룹 구성원 확인

Adprep은 각 명령(/forestprep, /domainprep 또는 /rodcprep)에 대해 지정된 자격 증명이 특정 그룹의 계정을 나타내는지 여부를 확인하기 위해 그룹 구성원 확인을 수행합니다. 이 확인을 수행하기 Adprep은 작업 마스터 역할 소유자를 연결합니다. 작업 마스터에서 Windows Server 2003을 실행하는 경우 Adprep.exe를 실행하여 모든 경우에 그룹 구성원 확인이 수행되도록 하려면 /user 및 /userdomain 명령줄 매개 변수를 지정해야 합니다.  
  
/User 및 /userdomain은 Windows Server 2012의 Adprep.exe에 대 한 새 매개 변수입니다. 이러한 매개 변수는 adprep 명령을 실행하는 사용자에 대해 사용자 계정 이름 및 사용자 도메인을 각각 지정합니다. Adprep.exe 명령줄 유틸리티는 /userdomain 및 /user 중 하나를 지정하고 나머지 하나는 생략하도록 허용하지 않습니다.  
  
하지만 Windows PowerShell이나 서버 관리자를 사용하여 AD DS를 설치하는 과정으로 Adprep 작업을 실행할 수도 있습니다. 이러한 작업은 adprep.exe와 동일한 기본 구현(adprep.dll)을 공유합니다. Windows PowerShell 및 서버 관리자 작업은 별도의 자격 증명 입력을 포함하며, adprep.exe에서와 동일한 요구 사항이 적용되지 않습니다. Windows PowerShell이나 서버 관리자를 사용하여 /userdomain이 아닌 /user의 값을 adprep.dll에 전달할 수 있습니다. /User가 지정 하는 경우 /userdomain 지정 하지 않으면 검사를 수행 하는 로컬 컴퓨터의 도메인이 사용 됩니다. 컴퓨터가 도메인에 가입되어 있지 않은 경우에는 그룹 구성원을 확인할 수 없습니다.  
  
그룹 구성원을 확인할 수 없는 경우 Adprep의 adprep 로그 파일에 경고 메시지가 표시되며, 작업이 계속 수행됩니다.  

```
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.  
```

/user 및 /userdomain 매개 변수를 지정하지 않고 Adprep.exe를 실행하고, 작업 마스터에서 Windows Server 2003을 실행하는 경우 Adprep.exe는 현재 로그온 사용자의 도메인에 있는 도메인 컨트롤러를 연결합니다. 현재 로그온 사용자가 도메인 계정이 아닌 경우 Adprep.exe에서 그룹 구성원 확인을 수행할 수 없습니다. 스마트 카드 자격 증명이 사용된 경우에도 /user 및 /userdomain을 모두 지정했더라도 Adprep.exe에서 그룹 구성원 확인을 수행할 수 없습니다.  
  
Adprep에서 작업을 성공적으로 완료하면 더 이상 작업이 필요하지 않습니다. 액세스 오류로 인해 Adprep을 실행하는 동안 오류가 발생하면 올바른 구성원으로 계정을 제공하십시오. 자세한 내용은 참조 [자격 증명 Adprep.exe를 실행 하 고 Active Directory 도메인 서비스를 설치 요구 사항](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)합니다.  
  
### <a name="syntax-for-adprep-in-windows-server-2012"></a>Windows Server 2012의 Adprep에 대한 구문

다음 구문을 사용하여 AD DS 설치와 별도로 adprep을 실행할 수 있습니다.  

```
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *  
```

보다 상세한 로깅을 생성하려면 명령에 /logdsid를 사용합니다. adprep.log는 %windir%\System32\Debug\Adprep\Logs에 있습니다.  

### <a name="running-adprep-using-smartcard"></a>스마트 카드를 사용하여 adprep 실행

Windows Server 2012 버전의 adprep.exe는 자격 증명으로 스마트 카드를 사용 하 여 작동 하지만 명령줄을 통해 스마트 카드 자격 증명을 지정 하는 쉬운 방법은 없습니다. 한 가지 방법은 PowerShell cmdlet Get-Credential을 통해 스마트 카드 자격 증명을 가져오는 것입니다. 그런 다음 반환된 PSCredential 개체의 사용자 이름을 사용합니다. 이 이름은 `@@...`로 표시됩니다. 암호는 스마트 카드의 PIN입니다.  

/user가 지정된 경우 Adprep.exe를 실행하려면 /userdomain이 필요합니다. 스마트 카드 자격 증명의 경우 /userdomain이 스마트 카드에 표시된 기본 사용자 계정의 도메인이어야 합니다.  

### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>Adprep /domainprep /gpprep 명령, 자동으로 실행되지 않음

adprep /domainprep /gpprep 명령은 AD DS 설치 과정에서 실행되지 않습니다. 이 명령은 RSOP(정책 결과 집합) 계획 모드 기능에 필요한 사용 권한을 설정합니다. 이 명령에 대한 자세한 내용은 [Microsoft 기술 자료 문서 324392](https://support.microsoft.com/kb/324392)를 참조하세요. Active Directory 도메인에서 이 명령을 실행해야 하는 경우 AD DS 설치와 별도로 명령을 실행할 수 있습니다. Windows Server 2003 SP1 이상을 실행하는 도메인 컨트롤러를 배포하는 준비 과정으로 이 명령이 이미 실행된 경우에는 명령을 다시 실행하지 않아도 됩니다.  

Adprep/domainprep/gpprep을 실행 하지 않고 Windows Server 2012를 실행 하는 도메인 컨트롤러를 기존 도메인에 안전 하 게 추가할 수 있지만 RSOP 계획 모드가 제대로 작동 하지 않습니다.  

## <a name="BKMK_PrereqCheck"></a>설치 필수 구성 요소 유효성 검사 AD DS

AD DS 설치 마법사는 설치 전에 다음 필수 구성 요소가 충족되었는지 확인합니다. 이를 통해 잠재적으로 설치를 방해할 수 있는 문제를 수정할 수 있습니다.  
  
예를 들어 Adprep 관련 필수 구성 요소에는 다음 항목이 포함됩니다.  

- Adprep 자격 증명 확인: adprep을 실행해야 하는 경우 설치 마법사는 사용자에게 필요한 Adprep 작업을 실행하는 데 필요한 권한이 있는지 확인합니다.  
- 스키마 마스터 사용 가능 여부 확인: 설치 마법사에서 adprep /forestprep을 실행해야 함을 확인한 경우 스키마가 온라인 상태인지 확인합니다. 온라인 상태가 아닐 경우 작업에 실패합니다.  
- 인프라 마스터 사용 가능 여부 확인: 설치 마법사에서 adprep /domainprep을 실행해야 함을 확인한 경우 인프라 마스터가 온라인 상태인지 확인합니다. 온라인 상태가 아닐 경우 작업에 실패합니다.

레거시 Active Directory 설치 마법사(dcpromo.exe)에서 가져온 기타 필수 구성 요소 확인으로는 다음과 같은 확인이 있습니다.  

- 포리스트 이름 확인: 포리스트 이름이 유효하고 현재 존재하는 이름이 아닌지 확인합니다.  
- NetBIOS 이름 확인: 제공된 NetBIOS 이름이 유효하고 기존의 이름과 충돌하지 않는지 확인합니다.  
- 구성 요소 경로 확인: Active Directory 데이터베이스, 로그 및 SYSVOL의 경로가 유효하고 이러한 항목에 대해 사용 가능한 디스크 공간이 충분한지 확인합니다.  
- 자식 도메인 이름 확인: 부모 도메인 이름 및 새로운 자식 도메인 이름이 유효하고 기존의 도메인과 충돌하지 않는지 확인합니다.  
- 트리 도메인 이름 확인: 지정된 트리 이름이 유효하고 현재 존재하는 이름이 아닌지 확인합니다.  

## <a name="BKMK_SystemReqs"></a>시스템 요구 사항

Windows server 2012에 대 한 시스템 요구 사항은 Windows 2008 Server 2008 r 2에서 변경 되지 않았습니다. 자세한 내용은 [Windows Server 2008 R2 SP1 시스템 요구 사항](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx) (https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx) 을 참조 하세요.  

일부 기능에는 추가 요구 사항이 포함될 수 있습니다. 예를 들어 가상 도메인 컨트롤러 복제 기능을 사용 하려면 PDC 에뮬레이터에서 Windows Server 2012를 실행 하 고 Hyper-v 역할이 설치 된 Windows Server 2012를 실행 하는 컴퓨터를 실행 해야 합니다.  

## <a name="BKMK_KnownIssues"></a>알려진 문제

이 섹션에는 Windows Server 2012의 AD DS 설치에 영향을 주는 알려진된 문제 중 일부를 나열 합니다. 기타 알려진된 문제에 대 한 참조 [도메인 컨트롤러 배포 문제 해결](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)합니다.  

- 원격으로 adprep /forestprep 실행 시 Windows 방화벽에 의해 스키마에 대한 WMI 액세스가 차단된 경우 %systemroot%\system32\debug\adprep에 있는 adprep 로그에 다음 오류가 로깅됩니다.  

   ```
   Adprep encountered a Win32 error.
   Error code: 0x6ba Error message: The RPC server is unavailable.  
   ```

   이 경우 스키마 마스터에서 adprep /forestprep을 직접 실행하거나 다음 명령 중 하나를 실행하여 WMI 트래픽이 Windows 방화벽을 통과하도록 허용하여 이 오류를 해결할 수 있습니다.

   Windows Server 2008 이상의 경우:

   ```
   netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=yes
   ```

   Windows Server 2003의 경우:

   ```
   netsh firewall set service RemoteAdmin enable
   ```

   adprep이 완료되면 다음 명령 중 하나를 실행하여 WMI 트래픽을 다시 차단할 수 있습니다.

   ```
   netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=no
   ```

   ```
   netsh firewall set service remoteadmin disable
   ```

- Ctrl + C를 입력하여 Install-ADDSForest cmdlet을 취소할 수 있습니다. 취소 작업은 설치를 중지하며 서버 상태에 대한 모든 변경 사항을 되돌립니다. 단, 취소 명령을 실행하고 나면 컨트롤이 Windows PowerShell로 반환되지 않으며 cmdlet이 무기한 정지될 수 있습니다.  
- **설치 하기 전에 대상 서버가 도메인에 가입 되지 않은 경우 스마트 카드 자격 증명을 사용 하 여 추가 도메인 컨트롤러를 설치 하지 못합니다.**  

   이 경우 반환된 오류 메시지는 다음과 같습니다.  

   복제 원본 도메인 컨트롤러 *원본 도메인 컨트롤러 이름*에 연결할 수 없습니다(예외: 로그온 실패: 알 수 없는 사용자 이름 또는 잘못된 암호).  

   대상 서버를 도메인에 가입시킨 후 스마트 카드를 사용하여 설치를 수행하면 설치가 제대로 수행됩니다.  
  
- **32비트 프로세스에서 ADDSDeployment 모듈이 실행되지 않습니다.** ADDSDeployment cmdlet 및 기본 64 비트 프로세스를 지원 하지 않는 다른 모든 cmdlet을 포함 하는 스크립트를 사용 하 여 Windows Server 2012의 배포 및 구성을 자동화 하는 경우 ADDSDeployment를 나타내는 오류와 함께 스크립트가 실패할 수 있습니다. cmdlet을 찾을 수 없습니다.  

   이 경우 기본 64비트 프로세스를 지원하지 않는 cmdlet과 별도로 ADDSDeployment cmdlet을 실행해야 합니다.  

- 복원 파일 시스템 이라는 Windows Server 2012에는 새로운 파일 시스템이 있습니다. ReFS(복원 파일 시스템)로 포맷된 데이터 볼륨에 Active Directory 데이터베이스, 로그 파일 또는 SYSVOL을 저장하지 마십시오. ReFS에 대한 자세한 내용은 [차세대 Windows 파일 시스템 개발: ReFS](https://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx)를 참조하세요.  
- 서버 관리자에서 Server Core 설치에서 AD DS 또는 기타 서버 역할을 실행 하 고 Windows Server 2012로 업그레이드 하는 서버 이벤트 및 상태가 예상 대로 수집 하는 경우에 서버 역할이 빨간색 상태로 나타날 수 있습니다. 예비 릴리스 Windows Server 2012의 Server Core 설치를 실행 하는 서버에도 영향을 줄 수 있습니다.  

### <a name="active-directory-domain-services-installation-hangs-if-an-error-prevents-critical-replication"></a>오류로 인해 중요한 복제가 수행되지 않는 경우 Active Directory Domain Services 설치가 정지됩니다.

중요 복제 단계를 수행하는 동안 AD DS 설치에 오류가 발생하면 설치가 무기한 정지될 수 있습니다. 예를 들어 네트워킹 오류로 인해 중요 복제를 완료하지 못한 경우 설치가 중단됩니다.  
  
서버 관리자를 사용하여 설치하는 경우 설치 진행률 페이지는 계속 열려 있을 수 있지만 화면에 오류가 보고되지 않으며 약 15분 동안 진행률이 바뀌지 않을 수 있습니다. Windows PowerShell을 사용하는 경우에는 Windows PowerShell 창에 표시된 진행률이 15분 이상 바뀌지 않습니다.  
  
이 문제가 발생하면 대상 서버의 %systemroot%\debug 폴더에 있는 dcpromo.log 파일을 확인하십시오. 일반적으로 이 로그 파일에는 반복된 복제 오류가 표시됩니다. 이 문제와 관련하여 알려진 일부 원인은 다음과 같습니다.  

- 네트워킹 문제는 승격 중인 대상 서버와 복제 원본 도메인 컨트롤러 간 중요한 복제가 수행되지 못하도록 합니다.  

   예를 들어 dcpromo.log에 다음 내용이 표시됩니다.  

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

   설치 프로세스에서 중요한 복제를 무기한 재시도하므로 기본 네트워크 문제가 해결되면 도메인 컨트롤러 설치가 계속 수행됩니다. 필요에 따라 ipconfig, nslookup 및 netmon과 같은 도구를 사용하여 네트워킹 문제를 조사합니다. 수준을 올리려는 도메인 컨트롤러와 AD DS 설치 중에 선택한 복제 파트너가 연결되어 있는지 확인합니다. 또한 이름 확인이 작동 중인지 확인합니다.  

   네트워크 연결 및 이름 확인에 대한 AD DS 설치 요구 사항은 설치가 시작되기 전 필수 구성 요소 확인 중에 유효성이 검사됩니다. 그러나 필수 구성 요소 유효성 검사가 발생한 후 설치가 완료되기 전에 일부 오류 조건이 발생할 수 있습니다(예: 복제 파트너가 설치 중에 사용할 수 없게 된 경우).  

- 복제본 도메인 컨트롤러를 설치하는 동안 설치 자격 증명에 대해 대상 서버의 로컬 관리자 계정이 지정되고 로컬 관리자 계정의 암호가 도메인 관리자 계정의 암호와 일치합니다. 이 경우 설치 마법사를 완료 수 있으며 "액세스가 거부 되었습니다." 오류가 발생 하기 전에 설치를 시작할 수 있습니다.  

   예를 들어 dcpromo.log에 다음 내용이 표시됩니다.  

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

   운영 체제를 다시 설치를 복구 하기 위해서는 필요한 오류는 로컬 관리자 계정 및 암호를 지정 하 여 발생 하는 경우 [메타 데이터 정리 작업을 수행할](https://technet.microsoft.com/library/cc816907(WS.10).aspx) 설치를 완료 한 다음 다시 도메인 관리자 자격 증명을 사용 하 여 AD DS 설치에 실패 한 도메인 컨트롤러에 대 한 계정입니다. 서버를 다시 시작하는 것으로는 이 오류가 해결되지 않습니다. 서버에서는 설치가 성공적으로 완료되지 않은 경우에도 AD DS가 설치된 것으로 나타내기 때문입니다.  

### <a name="BKMK_nonnormalDNSNameWarning"></a>Active Directory Domain Services 구성 마법사는 정규화 되지 않은 DNS 이름이 지정 된 경우 경고를 표시 합니다.

새 도메인이나 포리스트를 만들 때 정규화되지 않은 다국어 문자를 포함하는 DNS 도메인 이름을 지정하는 경우 Active Directory 도메인 서비스 구성 마법사에는 이름에 대한 DNS 쿼리가 실패할 수 있다는 경고가 표시됩니다. DNS 도메인 이름이 배포 구성 페이지에서 지정된 경우에도 나중에 마법사의 필수 구성 요소 확인 페이지에 경고가 표시됩니다.  

Füßball.com 이나 'ΣΤ'.com와 같은 정규화 되지 않은 이름을 사용 하는 DNS 도메인 이름을 지정 하는 경우 (정규화 된 버전: füssball.com 및 β), winhttp에 액세스 하려고 하는 클라이언트 애플리케이션 이름 확인 Api를 호출 하기 전에 이름을 정규화 합니다. 일부 대화 상자에 "'ΣΤ'.com"를 입력 하는 경우 "β" 및 DNS 서버가 일치 하는 것 "'ΣΤ'.com"에 대 한 리소스 레코드를 DNS 쿼리가 전송 됩니다. 따라서 사용자는 이름을 확인할 수 없습니다.  

다음 예제에서는 정규화되지 않은 IDN 이름 사용 시 발생할 수 있는 문제 중 하나가 설명됩니다.  

1. 정규화 되지 않은 이름을 사용 하 여 도메인 생성 되어 dns 서버에 등록: füßball.com  
2. 컴퓨터 "nps" 도메인에 가입 하 고 등록 된 이름을 가져옵니다: nps.füßball.com  
3. 클라이언트 애플리케이션 서버 nps.füßball.com에 연결 하려고 합니다.  
4. 클라이언트 애플리케이션 이름 확인 Api를 호출 하는 이름 nps.füßball.com을 해결 하려고 시도 합니다.  
5. 정규화로 인해 이름이 nps.füssball.com으로 변환 됩니다 및 nps.füßball.com으로 연결을 통해 쿼리  
6. 클라이언트 애플리케이션에는 등록 된 이름 nps.füßball.com 이므로 이름을 확인할 수 없으면  

Active Directory Domain Services 구성 마법사의 필수 구성 요소 확인 페이지에 경고가 표시되면 배포 구성 페이지로 돌아가 정규화된 DNS 도메인 이름을 지정하십시오. Windows PowerShell을 사용하여 새 도메인을 설치하는 경우에는 -DomainName 옵션에 대해 정규화된 DNS 이름을 지정하십시오.  

Idn에 대 한 자세한 내용은 참조 [처리 Idn 다국어 도메인 이름 ()](https://msdn.microsoft.com/library/windows/desktop/dd318142(v=vs.85).aspx)합니다.  
