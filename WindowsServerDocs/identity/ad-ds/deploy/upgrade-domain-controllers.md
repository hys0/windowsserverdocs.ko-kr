---
title: Windows Server 2016으로 도메인 컨트롤러 업그레이드
description: 이 문서에서는 Windows Server 2012 r 2에서 Windows Server 2016로 업그레이드 하는 방법을 설명 합니다.
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3e144a09c99d9b72d623956e868b3f573962ed94
ms.sourcegitcommit: 67833e36b8b2c6194a1426a974c5ad9c859fa4c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68329644"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Windows Server 2016으로 도메인 컨트롤러 업그레이드

적용 대상: Windows Server

이 항목에서는 windows server 2016의 Active Directory Domain Services에 대 한 배경 정보를 제공 하 고 Windows Server 2012 또는 Windows Server 2012 r 2에서 도메인 컨트롤러를 업그레이드 하는 프로세스에 대해 설명 합니다.

## <a name="pre-requisites"></a>필수 구성 요소

도메인을 업그레이드 하는 권장 방법은 최신 버전의 Windows Server를 실행 하는 도메인 컨트롤러를 승격 하 고 필요에 따라 이전 도메인 컨트롤러의 수준을 내리는 것입니다. 기존 도메인 컨트롤러의 운영 체제를 업그레이드할 때 이 방법이 선호됩니다. 이 목록에서는 최신 버전의 Windows Server를 실행 하는 도메인 컨트롤러의 수준을 올리기 전에 수행 해야 하는 일반적인 단계에 대해 설명 합니다.

1. 대상 서버가 시스템 요구 사항을 충족하는지 확인합니다.
1. 응용 프로그램 호환성을 확인 합니다.
1. Windows Server 2016로의 이동에 대 한 권장 사항 검토
1. 보안 설정을 확인합니다. 자세한 내용은 [Windows Server 2016의 AD DS와 관련 된 사용 되지 않는 기능 및 동작 변경 내용](../../../get-started/deprecated-features.md)을 참조 하세요.
1. 설치하려고 계획 중인 컴퓨터에서 대상 서버로 연결된 상태를 확인합니다.
1. 필요한 작업 마스터 역할의 가용성을 확인합니다.
   - 기존 도메인 및 포리스트에서 Windows Server 2016를 실행 하는 첫 번째 DC를 설치 하려면 설치를 실행 하는 컴퓨터에서 adprep/forestprep를 실행 하기 위해 **스키마 마스터** 에 연결 해야 합니다. 그리고.
   - 포리스트 스키마가 이미 확장 된 도메인에 첫 번째 DC를 설치 하려면 **인프라 마스터**에만 연결 하면 됩니다.
   - 기존 포리스트에 도메인을 설치 하거나 제거 하려면 **도메인 명명 마스터**에 연결 해야 합니다.
   - 도메인 컨트롤러를 설치 하려면 **RID 마스터** 에도 연결 해야 합니다.
   - 기존 포리스트에 첫 번째 읽기 전용 도메인 컨트롤러를 설치 하는 경우 도메인 명명 컨텍스트 또는 NDNC 라고도 하는 각 응용 프로그램 디렉터리 파티션에 대 한 **인프라 마스터** 에 연결 해야 합니다.

### <a name="installation-steps-and-required-administrative-levels"></a>설치 단계 및 필요한 관리 수준

다음 표에서는 이러한 단계를 수행 하기 위한 업그레이드 단계와 권한 요구 사항을 요약 하 여 설명 합니다.

|설치 작업|자격 증명 요구 사항|
| ----- | ----- |
|새 포리스트 설치|대상 서버의 로컬 관리자|
|기존 포리스트에 새 도메인 설치|Enterprise Admins|
|기존 도메인에 추가 DC 설치|Domain Admins|
|adprep /forestprep 실행|Schema Admins, Enterprise Admins 및 Domain Admins|
|adprep /domainprep 실행|Domain Admins|
|adprep /domainprep /gpprep 실행|Domain Admins|
|adprep /rodcprep 실행|Enterprise Admins|

Windows Server 2016의 새로운 기능에 대 한 자세한 내용은 [Windows server 2016의 새로운](../../../get-started/what-s-new-in-windows-server-2016.md)기능을 참조 하세요.

## <a name="supported-in-place-upgrade-paths"></a>지원되는 전체 업그레이드 경로

