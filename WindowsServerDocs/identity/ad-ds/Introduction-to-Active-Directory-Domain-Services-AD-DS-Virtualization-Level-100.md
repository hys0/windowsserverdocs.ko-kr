---
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
title: AD DS(Active Directory 도메인 서비스) 가상화 소개(수준 100)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b818ba5a58db38bdb3c0f630a8d9d2daa1494403
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878094"
---
# <a name="introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100"></a>AD DS(Active Directory 도메인 서비스) 가상화 소개(수준 100)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

AD DS(Active Directory 도메인 서비스) 환경의 가상화는 여러 해 동안 진행되어 왔습니다. Windows Server 2012부터, AD DS는 가상화 안전 기능을 도입 함으로써 도메인 컨트롤러 가상화에 대 한 향상 된 지원을 제공 합니다.

## <a name="safe-virtualization-of-domain-controllers"></a>도메인 컨트롤러의 안전한 가상화

가상 환경에는 논리적 클록 기반 복제 스키마에 종속된 분산 워크로드와 관련된 고유한 해결 과제가 있습니다. 예를 들어 AD DS 복제에서는 각 도메인 컨트롤러의 트랜잭션에 할당된 일정하게 증가하는 값(USN 또는 업데이트 시퀀스 번호라고 함)을 사용합니다. 각 도메인 컨트롤러의 데이터베이스 인스턴스에 invocationid 라는 id가 지정 됩니다. 도메인 컨트롤러의 InvocationID는 해당 USN과 함께 각 도메인 컨트롤러에서 수행되는 모든 쓰기 트랜잭션과 관련된 고유 식별자의 역할을 하므로 포리스트 내에서 고유해야 합니다.

AD DS 복제에서는 각 도메인 컨트롤러에서 InvocationID 및 USN을 사용하여 다른 도메인 컨트롤러에 복제해야 하는 변경 내용을 확인합니다. 도메인 컨트롤러에서 도메인 컨트롤러의 인식 시간에 롤백되고 USN이 완전히 다른 트랜잭션에 다시 사용 됩니다, 다른 도메인 컨트롤러가 해당 InvocationID의 컨텍스트에서 재사용된 USN와 관련 된 업데이트 이미 받은 생각 됩니다 때문에 복제는 수렴 되지 않습니다.

예를 들어 다음 그림에서는 VDC2, 즉 가상 컴퓨터에서 실행되는 대상 도메인 컨트롤러에서 USN 롤백이 감지된 경우 Windows Server 2008 R2 이하 운영 체제에서 발생하는 이벤트의 순서를 보여 줍니다. 이 그림에서는 VDC2 VDC2의 데이터베이스에 롤백되는 시간에 부적절 하 게 나타내는 복제 파트너에 게 이전에 표시 하는 최신 USN 값을 전송한는 복제 파트너를 감지할 때 VDC2에서 USN 롤백이 감지 발생 합니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

가상 컴퓨터 (VM) 쉽게 롤백할 수는 도메인 컨트롤러의 Usn (논리적 클록), 여 하이퍼바이저 관리자에 대 한 예를 들어, 도메인 컨트롤러의 인식 스냅숏을 적용 합니다. USN 및 USN 하는 방법에 대 한 자세한 내용은 롤백, USN 롤백이 감지 되지 않은 인스턴스를 설명 하기 위해 다른 그림을 포함 하 여 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)합니다.

Windows Server 2012부터, Vm-generation ID 라는 식별자를 노출 하는 하이퍼바이저 플랫폼에서 호스트 되는 AD DS 가상 도메인 컨트롤러 수 감지 하 고 적용할 롤백되는 경우 가상 컴퓨터는 시간에 VM 스냅숏의 응용 프로그램에서 AD DS 환경을 보호 하는 데 필요한 안전 조치 합니다. VM-생성 ID 설계에서는 하이퍼바이저 공급업체에 독립적인 메커니즘을 사용하여 이 식별자를 게스트 가상 컴퓨터의 주소 공간에 표시하므로 VM-생성 ID를 지원하는 모든 하이퍼바이저에서 안전한 가상화 환경을 일관되게 사용할 수 있습니다. 가상 컴퓨터 내에서 실행되는 서비스 및 응용 프로그램을 통해 이 식별자를 샘플링하여 가상 컴퓨터가 제시간에 롤백되었는지 감지할 수 있습니다.

### <a name="BKMK_HowSafeguardsWork"></a>이러한 가상화 세이프 가드는 어떻게 작동 하나요?
도메인 컨트롤러를 설치 하는 동안 AD DS 도메인 컨트롤러의 컴퓨터 개체 (디렉터리 정보 트리 또는 DIT 라고도 함)는 데이터베이스에 대 한 Msds-generationid 특성의 일부로 VM 생성 Id 식별자 처음 저장 합니다. VM 생성 ID는 가상 컴퓨터 내 Windows 드라이버를 통해 독립적으로 추적됩니다.

관리자가 이전 스냅숏에서 가상 컴퓨터를 복원하면 가상 컴퓨터 드라이버의 현재 VM 생성 ID 값이 DIT의 값과 비교됩니다.

두 값이 다르면 invocationID가 다시 설정되고 RID 풀이 삭제되므로 USN을 다시 사용할 수 없습니다. 값이 같으면 트랜잭션이 정상적으로 커밋됩니다.

또한 AD DS에서는 도메인 컨트롤러가 다시 부팅될 때마다 가상 컴퓨터의 현재 VM 생성 ID 값을 DIT의 값과 비교하며, 값이 다른 경우 invocationID를 다시 설정하고, RID 풀을 삭제하고, DIT를 새 값으로 업데이트합니다. 뿐만 아니라 안전한 복원을 완료하기 위해 SYSVOL 폴더를 비정식으로 동기화합니다. 이를 통해 종료된 VM에서의 스냅숏 적용으로 보호 기능을 확장할 수 있습니다. Windows Server 2012에 도입 된 이러한 보호 기능 배포 및 관리 가상화 된 환경에서 도메인 컨트롤러의 고유한 이점을 제대로 활용 하려면 AD DS 관리자를 사용 합니다.

다음 그림 가상화 안전 조치를 지 원하는 VM-생성 Id 하이퍼바이저에서 Windows Server 2012를 실행 하는 가상화 된 도메인 컨트롤러에서 동일한 USN 롤백이 감지 된 경우 적용 되는 방법을 보여 줍니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

이 예에서 하이퍼바이저가 VM-생성 ID 값의 변경을 감지한 경우, 가상화 DC(이전 예의 A~B)에 대한 InvocationID를 다시 설정하고, 하이퍼바이저에서 저장한 새 값(G2)과 일치하도록 VM에 저장된 VM-생성 ID 값을 업데이트하는 등 가상화 보호 기능이 트리거됩니다. 이러한 보호 기능은 두 도메인 컨트롤러 모두에 대해 복제가 수렴되도록 합니다.

