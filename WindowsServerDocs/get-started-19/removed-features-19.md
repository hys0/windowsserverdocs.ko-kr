---
title: 기능 제거 또는 Windows Server 2019 제거에 대 한 계획
description: 기능 및 Windows Server 2019부터 제거 되었거나 제거 기능에 알아봅니다.
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
ms.date: 05/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 820dfed8a0a58d3ccc64023325c373b761461ba8
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/27/2019
ms.locfileid: "65976519"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>기능 제거 또는 교체를 시작 하는 Windows Server 2019에 대 한 계획

>적용 대상: Windows Server 2019

Windows Server의 개별 릴리스에는 새로운 기능이 추가됩니다. 또한 더 나은 옵션이 추가되어 기능을 제거하는 경우도 종종 있습니다. 기능 및 Windows Server 2019에서 제거 하는 기능에 대 한 세부 정보는 다음과 같습니다.

> [!TIP]
> - [Windows 참가자 프로그램](https://insider.windows.com)에 가입하여 Windows Server 빌드에 대한 초기 액세스를 얻을 수 있습니다. 이는 변경된 기능을 테스트하는 좋은 방법입니다.
> - 다른 릴리스에 대한 질문이 있습니까? 에 대 한 정보를 확인 하세요 [Windows Server의 새로운 기능](../get-started/whats-new-in-windows-server.md)합니다.

**목록은 변경 될 수 있습니다 하 고 모든 영향을 받는 기능 또는 기능을 포함 하지 않을 수 있습니다.** 

## <a name="features-we-removed-in-this-release"></a>이 릴리스에서 제거된 기능

Windows Server 2019에 설치 된 제품 이미지에서은 다음 기능 및 기능을 제거 하는 것입니다. 대체 방법을 사용하지 않는 경우 이러한 기능에 의존하는 응용 프로그램 또는 코드는 이 릴리스에서 작동하지 않습니다.

|기능    |대체 기능|
|-----------|--------------------
|분산 스캔 관리(DSM)라고도 하는 비즈니스 스캔|이 보안 검사 및 스캐너 관리 기능을 제거 하는 것-이 기능을 지 원하는 장치가 없습니다.|
|Server Core 설치에는 이제 선택적 구성 요소 구성 요소를 인쇄 합니다.|인쇄 구성 요소가 Windows Server의 이전 릴리스에서 *비활성화* Server Core 설치 옵션에 기본적으로 합니다. Windows Server 2016에서 기본적으로 사용 하도록 설정 하는 변경 했습니다. Windows Server 2019 인쇄 해당 구성 요소는 다시 한 번 기본적으로 Server Core에 대 한 비활성화 됩니다. 인쇄 구성 요소를 사용 하도록 설정 해야 할 경우 있습니다 이렇게 실행 합니다 **Install-windowsfeature 인쇄 서버** cmdlet.|
|Server Core 설치의 [원격 데스크톱 연결 브로커 및 원격 데스크톱 가상화 호스트](../remote/remote-desktop-services/desktop-hosting-service.md)|대부분의 원격 데스크톱 서비스 배포는 원격 데스크톱 세션 호스트(RDSH)와 함께 위치하는 역할을 가지며, 이를 위해 데스크톱 환경 포함 서버가 필요합니다. RDSH와 일관성을 유지하기 위해 이러한 역할에 대해서도 데스크톱 환경 포함 서버를 요구하도록 변경하고 있습니다. 이러한 RDS 역할에서 사용 하기 위해 더 이상 사용할 수는 [Server Core 설치](../administration/server-core/what-is-server-core.md)합니다. 해야 할 경우 [원격 데스크톱 인프라의 일부로 이러한 역할을 배포할](../remote/remote-desktop-services/rds-deploy-infrastructure.md)를 할 수 있습니다 [데스크톱 환경 포함 Windows Server에 설치](../get-started/getting-started-with-server-with-desktop-experience.md)합니다. <br/><br/>이러한 역할은 Windows Server 2019의 데스크톱 경험 설치 옵션에도 포함됩니다. |

## <a name="features-were-no-longer-developing"></a>더 이상 개발하지 않는 기능

이러한 기능을 더 이상 적극적으로 개발 하 고 향후 업데이트에서이 제거할 수 없습니다. 일부 기능이 다른 기능으로 대체되었으며 일부 기능은 이제 다른 소스에서 사용할 수 있습니다. 

이러한 기능에 대한 교체 제안에 대한 피드백이 있는 경우 [피드백 허브 앱](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)을 사용할 수 있습니다. 

| 기능   | 대체 기능 |
|-----------|---------------------|
| Hyper-v에서 키 저장소 드라이브|Hyper-v에서 키 저장소 드라이브 기능이 더 이상 작업 중입니다. 1 세대 Vm을 사용 하는 경우 체크 아웃 [세대 1 VM 가상화 보안](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v) 옵션 앞에 대 한 정보에 대 한 합니다. 만드는 경우 새 Vm 보다 안전한 솔루션에 대 한 TPM 장치를 사용 하 여 2 세대 가상 컴퓨터를 사용 합니다. |
| 신뢰할 수 있는 플랫폼 모듈 (TPM) 관리 콘솔|TPM 관리 콘솔에서 이전에 제공 되는 정보에 제공 됩니다. 합니다 [ **장치 보안** ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) 페이지를 [Windows Defender 보안 센터](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)합니다. |
| 호스트 보호자 서비스에 대 한 Active Directory 증명 모드|호스트 보호자 서비스에 대 한 Active Directory 증명 모드를 더 이상 개발 하는 것-대신 새 증명 모드를 추가 했습니다 [호스트 키 증명](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md), 훨씬 더 간단 하 고 동일 하 게 Active Directory 기반과 호환 되는 증명 합니다.  이 새로운 모드는 설치 환경, 간편해 진 관리 및 Active Directory 증명 보다 더 적은 인프라 종속성을 사용 하 여 동일한 기능을 제공 합니다. 호스트 키 증명 필요한 어떤 Active Directory 증명 이외의 추가 하드웨어 요구 사항이 없습니다 있으므로 모든 기존 시스템에 새 모드와 호환 상태로 유지 됩니다. 참조 [보호 된 호스트 배포](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md) 증명 옵션에 대 한 자세한 내용은 합니다. |
| OneSync 서비스|OneSync 서비스 메일, 일정 및 사용자 앱에 대 한 데이터를 동기화합니다. 동일한 동기화를 제공 하는 Outlook 앱에 동기화 엔진을 추가 했습니다. |
| 원격 차등 압축 API 지원|네트워크를 통해 전송 되는 데이터 양을 최소화 하는 압축 기술을 사용 하 여 원격 소스와 데이터 동기화를 사용 하는 원격 차등 압축 API 지원 합니다. 이 지원은 Microsoft 제품에서 현재 사용 되지 않습니다. |
| WFP 간단한 필터 스위치 확장|WFP 간단한 필터 스위치 확장에는 개발자가 만들 수 [Hyper-v 가상 스위치 확장을 필터링 하는 단순한 네트워크 패킷](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering)합니다. 전체 필터링 확장 프로그램을 만들어 동일한 기능을 얻을 수 있습니다. 따라서 우리가에서는 제거할이 확장 나중에입니다. |