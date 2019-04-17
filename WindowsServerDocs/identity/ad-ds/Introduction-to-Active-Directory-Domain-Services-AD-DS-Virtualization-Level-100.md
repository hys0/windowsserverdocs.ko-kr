---
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
title: "(AD DS) Active Directory Domain Services Virtualization (수준을 100) 소개"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3c7fdc2e20bc4a27f2555af54f396a15f664d6c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100"></a>(AD DS) Active Directory Domain Services Virtualization (수준을 100) 소개

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다양 한 년에 대 한 Active Directory Domain Services (AD DS) 환경의 virtualization 지속적인 했습니다. Windows Server 2012 부터는 AD DS virtualization 안전 하 게 보호 기능을 소개 하 고 사용 복제 통해 가상 도메인 컨트롤러의 신속한 배포 도메인 컨트롤러 가상화에 대 한 향상 된 지원을 제공 합니다. 이러한 새로운 virtualization 기능 공개 하 게 비밀로 구름에 대 한 향상 된 지원을 제공, 하이브리드 환경 AD DS 일부는 온-프레미스 있을 경우와 클라우드와 AD DS 인프라 완전히 거주 하는 온-프레미스 합니다.

**이 문서에서**

-   [도메인 컨트롤러의 안전 virtualization](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#safe_virt_dc)

-   [가상화 도메인 컨트롤러 복제](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#virtualized_dc_cloning)

-   [배포 복제 가상화 도메인 컨트롤러 단계](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)

-   [문제 해결](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#troubleshooting)

## <a name="safe_virt_dc"></a>도메인 컨트롤러의 안전 virtualization
가상 환경을 고유한 과제 논리 시계 기반 복제 구성표를에 따라 달라 분산된 작업을 표시 합니다. 예를 들어, AD DS 복제 각 도메인 컨트롤러에서 거래에 할당 (USN 또는 업데이트 시퀀스 번호가 라고 함) 단순하게 증가 값을 사용 합니다. 각 도메인 컨트롤러의 데이터베이스 인스턴스도는 InvocationID 이라고 id는 제공 합니다. 도메인 컨트롤러의 InvocationID 및 해당 USN 함께 역할 모든 쓰기 트랜잭션와 관련 된 고유 식별자 각 도메인 컨트롤러에서 수행 하 고 숲 내 고유 해야 합니다.

AD DS 복제 다른 도메인 컨트롤러에 복제 해야 하는 변경 내용을 확인 하려면 각 도메인 컨트롤러에서 InvocationID 및 Usn를 사용 합니다. 도메인 컨트롤러 롤백됩니다 도메인 컨트롤러의 인식 외 시간에는 완전히 다른 거래에 대 한 USN를 다시 사용 하는 경우 다른 도메인 컨트롤러 다시 사용된 USN 해당 InvocationID 컨텍스트가 아래와 관련 된 업데이트 이미 받은 생각 되는 복제가 수렴 하지 않습니다.

예를 들어,는 다음 그림에서는 발생 하는 이벤트 순서 이전 운영 체제 및 Windows Server 2008 R2 USN 롤백 VDC2, 가상 컴퓨터에서 실행 되는 대상 도메인 컨트롤러에서 감지 되 면 합니다. 이 그림 USN 롤백 감지 복제 파트너 VDC2는 VDC2의 데이터베이스에 롤백으로 잘못 표시 되는 복제 파트너에 게 이전에 표시 된 최신 USN 값 보냈으며는 감지 VDC2에 발생 합니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

VM (가상 컴퓨터)를 쉽게 롤백할 도메인 컨트롤러의 Usn (해당 논리적 시계)가 하이퍼바이저 관리자 예를 들어 도메인 컨트롤러의 인식 외 스냅숏을 적용 합니다. USN 및 USN에 대 한 자세한 내용은 USN 롤백 감지 인스턴스 설명 하기 위해 다른 그림을 포함 하 여 롤백 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)합니다.

Windows Server 2012 부터는 VM-Generation ID 이라는 식별자 노출 하이퍼바이저 플랫폼에서 호스트 AD DS 가상 도메인 컨트롤러 검색 하 고 수 가상 컴퓨터 롤백됩니다 시간에서 VM 스냅숏은 적용 하는 경우 AD DS 환경을 보호 하기 위한 필요한 안전 사용 합니다. VM-GenerationID 디자인 게스트 가상 컴퓨터의 주소 공간에서이 식별자를 안전 하 게 virtualization 경험 VM-GenerationID 지 원하는 모든 하이퍼바이저의 지속적으로 사용할 수 있도록 하이퍼바이저 공급 업체 독립 메커니즘을 사용 합니다. 이 식별자 서비스와 응용 프로그램 내 가상 컴퓨터에서 실행 중인 경우 가상 컴퓨터 롤백 되었습니다 시간에서을 감지 하 여 샘플링 수 있습니다.

### <a name="BKMK_HowSafeguardsWork"></a>이러한 virtualization 되는지 궁금할은 어떻게 작동 하나요?
도메인 컨트롤러 설치 하는 동안 AD DS에 도메인 컨트롤러의 (디렉터리 정보 밤나무 또는 DIT 라고도 함) 데이터베이스에 컴퓨터 개체를 GenerationID 특성의 일환으로 VM GenerationID 식별자 처음에 저장 합니다. 가상 컴퓨터 내 Windows 드라이버로 인해 VM GenerationID 하지 추적 독립적으로 됩니다.

관리자가 이전 스냅숏을에서 가상 컴퓨터를 복원, 지정 된 가상 컴퓨터 드라이버에서 VM GenerationID DIT에서 값 비교 됩니다.

두 개의 값 인 다른는 invocationID 재설정 되 고 RID 풀 삭제 되므로 않아 USN 다시 사용 됩니다. 값 같으면 트랜잭션이 최선을 다하고 정상적으로 합니다.

AD DS 비교 지정 된 VM GenerationID DIT에 결과 대해 가상 컴퓨터에서 도메인 컨트롤러를 다시 부팅 하 고, 다른 invocationID를 다시 설정 하는 경우 RID 풀 버리고 DIT 새 값으로 업데이트 될 때마다 합니다. 또한 비 정식으로 안전 복원이 완료 하기 위해 SYSVOL 폴더를 동기화 합니다. 이렇게 하면 종료 된 Vm에서 스냅숏의 응용 프로그램을 확장 하 고 보호 기능이 있습니다. Windows Server 2012에서이 보호 기능 사용 AD DS 관리자 배포 하 고 관리 가상화 환경에 도메인 컨트롤러의 고유한 이점을 활용할 수 있습니다.

다음 그림에서는 virtualization 세이프 가드를 지 원하는 VM-GenerationID 하이퍼바이저에서 Windows Server 2012를 실행 하는 가상화 도메인 컨트롤러에서 동일한 USN 롤백 감지 되 면 적용 되는 방식을 보여 줍니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

이 경우 하이퍼바이저 VM-GenerationID 가치에 대 한 변경을 발견 하면 virtualization 되는지 궁금할 트리거됩니다를 포함 하 여 가상된 DC (출처: A 위 예제에서 b)에 대 한는 InvocationID 다시 및 하이퍼바이저 저장 하는 새 값 (g 2)에 맞게 VM에 저장 된 VM-GenerationID 값을 업데이트 합니다. 보호 기능 복제가 수렴 모두 도메인 컨트롤러에 대 한 있는지 확인 합니다.

Windows Server 2012와 AD DS VM-GenerationID 인식 하이퍼바이저에 호스트 가상 도메인 컨트롤러의 보호를 사용 하 고 실수로 응용 프로그램을 설치할 수 있도록 보장 스냅숏을 또는 다른 이러한 하이퍼바이저 사용 메커니즘 되돌릴 수 있는의 가상 컴퓨터의 상태 USN 거품 등 복제 문제를 방지 하거나 개체 느린) (여 AD DS 환경 방해 하지 않습니다. 그러나 도메인 컨트롤러 가상 컴퓨터 스냅숏을 적용 하 여 복원할 도메인 컨트롤러를 백업 하는 다른 메커니즘으로 권장 되지 않습니다. 계속 Windows Server 백업 또는 기타 VSS writer 기반 백업 솔루션을 사용 하는 것이 좋습니다.

> [!CAUTION]
> 도메인 컨트롤러 생산 환경에서 스냅숏을 실수로 되돌려집니다, 응용 프로그램에 대 한 공급 업체에 문의 하 고 스냅숏을 후 이러한 프로그램의 상태를 확인에 대 한 지침을 위해 해당 가상 컴퓨터에서 호스트 되는 서비스 복원 것이 좋습니다.

자세한 내용은 참조 [도메인 컨트롤러 안전 복원이 아키텍처 가상화](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)합니다.

## <a name="virtualized_dc_cloning"></a>가상화 도메인 컨트롤러 복제
Windows Server 2012 부터는 관리자 배포할 수 있는 쉽고 안전 하 게 복제 도메인 컨트롤러 기존 가상 도메인 컨트롤러를 복사 하 여 합니다. 가상 환경을 관리자가 더 이상 반복적으로 sysprep.exe을 사용 하 여 준비 서버 이미지를 배포, 홍보 도메인 컨트롤러 서버에 하 고 각 복제 도메인 컨트롤러를 배포 하기 위한 추가 구성 요구를 수행 합니다.

> [!NOTE]
> 관리자는 배포 하는 첫 번째 도메인 컨트롤러 등 sysprep.exe을 사용 하 여 서버 가상 하드 디스크 (VHD) 준비한 도메인 컨트롤러 서버 홍보 추가 구성 요구 사항을 완료 하는 도메인의 기존 프로세스를 수행 해야 합니다. 장애 복구 시나리오에서 최신 서버 백업을 사용 하는 도메인의 첫 번째 도메인 컨트롤러를 복원 하려면.

### <a name="scenarios-that-benefit-from-virtual-domain-controller-cloning"></a>가상 도메인 컨트롤러 복제의 활용 하는 시나리오

-   새 도메인 도메인 컨트롤러의 신속한 배포

-   신속 하 게 복제 사용 하는 도메인 컨트롤러의 신속한 배포 통해 AD DS 용량을 복원 하 여 업무 연속성 복구 하는 동안 복원

-   확대/축소 프로비저닝 증가 배율 요구 사항에 맞게 도메인 컨트롤러의 활용 하 여 개인 클라우드 배포 최적화

-   빠른 프로비저닝 배포 활성화 하 고 새로운 기능과 제품 출시 하기 전에 테스트 테스트 환경

-   복제 지사에서 기존 도메인 컨트롤러로 지점에서 빠르게 충족 증가 용량 요구 사항

많은 수의 도메인 컨트롤러를 신속 하 게 배포 하는 경우 계속 해 서 설치가 완료 된 후 도메인 컨트롤러 각 상태를 확인 하 여 기존 절차를 수행 합니다. 각 배치의 설치를 완료 한 후 자녀가 건강을 확인할 수 있는 적절 한 크기의 배치 도메인 컨트롤러를 배포 합니다. 10 권장된 일괄 크기가 조정 됩니다. 자세한 내용은 참조 [복제 가상화 도메인 컨트롤러 배포를 위해 단계](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)합니다.

### <a name="clear-separation-of-responsibilities"></a>책임 명확 하 게 분리
AD DS 관리자의 제어 가상화 도메인 컨트롤러 복제 허가입니다. 하이퍼바이저 관리자가 추가 도메인 컨트롤러 가상 도메인 컨트롤러를 복사 하 여 배포를 위해, AD DS 관리자는 선택한 도메인 컨트롤러에 권한을 부여 하 고 준비 단계 복제에 대 한 소스도 사용 하기를 실행 합니다.

가상 컴퓨터 공급 일반적으로 하이퍼바이저 관리자 purview 아래,와 하이퍼바이저 관리자 가상화 도메인 컨트롤러 승인 되 고 AD DS 관리자가 복제에 대 한 준비를 복사 하 여 복제본 도메인 컨트롤러 가상 컴퓨터를 구성할 수 있습니다.

> [!WARNING]
> 누구 든 지를 가상 도메인 컨트롤러 섬에는 하이퍼바이저 관리할 수 매우 신뢰할 수 있는 환경에 감사 합니다.

### <a name="how-does-virtual-domain-controller-cloning-work"></a>클라우드 복제 가상 도메인 컨트롤러 어떻게 되나요?
복제 하는 과정의 기존 가상 도메인 컨트롤러의 VHD (또는 복잡 한 구성 VM 도메인 컨트롤러) 복사본을 해줍니다 권한을 부여 하 복제 AD DS에 및 복제 구성 파일을 만듭니다. 이 단계 수를 줄일 수 및 관련 타임 복제 가상 도메인 컨트롤러 그렇지 않은 경우를 제거 하 여 배포 반복 배포 작업입니다.

복제본 도메인 컨트롤러는 다음 조건을 사용 하는 것은 다른 도메인 컨트롤러의 복사본을 감지 하:

1.  가상 컴퓨터에서 제공한 VM-Generation ID 값은 DIT에 저장 된 VM-Generation ID 값 다릅니다.

    > [!NOTE]
    > 하이퍼바이저 플랫폼 VM-Generation ID를 지원 해야 합니다 (Windows Server 2012 Hyper-v VM-Generation ID 지원).

2.  다음 위치 중 하나에 DCCloneConfig.xml 라고 하는 파일이 있는지 다음과 같습니다.

    -   DIT 있는 디렉터리

    -   %windir%\NTDS

    -   이동식 미디어 드라이브 루트

조건을 충족 되 면를 복제 도메인 컨트롤러도 프로비저닝 자체 복제 하는 과정 이동 합니다.

복제본 도메인 컨트롤러의 (도메인 컨트롤러 복사본을 나타내는) 원본 도메인 컨트롤러 보안 컨텍스트를 사용 하려면 (단일 마스터 작업 유연한 또는 FSMO 라고도 함) Windows Server 2012 주 도메인 컨트롤러 PDC () 에뮬레이터 작업 역할 마스터 소유자에 게 문의 합니다. PDC 에뮬레이터 Windows Server 2012를 실행 중 이어야 합니다 하지만 하이퍼바이저에서 실행 중 이어야 필요가 없습니다.

> [!NOTE]
> 원본 도메인 컨트롤러 참조 특성으로 스키마 확장 있는 경우 (컴퓨터 개체, NTDS 설정 개체) 복사본을 만들 수 복사 개체 중 하나에 해당 특성 복사 되거나 참조 복제 도메인 컨트롤러 하도록 업데이트 되지 않습니다.

PDC 에뮬레이터 요청한 도메인 컨트롤러가 복제에 대 한 권한이 있는지를 확인 한 후 새 계정을, SID, 이름 및 암호 복제 도메인 컨트롤러이 기계가를 식별 하는 포함 하 여 새 기계 id를 만들고이 복제 다시으로이 정보를 보내나요 합니다. 복제본 도메인 컨트롤러 AD DS 데이터베이스 파일 복제 역할을 준비 다음 및 컴퓨터 상태 정리도 됩니다.

자세한 내용은 참조 [아키텍처 복제 가상화 도메인 컨트롤러](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)합니다.

### <a name="cloning-components"></a>구성 요소 복제
복제 구성 요소 Windows PowerShell 및 관련된 XML 파일에 대 한 Active Directory 모듈에 새 cmdlet을 다음과 같습니다.

-   **새 ADDCCloneConfigFile** "이이 cmdlet 만들고 DCCloneConfig.xml 복제 트리거하를 사용할 수 있도록 오른쪽 위치에 배치 합니다. 또한 성공 복제 되도록 필수 검사를 수행 합니다. Windows PowerShell에 대 한 Active Directory 모듈에 포함 됩니다. 원격으로 사용 하 여 실행할 수 있습니다 또는 복제를 준비 하는 가상화 도메인 컨트롤러에서 로컬 실행할 수-오프 라인 옵션 합니다. 이름, 사이트 및 IP 주소 같은 복제 도메인 컨트롤러에 대 한 설정을 지정할 수 있습니다.

    필수 검사가 수행 하는 다음과 같습니다.

    > [!NOTE]
    > 필수 없는 검사 때 수행 되는 "옵션을 오프 라인으로 사용 됩니다. 자세한 내용은 참조 [오프 라인 모드에서 실행 New-ADDCCloneConfigFile](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)합니다.

    -   준비 DC 복제 권한이 부여 된 (의 구성원는 **복제 가능한 도메인 컨트롤러** 그룹)

    -   PDC 에뮬레이터 Windows Server 2012를 실행합니다.

    -   프로그램 또는 서비스가 실행 중인에서 나열 된 **Get ADDCCloningExcludedApplicationList** CustomDCCloneAllowList.xml (복제 구성 요소는이 목록의 끝에 자세히 설명)에 포함 되어 있습니다.

-   **DCCloneConfig.xml** "가상화 도메인 컨트롤러 복제할 성공적으로,이 파일에에서 있어야 DIT 있는 디렉터리 *%windir%\NTDS*, 또는 루트 이동식 미디어 드라이브에 있습니다. 검색 하 고 복제 시작 트리거 중 하나으로 사용 되 고, 외에도 복제 도메인 컨트롤러에 대 한 구성 설정을 지정 하는 방법을 제공 합니다.

    스키마와 DCCloneConfig.xml 파일에 대 한 샘플 파일에 모든 Windows Server 2012 컴퓨터에 저장 됩니다.

    -   %windir%\system32\DCCloneConfigSchema.xsd

    -   %windir%\system32\SampleDCCloneConfig.xml

    New-ADDCCloneConfigFile cmdlet DCCloneConfig.xml 파일을 사용 하는 것이 좋습니다. 이 파일을 만들 스키마 파일 XML 인식 편집기를 사용할 수도 수 있지만 오류가 발생할 가능성이 증가 파일을 수동으로 편집 합니다. Visual Studio 같은 XML 인식 편집기를 사용 하 여 편집할 수 있어야 파일이 편집 하는 경우 [XML 메모장](https://www.microsoft.com/download/details.aspx?displaylang=en&id=7973), 또는 제 3 자 응용 프로그램 (Notepad 사용 하지 않음).

-   **Get ADDCCloningExcludedApplicationList** "이이 cmdlet 확인할 수 있는 서비스 또는 설치 된 프로그램 DefaultDCCloneAllowList.xml 기본 지원 목록에 없는 복제 프로세스를 시작 하기 전에 원본 도메인 컨트롤러에서 실행 또는 사용자 정의 포함 명명된 CustomDCCloneAllowList.xml 파일을 나열 하 고 함으로써 하지 확인 된 복제 영향에 대 한 합니다.

    이 cmdlet 서비스를 제어 관리자에서 서비스에 대 한 소스 도메인 컨트롤러를 검색 하 고 설치 된 프로그램 아래에 나열 된 **HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall** 하는 기본 목록 (DefaultDCCloneAllowList.xml)에 지정 되지 않은 하거나, 한 경우이 제공 된, 사용자 정의 포함 목록 (CustomDCCloneAllowList.xml file) 합니다. Cmdlet 실행 하 여 반환 된 응용 프로그램 및 서비스 목록을 DefaultDCCloneAllowList.xml 또는 CustomDCCloneAllowList.xml 파일과 DC 원본에 설치 된 항목에 따라 실행 시 생성 되는 목록에 이미 제공 했습니다 무엇 간의 차이점은 합니다. 서비스 및 프로그램 안전 하 게 복제할 수 있는지 확인 한 경우 Get-ADDCCloningExcludedApplicationList 서비스 및 프로그램 출력 CustomDCCloneAllowList.xml 파일을 추가할 수 있습니다. 서비스 되거나 설치 된 프로그램을 안전 하 게 복제 될 경우을 확인 하려면 다음과 같은 평가 합니다.

    -   서비스 또는 컴퓨터 id 이름, SID, 암호, 등과 같은 영향이 설치 된 프로그램은 인가요?

    -   서비스는 또는 프로그램 스토어 상태 로컬 컴퓨터에 설치 복제에 그 기능에 영향을 줄 수 있는?

    확인 하는 경우 서비스 또는 프로그램 안전 하 게를 복제 하는 응용 프로그램의 소프트웨어 공급 업체를 사용 해야 합니다.

    > [!NOTE]
    > CustomDCCloneAllowList.xml 파일의 프로그램 또는 다른 서비스를 제공 하기 전에 필요한 라이선스 가상 컴퓨터에 포함 된 소프트웨어를 복사할 수 있는지 확인 합니다.

    응용 프로그램을 복제할 수 없는 경우 제거 원본 도메인 컨트롤러에서 복제 미디어를 만들기 전에 합니다. 응용 프로그램 cmdlet 출력에 표시 되 면 CustomDCCloneAllowList.xml 파일에 포함 되지 않은 경우, 복제 실패 합니다. 성공 하려면 복제할, 서비스 또는 프로그램 cmdlet 출력 나열 되지 해야 합니다. 즉, 응용 프로그램 될 CustomDCCloneAllowList.xml 파일에 포함 된 하거나 소스 도메인 컨트롤러에서 제거 합니다.

    다음 표에서 Get-ADDCCloningExcludedApplicationList 실행 하기 위한 옵션에 설명 합니다.

    |||
    |-|-|
    |인수|설명|
    |*<no argument specified>*|프로그램 또는 서비스 목록을 복제에 대 한 설명 하지는 콘솔에 표시 됩니다. 허용 되는 위치에 CustomDCCloneAllowList.XML 있으면 해당 파일 (될 수도 있는 아무 목록이 일치 하는 경우) 디스플레이 남아 있는 서비스를 제공 하며 프로그램을 사용 합니다.|
    |-GenerateXml|서비스 입력 CustomDCCloneAllowList.XML 파일 및 본체에 나열 된 프로그램 만듭니다.|
    |힘|기존 CustomDCCloneAllowList.XML 파일을 덮어씁니다.|
    |경로|폴더 경로 CustomDCCloneAllowList.XML 만들 수 있습니다.|

-   **DefaultDCCloneAllowList.xml** "이이 파일은 모든 Windows에서 기본적으로 제공 Server 2012 도메인 컨트롤러 in는 *%windir%\system32*. 서비스 목록과 설치 된 프로그램 기본적으로 안전 하 게 복제 될 수 있습니다. 위치나이 파일의 내용을 변경 하지 또는 복제 실패 합니다.

-   **CustomDCCloneAllowList.xml** "DefaultDCCloneAllowList.xml 파일에 나열 된 외부에 있는 원본 도메인 컨트롤러에 있는 설치한 프로그램 또는 서비스를 사용 하는 경우 이러한 서비스와 프로그램 해야 수이 파일에 포함 됩니다. 에 나열 되지 않은 설치 된 프로그램 또는 서비스를 찾으려면는 DefaultDCCloneAllowList.xml 파일에서 실행는 **Get ADDCCloningExcludedApplicationList** cmdlet 합니다. 사용 해야는 **"GenerateXml** 인수 XML 파일 생성할 수 있습니다.

    복제 프로세스가이 파일에 대 한 순서 대로 다음 위치를 확인 하 고 폴더의 내용에 관계 없이 발견 XML 첫 번째 파일을 사용 하 여 다음과 같습니다.

    1.  레지스트리 키:

        ```
        HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters
        AllowListFolder (REG_SZ)
        ```

    2.  작업 디렉터리 DSA

    3.  %systemroot%\NTDS

    4.  순서로 나열 루트 드라이브의 드라이브 문자가의 읽기/쓰기 이동식 미디어

### <a name="deployment-scenarios"></a>배포 시나리오
다음과 같은 배포 시나리오 가상 도메인 컨트롤러 복제 지원 됩니다.

-   원본 도메인 컨트롤러의 (vhd) 가상 하드 디스크 파일의 복사본을 적용 하 여 복제본 도메인 컨트롤러를 배포 합니다.

-   하이퍼바이저 노출 내보내기/가져오기 의미를 사용 하 여 원본 도메인 컨트롤러의 가상 컴퓨터에 복사 하 여 복제본 도메인 컨트롤러를 배포 합니다.

> [!NOTE]
> 섹션에 나와 있는 단계 [복제 가상화 도메인 컨트롤러 배포를 위해 단계](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc) 내보내기/가져오기 기능은의 Windows Server 2012 Hyper-v를 사용 하 여 가상 시스템 복사 보여 줍니다.

## <a name="steps_deploy_vdc"></a>배포 복제 가상화 도메인 컨트롤러 단계

-   [필수](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#prerequisites)

-   [1 단계: 원본 가상화 도메인 컨트롤러를 복제 될 수 있는 권한을 부여합니다](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk4_grant_source)

-   [2 단계: 실행 Get-ADDCCloningExcludedApplicationList cmdlet](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet)

-   [3 단계: New-ADDCCloneConfigFile 실행](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk5_create_insert_dccloneconfig)

-   [4 단계: 내보내고 원본 도메인 컨트롤러의 가상 컴퓨터를 가져오려면 다음](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk7_export_import_vm_sourcedc)

### <a name="prerequisites"></a>필수

-   다음 절차에 나와 있는 단계를 완료 하려면 관리자 도메인 그룹의 회원 또는 해당 사용 권한을에 할당 합니다.

-   이 가이드에 사용 된 Windows PowerShell 명령 관리자 명령 프롬프트를 실행 해야 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **Windows PowerShell** 아이콘을 클릭 하 고 **관리자 권한으로 실행**합니다.

-   Hyper-v 서버 역할이 설치와 Windows Server 2012 서버 (**HyperV1**).

-   Hyper-v 서버 역할이 설치를 사용 하 여 두 번째 Windows Server 2012 서버 (**HyperV2**).

    > [!NOTE]
    > -   하이퍼바이저 VM-Generation id입니다.를 지원 하는지 확인 하려면 해당 하이퍼바이저의 공급 업체에 문의 해야 다른 하이퍼바이저를 사용 하는 경우 하이퍼바이저 VM-Generation ID를 지원 하지 않는 경우 DCCloneConfig.xml 제공한 새 VM에 DSRM 디렉터리 서비스 복원 모드 () 부팅 됩니다.
    > -   이 가이드 AD DS 서비스의 사용 가능 여부를 높이려면 권장 하 고 방지 실패 잠재적으로 단일 지점 서로 다른 두 가지 Hyper-v 호스트를 사용 하는 지침을 제공 합니다. 그러나 두 Hyper-v 호스트 가상 도메인 컨트롤러 복제 하는 데 필요 하지 않습니다.
    > -   각 Hyper-v 서버에서 로컬 관리자가 그룹의 회원 있어야 (**HyperV1** 및 **HyperV2**).
    > -   성공적으로 가져오는 파일 및 내보내기 VHD Hyper-v를 사용 하 여, 하기 위해 두 Hyper-v 호스트 가상 네트워크 스위치가 이름이 같은 있어야 합니다. 예를 들어 있는 경우 가상 네트워크 켜기 **HyperV1** 가상 네트워크 켜려면 되어야 다음 VNet 라는 **HyperV2** VNet 이름이 지정 합니다.
    > -   하는 경우 두 Hyper-v 호스트 (**HyperV1** 및 **HyperV2**) 다른 프로세서가, 가상 컴퓨터를 종료 (**VirtualDC1**) 내보내기 VM 마우스 오른쪽 단추로 클릭, 클릭 하려는 **설정**, 클릭 **프로세서**, 고 **프로세서 호환성** 선택 **마이그레이션 물리적 프로세서를 다른 버전으로 컴퓨터에** 클릭 하 고 **확인**합니다.

-   배포 된 Windows Server 2012 하는 도메인 컨트롤러 (가상화 또는 물리적) PDC 에뮬레이터 역할 섬에는 (**d c 1**). Windows Server 2012 도메인 컨트롤러에 PDC 에뮬레이터 역할 호스트 있는지 여부를 확인 하려면 다음과 같은 Windows PowerShell 명령을 실행 합니다.

    ```
    Get-ADComputer (Get-ADDomainController "Discover "Service "PrimaryDC").name "Property operatingsystemversion | fl
    ```

    OperatingSystemVersion 값 6.2 버전으로 되돌아가야. 필요한 경우, Windows Server 2012를 실행 하는 도메인 컨트롤러에 PDC 에뮬레이터 역할을 전송할 수 있습니다. 자세한 내용은 참조 [이전 하거나 도메인 컨트롤러 역할 FSMO 중단을 사용 하 여 Ntdsutil.exe](https://support.microsoft.com/kb/255504)합니다.

-   배포 된 Windows Server 2012 게스트 가상화 도메인 컨트롤러 (**VirtualDC1**) Windows Server 2012 도메인 컨트롤러 PDC 에뮬레이터 역할 호스트와 같은 도메인에 (**d c 1**). 이 복제에 사용 되는 원본을 도메인 컨트롤러 됩니다. Windows Server 2012 Hyper-v 서버에 게스트 가상 도메인 컨트롤러 호스팅할 (**HyperV1**).

    > [!NOTE]
    > -   성공 하려면 복제에 대 한 소스 VHD 미디어를 만든 후 내렸습니다 DC의 복사본을 만드는 데 사용 되는 원본을 도메인 컨트롤러 수 없습니다.
    > -   VM 또는 그 VHD 복사 전에 원본 도메인 컨트롤러를 종료 합니다.
    > -   하지 VHD 복제 하거나 스냅숏을 삭제 표시 기간 값 (또는 삭제 개체 수명 값 Active Directory 휴지통 설정 되어 있는 경우)를 보다 오래 된 복원 해야 합니다. 기존 도메인 컨트롤러의 VHD 복사 하는 경우 반드시 VHD 파일은 이전 버전의 삭제 표시 기간 (기본적으로 60 일) 값 합니다. 하지 복제 미디어를 만드는 뛰 도메인 컨트롤러의 VHD 복사 해야 합니다.

    도킹 플로피 가상 드라이브 (VFD) 소스 DC 있을 수 있습니다. 새 VM 가져오기 하려고 할 때 공유 문제가 발생할 수 있습니다.

    Windows Server 2012 도메인 컨트롤러에만 VM-GenerationID 하이퍼바이저에 호스트 복제할 원본으로 사용할 수 있습니다. 원본 Windows Server 2012 도메인 컨트롤러 복제에 사용 되는 건강 상태 여야 합니다. 실행 원본 도메인 컨트롤러의 상태를 확인 하려면 [dcdiag](https://technet.microsoft.com/library/cc731968(WS.10).aspx)합니다. Dcdiag에서 반환 되는 출력을 더 잘 이해 참조 하십시오 [무엇을 DCDIAG 실제로... 수행 하나요?](http://blogs.technet.com/b/askds/archive/2011/03/22/what-does-dcdiag-actually-do.aspx).

    원본 도메인 컨트롤러 DNS 서버를 경우 복제 도메인 컨트롤러 DNS 서버 수도 있습니다. DNS 서버가 해당 호스트 Active Directory 통합 영역을 선택 합니다.

    DNS 클라이언트 설정을 복제 됩니다 하지만 대신 DCCloneConfig.xml 파일에 지정 합니다. 지정 하지 않은 경우 복제 도메인 컨트롤러를 가리킵니다 자체 기본 설정 DNS 서버도 기본적으로. 복제 도메인 컨트롤러 DNS 위임이 없을 것입니다. 부모 DNS 영역 관리자 DNS 위임 필요에 따라 복제 도메인 컨트롤러에 대 한 업데이트 해야 합니다.

    > [!WARNING]
    > Virtualization 되는지 궁금할 Active Directory 경량 디렉터리 서비스 (AD LDS)를 확장 하지 않습니다. 따라서 하지 않아야이 광고 LDS 인스턴스 CustomDCCloneAllowList.xml에 추가 하 여 광고 LDS 인스턴스 호스트 하는 AD DS 도메인 컨트롤러 복제할 합니다. 광고 LDS VM-Generation ID 인식 되지 않으므로 복제 광고 lds 도메인 컨트롤러에 발생할 수 있습니다 USN 롤백 일으킨 확산 AD LDS 해당 구성 집합입니다.

    다음 서버 역할 복제에 대 한 지원 되지 않습니다.

    -   DHCP(Dynamic Host Configuration Protocol) DHCP)

    -   Active Directory 인증서 서비스 (AD CS)

    -   Active Directory 무게는 가벼우며 디렉터리 서비스 (AD LDS)

### <a name="bkmk4_grant_source"></a>1 단계: 원본 가상화 도메인 컨트롤러를 복제 될 수 있는 권한을 부여합니다
이 절차에 권한을 부여 하면 원본 도메인 컨트롤러를 사용 하 여 복제할 **Active Directory 관리 센터** 원본 도메인 컨트롤러에 추가 하 고 **복제 가능한 도메인 컨트롤러** 그룹 합니다.

##### <a name="to-grant-the-source-virtualized-domain-controller-the-permission-to-be-cloned"></a>원본 가상화 도메인 컨트롤러 복제 될 수 있는 권한을 부여 하려면

1.  모든 준비를 복제 하는 도메인 컨트롤러와 동일한 도메인 도메인 컨트롤러에서 (**VirtualDC1**) 열기, **Active Directory 관리 센터** (ADAC) 가상화 도메인 컨트롤러 개체를 찾습니다 (도메인 컨트롤러 아래에 있는 일반적으로 **도메인 컨트롤러** 컨테이너 ADAC에), 마우스 오른쪽 단추로 클릭, 선택 **그룹에 추가** 고 **선택할 개체 이름을 입력** 유형 **복제 가능한 도메인 컨트롤러** 차례로 클릭 하 고 **확인**합니다.

    이 단계 수행 그룹 구성원 업데이트 복제 수행할 수 있는 전에 PDC 에뮬레이터 복제 해야 합니다. 하는 경우는 **복제 가능한 도메인 컨트롤러** 그룹을 찾을 수 없는, Windows Server 2012를 실행 하는 도메인 컨트롤러에서 PDC 에뮬레이터 역할을 호스트할 수 있습니다.

    > [!NOTE]
    > Windows Server 2012 도메인 컨트롤러에서 ADAC를 열려면 Windows PowerShell 및 유형 엽니다 **dsac.exe**합니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

다음 Windows PowerShell cmdlet 이전 절차와 같은 기능을 수행합니다.


    Add-ADGroupMember "Identity "CN=Cloneable Domain Controllers,CN=Users, DC=Fabrikam,DC=Com" "Member "CN=VirtualDC1,OU=Domain Controllers,DC=Fabrikam,DC=com"


### <a name="bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet"></a>2 단계: 실행 Get-ADDCCloningExcludedApplicationList cmdlet
이 절차의 실행는 `Get-ADDCCloningExcludedApplicationList`프로그램 또는 복제 하는 것에 대 한 평가 하지 되는 서비스를 식별 하는 소스 가상화 도메인 컨트롤러에서 cmdlet 합니다. DCCloneConfig.xml 파일 만들지는 New-ADDCCloneConfigFile cmdlet 제외 응용 프로그램을 발견 때문에 New-ADDCCloneConfigFile cmdlet 하기 전에 Get-ADDCCloningExcludedApplicationList cmdlet 실행 해야 합니다.

##### <a name="to-identify-applications-or-services-that-run-on-a-source-domain-controller-which-have-not-been-evaluated-for-cloning"></a>응용 프로그램 또는 하지 복제에 대 한 평가 되는 소스 도메인 컨트롤러에서 실행 하는 서비스가 사용자의 신원을 확인 하려면

1.  원본 도메인 컨트롤러의 (**VirtualDC1**)를 클릭 **서버 관리자**, 클릭 **도구**, 클릭 **Active Directory Windows PowerShell 모듈** 다음 명령을 입력 하 고:


    Get-ADDCCloningExcludedApplicationList


2.  반환된 서비스 및 설치 된 프로그램 목록 여부 자녀가 안전 하 게 복제 확인 하는 소프트웨어 공급 업체와 검사 합니다. 응용 프로그램 또는 서비스가 목록에서 안전 하 게 복제 될 수 없는, 원본 도메인 컨트롤러에서 제거 해야 또는 복제 실패 합니다.

3.  결정 된 복제할 안전 하 게 설치 된 프로그램 및 서비스 집합을 사용 하 여 다시 명령을 실행 하는 **"GenerateXML** 스위치 이러한을 제공 하기 위해 서비스를 제공 하며의 프로그램은 **CustomDCCloneAllowList.xml** 파일 합니다.


    Get-ADDCCloningExcludedApplicationList GenerateXml


### <a name="bkmk5_create_insert_dccloneconfig"></a>3 단계: New-ADDCCloneConfigFile 실행
원본 도메인 컨트롤러에서 New-ADDCCloneConfigFile 실행 하 고 필요에 따라 복제 도메인 컨트롤러의 이름, IP 주소, DNS 확인자 등에 대 한 구성 설정을 지정 합니다.

예를 들어 VirtualDC2 고정 IPv4 주소와 라는 복제 도메인 컨트롤러를 만들려면 입력 합니다.


    New-ADDCCloneConfigFile "Static -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.255.0" -CloneComputerName "VirtualDC2" -IPv4DefaultGateway "10.0.0.3" -SiteName "REDMOND"

> [!NOTE]
> 복제본 도메인 컨트롤러 DCCloneConfig.xml 파일에는 다른 사이트를 지정 하지 않으면 원본 도메인 컨트롤러와 같은 사이트에 배치 됩니다. IP 주소를 기준 복제 도메인 컨트롤러의 DCCloneConfig.xml 파일에 적합 한 사이트를 지정 하는 것이 좋습니다.

컴퓨터 이름이입니다. 지정 하지 않으면 다음과 같은 알고리즘에 따라 고유한 이름을 생성 됩니다.

-   접두사 처음 8 소스 도메인 컨트롤러의 컴퓨터 이름을 자가 합니다. 예를 들어, SourceCo 접두사 문자열로 SourceComputer의 소스 컴퓨터 이름을 잘립니다.

-   서식의 고유한 명명 접미사 "" CL*nnnn*"접두사 문자열에 추가 되 *nnnn*PDC 현재 사용 중인 결정 0001-9999에서 사용 가능한 다음 값은 합니다. 예를 들어, 0047 번호가 허용 되는 범위에 있으면의 컴퓨터 이름 접두사 SourceCo, 위 예제를 사용 하 여 복제 컴퓨터를 사용 하 여 파생된 이름 설정 됩니다 SourceCo CL0047으로 합니다.

> [!NOTE]
> 드 서버 GC ()가 제대로 작동 하도록 New-ADDCCloneConfigFile cmdlet 필요 합니다. 원본 도메인 컨트롤러 구성원에는 **복제 가능한 도메인 컨트롤러** 그룹 GC에 반영 해야 합니다. PDC 에뮬레이터와 동일한 도메인 컨트롤러 되도록 GC 필요는 없지만 같은 사이트에 있어야 것이 좋습니다. GC 사용할 수 없는 경우 명령이 실패 오류가 발생 하 여 "서버 작동 하지 않습니다." 자세한 내용은 참조 [도메인 컨트롤러 문제 해결 가상화](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)합니다.

고정 IPv4 설정을 사용 하 여 Clone1 라는 복제 도메인 컨트롤러를 만들고 기본 설정 및 대체 wins 지정 하려면 다음을 입력 합니다.


    New-ADDCCloneConfigFile "CloneComputerName "Clone1" "Static -IPv4Address "10.0.0.5" "IPv4DNSResolver "10.0.0.1" "IPv4SubnetMask "255.255.0.0" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


> [!NOTE]
> 모두 지정 해야 wins 지정 하면 **"PreferredWINSServer** 및 **" AlternateWINSServer**합니다. 이러한 인수의만 지정 복제 dcpromo.log에에서 오류 코드 0x80041005 표시 된 작동 하지 않습니다.

동적 IPv4 설정을 사용 하 여 Clone2 라는 복제 도메인 컨트롤러를 만들려면 다음을 입력 합니다.


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" 


> [!NOTE]
> 이 경우 DHCP를에서 있어야 환경 복제 액세스 하 고 IP 주소 및 기타 관련 된 네트워크 설정 얻을 수 있습니다.

동적 IPv4 설정을 사용 하 여 Clone2 라는 복제 도메인 컨트롤러를 만들고 기본 설정 및 대체 wins 지정 하려면 다음을 입력 합니다.


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" -SiteName "REDMOND" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


동적 IPv6 설정, 복제 도메인 컨트롤러를 입력 합니다.


    New-ADDCCloneConfigFile -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


고정 IPv6 설정을, 복제 도메인 컨트롤러를 입력 합니다.


    New-ADDCCloneConfigFile "Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


> [!NOTE]
> 것뿐입니다 정적 및 동적 설정 IPv6 설정을 지정을 포함 하 여가 **-고정** 전환 합니다. 포함 하 여는 **-고정** 스위치를 사용 하면 하나 이상을 지정 필수 **IPv6DNSResolver**합니다. 고정 IPv6 주소 비저장 주소 라우터 할당 된 접두사와 자동 구성 (SLAAC)을 통해 구성 예정입니다. 동적 IPv6와 DNS 확인자는 선택적 이지만 복제 IPv6 주소과 구성 정보 DNS 서브넷에 IPv6 가능 DHCP 서버에 연결할 수 것으로 기대 합니다.

#### <a name="BKMK_OfflineMode"></a>오프 라인 모드에서 New-ADDCCloneConfigFile 실행
소스 도메인 컨트롤러 미디어 복제 (원본 도메인 컨트롤러 복제 권한이 부여 된, Get-ADDCCloningExcludedApplicationList cmdlet 했습니다. 즉, 실행 및 등)에 대 한 준비를 복사본을 여러 개 있는 경우 각 사본 미디어에 대 한 여러 설정을 지정 하려면 New-ADDCCloneConfigFile 오프 라인 모드에서 실행할 수 있습니다. 개별적으로 각 VM 각 복사본을 가져와서 준비 보다 효율적 될 수 있습니다.

이 경우 도메인 관리자 수 오프 라인 디스크 탑재을 사용 하 원격 서버 관리 도구 RSAT () 실행 New-ADDCCloneConfigFile cmdlet-오프 라인 인수와 Windows Server 2012에 포함 된 새로운 Windows PowerShell 옵션을 사용 하 여 공장 같은 자동화 수 있는 XML 파일을 추가 하기 위해 합니다. 오프 라인 디스크 New-ADDCCloneConfigFile cmdlet 오프 라인 모드에서 실행 하는 데 장착 하는 방법에 대 한 자세한 내용은 참조 [오프 라인 시스템 디스크에 추가 XML](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_Offline)합니다.

해당 필수 패스를 검사 하려면 소스 미디어에서 로컬 cmdlet를 실행 먼저 해야 합니다. 오프 라인 모드에서 cmdlet 도메인에 가입 컴퓨터에서 동일한 도메인 또는 없을 수 있는 컴퓨터에서 실행 될 수 있으므로 필수 검사가 수행 되지 않습니다. 로컬에서 cmdlet을 실행 한 후 DCCloneConfig.xml 파일을 만듭니다. 이후에 오프 라인 모드를 사용 하려면 로컬로 생성 되는 DCCloneConfig.xml 삭제할 수 있습니다.

복제본 도메인 컨트롤러를 만들려면 붙은 CloneDC1 REDMOND 이라고 하는 사이트에서 오프 라인 모드에서 "정적 IPv4 주소를 입력 합니다.


    New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS


고정 IPv4와 고정 IPv6 설정을 입력 오프 라인 모드에서 Clone2 라는 복제 도메인 컨트롤러 만들려면 다음과 같습니다.


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS


만들어 복제본 도메인 컨트롤러 고정 IPv4와 동적 IPv6 설정 오프 라인 모드에서 DNS 확인자 설정에 대 한 여러 DNS 서버를 지정를 입력 합니다.


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS 


동적 IPv4와 고정 IPv6 설정을 입력 오프 라인 모드에서 Clone1 라는 복제 도메인 컨트롤러 만들려면 다음과 같습니다.


    New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS


동적 IPv4와 동적 IPv6 설정 오프 라인 모드에서 복제본 도메인 컨트롤러를 만들려면 입력 합니다.


    New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS


### <a name="bkmk7_export_import_vm_sourcedc"></a>4 단계: 내보내고 원본 도메인 컨트롤러의 가상 컴퓨터를 가져오려면 다음
이 절차의 소스 가상화 도메인 컨트롤러의 가상 컴퓨터 내보내고 가상 컴퓨터를 가져오려면 다음 합니다. 도메인에 복제 가상화 도메인 컨트롤러를 만들어집니다.

각 Hyper-v 호스트 로컬 관리자가 그룹의 회원 해야 합니다. 각 서버에 대 한 다른 자격 증명을 사용 하는 경우 서로 다른 Windows PowerShell 세션에 VM 내보내고를 Windows PowerShell cmdlet을 실행 합니다.

원본 도메인 컨트롤러에서 스냅숏을 인 삭제 해야 VM 스냅숏을 프로세서 설정이 대상 hyper v 호스트과 호환 되지 않는 경우 가져오기가 원본 도메인 컨트롤러 내보낼 됩니다. 프로세서 설정이 원본과 대상 hyper v 호스트 사이의 호환 경우 내보내기 수 있으며 미리 스냅숏을 삭제 하지 않고 소스를 복사할 수 있습니다. 하지만을 가져온 후 스냅숏은 삭제 해야 복제 VM에서에서 시작 하기 전에 합니다.

##### <a name="to-copy-a-virtual-domain-controller-by-exporting-and-then-importing-the-virtualized-source-domain-controller"></a>가상 도메인 컨트롤러 내보내고 다음 가상화 원본 도메인 컨트롤러를 가져와 복사

1.  **HyperV1**, 종료 원본 도메인 컨트롤러 (**VirtualDC1**).

    ![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

    Stop-VM-VirtualDC1-ComputerName HyperV1 표시 된 이름


2.  **HyperV1**스냅숏을 삭제 한 다음 c:\CloneDCs 디렉터리 원본 도메인 컨트롤러 (VirtualDC1) 내보낼 합니다.

> [!NOTE]
> 스냅숏을, 때마다 새로운 AVHD 파일이 만들어집니다 역할을 디스크 차이 하기 때문에 연결 된 모든 스냅숏을 삭제 해야 합니다. 체인 영향을 만듭니다. 스냅숏을 수행 하 고 VHD DCCLoneConfig.xml 파일 삽입 복제본 DIT 이전 버전에서 만들기 되거나 잘못 된 VHD 파일 구성 파일 삽입 될 수 있습니다. 이러한 모든 AVHDs 기본 VHD에 병합 스냅샷을 삭제 합니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *


    Get-VMSnapshot VirtualDC1 | Remove-VMSnapshot -IncludeAllChildSnapshots
    Export-VM -Name VirtualDC1 -ComputerName HyperV1 -Path c:\CloneDCs\VirtualDC1


3.  폴더를 복사 **virtualdc1** 의 c:\Import 디렉터리 **HyperV2**합니다.

4.  **HyperV2**를 사용 하 여 **Hyper-v 관리자**, 가상 컴퓨터를 가져오려면 (사용 하는 **가져오기 가상 컴퓨터** 마법사에서 **Hyper-v 관리자**) 폴더에서 **c:\Import\virtualdc1** 와 관련 된 모두 삭제 **스냅숏을**합니다.

사용 하는 **가상 컴퓨터에 복사 (새 고유 ID를 생성)** 가상 컴퓨터 가져올 때 옵션입니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

    $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Machines"
    $vm = Import-VM -Path $path.fullname -Copy -GenerateNewId
    Rename-VM $vm VirtualDC2


여러 복제 도메인 컨트롤러를 동일한 원본 도메인 컨트롤러에서:

  -   UI:에 **가져오기 가상 컴퓨터** 마법사를에 대 한 새 위치를 지정 **가상 컴퓨터 구성 폴더**, **스냅숏 스토어**, **폴더 스마트 페이징**, 다른 및 **위치** 가상 컴퓨터에 대해 가상 하드 디스크에 대 한 합니다.

  -   Windows PowerShell:에 대 한 다음 매개 변수를 사용 하 여 가상 컴퓨터에 대 한 새 위치를 지정는 `Import-VM`cmdlet:

        $path Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual 컴퓨터" = Import-VM-경로 $path.fullname-복사 경로"-GenerateNewId 경로"-ComputerName HyperV2-VhdDestinationPath"-SnapshotFilePath"경로"-SmartPagingFilePath"경로"-VirtualMachinePath"


> [!NOTE]
> 동시에 여러 복제본 도메인 컨트롤러를 만들기 위한 권장된 일괄 크기가 10 합니다. 기본적으로는 16 분산 파일 시스템 복제 (DFSR)에 대 한 및 10에 대 한 파일 FRS (복제 서비스) 최대 아웃 바운드 복제 연결 하 여 최대 제한 됩니다. 배포 하지 마십시오 복제 도메인 컨트롤러의 추천된 수를 초과 동시에 해당 번호로 완전히 귀하의 환경에 대 한 테스트 한 하지 않으면 합니다.

5.  **HyperV1**, 소스 도메인 컨트롤러를 다시 시작 (**(VirtualDC1**) 온라인 다시 가져올 수 있습니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *

    Start-VM -Name VirtualDC1 -ComputerName HyperV1


6.  에 **HyperV2**, 가상 컴퓨터를 시작 (**VirtualDC2**) 도메인에 있는 온라인 복제 도메인 컨트롤러도 가져올 수 있습니다.

![AD DS 소개](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell 해당 하는 명령 *


    Start-VM -Name VirtualDC2 -ComputerName HyperV2

> [!NOTE]
> 성공 하려면 복제할 PDC 에뮬레이터 실행 중 이어야 합니다. 종료 경우 시작 된 것 이므로 인식 즉 수행된 초기 동기화 PDC 에뮬레이터 역할을 갖고 되어 있는지 확인 합니다. 자세한 내용은 참조 Microsoft [KB 문서 305476](https://support.microsoft.com/kb/305476)합니다.

복제 완료 된 후 성공 복제 작동 하도록 복제 컴퓨터의 이름을 확인 합니다. VM에서 DSRM 디렉터리 서비스 복원 모드 () 시작 되지 않았습니다를 확인 합니다. 에 로그인 하 고 없음 로그온 서버를 사용할 수 없다는 오류 메시지가 나타나면 하려고 하면 시도 로깅 DSRM 하세요. DC 성공적으로 복제 하지 않은 경우 DSRM에서 부팅 되 이벤트 뷰어에서 로그 확인 하 고 dcpromo %systemroot%/debug 폴더에서 기록 합니다.

복제 도메인 컨트롤러의 회원 됩니다는 **복제 가능한 도메인 컨트롤러** 그룹 구성원 원본 도메인 컨트롤러에서 복사 때문에 있습니다. 모범 사례로 두어야는 **복제 가능한 도메인 컨트롤러** 그룹 비어까지 준비가 복제 작업을 수행할 수 있으며 복제 작업이 완료 된 후 구성원 제거 해야 합니다.

원본 도메인 컨트롤러 미디어를 백업에 저장 하는 경우 복제 도메인 컨트롤러는도 백업 미디어를 저장 합니다. 실행할 수 `wbadmin get versions`백업 미디어 복제 도메인 컨트롤러에 표시 됩니다. 도메인 관리자 그룹의 회원 실수로 복원 않도록 복제 도메인 컨트롤러에 백업 미디어를 삭제 해야 합니다. Wbadmin.exe를 사용 하 여 시스템 상태 백업을 삭제 하는 방법에 대 한 자세한 내용은 참조 [Wbadmin systemstatebackup 삭제](https://technet.microsoft.com/library/cc742081(v=WS.10).aspx)합니다.

## <a name="troubleshooting"></a>문제 해결
하는 경우 복제 도메인 컨트롤러 (**VirtualDC2**) 시작에 DSRM 디렉터리 서비스 복원 모드 ()를 반환 하지 않습니다 표준 모드를에 다음에 자체 다시 부팅 합니다. DSRM에서 시작 하는 도메인 컨트롤러에 로그온 할 때 사용 하 여 **. \Administrator** DSRM 암호를 지정 하 고 있습니다.

복제 오류에 대 한 해결 한 dcpromo.log 복제 재시도 안 나타내지 않습니다 확인 합니다. 복제 재시도 수 없으면를 안전 하 게 미디어를 삭제 합니다. 복제 시도할 수 있는 다시, 복제 다시 시도 하기 위해 DS 복원 모드 부팅 플래그를 제거 해야 합니다.

1.  관리자 권한 명령 (오른쪽 클릭 Windows Server 2012 하 고 선택 관리자 권한으로 실행)를 선택한 다음와 Windows Server 2012 열기 **msconfig**합니다.

2.  에 **부팅** 탭의 **부팅 옵션**취소 **안전 부팅** (이미 옵션을 선택 되어 **활성화 Active Directory 복구**).

3.  클릭 **확인** 메시지가 표시 되 면를 다시 시작 합니다.

가상화 도메인 컨트롤러에 대 한 더 많은 문제 해결 정보를 참조 하세요. [도메인 컨트롤러 문제 해결 가상화](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)합니다.