Windows Server 2012와 AD DS VM-생성 Id 인식 하이퍼바이저에서 호스트 되는 가상 도메인 컨트롤러에 보호 기능을 적용 하 고 되도록 실수로 응용 프로그램의 스냅숏 또는 다른 이러한 하이퍼바이저 지원 메커니즘이 롤백 할 수 있는 가상 컴퓨터의 상태 (USN 버블 같은 복제 문제를 방지 또는 느린 개체가)에서 AD DS 환경을 방해 하지 않도록 합니다. 그러나 가상 컴퓨터 스냅숏을 적용하여 도메인 컨트롤러를 복원하는 것은 도메인 컨트롤러 백업의 대체 메커니즘으로 권장되지 않습니다. Windows Server 백업 또는 기타 VSS 기록기 기반 백업 솔루션을 계속 사용하는 것이 좋습니다.

> [!CAUTION]
> 프로덕션 환경에서 도메인 컨트롤러가 실수로 스냅숏으로 되돌려 진 응용 프로그램 공급 업체에 문의 하 고 스냅숏 이후에 이러한 프로그램의 상태를 확인에 대 한 지침은 해당 가상 컴퓨터에서 호스팅되는 서비스 복원 것이 좋습니다.

자세한 내용은 참조 [도메인 컨트롤러 안전 복원 아키텍처를 가상화](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)합니다.

## <a name="virtualized_dc_cloning"></a>가상화 된 도메인 컨트롤러 복제
Windows Server 2012 부터는 관리자 쉽고 안전 하 게 배포할 수 복제 도메인 컨트롤러는 기존 가상 도메인 컨트롤러를 복사 하 여 합니다. 가상 환경에서는 더 이상 관리자가 sysprep.exe를 사용하여 준비된 서버 이미지를 반복적으로 배포하고, 서버를 도메인 컨트롤러로 승격시킨 다음, 각 복제본 도메인 컨트롤러를 배포하기 위한 추가 구성 요구 사항을 완료할 필요가 없습니다.

> [!NOTE]
> 관리자는 기존 프로세스(예: sysprep.exe를 사용하여 서버 VHD(가상 하드 디스크)를 준비하고, 서버를 도메인 컨트롤러로 승격시킨 다음, 추가 구성 요구 사항 완료)에 따라 도메인의 첫 번째 도메인 컨트롤러를 배포해야 합니다. 재해 복구 시나리오에서는 최신 서버 백업을 사용하여 도메인의 첫 번째 도메인 컨트롤러를 복원합니다.

### <a name="scenarios-that-benefit-from-virtual-domain-controller-cloning"></a>가상 도메인 컨트롤러 복제를 활용하는 시나리오

-   새 도메인에서 추가 도메인 컨트롤러의 신속한 배포

-   복제를 사용해 도메인 컨트롤러를 신속하게 배포하여 AD DS 용량을 복원함으로써 재해 복구 중 비즈니스 연속성을 신속하게 복원

-   도메인 컨트롤러의 유연한 프로비전을 활용하여 증가된 확장 요구 사항을 충족함으로써 사설 클라우드 배포 최적화

-   프로덕션 출시 전 새로운 기능의 테스트 및 배포를 지원하는 신속한 테스트 환경 프로비전

-   지점에서 기존 도메인 컨트롤러를 복제하여 지점의 증가된 용량 요구 사항을 신속하게 충족

많은 도메인 컨트롤러를 신속하게 배포하는 동안 계속 기존 절차를 따르면서 설치가 완료된 후 각 도메인 컨트롤러의 상태에 대한 유효성을 검사할 수 있습니다. 각 배치의 설치가 완료된 후 해당 상태의 유효성을 검사할 수 있도록 도메인 컨트롤러를 합당한 크기의 배치로 배포하세요. 권장 배치 크기는 10입니다. 자세한 내용은 [가상화된 복제 도메인 컨트롤러 배포 단계](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)를 참조하십시오.

### <a name="clear-separation-of-responsibilities"></a>책임 분리 해제
가상화된 도메인 컨트롤러를 복제할 권한은 AD DS 관리자가 제어합니다. 하이퍼바이저 관리자가 가상 도메인 컨트롤러를 복사하여 추가 도메인 컨트롤러를 배포하려면 AD DS 관리자가 도메인 컨트롤러를 선택하고 권한을 부여한 후 준비 단계를 실행하여 해당 도메인 컨트롤러를 복제 원본으로 사용하도록 설정해야 합니다.

가상 컴퓨터 프로비전에 대한 권한을 부여 받은 하이퍼바이저 관리자는 AD DS 관리자가 권한을 부여하고 복제를 준비한 가상화된 도메인 컨트롤러를 복사하여 복제본 도메인 컨트롤러 가상 컴퓨터를 프로비전할 수 있습니다.

> [!WARNING]
> 가상 도메인 컨트롤러를 호스트하는 하이퍼바이저는 환경 내에서 신뢰할 수 있고 감사 받은 사람이 관리해야 합니다.

### <a name="how-does-virtual-domain-controller-cloning-work"></a>가상 도메인 컨트롤러 복제 작업 방식
복제 과정의 기존 가상 도메인 컨트롤러의 VHD (또는 좀 더 복잡 한 구성, 도메인 컨트롤러 VM에 대 한), 복사본을 만드는 AD DS에서 복제 하 고 복제 구성 파일을 만들기 위한 권한을 부여 합니다. 이 프로세스는 반복적인 배포 작업을 제거하여 복제본 가상 도메인 컨트롤러를 배포하는 데 필요한 단계를 줄이고 시간을 단축합니다.

복제 도메인 컨트롤러는 다음 조건을 사용하여 자신이 다른 도메인 컨트롤러의 복사본임을 감지합니다.

1.  가상 컴퓨터에서 제공한 VM-Generation ID 값이 DIT에 저장된 VM-Generation ID 값과 다릅니다.

    > [!NOTE]
    > 하이퍼바이저 플랫폼에서 Vm-generation ID를 지원 해야 합니다 (Windows Server 2012 Hyper-v는 Vm-generation ID 지원).

2.  DCCloneConfig.xml 파일이 다음 위치 중 하나에 있어야 합니다.

    -   DIT가 있는 디렉터리

    -   %windir%\NTDS

    -   이동식 미디어 드라이브의 루트

이러한 조건이 충족되면 자체를 복제본 도메인 컨트롤러로 프로비전하는 복제 프로세스를 진행합니다.

