---
title: Windows Server 버전 1803 - 제거된 기능
description: Windows Server 버전 1803 또는 이후 버전에서 지원이 중단되거나 제거될 기능에 대해 설명합니다.
ms.prod: windows-server
ms.mktglfcycl: plan
ms.localizationpriority: medium
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.date: 10/22/2019
ms.openlocfilehash: c3c948e447d060d1ce733778c3362d83ad116708
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948208"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1803"></a>Windows Server, 버전 1803부터 제거되었거나 교체 예정인 기능

> 적용 대상: Windows Server, 버전 1803

Windows Server의 개별 릴리스에는 새로운 기능이 추가됩니다. 또한 더 나은 옵션이 추가되어 기능을 제거하는 경우도 종종 있습니다. Windows Server 버전 1803에서 제거된 기능에 대한 자세한 내용은 다음과 같습니다.   

> [!TIP]
> - [Windows 참가자 프로그램](https://insider.windows.com)에 가입하여 Windows Server 빌드에 대한 초기 액세스를 얻을 수 있습니다. 이는 변경된 기능을 테스트하는 좋은 방법입니다.
> - 다른 릴리스에 대한 질문이 있습니까? [Windows Server에서 제거되었거나 교체 예정인 기능](../get-started-19/removed-features.md)을 확인하세요.

**이 목록은 변경될 수 있으며 영향을 받는 기능이 일부 생략되었을 수 있습니다.** 

## <a name="features-we-removed-in-this-release"></a>이 릴리스에서 제거된 기능

Windows Server 버전 1803에서 설치된 제품 이미지에서 다음과 같은 기능을 제거했습니다. 대체 방법을 사용하지 않는 경우 이러한 기능에 의존하는 애플리케이션 또는 코드는 이 릴리스에서 작동하지 않습니다.   

| 기능    | 대체 기능 |
| ----------- | -------------------- |
| [파일 복제 서비스](https://support.microsoft.com/help/4025991/windows-server-version-1709-no-longer-supports-frs)|Windows Server 2003 R2에서 도입된 파일 복제 서비스가 DFS 복제로 대체되었습니다. [SYSVOL을 사용하여 FRS를 사용하는 모든 도메인 컨트롤러를 DFS 복제로 마이그레이션](https://blogs.technet.microsoft.com/filecab/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol/)해야 합니다. |
| Hyper-V 네트워크 가상화(HNV)|이제 [네트워크 가상화](../networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)가 네트워크 컨트롤러, 소프트웨어 부하 분산, 사용자 정의 라우팅 및 액세스 제어 목록 또한 포함하는 [소프트웨어 정의 네트워킹](../networking/sdn/software-defined-networking.md)(SDN) 솔루션의 일부로 Windows Server에 포함됩니다. |

## <a name="features-were-no-longer-developing"></a>더 이상 개발하지 않는 기능

이러한 기능은 더 이상 적극적으로 개발되지 않으며 향후 업데이트에서 제거될 수 있습니다. 일부 기능이 다른 기능으로 대체되었으며 일부 기능은 이제 다른 소스에서 사용할 수 있습니다. 

>[!NOTE]
> 아래에서 설명하는 기능 및 역할 중 일부는 Windows Server 버전 1803에 제공된 Server Core 설치 옵션에 포함되지 않습니다. 해당 기능 및 역할은 데스크톱 경험 설치 옵션으로 Server에 *존재하며* 가장 최근에 Windows Server 2016과 함께 릴리스되었고 Windows Server 2019에서 다시 릴리스될 예정입니다.

이러한 기능에 대한 교체 제안에 대한 피드백이 있는 경우 [피드백 허브 앱](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)을 사용할 수 있습니다. 

| 기능 또는 역할    | 대체 기능 |
| ----------- | --------------------- |
| 분산 스캔 관리(DSM)라고도 하는 비즈니스 스캔|[스캔 관리 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759124\(v%3dws.11\))은 Windows Server 2008 R2에서 도입되었으며 기업에서의 보안 스캔 및 스캔 프로그램의 관리를 지원합니다. 이 기능에는 더 이상 투자하지 않으며 이 기능을 지원하는 디바이스가 제공되지 않습니다. |
| IPv4/6 전환 기술(6to4, ISATAP, 직접 터널)|6to4는 Windows 10 버전 1607(1주년 업데이트)부터, ISATAP는 Windows 10 버전 1703(크리에이터스 업데이트)부터 기본적으로 사용할 수 없으며, 직접 터널은 이전부터 항상 기본적으로 사용할 수 없습니다. 대신 기본 IPv6 지원을 사용하세요. |
| [MultiPoint 서비스](../remote/multipoint-services/multipoint-services.md)|더 이상 Windows Server의 일부로 MultiPoint 서비스 역할을 개발하지 않습니다. MultiPoint 커넥터 서비스는 Windows Server 및 Windows 10에 대한 [주문형 기능](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)을 통해 사용할 수 있습니다. [원격 데스크톱 서비스](../remote/remote-desktop-services/welcome-to-rds.md), 특히 원격 데스크톱 서비스 세션 호스트를 사용하여 RDP 연결을 제공할 수 있습니다. |
| [오프라인 기호 패키지](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)(디버그 기호 MSI)|더 이상 기호 패키지를 다운로드 가능한 MSI로 사용할 수 없습니다. 대신, [Microsoft 기호 서버를 Azure 기반 기호 저장소로 이동](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/)하고 있습니다. Windows 기호가 필요한 경우 Microsoft 기호 서버에 연결하여 기호를 로컬로 캐시하거나 인터넷에 액세스할 수 있는 컴퓨터에서 SymChk.exe로 매니페스트 파일을 사용합니다. |
| Server Core 설치의 [원격 데스크톱 연결 브로커 및 원격 데스크톱 가상화 호스트](../remote/remote-desktop-services/desktop-hosting-service.md)|대부분의 원격 데스크톱 서비스 배포는 원격 데스크톱 세션 호스트(RDSH)와 함께 위치하는 역할을 가지며, 이를 위해 데스크톱 환경 포함 서버가 필요합니다. RDSH와 일관성을 유지하기 위해 이러한 역할에 대해서도 데스크톱 환경 포함 서버를 요구하도록 변경하고 있습니다. 더 이상 [Server Core 설치](../administration/server-core/what-is-server-core.md)에 사용하기 위해 이러한 RDS 역할을 개발하지 않습니다. [이러한 역할을 원격 데스크톱 인프라의 일부로 배포](../remote/remote-desktop-services/rds-deploy-infrastructure.md)해야 하는 경우 [데스크톱 환경 포함 Windows Server 2016에 설치할](getting-started-with-server-with-desktop-experience.md) 수 있습니다. <br/><br/>이러한 역할은 Windows Server 2019의 데스크톱 경험 설치 옵션에도 포함됩니다. [Windows Server 2019의 Windows 참가자 빌드](https://docs.microsoft.com/windows-insider/at-work/)에서 테스트할 수 있습니다. LTSC 이미지를 선택하도록 하십시오. |
| [RemoteFX 3D 비디오 어댑터(vGPU)](../remote/remote-desktop-services/rds-remotefx-vgpu.md)|가상화된 환경에 대한 새 그래픽 가속 옵션을 개발하고 있습니다. 대신 [개별 디바이스 할당(DDA)](../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)을 사용할 수도 있습니다. |
| 그룹 정책의 [소프트웨어 제한 정책](../identity/software-restriction-policies/software-restriction-policies.md)|사용자가 액세스할 수 있는 앱과 커널에서 실행할 수 있는 코드를 제어하기 위해 그룹 정책을 통해 소프트웨어 제한 정책을 사용하는 대신 [AppLocker](https://docs.microsoft.com/windows/security/threat-protection/applocker/applocker-overview) 또는 [Windows Defender Application Control](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control)을 사용할 수 있습니다. |
| SAS 패브릭을 사용하는 공유 구성의 스토리지 공간|대신 [스토리지 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)를 배포합니다. [스토리지 공간 다이렉트 하드웨어 요구 사항](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)에 설명된 대로 스토리지 공간 다이렉트는 비공유 구성에서 HLK 인증 SAS 엔클로저의 사용을 지원합니다. |
| Windows Server Essentials Experience|Windows Server Standard 또는 Windows Server Datacenter SKU에 대해 더 이상 Essentials 환경 역할을 개발하지 않습니다. 중소 규모 기업을 위해 사용하기 쉬운 서버 솔루션을 필요로 하는 경우 이 새로운 [Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business) 솔루션을 확인하거나 [Windows Server 2016 Essentials](https://docs.microsoft.com/windows-server-essentials/get-started/get-started)를 사용하세요. |

