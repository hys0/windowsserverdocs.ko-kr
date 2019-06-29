---
title: Windows Server 2016으로 도메인 컨트롤러 업그레이드
description: 이 문서에서는 Windows Server 2012 R2에서 Windows Server 2016으로 업그레이드 하는 방법 설명
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 02124a05967b793890630d487b9bcf53081d3f62
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469446"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Windows Server 2016으로 도메인 컨트롤러 업그레이드

적용 대상: Windows Server 2016

이 항목에서는 Windows Server 2016의 Active Directory Domain Services에 대 한 배경 정보를 제공 하 고 Windows Server 2012 또는 Windows Server 2012 R2에서 도메인 컨트롤러를 업그레이드 하기 위한 과정을 설명 합니다.

## <a name="pre-requisites"></a>필수 구성 요소

도메인을 업그레이드 하는 최신 버전의 Windows Server를 실행 하 고 필요에 따라 이전 도메인 컨트롤러 수준 내리기 도메인 컨트롤러를 승격 하는 것이 좋습니다. 기존 도메인 컨트롤러의 운영 체제를 업그레이드할 때 이 방법이 선호됩니다. 이 목록에서는 최신 버전의 Windows Server를 실행 하는 도메인 컨트롤러의 수준을 올리기 전에 수행 하려면 일반 단계를 다룹니다.