원본 도메인 컨트롤러 (도메인 컨트롤러 해당 복사본이 나타내는)의 보안 컨텍스트를 사용 하는 복제 도메인 컨트롤러를 (신축 단일 마스터 작업 또는 FSMO 라고도 함) Windows Server 2012 주 도메인 컨트롤러 (PDC) 에뮬레이터 작업 마스터 역할 소유자에 게 문의 하십시오. PDC 에뮬레이터에 Windows Server 2012를 실행 해야 하지만 하이퍼바이저에서 실행 될 필요는 없습니다.

> [!NOTE]
> 원본 도메인 컨트롤러를 참조하는 특성을 가진 스키마 확장이 있고 해당 특성이 복제본을 만들기 위해 복사된 개체(컴퓨터 개체, NTDS 설정 개체) 중 하나에 있는 경우에는 복제 도메인 컨트롤러를 참조하도록 특성이 복사되거나 업데이트되지 않습니다.

PDC 에뮬레이터는 요청하는 도메인 컨트롤러에 복제 권한이 있는지 확인한 후 이 컴퓨터를 복제본 도메인 컨트롤러로 식별하는 새 계정, SID, 이름 및 암호가 포함된 새 컴퓨터 ID를 만들고 이 정보를 복제본에 다시 전송합니다. 그러면 복제 도메인 컨트롤러는 복제본 역할을 할 AD DS 데이터베이스 파일을 준비하고 컴퓨터 상태를 정리합니다.

자세한 내용은 참조 [가상화 된 도메인 컨트롤러 복제 아키텍처](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)합니다.

### <a name="cloning-components"></a>복제 구성 요소
복제 구성 요소에는 Windows PowerShell용 Active Directory 모듈의 새 cmdlet 및 관련 XML 파일이 포함됩니다.

-   **New-addccloneconfigfile** "이이 cmdlet을 만들고 복제 트리거를 사용할 수 있도록를 올바른 위치에 DCCloneConfig.xml을 배치 합니다. 또한 성공적인 복제를 위해 필수 구성 요소 확인을 수행합니다. 이 cmdlet은 Windows PowerShell용 Active Directory 모듈에 포함되어 있습니다. 복제를 준비할 가상화된 도메인 컨트롤러에서 로컬로 실행하거나 -offline 옵션을 사용하여 원격으로 실행할 수 있습니다. 복제 도메인 컨트롤러에 대해 이름, 사이트 및 IP 주소와 같은 설정을 지정할 수 있습니다.

    이 cmdlet이 수행하는 필수 구성 요소 확인은 다음과 같습니다.

    > [!NOTE]
    > 필수 구성 요소 확인 없는 때 수행 되는 "오프 라인 옵션이 사용 됩니다. 자세한 내용은 [오프라인 모드에서 New-ADDCCloneConfigFile 실행](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)을 참조하십시오.

    -   준비 중인 DC에 복제 권한이 있는지 여부(즉, **Cloneable Domain Controllers** 그룹의 구성원인지 여부)

    -   PDC 에뮬레이터는 Windows Server 2012를 실행 합니다.

    -   **Get-ADDCCloningExcludedApplicationList** 를 실행하여 나열되는 모든 프로그램 또는 서비스가 CustomDCCloneAllowList.xml(이 복제 구성 요소 목록 끝에 자세히 설명되어 있음)에 포함되어 있는지 여부

