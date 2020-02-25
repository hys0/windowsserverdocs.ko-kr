---
ms.assetid: fde99b44-cb9f-49bf-b888-edaeabe6b88d
title: 응용 프로그램 공급업체를 위한 가상화된 도메인 컨트롤러 복제 테스트 지침
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 4926fabe255f964b6d39e6c39c5e794a37423111
ms.sourcegitcommit: 1c75e4b3f5895f9fa33efffd06822dca301d4835
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77517468"
---
# <a name="virtualized-domain-controller-cloning-test-guidance-for-application-vendors"></a>응용 프로그램 공급업체를 위한 가상화된 도메인 컨트롤러 복제 테스트 지침

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 가상화 된 DC (도메인 컨트롤러) 복제 프로세스가 완료 된 후 응용 프로그램이 계속 해 서 예상 대로 작동 하도록 하기 위해 응용 프로그램 공급 업체에서 고려해 야 할 사항에 대해 설명 합니다. 응용 프로그램 공급 업체 및 추가 테스트를 보장할 수 있는 시나리오에 관심이 있는 복제 프로세스의 이러한 측면을 다룹니다. 응용 프로그램이 복제 된 가상화 된 도메인 컨트롤러에서 작동 하는지 확인 한 응용 프로그램 공급 업체는이 항목의 맨 아래에 있는 커뮤니티 콘텐츠에 응용 프로그램의 이름을 나열 하는 것이 좋습니다. 사용자가 유효성 검사에 대해 자세히 알아볼 수 있는 조직의 웹 사이트입니다.