1. 대상 서버가 시스템 요구 사항을 충족하는지 확인합니다.
2. 응용 프로그램 호환성을 확인 합니다.
3. Windows Server 2016으로 전환 하는 것에 대 한 권장 사항 검토
4. 보안 설정을 확인합니다. 자세한 내용은 [사용 되지 않는 기능 및 동작 변경 내용은 Windows Server 2016에서 AD DS 관련](https://docs.microsoft.com/windows-server/get-started/deprecated-features)합니다.
5. 설치하려고 계획 중인 컴퓨터에서 대상 서버로 연결된 상태를 확인합니다.
6. 필요한 작업 마스터 역할의 가용성을 확인합니다.
   - 설치를 실행 하는 컴퓨터에서 기존 도메인 및 포리스트를 Windows Server 2016을 실행 하는 첫 번째 DC를 설치 하려면에 대 한 연결을 해야 합니다 **스키마 마스터** 인프라 마스터와 adprep /forestprep을 실행 하려면 하려면 adprep /domainprep을 실행 합니다.
   - 포리스트 스키마가 이미 확장된 도메인에 첫 번째 DC를 설치하려면 인프라 마스터에만 연결하면 됩니다.
   - 를 설치 하거나 기존 포리스트에 도메인을 제거 하려면 연결 해야 합니다 **도메인 명명 마스터**합니다.
   - 모든 도메인 컨트롤러 설치에도 연결 해야 합니다 **RID 마스터입니다.**
   - 기존 포리스트에 첫 번째 읽기 전용 도메인 컨트롤러를 설치할 경우에는 비도메인 명명 컨텍스트 또는 NDNC라고도 하는 각 응용 프로그램 디렉터리 파티션용 인프라 마스터에 연결해야 합니다.

### <a name="installation-steps-and-required-administrative-levels"></a>설치 단계 및 필요한 관리 수준

다음 표에서 업그레이드 단계 및 이러한 단계를 수행 하는 사용 권한 요구 사항 요약

|설치 작업|자격 증명 요구 사항|
| ----- | ----- |
|새 포리스트 설치|대상 서버의 로컬 관리자|
|기존 포리스트에 새 도메인 설치|Enterprise Admins|
|기존 도메인에 추가 DC 설치|Domain Admins|
|adprep /forestprep 실행|Schema Admins, Enterprise Admins 및 Domain Admins|
|adprep /domainprep 실행|Domain Admins|
|adprep /domainprep /gpprep 실행|Domain Admins|
|adprep /rodcprep 실행|Enterprise Admins|

Windows Server 2016의 새로운 기능에 대 한 자세한 내용은 참조 하세요. [Windows Server 2016의 새로운 기능](../../../get-started/what-s-new-in-windows-server-2016.md)합니다.

## <a name="supported-in-place-upgrade-paths"></a>지원되는 전체 업그레이드 경로

64 비트 버전의 Windows Server 2012 또는 Windows Server 2012 R2를 실행 하는 도메인 컨트롤러는 Windows Server 2016으로 업그레이드할 수 있습니다. Windows Server 2016에서 64 비트 버전에만 제공 되므로 64 비트 버전 업그레이드만 지원 됩니다.

|이 버전을 실행 하는 경우|이러한 버전으로 업그레이드 가능|
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

지원 되는 업그레이드 경로 대 한 자세한 내용은 참조 하세요. [업그레이드 경로 지원](../../../get-started/supported-upgrade-paths.md)

## <a name="adprep-and-domainprep"></a>Adprep 및 Domainprep

Windows Server 2016 운영 체제에는 기존 도메인 컨트롤러의 현재 위치 업그레이드를 수행 하는 경우 adprep /forestprep 및 adprep /domainprep을 수동으로 실행 해야 합니다.  Adprep /forestprep 포리스트에 한 번만 실행 해야 합니다.  Adprep /domainprep을 Windows Server 2016으로 업그레이드 하는 도메인 컨트롤러에는 각 도메인에 한 번 실행 해야 합니다.

새 Windows Server 2016 서버를 승격 하는 경우 이러한 작업을 수동으로 실행할 필요가 없습니다.  PowerShell에 통합 되어 이러한 및 서버 관리자에서 발생 합니다.

Adprep을 실행 하는 방법은 참조 하세요. [Adprep 실행](https://technet.microsoft.com/library/dd464018.aspx)

## <a name="functional-level-features-and-requirements"></a>기능 수준 기능 및 요구 사항

Windows Server 2016 Windows Server 2003 포리스트 기능 수준이 필요 합니다. 즉, 기존 Active Directory 포리스트에 Windows Server 2016를 실행 하는 도메인 컨트롤러를 추가 하려면 먼저 포리스트 기능 수준을 Windows Server 2003 이상 이어야 합니다. 포리스트에 Windows Server 2003 이상을 실행하는 도메인 컨트롤러가 포함되지만 포리스트 기능 수준이 여전히 Windows 2000인 경우에는 설치도 차단됩니다.

Windows 2000 도메인 컨트롤러를 포리스트에 Windows Server 2016 도메인 컨트롤러를 추가 하기 전에 제거 해야 합니다. 이 경우 다음 단계를 따르는 것이 좋습니다.

1. Windows Server 2003 이상을 실행하는 도메인 컨트롤러를 설치합니다. 이러한 도메인 컨트롤러는 Windows Server의 평가판에 배포될 수 있습니다. 이 단계는 필수 구성 요소와 해당 운영 체제 릴리스에 대 한 adprep.exe를 실행 해야 합니다.
1. Windows 2000 도메인 컨트롤러를 제거합니다. 특히 제거된 모든 도메인 컨트롤러의 도메인 컨트롤러 계정을 제거하려면 도메인 및 사용된 Active Directory 사용자, 컴퓨터에서 Windows Server 2000 도메인 컨트롤러를 강제로 제거하거나 적절하게 해당 컨트롤러의 수준을 내립니다.
1. 포리스트 기능 수준을 Windows Server 2003 이상으로 올립니다.
1. Windows Server 2016을 실행 하는 도메인 컨트롤러를 설치 합니다.
1. 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러를 제거합니다.

### <a name="rolling-back-functional-levels"></a>기능 수준 롤백하는 중

포리스트 기능 수준 (FFL) 특정 값으로 설정한 후 롤백할 하거나 다음 예외를 사용 하 여 포리스트 기능 수준은 낮출 수 없습니다.

- Windows Server 2012 R2 FFL에서 업그레이드 하는 경우에 Windows Server 2012 R2로 다시 낮출 수 있습니다.
- Windows Server 2008 R2 FFL에서 업그레이드 하는 경우에 Windows Server 2008 R2로 다시 낮출 수 있습니다.

도메인 기능 수준을 특정 값으로 설정한 후 롤백할 하거나 다음 예외를 사용 하 여 도메인 기능 수준은 낮출 수 없습니다.

- Windows Server 2012 또는 Windows Server 2012 R2 도메인 기능 수준이 옵션이 다시 Windows Server 2016 도메인 기능 수준을 올릴 때 포리스트 기능 수준을 Windows Server 2012 또는 아래 인 경우

낮은 기능 수준에서 사용할 수 있는 기능에 대한 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 기능 수준 이해](../active-directory-functional-levels.md)를 참조하세요.

## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>다른 서버 역할 및 Windows 운영 체제와 AD DS의 상호 운용성

AD DS는 다음과 같은 Windows 운영 체제에서는 지원되지 않습니다.

- Windows MultiPoint Server
- Windows Server 2016 Essentials

AD DS는 다음과 같은 서버 역할 또는 역할 서비스도 실행하는 서버에는 설치할 수 없습니다.

- Microsoft Hyper-V Server 2016
- 원격 데스크톱 연결 브로커

## <a name="administration-of-windows-server-2016-servers"></a>Windows Server 2016 서버를 관리

도메인 컨트롤러와 Windows Server 2016을 실행 하는 다른 서버를 관리 하는 원격 서버 관리 도구에 대 한 Windows 10을 사용 합니다. Windows 10을 실행 하는 컴퓨터에서 Windows Server 2016 원격 서버 관리 도구를 실행할 수 있습니다.

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Windows Server 2016으로 업그레이드 하는 단계별 지침

다음은 Windows Server 2016으로 Contoso 포리스트에 Windows Server 2012 R2에서 업그레이드 하는 간단한 예제입니다.

![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1. 새 Windows Server 2016를 포리스트에 조인 합니다. 메시지가 표시 되 면 다시 시작 합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)

1. 도메인 관리자 계정 사용 하 여 새 Windows Server 2016에 로그인 합니다.
1. **서버 관리자**아래에 있는 **역할 및 기능 추가**를 설치 **Active Directory Domain Services** 새 Windows Server 2016에서. Adprep는 2012 R2 포리스트 및 도메인에 자동으로 실행 됩니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png)