-   **DCCloneConfig.xml** "가상화 된 도메인 컨트롤러를 성공적으로 복제 하려면이 파일이 있어야 DIT가 있는 디렉터리에 *%windir%\NTDS*, 또는 이동식 미디어 드라이브의 루트입니다. 이 파일은 복제를 감지하고 초기화하는 트리거 중 하나로 사용될 뿐 아니라 복제 도메인 컨트롤러에 대한 구성 설정을 지정하는 수단을 제공합니다.

    스키마와 DCCloneConfig.xml 파일에 대 한 샘플 파일에서 모든 Windows Server 2012 컴퓨터에 저장 됩니다.

    -   %windir%\system32\DCCloneConfigSchema.xsd

    -   %windir%\system32\SampleDCCloneConfig.xml

    New-ADDCCloneConfigFile cmdlet을 사용하여 DCCloneConfig.xml 파일을 만드는 것이 좋습니다. XML 인식 편집기에서 스키마 파일을 사용하여 이 파일을 만들 수도 있지만 파일을 수동으로 편집하면 오류가 발생할 가능성이 높아집니다. 파일을 편집할 경우 메모장을 사용하지 말고 Visual Studio, [XML Notepad](https://www.microsoft.com/download/details.aspx?displaylang=en&id=7973)또는 타사 응용 프로그램과 같은 XML 인식 편집기를 사용하여 작업을 수행해야 합니다.

-   **Get-addccloningexcludedapplicationlist** "기본 지원 목록 (DefaultDCCloneAllowList.xml)에 있는 서비스 또는 설치 된 프로그램을 확인 하려면 복제 프로세스를 시작 하기 전에 원본 도메인 컨트롤러에서이 cmdlet을 실행 또는 사용자 정의 포함 customdccloneallowlist.xml을 나열 하 고 있으므로 평가 하지 못한 복제 영향입니다.

    이 cmdlet은 원본 도메인 컨트롤러에서 기본 목록(DefaultDCCloneAllowList.xml)에 지정되어 있지 않거나, 제공된 경우 사용자 정의 포함 목록(CustomDCCloneAllowList.xml 파일)에 지정되어 있지 않은 서비스 제어 관리자의 서비스 및 **HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall** 아래에 나열된 설치된 프로그램을 검색합니다. 이 cmdlet을 실행한 경우 DefaultDCCloneAllowList.xml 또는 CustomDCCloneAllowList.xml 파일에 이미 제공된 목록 중 원본 DC에 설치된 항목을 기반으로 런타임 시 구성된 목록에 없는 응용 프로그램 및 서비스 목록이 반환됩니다. 서비스 및 프로그램을 안전하게 복제할 수 있는 것으로 확인한 경우 Get-ADDCCloningExcludedApplicationList의 서비스 및 프로그램 출력을 CustomDCCloneAllowList.xml 파일에 추가할 수 있습니다. 서비스 또는 설치된 프로그램을 안전하게 복제할 수 있는지 확인하려면 다음 조건을 평가하세요.

    -   서비스 또는 설치된 프로그램이 이름, SID, 암호 등과 같은 컴퓨터 ID의 영향을 받습니까?

    -   서비스 또는 설치된 프로그램이 복제본에서 해당 기능에 영향을 줄 수 있는 상태를 컴퓨터에 로컬로 저장합니까?

    응용 프로그램의 소프트웨어 공급업체와 함께 서비스 또는 프로그램을 안전하게 복제할 수 있는지 확인해야 합니다.

    > [!NOTE]
    > CustomDCCloneAllowList.xml 파일에서 추가 서비스 또는 프로그램을 프로비전하기 전에 가상 컴퓨터에 포함된 해당 소프트웨어를 복사하는 데 필요한 라이선스가 있는지 확인하세요.

    응용 프로그램이 복제 가능하지 않은 경우 복제 미디어를 만들기 전에 원본 도메인 컨트롤러에서 해당 응용 프로그램을 제거하세요. 응용 프로그램이 cmdlet 출력에 나타나지만 CustomDCCloneAllowList.xml 파일에 포함되어 있지 않으면 복제에 실패합니다. 복제에 성공하려면 cmdlet 출력에 어떤 서비스나 프로그램도 나열되어서는 안 됩니다. 즉, 응용 프로그램이 CustomDCCloneAllowList.xml 파일에 포함되어 있거나, 그렇지 않은 경우 원본 도메인 컨트롤러에서 제거되어야 합니다.

    다음 표에서는 Get-ADDCCloningExcludedApplicationList를 실행하는 옵션을 설명합니다.

    |||
    |-|-|
    |인수|설명|
    |*<no argument specified>*|복제 대상으로 고려되지 않은 서비스 또는 프로그램 목록을 콘솔에 표시합니다. 허용되는 위치 중 하나에 CustomDCCloneAllowList.XML이 이미 있는 경우 이 파일을 사용하여 나머지 서비스 및 프로그램을 표시합니다(목록이 일치하는 경우 나머지 서비스 및 프로그램이 없을 수도 있음).|
    |-GenerateXml|콘솔에 나열된 서비스 및 프로그램으로 채워진 CustomDCCloneAllowList.XML 파일을 만듭니다.|
    |-Force|기존 CustomDCCloneAllowList.XML 파일을 덮어씁니다.|
    |-Path|CustomDCCloneAllowList.XML을 만들 폴더 경로입니다.|

-   **DefaultDCCloneAllowList.xml** "이이 파일은 모든 Windows에 기본적으로 Server 2012 도메인 컨트롤러 in the *%windir%\system32*입니다. 기본적으로 안전하게 복제할 수 있는 서비스 및 설치된 프로그램을 나열합니다. 이 파일의 위치나 내용을 변경해서는 안 됩니다. 그렇지 않으면 복제에 실패합니다.

-   **CustomDCCloneAllowList.xml** "서비스 또는 DefaultDCCloneAllowList.xml 파일에 나열 된 외부에 있는 원본 도메인 컨트롤러에 상주 하는 설치 된 프로그램이 있으면 해당 서비스 및 프로그램 포함 되어야 합니다이 파일에. DefaultDCCloneAllowList.xml 파일에 나열되지 않은 서비스 또는 설치된 프로그램을 찾으려면 **Get-ADDCCloningExcludedApplicationList** cmdlet을 실행합니다. 이 방법을 사용할지는 **"GenerateXml** XML 파일을 생성 하는 인수입니다.

    복제 프로세스에서는 다음 위치를 순서대로 확인하여 이 파일을 찾으며, 다른 폴더의 내용에 관계없이 맨 처음 찾은 XML 파일을 사용합니다.

    1.  다음 레지스트리 키

        ```
        HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters
        AllowListFolder (REG_SZ)
        ```

    2.  DSA 작업 디렉터리

    3.  %systemroot%\NTDS

    4.  드라이브의 루트에서 시작하여 드라이브 문자 순의 이동식 읽기/쓰기 미디어

### <a name="deployment-scenarios"></a>배포 시나리오
가상 도메인 컨트롤러 복제에 지원되는 배포 시나리오는 다음과 같습니다.

-   원본 도메인 컨트롤러의 가상 하드 디스크 (vhd) 파일의 복사본을 만들어 여는 복제 도메인 컨트롤러를 배포 합니다.

-   하이퍼바이저에서 표시하는 내보내기/가져오기 의미 체계를 사용해 원본 도메인 컨트롤러의 가상 컴퓨터를 복사하여 복제 도메인 컨트롤러를 배포합니다.

> [!NOTE]
> 섹션의 단계 [복제 가상화 된 도메인 컨트롤러 배포 단계](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc) 의 Windows Server 2012 Hyper-v의 내보내기/가져오기 기능을 사용 하 여 가상 컴퓨터를 복사를 보여 줍니다.

## <a name="steps_deploy_vdc"></a>복제 가상화 된 도메인 컨트롤러를 배포 하는 단계

-   [필수 구성 요소](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#prerequisites)

-   [1단계: 원본 가상화 된 도메인 컨트롤러 복제 권한 부여](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk4_grant_source)

-   [2단계: Get-addccloningexcludedapplicationlist cmdlet 실행](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet)

-   [3 단계: New-addccloneconfigfile 실행](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk5_create_insert_dccloneconfig)

-   [4 단계: 내보내기 및 다음 원본 도메인 컨트롤러의 가상 컴퓨터 가져오기](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk7_export_import_vm_sourcedc)

### <a name="prerequisites"></a>필수 구성 요소

-   다음 절차의 단계를 완료하려면 Domain Admins 그룹의 구성원이거나 이 그룹에 할당된 상응하는 사용 권한이 있어야 합니다.

-   이 가이드에서 사용 하는 Windows PowerShell 명령은 관리자 권한 명령 프롬프트에서 실행 되어야 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 하 고 **Windows PowerShell** 아이콘을 클릭 한 다음 **관리자 권한으로 실행**합니다.

-   Hyper-v 서버 역할이 설치 된 Windows Server 2012 서버 (**HyperV1**).

-   Hyper-v 서버 역할이 설치 된 두 번째 Windows Server 2012 서버 (**HyperV2**).

    > [!NOTE]
    > -   다른 하이퍼바이저를 사용하는 경우 해당 하이퍼바이저의 공급업체에 문의하여 하이퍼바이저가 VM-Generation ID를 지원하는지 확인해야 합니다. 하이퍼바이저가 VM-Generation ID를 지원하지 않는 경우 DCCloneConfig.xml을 제공하면 새 VM이 DSRM(디렉터리 서비스 복원 모드)으로 부팅됩니다.
    > -   AD DS 서비스의 가용성을 높이기 위해 이 가이드에서는 두 개의 서로 다른 Hyper-V 호스트를 사용하도록 권장하고 사용 방법에 대한 지침을 제공합니다. 두 개의 서로 다른 Hyper-V 호스트를 사용하면 잠재적으로 단일 실패 지점을 방지하는 데 도움이 됩니다. 그러나 가상 도메인 컨트롤러 복제를 수행하는 데에는 두 개의 Hyper-V 호스트가 필요하지 않습니다.
    > -   각 Hyper-V 서버(**HyperV1** 및 **HyperV2**)에서 로컬 관리자 그룹의 구성원이어야 합니다.
    > -   Hyper-V를 사용하여 VHD 파일을 가져오고 내보내려면 두 Hyper-V 호스트에서 가상 네트워크 스위치의 이름이 같아야 합니다. 예를 들어 **HyperV1**에 VNet이라는 가상 네트워크 스위치가 있는 경우 **HyperV2**에도 VNet이라는 가상 네트워크 스위치가 있어야 합니다.
    > -   두 Hyper-V 호스트(**HyperV1** 및 **HyperV2**)의 프로세서가 서로 다른 경우 내보내려는 가상 컴퓨터(**VirtualDC1**)를 종료하고 VM을 마우스 오른쪽 단축한 다음 **설정**, **프로세스**를 차례로 클릭합니다. 그런 다음 **프로세서 호환성**에서 **다른 프로세서 버전을 사용하는 물리적 컴퓨터로 마이그레이션**을 선택하고 **확인**을 클릭합니다.

-   배포 된 Windows Server 2012 도메인 컨트롤러 (가상 또는 실제) PDC 에뮬레이터 역할을 호스팅하는 (**DC1**). PDC 에뮬레이터 역할이 Windows Server 2012 도메인 컨트롤러에서 호스팅되는 여부를 확인 하려면 다음 Windows PowerShell 명령을 실행 합니다.

    ```
    Get-ADComputer (Get-ADDomainController "Discover "Service "PrimaryDC").name "Property operatingsystemversion | fl
    ```

    OperatingSystemVersion 값이 버전 6.2로 반환되어야 합니다. 필요한 경우에 Windows Server 2012를 실행 하는 도메인 컨트롤러에 PDC 에뮬레이터 역할을 전송할 수 있습니다. 자세한 내용은 [Ntdsutil.exe를 사용하여 FSMO 역할을 점유하거나 도메인 컨트롤러에 전송](https://support.microsoft.com/kb/255504)을 참조하세요.

-   배포 된 Windows Server 2012 게스트 가상화 된 도메인 컨트롤러 (**VirtualDC1**) PDC 에뮬레이터 역할을 호스팅하는 Windows Server 2012 도메인 컨트롤러와 동일한 도메인에는 (**DC1**). 이 도메인 컨트롤러가 복제에 사용되는 원본 도메인 컨트롤러가 됩니다. 게스트 가상 도메인 컨트롤러는 Windows Server 2012 Hyper-v 서버에서 호스트 됩니다 (**HyperV1**).

    > [!NOTE]
    > -   복제에 성공하려면 복제본을 만드는 데 사용되는 원본 도메인 컨트롤러가 원본 VHD 미디어가 만들어진 이후에 강등된 DC가 아니어야 합니다.
    > -   VM 또는 해당 VHD를 복사하기 전에 원본 도메인 컨트롤러를 종료합니다.
    > -   VHD를 복제하거나 삭제 표시 기간 값(또는 Active Directory 휴지통을 사용하는 경우 삭제된 개체 기간 값)보다 오래된 스냅숏을 복원해서는 안 됩니다. 기존 도메인 컨트롤러의 VHD를 복사할 경우 VHD 파일이 삭제 표시 기간 값(기본적으로 60일)보다 오래되지 않았는지 확인하세요. 실행 중인 도메인 컨트롤러의 VHD를 복사하여 복제 미디어를 만들어서는 안 됩니다.

    원본 DC에 있는 모든 VFD(가상 플로피 디스크)를 꺼냅니다. 이러한 디스크는 새 VM을 가져오려고 할 때 공유 문제를 일으킬 수 있습니다.

    Windows Server 2012 도메인 컨트롤러에만 VM-생성 Id 하이퍼바이저에서 호스트를 복제에 대 한 원본으로 사용할 수 있습니다. 복제에 사용 되는 원본 Windows Server 2012 도메인 컨트롤러는 정상 상태에 있어야 합니다. 원본 도메인 컨트롤러의 상태를 확인하려면 [dcdiag](https://technet.microsoft.com/library/cc731968(WS.10).aspx)를 실행합니다. Dcdiag에서 반환 되는 출력을 보다 잘 이해을 확보 하려면 참조 [DCDIAG를 실제로 수행... 수행?](http://blogs.technet.com/b/askds/archive/2011/03/22/what-does-dcdiag-actually-do.aspx)합니다.

    원본 도메인 컨트롤러가 DNS 서버인 경우에는 복제된 도메인 컨트롤러도 DNS 서버가 됩니다. Active Directory 통합 영역만 호스트하는 DNS 서버를 선택해야 합니다.

    DNS 클라이언트 설정은 복제되는 것이 아니라 DCCloneConfig.xml 파일에 지정됩니다. 이 설정이 지정되지 않으면 복제된 도메인 컨트롤러에서 기본적으로 자체를 기본 설정 DNS 서버로 가리킵니다. 복제된 도메인 컨트롤러에는 DNS 대상이 없습니다. 부모 DNS 영역의 관리자는 필요에 따라 복제된 도메인 컨트롤러에 대한 DNS 위임을 업데이트해야 합니다.

    > [!WARNING]
    > 가상화 보호 기능은 AD LDS(Active Directory Lightweight Directory Services)로 확장되지 않습니다. 따라서 이 AD LDS 인스턴스를 CustomDCCloneAllowList.xml에 추가하여 AD LDS 인스턴스를 호스트하는 AD DS 도메인 컨트롤러를 복제하려고 해서는 안 됩니다. AD LDS는 VM-Generation ID를 인식하지 않으므로 AD LDS가 있는 도메인 컨트롤러를 복제할 경우 해당 AD LDS 구성 집합에서 USN 롤백으로 인한 불일치가 발생할 수 있습니다.

    다음 서버 역할은 복제에 지원되지 않습니다.

    -   DHCP(동적 호스트 구성 프로토콜)

    -   AD CS(Active Directory 인증서 서비스)

    -   AD LDS(Active Directory Lightweight Directory Services)

### <a name="bkmk4_grant_source"></a>1 단계: 가상화된 도메인 컨트롤러에 복제 권한 부여
이 절차에서는 **Active Directory 관리 센터**를 사용하여 **Cloneable Domain Controllers** 그룹에 원본 도메인 컨트롤러를 추가하는 방식으로 원본 도메인 컨트롤러에 복제 권한을 부여합니다.

##### <a name="to-grant-the-source-virtualized-domain-controller-the-permission-to-be-cloned"></a>가상화된 원본 도메인 컨트롤러에 복제 권한을 부여하려면

1.  복제를 준비 중인 도메인 컨트롤러(**VirtualDC1**)와 동일한 도메인에 있는 도메인 컨트롤러에서 ADAC( **Active Directory 관리 센터** )를 열고 가상화된 도메인 컨트롤러 개체(도메인 컨트롤러는 일반적으로 ADAC의 **Domain Controllers** 컨테이너 아래에 있음)를 찾아 마우스 오른쪽 단추로 클릭한 후 **그룹에 추가** 를 선택하고 **선택할 개체 이름을 입력하세요** 아래에 **Cloneable Domain Controllers** 를 입력한 다음 **확인**을 클릭합니다.

    복제를 수행하려면 먼저 이 단계에서 수행한 그룹 등록을 PDC 에뮬레이터에 복제해야 합니다. 하는 경우는 **복제 가능 도메인 컨트롤러** 그룹을 찾을 수 없습니다, Windows Server 2012를 실행 하는 도메인 컨트롤러에 PDC 에뮬레이터 역할을 호스팅할 수 있습니다.

    > [!NOTE]
    > Windows Server 2012 도메인 컨트롤러에서 ADAC를 열려면 유형 및 Windows PowerShell을 열고 **dsac.exe**합니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *

다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다.


    Add-ADGroupMember "Identity "CN=Cloneable Domain Controllers,CN=Users, DC=Fabrikam,DC=Com" "Member "CN=VirtualDC1,OU=Domain Controllers,DC=Fabrikam,DC=com"


### <a name="bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet"></a>2 단계: Get-ADDCCloningExcludedApplicationList cmdlet 실행
이 절차에서는 가상화된 원본 도메인 컨트롤러에서 `Get-ADDCCloningExcludedApplicationList` cmdlet을 실행하여 복제에 대해 평가되지 않은 프로그램 또는 서비스를 식별합니다. New-ADDCCloneConfigFile cmdlet은 제외된 응용 프로그램을 감지한 경우 DCCloneConfig.xml 파일을 만들지 않으므로 New-ADDCCloneConfigFile cmdlet을 실행하기 전에 Get-ADDCCloningExcludedApplicationList cmdlet을 실행해야 합니다.

##### <a name="to-identify-applications-or-services-that-run-on-a-source-domain-controller-which-have-not-been-evaluated-for-cloning"></a>복제에 대해 평가되지 않은 원본 도메인 컨트롤러에서 실행되는 응용 프로그램 또는 서비스를 식별하려면

1.  원본 도메인 컨트롤러(**VirtualDC1**)에서 **서버 관리자**, **도구**, **Windows PowerShell용 Active Directory 모듈**을 차례로 클릭하고 다음 명령을 입력합니다.


    Get-addccloningexcludedapplicationlist


2.  소프트웨어 공급업체와 함께 반환된 서비스 및 설치된 프로그램 목록을 검사하여 안전하게 복제할 수 있는지 확인합니다. 목록의 응용 프로그램 또는 서비스를 안전하게 복제할 수 없는 경우 원본 도메인 컨트롤러에서 제거해야 합니다. 그렇지 않으면 복제에 실패합니다.

3.  서비스와 안전 하 게 복제할 결정 된 설치 된 프로그램 집합에서 사용 하 여 다시 명령을 실행 하는 **"GenerateXML** 이러한 프로 비전 하는 스위치 서비스 및 프로그램을 **CustomDCCloneAllowList.xml** 파일입니다.


    Get-addccloningexcludedapplicationlist GenerateXml


### <a name="bkmk5_create_insert_dccloneconfig"></a>3 단계: New-ADDCCloneConfigFile 실행
원본 도메인 컨트롤러에서 New-ADDCCloneConfigFile을 실행하고, 선택적으로 복제 도메인 컨트롤러에 대한 구성 설정(예: 이름, IP 주소 및 DNS 확인자)을 지정합니다.

예를 들어 정적 IPv4 주소를 사용하는 VirtualDC2라는 복제 도메인 컨트롤러를 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile "Static -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.255.0" -CloneComputerName "VirtualDC2" -IPv4DefaultGateway "10.0.0.3" -SiteName "REDMOND"

> [!NOTE]
> 복제 도메인 컨트롤러는 DCCloneConfig.xml 파일에서 다른 사이트를 지정하지 않는 한 원본 도메인 컨트롤러와 같은 사이트에 배치됩니다. DCCloneConfig.xml 파일에서 IP 주소를 기반으로 복제 도메인 컨트롤러에 적절한 사이트를 지정하는 것이 좋습니다.

컴퓨터 이름은 선택 사항입니다. 컴퓨터 이름을 지정하지 않으면 다음 알고리즘에 따라 고유한 이름이 생성됩니다.

-   접두사는 원본 도메인 컨트롤러 컴퓨터 이름의 처음 8자입니다. 예를 들어 SourceComputer라는 원본 컴퓨터 이름은 SourceCo라는 접두사 문자열로 잘립니다.

-   서식의 고유한 이름 접미사 "" CL*nnnn*"접두사 문자열에 추가 됩니다 여기서 *nnnn* 0001에서 9999 사이의 PDC 현재 사용 중인 결정 하는 다음 사용 가능한 값입니다. 예를 들어 위 예의 컴퓨터 이름 접두사 SourceCo를 사용할 경우 허용된 범위에서 다음에 사용 가능한 숫자가 0047이면 복제 컴퓨터에 사용할 파생된 이름은 SourceCo-CL0047로 설정됩니다.

> [!NOTE]
> New-ADDCCloneConfigFile cmdlet이 제대로 작동하려면 GC(글로벌 카탈로그) 서버가 필요합니다. 원본 도메인 컨트롤러의 멤버 자격에는 **복제 가능 도메인 컨트롤러** 그룹 GC에 반영 되어야 합니다. GC는 PDC 에뮬레이터와 같은 도메인 컨트롤러일 필요는 없지만 같은 사이트에 있는 것이 좋습니다. GC를 사용할 수 없는 경우 명령이 실패 오류가 발생 하 여 "서버가 작동 하지 않습니다." 자세한 내용은 참조 [가상화 된 도메인 컨트롤러 문제 해결](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)합니다.

정적 IPv4 설정을 사용하는 Clone1이라는 복제 도메인 컨트롤러를 만들고 기본 설정 및 대체 WINS 서버를 지정하려면 다음을 입력합니다.


    New-ADDCCloneConfigFile "CloneComputerName "Clone1" "Static -IPv4Address "10.0.0.5" "IPv4DNSResolver "10.0.0.1" "IPv4SubnetMask "255.255.0.0" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


> [!NOTE]
> 둘 다 지정 해야 WINS 서버를 지정 하면 **"PreferredWINSServer** 및 **" AlternateWINSServer**합니다. 두 인수 중 하나만 지정하면 복제에 실패하고 dcpromo.log에 오류 코드 0x80041005가 표시됩니다.

동적 IPv4 설정을 사용하는 Clone2라는 복제 도메인 컨트롤러를 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" 


> [!NOTE]
> 이 경우 복제본이 IP 주소 및 기타 관련 네트워크 설정을 가져올 수 있는 환경에 DHCP 서버가 있어야 합니다.

동적 IPv4 설정을 사용하는 Clone2라는 복제 도메인 컨트롤러를 만들고 기본 설정 및 대체 WINS 서버를 지정하려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" -SiteName "REDMOND" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


동적 IPv6 설정을 사용하는 복제 도메인 컨트롤러를 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


정적 IPv6 설정을 사용하는 복제 도메인 컨트롤러를 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile "Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


> [!NOTE]
> 정적 및 동적 설정 간의 유일한 차이점은 포함 IPv6 설정을 지정할 때 **-정적** 전환 합니다. 포함 된 **-정적** 스위치를 사용 하면 하나 이상을 지정 하기 위한 필수 사항이 **IPv6DNSResolver**합니다. 정적 IPv6 주소는 라우터에서 할당 된 접두사가 있는 상태 비저장 주소 자동 구성 여 SLAAC ()를 통해 구성 해야 합니다. 동적 i p v 6을 DNS 확인자는 선택적 이지만 복제본이 IPv6 주소 및 DNS 구성 정보를 얻으려면 서브넷에는 IPv6 지원 DHCP 서버를 연결할 수 있는 것으로 예상 합니다.

#### <a name="BKMK_OfflineMode"></a>오프 라인 모드에서 New-addccloneconfigfile 실행
복제 준비된(원본 도메인 컨트롤러에 대한 복제 권한이 부여되고, Get-ADDCCloningExcludedApplicationList cmdlet이 실행되었으며 기타 작업이 수행된 상황을 의미함) 원본 도메인 컨트롤러의 복사본이 여러 개인 경우 미디어의 각 복사본에 대해 서로 다른 설정을 지정하려면 New-ADDCCloneConfigFile을 오프라인 모드에서 실행하면 됩니다. 이는 각 복사본을 가져오는 등의 방법으로 각 VM을 개별적으로 준비하는 것보다 효율적일 수 있습니다.

이 경우 도메인 관리자가 오프 라인 디스크를 탑재를 원격 서버 관리 도구 (RSAT) New-addccloneconfigfile cmdlet을 실행 하려면-offline 인수를 Windows Server 2012에 포함 된 새 Windows PowerShell 옵션을 사용 하 여 팩터리 같은 자동화할 수 있는 XML 파일을 추가 하기 위해 합니다. 오프라인 모드에서 New-ADDCCloneConfigFile cmdlet을 실행하기 위해 오프라인 디스크를 탑재하는 방법에 대한 자세한 내용은 [오프라인 시스템 디스크에 XML 추가](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_Offline)를 참조하십시오.

먼저 원본 미디어에서 로컬로 cmdlet을 실행하여 필수 구성 요소 확인을 통과하는지 확인합니다. 이 cmdlet은 같은 도메인에 없는 컴퓨터 또는 도메인에 가입된 컴퓨터에서 실행될 수 있으므로 필수 구성 요소 확인은 오프라인 모드에서 수행되지 않습니다. cmdlet을 로컬로 실행하면 DCCloneConfig.xml 파일이 만들어집니다. 이후에도 계속 오프라인 모드를 사용하려는 경우 로컬로 만들어진 DCCloneConfig.xml을 삭제할 수 있습니다.

복제 도메인 컨트롤러를 만들고 이라는 CloneDC1 REDMOND 이라고 하는 사이트의 오프 라인 모드에서는 "정적 IPv4 주소, 유형:


    New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS


정적 IPv4 및 정적 IPv6 설정을 사용하는 Clone2라는 복제 도메인 컨트롤러를 오프라인 모드에서 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS


정적 IPv4 및 동적 IPv6 설정을 사용하는 복제 도메인 컨트롤러를 오프라인 모드에서 만들고 DNS 확인자 설정에 대해 여러 DNS 서버를 지정하려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS 


동적 IPv4 및 정적 IPv6 설정을 사용하는 Clone1라는 복제 도메인 컨트롤러를 오프라인 모드에서 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS


동적 IPv4 및 동적 IPv6 설정을 사용하는 복제 도메인 컨트롤러를 오프라인 모드에서 만들려면 다음을 입력합니다.


    New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS


### <a name="bkmk7_export_import_vm_sourcedc"></a>4 단계: 원본 도메인 컨트롤러의 가상 컴퓨터를 내보낸 다음 가져오기
이 절차에서는 가상화된 원본 도메인 컨트롤러의 가상 컴퓨터를 내보낸 다음 해당 가상 컴퓨터를 가져옵니다. 이 작업에서는 가상화된 복제 도메인 컨트롤러가 도메인에 만들어집니다.

각 Hyper-V 호스트에서 로컬 관리자 그룹의 구성원이어야 합니다. 각 서버에 서로 다른 자격 증명을 사용하는 경우 Windows PowerShell cmdlet을 실행하여 VM을 내보내고 여러 Windows PowerShell 세션에서 가져옵니다.

원본 도메인 컨트롤러에 스냅숏이 있는 경우 원본 도메인 컨트롤러를 내보내기 전에 이러한 스냅숏을 삭제해야 합니다. 스냅숏에 대상 Hyper-V 호스트와 호환되지 않는 프로세서 설정이 있는 경우 VM에서 가져오지 않기 때문입니다. 프로세서 설정이 원본 및 대상 Hyper-V 호스트 간에 호환되는 경우에는 스냅숏을 미리 삭제하지 않고도 원본을 내보내고 복사할 수 있습니다. 그러나 가져온 후 복제 VM을 시작하기 전에 스냅숏을 삭제해야 합니다.

##### <a name="to-copy-a-virtual-domain-controller-by-exporting-and-then-importing-the-virtualized-source-domain-controller"></a>가상화된 원본 도메인 컨트롤러를 내보낸 다음 가져오는 방식으로 가상 도메인 컨트롤러를 복사하려면

1.  **HyperV1**에서 원본 도메인 컨트롤러(**VirtualDC1**)를 종료합니다.

    ![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *

    STOP-VM-VirtualDC1-ComputerName HyperV1 이름 지정


2.  **HyperV1**에서 스냅숏을 삭제한 다음 원본 도메인 컨트롤러(VirtualDC1)를 c:\CloneDCs 디렉터리로 내보냅니다.

> [!NOTE]
> 스냅숏이 만들어질 때마다 차이점 보관용 디스크 역할을 하는 새 AVHD 파일이 만들어지므로 연결된 모든 스냅숏을 삭제해야 합니다. 이는 체인 효과를 만듭니다. 스냅숏을 만들고 DCCLoneConfig.xml 파일을 VHD에 삽입하면 더 이상 이전 버전의 DIT에서 복제본이 만들어지거나 잘못된 VHD 파일에 구성 파일이 삽입되는 일이 없어집니다. 스냅숏을 삭제하면 이러한 AVHD가 모두 기본 VHD에 병합됩니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *


    Get-VMSnapshot VirtualDC1 | Remove-VMSnapshot -IncludeAllChildSnapshots
    Export-VM -Name VirtualDC1 -ComputerName HyperV1 -Path c:\CloneDCs\VirtualDC1


3.  **virtualdc1** 폴더를 **HyperV2**의 c:\Import 디렉터리에 복사합니다.

4.  **HyperV2**에서 **Hyper-V 관리자**를 사용하여 **c:\Import\virtualdc1** 폴더에서 가상 컴퓨터를 가져오고( **Hyper-V 관리자**의 **가상 컴퓨터 가져오기** 마법사 사용) 연결된 모든 **스냅숏**을 삭제합니다.

가상 컴퓨터를 가져올 때 **가상 컴퓨터 복사(새로운 고유 ID 만들기)** 옵션을 사용합니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *

    $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Machines"
    $vm = Import-VM -Path $path.fullname -Copy -GenerateNewId
    Rename-VM $vm VirtualDC2


같은 원본 도메인 컨트롤러에서 여러 복제 도메인 컨트롤러를 만들려면

  -   UI: **가상 컴퓨터 가져오기** 마법사에서 **가상 컴퓨터 구성 폴더**, **스냅숏 저장소**, **스마트 페이징 폴더**및 가상 컴퓨터용 가상 하드 디스크의 다른 **위치** 에 대한 새 위치를 지정합니다.

  -   Windows PowerShell:에 대 한 다음 매개 변수를 사용 하 여 가상 컴퓨터에 대 한 새 위치를 지정 하는 `Import-VM` cmdlet:

        $path Get-childitem "컴퓨터 C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual" IMPORT-VM =-경로 $path.fullname-복사-GenerateNewId-ComputerName HyperV2-VhdDestinationPath "path"-SnapshotFilePath "path"-SmartPagingFilePath "path"-VirtualMachinePath "경로"


> [!NOTE]
> 여러 복제 도메인 컨트롤러를 동시에 만드는 데 권장되는 배치 크기는 10입니다. 최대 개수는 최대 아웃바운드 복제 연결 수에 의해 제한되며, 기본적으로 DFSR(분산 파일 시스템 복제)의 경우 16개, FRS(파일 복제 서비스)의 경우 10개입니다. 환경에서 해당 개수를 철저히 테스트하지 않은 경우 권장 개수보다 많은 복제 도메인 컨트롤러를 동시에 배포해서는 안 됩니다.

5.  **HyperV1**에서 원본 도메인 컨트롤러(**(VirtualDC1**)를 다시 시작하여 온라인 상태로 다시 전환합니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *

    Start-VM -Name VirtualDC1 -ComputerName HyperV1


6.  **HyperV2**에서 가상 컴퓨터(**VirtualDC2**)를 시작하여 도메인의 복제 도메인 컨트롤러로 다시 온라인 상태로 전환합니다.

![AD DS 소개 (영문)](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *


    Start-VM -Name VirtualDC2 -ComputerName HyperV2

> [!NOTE]
> 복제에 성공하려면 PDC 에뮬레이터를 실행해야 합니다. PDC 에뮬레이터가 종료된 경우 PDC 에뮬레이터 역할을 소유하고 있음을 인식하도록 PDC 에뮬레이터를 시작하고 초기 동기화를 수행했는지 확인합니다. 자세한 내용은 Microsoft [기술 자료 문서 305476](https://support.microsoft.com/kb/305476)을 참조하세요.

복제가 완료되면 복제 컴퓨터의 이름을 확인하여 복제 작업에 성공했는지 확인합니다. VM이 DSRM(디렉터리 서비스 복원 모드)으로 시작되지 않았는지 확인합니다. 로그온 시 사용 가능한 로그온 서버가 없음을 나타내는 오류가 발생하는 경우 DSRM에서 로그온해 보세요. DC가 제대로 복제되지 않았으며 DSRM으로 부팅된 경우 이벤트 뷰어의 로그 및 %systemroot%/debug 폴더의 dcpromo 로그를 확인하세요.

복제된 도메인 컨트롤러는 원본 도메인 컨트롤러의 구성원 자격을 복사하므로 **Cloneable Domain Controllers** 그룹의 구성원이 됩니다. 하나의 모범 사례로서, 복제 작업을 수행할 준비가 될 때까지 **Cloneable Domain Controllers** 그룹을 빈 상태로 두고 복제 작업이 완료된 후 구성원을 제거해야 합니다.

원본 도메인 컨트롤러가 백업 미디어를 저장하는 경우 복제된 도메인 컨트롤러도 백업 미디어를 저장합니다. `wbadmin get versions` 를 실행하여 복제된 도메인 컨트롤러에서 백업 미디어를 표시할 수 있습니다. Domain Admins 그룹의 구성원은 복제된 도메인 컨트롤러에서 백업 미디어를 삭제하여 실수로 복원되지 않도록 해야 합니다. Wbadmin.exe를 사용 하 여 시스템 상태 백업을 삭제 하는 방법에 대 한 자세한 내용은 참조 [Wbadmin delete systemstatebackup](https://technet.microsoft.com/library/cc742081(v=WS.10).aspx)합니다.

## <a name="troubleshooting"></a>문제 해결
복제 도메인 컨트롤러(**VirtualDC2**)는 DSRM(디렉터리 서비스 복원 모드)으로 시작된 경우 다음 재부팅 시 자동으로 표준 모드로 돌아가지 않습니다. DSRM으로 시작된 도메인 컨트롤러에 로그온하려면 **.\Administrator** 를 사용하고 DSRM 암호를 지정하세요.

복제 실패의 원인을 해결하고 dcpromo.log가 복제를 다시 시도할 수 없음을 나타내지 않는지 확인해야 합니다. 복제를 다시 시도할 수 없는 경우 미디어를 안전하게 삭제합니다. 복제를 다시 시도할 수 있는 경우 복제를 다시 시도하려면 DS 복원 모드 부팅 플래그를 제거해야 합니다.

1.  관리자 권한 명령 (오른쪽 Windows Server 2012를 클릭 하 고 관리자 권한으로 실행 선택), 및를 입력 한 후 Windows Server 2012 열기 **msconfig**합니다.

2.  **부팅** 탭의 **부팅 옵션**에서 **안전 부팅** ( **Active Directory 복구 사용**옵션이 이미 선택되어 있는 경우)을 선택 취소합니다.

3.  **확인** 을 클릭하고 메시지가 나타나면 다시 시작합니다.

가상화된 도메인 컨트롤러에 대한 추가 문제 해결 정보는 [가상화된 도메인 컨트롤러 문제 해결](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)을 참조하십시오.


