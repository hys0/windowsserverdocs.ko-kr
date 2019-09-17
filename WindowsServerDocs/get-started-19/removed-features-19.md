---
title: Windows Server 2019에서 제거되었거나 제거 예정인 기능
description: Windows Server 2019부터 제거되었거나 제거 예정인 기능에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: jasongerend
ms.author: jgerend
manager: jasgro
ms.date: 08/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0f6b6ac42c096c6c80404c2d650905e73da8a97a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868652"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>Windows Server 2019부터 제거되었거나 교체 예정인 기능

>적용 대상: Windows Server 2019

Windows Server의 개별 릴리스에는 새로운 기능이 추가됩니다. 또한 더 나은 옵션이 추가되어 기능을 제거하는 경우도 종종 있습니다. Windows Server 2019에서 제거된 기능에 대한 자세한 내용은 다음과 같습니다.

> [!TIP]
> - [Windows 참가자 프로그램](https://insider.windows.com)에 가입하여 Windows Server 빌드에 대한 초기 액세스를 얻을 수 있습니다. 이는 변경된 기능을 테스트하는 좋은 방법입니다.
> - 다른 릴리스에 대한 질문이 있습니까? [Windows Server에서 제거되었거나 교체 예정인 기능](removed-features.md)을 확인하세요.

**이 목록은 변경될 수 있으며 영향을 받는 기능이 일부 생략되었을 수 있습니다.** 

## <a name="features-we-removed-in-this-release"></a>이 릴리스에서 제거된 기능

Windows Server 2019에서 설치된 제품 이미지에서 다음과 같은 기능을 제거할 예정입니다. 대체 방법을 사용하지 않는 경우 이러한 기능에 의존하는 애플리케이션 또는 코드는 이 릴리스에서 작동하지 않습니다.

| 기능   | 대체 기능 |
| --------- | -------------------- |
| 분산 스캔 관리(DSM)라고도 하는 비즈니스 스캔|이 보안 스캔 및 스캐너 관리 기능을 제거할 예정입니다. 이 기능을 지원하는 디바이스가 없습니다. |
| 인쇄 구성 요소 - 현재 Server Core 설치에 대한 선택적 구성 요소|Windows Server의 이전 릴리스에서 인쇄 구성 요소는 Server Core 설치 옵션에서 기본적으로 *비활성화*되었습니다. Windows Server 2016에서는 기본적으로 활성화되도록 변경했습니다. Windows Server 2019에서 해당 인쇄 구성 요소는 Server Core에 대해 다시 한 번 기본적으로 비활성화됩니다. 인쇄 구성 요소를 활성화해야 하는 경우 **Install-WindowsFeature Print-Server** cmdlet을 실행하여 수행할 수 있습니다. |
| Server Core 설치의 [원격 데스크톱 연결 브로커 및 원격 데스크톱 가상화 호스트](../remote/remote-desktop-services/desktop-hosting-service.md)|대부분의 원격 데스크톱 서비스 배포는 원격 데스크톱 세션 호스트(RDSH)와 함께 위치하는 역할을 가지며, 이를 위해 데스크톱 환경 포함 서버가 필요합니다. RDSH와 일관성을 유지하기 위해 이러한 역할에 대해서도 데스크톱 환경 포함 서버를 요구하도록 변경하고 있습니다. 이러한 RDS 역할은 [Server Core 설치](../administration/server-core/what-is-server-core.md)에서 더 이상 사용할 수 없습니다. [이러한 역할을 원격 데스크톱 인프라의 일부로 배포](../remote/remote-desktop-services/rds-deploy-infrastructure.md)해야 하는 경우 [데스크톱 환경 포함 Windows Server에 설치할](../get-started/getting-started-with-server-with-desktop-experience.md) 수 있습니다. <br/><br/>이러한 역할은 Windows Server 2019의 데스크톱 경험 설치 옵션에도 포함됩니다. |

## <a name="features-were-no-longer-developing"></a>더 이상 개발하지 않는 기능

이러한 기능은 더 이상 적극적으로 개발되지 않으며 향후 업데이트에서 제거될 수 있습니다. 일부 기능이 다른 기능으로 대체되었으며 일부 기능은 이제 다른 소스에서 사용할 수 있습니다. 

이러한 기능에 대한 교체 제안에 대한 피드백이 있는 경우 [피드백 허브 앱](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)을 사용할 수 있습니다. 

| 기능     | 대체 기능 |
| ----------- | --------------------- |
| Hyper-V의 키 스토리지 드라이브|Hyper-V의 Key Storage Drive 기능에 대해 더 이상 사용하지 않습니다. 1세대 VM을 사용하는 경우 향후 옵션에 대한 정보는 [1세대 VM 가상화 보안](../virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v.md)을 참조하세요. 새 VM을 만드는 경우 보다 안전한 솔루션에 대한 TPM 디바이스로 2세대 가상 머신을 사용합니다. |
| TPM(신뢰할 수 있는 플랫폼 모듈) 관리 콘솔|TPM 관리 콘솔에서 이전에 제공되었던 정보는 이제 [Windows Defender 보안 센터](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)의 [**디바이스 보안**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) 페이지에서 제공됩니다. |
| 호스트 보호자 서비스 Active Directory 증명 모드|호스트 보호자 서비스 Active Directory 증명 모드를 더 이상 개발하지 않습니다. 대신 훨씬 더 간단하고 Active Directory 기반 증명과 동등하게 호환되는 새 증명 모드인 [호스트 키 증명](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)을 추가했습니다.  이 새 모드는 설정 환경과 동일한 기능, Active Directory 증명보다 간편한 관리 및 더 적은 인프라 종속성을 제공합니다. 호스트 키 증명에는 Active Directory 증명에서 필요한 것 이외의 추가 하드웨어 요구 사항이 없으므로 모든 기존 시스템은 새 모드와 호환 상태로 유지됩니다. 증명 옵션에 대한 자세한 내용은 [보호된 호스트 배포](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)를 참조하세요. |
| OneSync 서비스 | OneSync 서비스는 메일, 일정 및 사용자 앱에 대한 데이터를 동기화합니다. 동일한 동기화를 제공하는 동기화 엔진을 Outlook 앱에 추가했습니다. |
| 원격 차등 압축 API 지원 | 원격 차등 압축 API 지원을 통해 압축 기술을 사용하여 원격 소스와 데이터를 동기화하여 네트워크를 통해 전송되는 데이터의 양이 최소화되었습니다. |
| WFP 경량 필터 스위치 확장 | WFP 경량 필터 스위치 확장을 통해 개발자는 [Hyper-V 가상 스위치에 대한 단순 네트워크 패킷 필터링 확장](https://docs.microsoft.com/windows-hardware/drivers/network/using-virtual-switch-filtering)을 빌드할 수 있습니다. 전체 필터링 확장을 만들어 동일한 기능을 얻을 수 있습니다. 따라서 향후 이 확장을 제거할 예정입니다. |