1. **서버 관리자**노란색 삼각형을 클릭 하 고 드롭다운 목록에서 클릭 **서버를 도메인 컨트롤러로 승격**합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)

1. 에 **배포 구성** 화면에서 **도메인 컨트롤러를 기존 포리스트에 추가** 고 다음을 클릭 합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)

1. 에 **도메인 컨트롤러 옵션** 화면에서 입력 합니다 **디렉터리 서비스 복원 모드 (DSRM)** 암호 하 고 다음 합니다.
1. 화면 나머지 클릭 **다음**합니다.
1. 에 **필수 구성 요소 검사** 화면에서 클릭 **설치**합니다. 다시 시작 하면 완료 되 면 수 다시 로그인 합니다.
1. Windows Server 2012 R2 서버에서의 **서버 관리자**, 도구 선택 **Windows PowerShell 용 Active Directory 모듈**합니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)

1. PowerShell 창에서 이동-ADDirectoryServerOperationMasterRole 사용 하 여 FSMO 역할을 이동 합니다. 각-OperationMasterRole의 이름을 입력 하거나 숫자를 사용 하 여 역할을 지정할 수 있습니다. 자세한 내용은 참조 하세요. [ADDirectoryServerOperationMasterRole 이동](https://technet.microsoft.com/library/hh852302.aspx)

   ``` powershell
   Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
   ```

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)

1. 역할에 Windows Server 2016 서버로 이동 하 여 이동 되었는지 확인 **서버 관리자**아래에 있는 **도구**를 선택 **Windows PowerShell 용 Active Directory 모듈**합니다. 사용 된 `Get-ADDomain` 및 `Get-ADForest` FSMO 역할 소유자를 확인 하기 위한 cmdlet입니다.

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)

   ![업그레이드](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)

1. 수준 내리기 및 Windows Server 2012 R2 도메인 컨트롤러를 제거 합니다. Dc 수준 내리기에 대 한 내용은 참조 [도메인 컨트롤러 수준 내리기 및 도메인](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)
1. 서버 강등 되 고 제거 되 면 포리스트 기능 및 Windows Server 2016 도메인 기능 수준을 올릴 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Active Directory Domain Services 설치 및 제거의 새로운 기능](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)  
- [Active Directory Domain Services 설치 &#40;수준 100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)
- [Windows Server 2016 기능 수준](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