## <a name="overview-of-virtualized-dc-cloning"></a>가상화 된 DC 복제 개요
가상화 된 도메인 컨트롤러 복제 프로세스는 [AD DS (Active Directory Domain Services) 가상화 (수준 100)](https://docs.microsoft.com/windows-server/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) 및 [가상화 된 도메인 컨트롤러 기술 참조 (수준 300)](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-)에 자세히 설명 되어 있습니다. 응용 프로그램의 관점에서 보면 응용 프로그램에 대 한 복제의 영향을 평가할 때 고려해 야 할 몇 가지 고려 사항이 있습니다.

-   원래 컴퓨터는 제거 되지 않습니다. 네트워크에 유지 되 고 클라이언트와 상호 작용 합니다. 원본 컴퓨터의 DNS 레코드를 제거 하는 이름 바꾸기와 달리 원본 도메인 컨트롤러의 원래 레코드는 그대로 유지 됩니다.

-   복제 프로세스 중에는 복제 프로세스가 시작 될 때까지 새 컴퓨터가 이전 컴퓨터의 id를 사용 하 여 짧은 시간 동안 실행 되며 필요한 변경을 수행 합니다. 호스트에 대 한 레코드를 만드는 응용 프로그램에서는 복제 프로세스 중에 복제 된 컴퓨터가 원래 호스트에 대 한 레코드를 덮어쓰지 않도록 해야 합니다.

-   복제는 다른 서버 역할을 복제 하는 일반적인 용도의 확장이 아니라 가상화 된 도메인 컨트롤러에 대 한 특정 배포 기능입니다. 일부 서버 역할은 특히 복제를 지원 하지 않습니다.

    -   DHCP(동적 호스트 구성 프로토콜)

    -   AD CS(Active Directory 인증서 서비스)

    -   AD LDS(Active Directory Lightweight Directory Services)

-   복제 프로세스의 일부로 원래 DC를 나타내는 전체 VM이 복사 되므로 해당 VM의 모든 응용 프로그램 상태도 복사 됩니다. 응용 프로그램이 복제 된 DC에서 로컬 호스트의 상태를 변경 하는 경우 또는 서비스를 다시 시작 하는 등의 작업이 필요한 지를 확인 합니다.

-   복제의 일부로 새 DC는 새 컴퓨터 id를 가져오고 토폴로지에서 복제본 DC로 스스로를 프로 비전 합니다. 응용 프로그램이 컴퓨터 id (예: 이름, 계정, SID 등)에 종속 되는지 여부를 확인 합니다. 복제에서 컴퓨터 id의 변경에 자동으로 적응 됩니까? 해당 응용 프로그램이 데이터를 캐시 하는 경우 캐시 될 수 있는 컴퓨터 id 데이터를 사용 하지 않는지 확인 합니다.

## <a name="what-is-interesting-for-application-vendors"></a>응용 프로그램 공급 업체에 게는 흥미로운 점이 있나요?

### <a name="customdccloneallowlistxml"></a>Customdccloneallowlist.xml
응용 프로그램 또는 서비스를 실행 하는 도메인 컨트롤러는 응용 프로그램 또는 서비스가 다음 중 하나에 해당 하는 경우에만 복제할 수 있습니다.

-   Get-addccloningexcludedapplicationlist Windows PowerShell cmdlet을 사용 하 여 Customdccloneallowlist.xml 파일에 추가 되었습니다.

-또는-

-   도메인 컨트롤러에서 제거 됨

사용자가 Get-addccloningexcludedapplicationlist cmdlet을 처음 실행 하면 도메인 컨트롤러에서 실행 되는 서비스 및 응용 프로그램 목록이 반환 되지만 복제에 지원 되는 서비스 및 응용 프로그램의 기본 목록에는 표시 되지 않습니다. 기본적으로 서비스 또는 응용 프로그램은 나열 되지 않습니다. 안전 하 게 복제할 수 있는 응용 프로그램 및 서비스 목록에 서비스 또는 응용 프로그램을 추가 하기 위해 사용자는 Customdccloneallowlist.xml 파일에 추가 하기 위해-GenerateXML 옵션과 함께 Get-addccloningexcludedapplicationlist cmdlet을 다시 실행 합니다. 자세한 내용은 [2 단계: get-addccloningexcludedapplicationlist Cmdlet 실행](https://docs.microsoft.com/powershell/module/addsadministration/get-addccloningexcludedapplicationlist)을 참조 하세요.

### <a name="distributed-system-interactions"></a>분산 시스템 상호 작용
일반적으로 로컬 컴퓨터와 격리 된 서비스는 복제에 참여할 때 통과 하거나 실패 합니다. 분산 서비스는 잠시 동안 네트워크에 호스트 컴퓨터의 인스턴스를 두 개 포함 하는 것을 걱정 해야 합니다. 복제본이 id의 새 공급 업체로 등록 된 파트너 시스템에서 정보를 가져오려고 시도 하는 서비스 인스턴스로 매니페스트 될 수 있습니다. 또는 서비스의 두 인스턴스는 서로 다른 결과를 사용 하 여 동시에 정보를 AD DS 데이터베이스로 푸시할 수 있습니다. 예를 들어 WTT (Windows 테스트 기술) 서비스가 있는 두 대의 컴퓨터가 도메인 컨트롤러를 사용 하 여 네트워크에 있는 경우 어떤 컴퓨터가 통신 하는지 명확 하지 않습니다.

분산 된 DNS 서버 서비스의 경우 복제 프로세스는 복제 도메인 컨트롤러가 새 IP 주소를 사용 하 여 시작 될 때 원본 도메인 컨트롤러의 DNS 레코드를 덮어쓰는 것을 신중 하 게 방지 합니다.

복제를 마칠 때까지 컴퓨터를 사용 하 여 이전 id를 모두 제거 하면 안 됩니다. 새 도메인 컨트롤러를 새 컨텍스트 내에서 수준을 올린 후 Sysprep 공급자를 실행 하 여 컴퓨터의 추가 상태를 정리 합니다. 예를 들어이 시점에서 컴퓨터의 이전 인증서가 제거 되 고 컴퓨터에서 액세스할 수 있는 암호화 암호가 변경 됩니다.

복제 타이밍을 다양 하 게 만드는 가장 큰 요인은 PDC에서 복제할 개체의 수입니다. 이전 미디어는 복제를 완료 하는 데 필요한 시간을 늘립니다.

서비스 또는 응용 프로그램을 알 수 없기 때문에 실행이 중단 됩니다. 복제 프로세스는 비 Windows 서비스의 상태를 변경 하지 않습니다.

또한 새 컴퓨터에는 원래 컴퓨터와 다른 IP 주소가 있습니다. 이러한 동작은 서비스 또는 응용 프로그램이이 환경에서 작동 하는 방식에 따라 서비스 또는 응용 프로그램에 부작용을 일으킬 수 있습니다.

## <a name="additional-scenarios-suggested-for-testing"></a>테스트에 대해 제안 되는 추가 시나리오

### <a name="cloning-failure"></a>복제 오류
복제에 실패 하는 경우 컴퓨터가 안전 모드 형태의 DSRM (디렉터리 서비스 복구 모드)으로 부팅 되기 때문에 서비스 공급 업체는이 시나리오를 테스트 해야 합니다. 이 시점에서 컴퓨터가 복제를 완료 하지 않았습니다. 일부 상태가 변경 되었을 수 있으며, 일부 상태는 원래 도메인 컨트롤러에서 남아 있을 수 있습니다. 이 시나리오를 테스트 하 여 응용 프로그램에 미칠 수 있는 영향을 파악 합니다.

복제 실패를 유도 하려면 복제 권한을 부여 하지 않고 도메인 컨트롤러를 복제 해 보세요. 이 경우 컴퓨터는 IP 주소만 변경 하 고 원래 도메인 컨트롤러에서 대부분의 상태를 유지 합니다. 복제할 도메인 컨트롤러 권한을 부여 하는 방법에 대 한 자세한 내용은 [1 단계: 가상화 된 원본 도메인 컨트롤러에 복제할 수 있는 권한 부여](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/virtualized-domain-controller-deployment-and-configuration)를 참조 하세요.

### <a name="pdc-emulator-cloning"></a>PDC 에뮬레이터 복제
PDC 에뮬레이터가 복제 될 때 추가 다시 부팅이 있으므로 서비스 및 응용 프로그램 공급 업체는이 시나리오를 테스트 해야 합니다. 또한 복제 프로세스 중에는 새 복제본이 PDC 에뮬레이터와 상호 작용할 수 있도록 임시 id로 대부분의 복제를 수행 합니다.

### <a name="writable-versus-read-only-domain-controllers"></a>쓰기 가능한 읽기 전용 도메인 컨트롤러 및 읽기 전용 도메인 컨트롤러
서비스 및 응용 프로그램 공급 업체는 서비스가 실행 되도록 계획 된 동일한 유형의 도메인 컨트롤러 (즉, 쓰기 가능 또는 읽기 전용 도메인 컨트롤러)를 사용 하 여 복제를 테스트 해야 합니다.
