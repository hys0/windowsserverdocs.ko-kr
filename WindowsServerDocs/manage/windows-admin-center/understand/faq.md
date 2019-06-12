---
title: Windows Admin Center 질문과 대답
description: Windows Admin Center에 대한 대답 확인(Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.openlocfilehash: 5c306dd181d4db400e6ab5bab919399fdebca9f3
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811669"
---
# <a name="windows-admin-center-frequently-asked-questions"></a>Windows Admin Center 질문과 대답

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

다음은 Windows Admin Center에 대한 가장 일반적으로 묻는 질문과 대답입니다.

## <a name="what-is-windows-admin-center"></a>Windows Admin Center란?

Windows Admin Center는 브라우저 기반 경량 GUI 플랫폼이자, Windows Server 및 Windows 10을 관리하는 IT 관리자를 위한 도구 세트입니다. 서버 관리자 및 MMC(Microsoft Management Console)와 같은 친숙한 기본 제공 관리 도구의 현대화된 단순한 통합 및 보안 환경으로의 혁신입니다.

## <a name="can-i-use-windows-admin-center-in-production-environments"></a>프로덕션 환경에서 Windows Admin Center를 사용할 수 있습니까?

예 Windows Admin Center는 일반적으로 사용 가능하고 광범위한 사용 및 프로덕션 배포에 준비되어 있습니다. 현재 플랫폼 기능 및 핵심 도구에는 Microsoft의 표준 릴리스 조건 및 유용성, 안정성, 성능, 내게 필요한 옵션, 보안 및 채택에 대 한 우리의 품질 기준을 충족합니다.

[!INCLUDE [support-policy](../includes/support-policy.md)]

## <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Windows Admin Center를 사용하는 비용은 얼마입니까?

Windows Admin Center는 Windows 이외에 추가 비용이 들지 않습니다. 유효한 Windows Server 또는 Windows 10 라이선스를 가지고 추가 비용 없이 Windows Admin Center(별도 다운로드를 통해 사용 가능)를 사용할 수 있습니다. Windows 추가 EULA에 의해 사용권이 부여됩니다.

## <a name="what-versions-of-windows-server-can-i-manage-with-windows-admin-center"></a>Windows Admin Center를 통해 관리할 수 있는 Windows Server 버전은 무엇입니까?

Windows Server 2019 릴리스에서 주요 테마를 사용 하도록 설정 하려면 Windows Server 2019에 대 한 Windows Admin Center 최적화 됩니다: 특히 하이브리드 클라우드 시나리오 및 하이퍼 수렴 형 인프라 관리 합니다. Windows Admin Center Windows Server 2019를 사용 하 여 가장 잘 작동 하지만 다양 한 고객은 이미 사용 하는 버전 관리를 지원 합니다. Windows Server 2012 및 최신 완전히 지원 됩니다. Windows Server 2008 R2 관리에 대 한 제한 된 기능 이기도 합니다.

## <a name="is-windows-admin-center-a-complete-replacement-for-all-traditional-in-box-and-rsat-tools"></a>Windows Admin Center가 모든 기존의 기본 제공 및 RSAT 도구를 대체할 수 있나요?

아니요. Windows Admin Center는 여러 일반적인 시나리오를 관리할 수는 있지만 기존의 모든 MMC(Microsoft Management Console) 도구를 완전히 대신하지 않습니다. 에 자세히 살펴보고 Windows Admin Center 사용 하 여 포함 된 도구에 대해 자세히 알아보세요 [서버 관리](../use/manage-servers.md) 설명서에 있습니다. Windows Admin Center는 해당 서버 관리자 솔루션에서 다음과 같은 주요 기능이 있습니다.

* 리소스 및 리소스 사용률 표시
* 인증서 관리
* 장치 관리
* 이벤트 뷰어
* 파일 탐색기
* 방화벽 관리
* 설치 된 앱 관리
* 로컬 사용자 및 그룹 구성
* 네트워크 설정
* 프로세스 보기/종료 및 프로세스 덤프 만들기
* 레지스트리 편집
* 예약 된 작업 관리
* Windows 서비스 관리
* 역할 및 기능 활성화/비활성화
* Hyper-V VM 및 가상 스위치 관리
* 저장소 관리
* 저장소 복제본 관리
* Windows 업데이트 관리
* PowerShell 콘솔
* 원격 데스크톱 연결

Windows Admin Center는 또한 이러한 솔루션을 제공합니다.

* 컴퓨터 관리 - Windows 10 클라이언트 PC를 관리하기 위한 서버 관리자 기능 중 일부를 제공합니다.
* 장애 조치 클러스터 관리자 - 장애 조치 클러스터 및 클러스터 리소스에 대한 지속적인 관리를 지원합니다.
* 하이퍼 컨버지드 클러스터 관리자 - 저장소 공간 다이렉트 및 Hyper-V에 완전히 새로운 맞춤형 경험을 제공합니다. 대시보드 기능과 차트 및 모니터링 알림을 강조합니다.

Active Directory, DHCP, DNS, IIS 등의 역할이 아직 Windows Admin Center에 표시되는 관리 기능과 동등한 기능을 갖추지 않았기 때문에 Windows Admin Center는 RSAT(원격 서버 관리 도구)를 보완하며 이를 대체하지 않습니다.

## <a name="can-windows-admin-center-be-used-to-manage-the-free-microsoft-hyper-v-server"></a>무료 Microsoft Hyper-V Server를 관리하기 위해 Windows Admin Center를 사용할 수 있습니까?

예 Windows Admin Center는 Microsoft Hyper-V Server 2016 및 Microsoft Hyper-V Server 2012 R2를 관리하는데 사용할 수 있습니다.

## <a name="can-i-deploy-windows-admin-center-on-a-windows-10-computer"></a>Windows 10 컴퓨터에서 Windows Admin Center를 배포할 수 있습니까?

예, Windows Admin Center는 데스크톱 모드에서 실행되는 Windows 10(버전 1709 이상)에 설치할 수 있습니다.  Windows Admin Center 게이트웨이 모드에서 큰 또는 Windows Server 2016을 사용 하 여 서버에 설치 되어 있을 수도 있습니다 및 Windows 10 컴퓨터에서 웹 브라우저를 통해 액세스 합니다. [설치 옵션에 대해 자세히 알아보세요](../plan/installation-options.md).

## <a name="ive-heard-that-windows-admin-center-uses-powershell-under-the-hood-can-i-see-the-actual-scripts-that-it-uses"></a>저도 들어 보았습니다 내부에서 PowerShell을 사용 하는 Windows Admin Center, 실제 스크립트를 사용 하 여 볼 수는?

예! 합니다 [Showscript 기능](../use/get-started.md#view-powershell-scripts-used-in-windows-admin-center) Windows Admin Center 미리 보기 1806에서 추가한 및 GA 채널에 포함 됩니다.

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-windows-server-2008-r2-or-earlier"></a>Windows Admin Center가 Windows Server 2008 R2 또는 이전 버전을 관리할 계획이 있습니까?

Windows Admin Center 지 원하는 **제한** Windows Server 2008 R2를 관리 하는 기능입니다. Windows Admin Center는 Windows Server 2008 R2 및 이전에서는 존재하지 않는 PowerShell 기능 및 플랫폼 기술에 의존하므로 완전한 지원은 불가능합니다. Microsoft는 고객을 권장 하므로 Windows Server 2008/2008 R2 2020 년 1 월에에서 대 한 지원이 끝 도달 [Azure 또는 Windows Server의 최신 버전으로 업그레이드 하는 이동](https://www.microsoft.com/en-us/cloud-platform/windows-server-2008)합니다.

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-linux-connections"></a>Windows Admin Center가 Linux 연결을 관리할 계획이 있습니까?

고객 요청으로 인해 조사 하는 것 이지만 현재 계획은 없습니다 잠긴를 배달 하려면 및 SSH를 통해 지원 콘솔 연결에만 구성 될 수 있습니다.

## <a name="which-web-browsers-are-supported-by-windows-admin-center"></a>Windows Admin Center는 어떤 웹 브라우저를 지원하나요?

최신 버전의 Microsoft Edge(Windows 10 버전 1709 이상) 및 Google Chrome 브라우저가 Windows 10에서 테스트 및 지원됩니다. [브라우저 보기 관련 알려진 문제](../support/known-issues.md#browser-specific-issues)합니다. 다른 최신 웹 브라우저 또는 다른 플랫폼의 일부분이 아닌 현재 우리 테스트 매트릭스 및 되지 않으므로 *공식적으로* 지원 합니다.

## <a name="how-does-windows-admin-center-handle-security"></a>Windows Admin Center가 보안을 어떻게 처리합니까?

브라우저에서 Windows Admin Center 게이트웨이로의 트래픽은 HTTPS를 사용합니다. 게이트웨이에서 관리되는 서버로의 트래픽은 WinRM을 통한 표준 PowerShell 및 WMI입니다. LAPS(로컬 관리자 암호 솔루션), 리소스 기반 제한 위임, AD 또는 Azure AD를 사용하는 게이트웨이 액세스 제어, 대상 서버 관리를 위한 역할 기반 액세스 제어를 지원합니다.

## <a name="does-windows-admin-center-use-credssp"></a>Windows Admin Center CredSSP를 사용 하나요?

예, 몇 가지 사례 Windows Admin Center CredSSP에 필요합니다. 이 인증에 대 한 자격 증명 관리를 위한 대상으로 하는 특정 서버 이외의 컴퓨터에 전달 해야 합니다. 예를 들어, 가상 컴퓨터에서 관리 하는 경우 **서버 B**, 해당 가상 컴퓨터의 vhdx 파일에서 호스트 되는 파일 공유에 저장 하지만 **서버 C**, Windows Admin Center CredSSP를 사용 해야 합니다 사용 하 여 인증 **서버 C** 파일 공유에 액세스할 수 있습니다.

Windows Admin Center CredSSP 구성에서 승인 확인 한 후에 자동으로 처리 합니다. CredSSP를 구성 하기 전에 Windows Admin Center 최근 CredSSP가 있는지 확인 [업데이트](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)합니다. 서버 개요에 해당-를 사용 하지 않도록 설정 하는 옵션이 배지가 됩니다 CredSSP를 사용 하는 동안

![CredSSP 서버 개요](../media/CredSSP-overview.png)

CredSSP는 다음 영역에서 현재 사용 됩니다.

- 세분화 된 virtual machines 도구 (위 예입니다.)에서 SMB 저장소를 사용 하 여
- 업데이트를 사용 하 여 도구에 장애 조치 또는 하이퍼 수렴 형 클러스터 관리 솔루션을 수행 하는 [클러스터 인식 업데이트](https://docs.microsoft.com/windows-server/failover-clustering/cluster-aware-updating) 

## <a name="are-there-any-cloud-dependencies"></a>클라우드 종속성이 있습니까?

Windows Admin Center에는 인터넷 액세스가 필요하지 않으므로 Microsoft Azure가 필요하지 않습니다. Windows Admin Center는 실제 시스템이나 모든 하이퍼바이저의 가상 컴퓨터, 또는 모든 클라우드에서 실행되는 Windows Server 및 Windows 인스턴스를 관리합니다. 시간의 흐름에 따라 다양한 Azure 서비스와의 통합이 추가될 예정이지만 선택적인 부가 가치 기능이며 Windows Admin Center를 사용하기 위한 필수 사항은 아닙니다.

## <a name="are-there-any-other-dependencies-or-prerequisites"></a>기타 종속성 또는 필수 구성 요소가 있습니까?

Windows Admin Center는 Windows 10 Fall Anniversary Update(1709) 이상 또는 Windows Server 2016 이상에 설치할 수 있습니다. Windows Server 2008 R2, 2012, 또는 2012 R2를 관리하려면 해당 서버에 Windows Management Framework 5.1을 설치해야 합니다. 다른 종속성은 없습니다. IIS와, 에이전트, SQL Server는 필요하지 않습니다.

## <a name="what-about-extensibility-and-3rd-party-support"></a>확장성 및 타사 지원은 어떻게 됩니까?

Windows Admin Center 사용자가 자신의 확장을 쓸 수 있도록 사용 가능한 SDK에 있습니다. 플랫폼으로서 에코 시스템 확장 및 파트너 확장성 지원이 처음부터 주요 우선 순위입니다. [Windows Admin Center SDK에 대한 자세한 내용을 읽어보십시오](../extend/extensibility-overview.md).

## <a name="can-i-manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Windows Admin Center를 사용하여 하이퍼 컨버지드 인프라를 관리할 수 있습니까?

예 Windows Admin Center Windows Server 2016 또는 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터의 관리를 지원 합니다. 하이퍼 수렴 형 클러스터 관리자 솔루션 Windows Admin Center 이전에 미리 보기로 제공에서 되었지만 이제 **공급**, 미리 보기에서 몇 가지 새로운 기능을 사용 하 여 합니다. 자세한 내용은 [하이퍼 컨버지드 인프라 관리에 대해 자세히 읽어보세요](../use/manage-hyper-converged.md).

## <a name="does-windows-admin-center-require-system-center"></a>Windows Admin Center에 System Center가 필요합니까?

아니요. Windows Admin Center는 System Center를 보완하지만 System Center가 필요하지는 않습니다. [Windows Admin Center 및 System Center에 대 한 자세한 정보를 읽을](related-management.md#system-center)합니다.

## <a name="can-windows-admin-center-replace-system-center-virtual-machine-manager-scvmm"></a>Windows Admin Center가 SCVMM(System Center Virtual Machine Manager)를 대체할 수 있습니까?

Windows Admin Center 및 SCVMM은 상호 보완적입니다. Windows Admin Center는 기존 MMC(Microsoft Management Console) 스냅인 및 서버 관리자 환경을 대체하기 위해 고안되었습니다.  Windows Admin Center는 SCVMM의 모니터링 측면을 대체하기 위해 고안된 것이 아닙니다. [Windows Admin Center 및 System Center에 대 한 자세한 정보를 읽을](related-management.md#system-center)합니다.

## <a name="what-is-windows-admin-center-preview-which-version-is-right-for-me"></a>Windows Admin Center 미리 보기는 무엇이며, 나에게 적합한 버전은 무엇입니까?

Windows Admin Center는 두 버전으로 다운로드할 수 있습니다.

### <a name="windows-admin-center"></a>Windows Admin Center

* 자주 업데이트할 수 없거나 프로덕션 환경에서 사용하는 릴리스에 대한 추가 유효성 검사를 원하는 IT 관리자에게 이 버전이 적합합니다. 현재 일반 공급 (GA) 릴리스는 Windows Admin Center 1904입니다.
* [!INCLUDE [support-policy](../includes/support-policy.md)]
* 최신 릴리스를 가져오려는 [여기에서 다운로드](https://aka.ms/WACDownload)합니다.

### <a name="windows-admin-center-preview"></a>Windows Admin Center 미리 보기

> [!NOTE]
> 현재 GA 버전 (Windows Admin Center 1904)는 모든 이전 미리 보기 기능을 포함합니다.
> Insider Preview는 향후 몇 개월 내에 반환 됩니다.

* 일반 흐름에서 최신 및 최고의 기능을 원하는 IT 관리자에게 이 버전이 적합합니다. 우리의 목적은 후속 업데이트 해제 매월 제공 하는 것 정도입니다. 핵심 플랫폼은 계속해서 프로덕션을 지원하며 라이선스는 프로덕션 사용권을 제공합니다. 그러나 미리 보기로 명확하게 표시된 평가 및 테스트에 적합한 새로운 도구와 기능이 도입될 것입니다.
* 등록 된 참가자 최신 Insider Preview 릴리스를 가져오려면 Windows Admin Center 미리 보기에서 직접 다운로드할 수는 [Windows Server Insider Preview 다운로드 페이지](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), 추가 다운로드 드롭다운 목록에서. 아직 참가자로 등록하지 않은 경우 Windows 비즈니스용 참가자 포털에서 [Windows Server 시작](https://insider.windows.com/en-us/for-business-getting-started-server/)을 참조합니다.

## <a name="why-was-windows-admin-center-chosen-as-the-final-name-for-project-honolulu"></a>"Windows Admin Center"가 "Project Honolulu"의 최종 이름으로 선택된 이유는 무엇입니까?

Windows Admin Center는 "Project Honolulu"의 공식 제품 이름이며 다양한 핵심 관리 시나리오에서 IT 관리자를 위한 통합된 환경의 비전을 강화합니다. 또한 투자 방식 및 제공 사항에 중요한 IT 관리자의 사용자 요구에 대한 고객 포커스를 강조합니다.

## <a name="where-can-i-learn-more-about-windows-admin-center-or-get-more-details-on-the-topics-above"></a>어디에서 Windows Admin Center에 대한 자세한 내용이나 위의 항목에 대해 더 많은 세부 정보를 가져올 수 있습니까?

[시작 페이지](https://aka.ms/WindowsAdminCenter)는 시작할 수 있는 최고의 지점이며 새로 분류된 설명서 콘텐츠, 다운로드 위치, 피드백, 참조 정보 및 기타 리소스를 제공하는 방법에 대한 링크를 제공합니다.

## <a name="what-is-the-version-history-of-windows-admin-center"></a>Windows Admin Center 버전 기록을 란?

[여기 버전 기록을 봅니다.](../overview.md#release-history)

## <a name="im-having-an-issue-with-windows-admin-center-where-can-i-get-help"></a>Windows Admin Center와 관련하여 문제가 있습니다. 어디에서 도움을 얻을 수 있습니까?

[문제 해결 가이드](../use/troubleshooting.md)와 [알려진 문제](../use/known-issues.md) 목록을 참조하십시오.