64 비트 버전의 Windows Server 2012 또는 Windows Server 2012 r 2를 실행 하는 도메인 컨트롤러는 Windows Server 2016로 업그레이드할 수 있습니다. Windows Server 2016만 64 비트 버전으로 제공 되므로 64 비트 버전 업그레이드만 지원 됩니다.

|이 버전을 실행 중인 경우:|업그레이드 가능한 버전|
| ----- | ----- |
|Windows Server 2012 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard 또는 Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 작업 그룹|Windows Storage Server 2016 작업 그룹|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 작업 그룹|

지원 되는 업그레이드 경로에 대 한 자세한 내용은 [지원 되는 업그레이드 경로](../../../get-started/supported-upgrade-paths.md) 를 참조 하세요.

## <a name="adprep-and-domainprep"></a>Adprep 및 Domainprep

기존 도메인 컨트롤러를 Windows Server 2016 운영 체제로 전체 업그레이드 하는 경우에는 adprep/forestprep 및 adprep/domainprep를 수동으로 실행 해야 합니다.  Adprep/forestprep는 포리스트에서 한 번만 실행 해야 합니다.  Adprep/domainprep는 Windows Server 2016로 업그레이드 하는 도메인 컨트롤러가 있는 각 도메인에서 한 번만 실행 해야 합니다.

새 Windows Server 2016 서버를 승격 하는 경우 이러한 서버를 수동으로 실행할 필요가 없습니다.  이러한 기능은 PowerShell 및 서버 관리자 환경에 통합 되어 있습니다.

Adprep 실행에 대 한 자세한 내용은 [Adprep 실행](https://technet.microsoft.com/library/dd464018.aspx) 을 참조 하세요.

## <a name="functional-level-features-and-requirements"></a>기능 수준 기능 및 요구 사항

Windows Server 2016에는 Windows Server 2003 포리스트 기능 수준이 필요 합니다. 즉, Windows Server 2016를 실행 하는 도메인 컨트롤러를 기존 Active Directory 포리스트에 추가 하려면 포리스트 기능 수준이 Windows Server 2003 이상 이어야 합니다. 포리스트에 Windows Server 2003 이상을 실행하는 도메인 컨트롤러가 포함되지만 포리스트 기능 수준이 여전히 Windows 2000인 경우에는 설치도 차단됩니다.

포리스트에 Windows Server 2016 도메인 컨트롤러를 추가 하기 전에 windows 2000 도메인 컨트롤러를 제거 해야 합니다. 이 경우 다음 단계를 따르는 것이 좋습니다.

1. Windows Server 2003 이상을 실행하는 도메인 컨트롤러를 설치합니다. 이러한 도메인 컨트롤러는 Windows Server의 평가판에 배포될 수 있습니다. 또한이 단계에서는 해당 운영 체제 릴리스에 대 한 adprep.exe를 필수 구성 요소로 실행 해야 합니다.
1. Windows 2000 도메인 컨트롤러를 제거합니다. 특히 제거된 모든 도메인 컨트롤러의 도메인 컨트롤러 계정을 제거하려면 도메인 및 사용된 Active Directory 사용자, 컴퓨터에서 Windows Server 2000 도메인 컨트롤러를 강제로 제거하거나 적절하게 해당 컨트롤러의 수준을 내립니다.
1. 포리스트 기능 수준을 Windows Server 2003 이상으로 올립니다.
1. Windows Server 2016를 실행 하는 도메인 컨트롤러를 설치 합니다.
1. 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러를 제거합니다.

### <a name="rolling-back-functional-levels"></a>기능 수준 롤백

FFL (포리스트 기능 수준)을 특정 값으로 설정한 후에는 포리스트 기능 수준을 롤백하거나 낮출 수 없습니다. 단, 다음과 같은 예외가 있습니다.

- Windows Server 2012 R2 FFL에서 업그레이드 하는 경우 Windows Server 2012 R2로 다시 낮출 수 있습니다.
- Windows Server 2008 R2 FFL에서 업그레이드 하는 경우 Windows Server 2008 R2로 다시 낮출 수 있습니다.

도메인 기능 수준을 특정 값으로 설정한 후에는 도메인 기능 수준을 롤백하거나 낮출 수 없습니다. 단, 다음과 같은 예외가 있습니다.

- 도메인 기능 수준을 Windows server 2016로 올릴 때 포리스트 기능 수준이 Windows Server 2012 이하인 경우 도메인 기능 수준을 Windows Server 2012 또는 Windows Server 2012 r 2로 다시 롤백할 수 있습니다.

낮은 기능 수준에서 사용할 수 있는 기능에 대한 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 기능 수준 이해](../active-directory-functional-levels.md)를 참조하세요.

## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>다른 서버 역할 및 Windows 운영 체제와 AD DS의 상호 운용성

AD DS는 다음과 같은 Windows 운영 체제에서는 지원되지 않습니다.

- Windows MultiPoint Server
- Windows Server 2016 Essentials

AD DS는 다음과 같은 서버 역할 또는 역할 서비스도 실행하는 서버에는 설치할 수 없습니다.

- Microsoft Hyper-V Server 2016
- 원격 데스크톱 연결 브로커

## <a name="administration-of-windows-server-2016-servers"></a>Windows Server 2016 서버 관리

Windows 10 용 원격 서버 관리 도구를 사용 하 여 Windows Server 2016를 실행 하는 도메인 컨트롤러 및 기타 서버를 관리할 수 있습니다. Windows 10을 실행 하는 컴퓨터에서 Windows Server 2016 원격 서버 관리 도구를 실행할 수 있습니다.

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Windows Server 2016로 업그레이드 하는 방법에 대 한 단계별 가이드

다음은 Contoso 포리스트를 Windows Server 2012 r 2에서 Windows Server 2016로 업그레이드 하는 간단한 예입니다.

![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1. 포리스트에 새로운 Windows Server 2016을 가입 시킵니다. 메시지가 표시 되 면 다시 시작 합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)

1. 도메인 관리자 계정을 사용 하 여 새 Windows Server 2016에 로그인 합니다.
1. **서버 관리자**의 **역할 및 기능 추가**에서 새로운 Windows Server 2016에 **Active Directory Domain Services** 를 설치 합니다. 그러면 2012 R2 포리스트와 도메인에서 adprep이 자동으로 실행 됩니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png)

1. **서버 관리자**에서 노란색 삼각형을 클릭 하 고 드롭다운에서 **서버를 도메인 컨트롤러로 승격**을 클릭 합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)

1. **배포 구성** 화면에서 **기존 포리스트에 도메인 컨트롤러 추가** 를 선택 하 고 다음을 클릭 합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)

1. **도메인 컨트롤러 옵션** 화면에서 **DSRM (디렉터리 서비스 복원 모드)** 암호를 입력 하 고 다음을 클릭 합니다.
1. 나머지 화면에서 **다음**을 클릭 합니다.
1. **필수 구성 요소 확인** 화면에서 **설치**를 클릭 합니다. 다시 시작이 완료 되 면 다시 로그인 할 수 있습니다.
1. Windows Server 2012 R2 서버에서 **서버 관리자**의 도구 아래에서 **Windows PowerShell 용 모듈 Active Directory**을 선택 합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)

1. PowerShell windows에서 Move-ADDirectoryServerOperationMasterRole을 사용 하 여 FSMO 역할을 이동 합니다. 각 OperationMasterRole의 이름을 입력 하거나 숫자를 사용 하 여 역할을 지정할 수 있습니다. 자세한 내용은 [Move-ADDirectoryServerOperationMasterRole](https://technet.microsoft.com/library/hh852302.aspx) 을 참조 하세요.

    ``` powershell
    Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
    ```

    ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)

1. Windows Server 2016 서버로 이동 하 여 역할이 이동 되었는지 확인 하 고, **서버 관리자**의 **도구**에서 **Active Directory Module for Windows PowerShell**을 선택 합니다. `Get-ADDomain` 및`Get-ADForest` cmdlet을 사용 하 여 FSMO 역할 소유자를 확인 합니다.

    ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)

    ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)

1. Windows Server 2012 R2 도메인 컨트롤러의 수준을 내리고 제거 합니다. Dc 수준 내리기에 대 한 자세한 내용은 [도메인 컨트롤러 및](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md) 도메인 수준 내리기를 참조 하세요.
1. 서버가 강등 되 고 제거 되 면 포리스트 기능 및 도메인 기능 수준을 Windows Server 2016로 올릴 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Active Directory Domain Services 설치 및 제거의 새로운 기능](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)
- [Active Directory Domain Services &#40;수준 100 설치&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)
- [Windows Server 2016 기능 수준](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
