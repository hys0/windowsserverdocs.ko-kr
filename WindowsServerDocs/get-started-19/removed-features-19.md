---
title: 제거 되었거나 Windows Server 2019에서 제거 될 예정인 기능
description: 기능 및 제거 또는 Windows Server 2019부터 제거 될 예정인 기능에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: jasgro
ms.date: 03/29/2019
ms.localizationpriority: medium
ms.openlocfilehash: 470857616a9b36d238de031b4ccf80a68eff1e61
ms.sourcegitcommit: 971f6538e8d89af84ef50fc8aab2188bdf6f47cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "9279134"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>제거 되었거나 Windows Server 2019 교체 될 예정인 기능

>적용 대상: WindowsServer 2019

Windows Server의 개별 릴리스에는 새로운 기능이 추가됩니다. 또한 더 나은 옵션이 추가되어 기능을 제거하는 경우도 종종 있습니다. Windows Server 2019에서 제거 된 특징과 기능에 대 한 자세한 내용은 다음과 같습니다.   

> [!TIP]
> - [Windows 참가자 프로그램](https://insider.windows.com)에 가입하여 Windows Server 빌드에 대한 초기 액세스를 얻을 수 있습니다. 이는 변경된 기능을 테스트하는 좋은 방법입니다.
> - 다른 릴리스에 대한 질문이 있습니까? [Windows Server, 버전 1803](../get-started/windows-server-1803-removed-features.md), [Windows Server, 버전 1709](../get-started/removed-features-1709.md), 및 [Windows Server 2016](../get-started/deprecated-features.md)에 대 한 정보를 확인 합니다.

**이 목록은 변경될 수 있으며 영향을 받는 기능이 일부 생략되었을 수 있습니다.** 

## <a name="features-we-removed-in-this-release"></a>이 릴리스에서 제거된 기능

Windows Server 2019의 설치 제품 이미지에서 다음 특징과 기능을 제거는 예정입니다. 대체 방법을 사용하지 않는 경우 이러한 기능에 의존하는 응용 프로그램 또는 코드는 이 릴리스에서 작동하지 않습니다.   

|기능    |대체 기능|
|-----------|--------------------
|분산 스캔 관리(DSM)라고도 하는 비즈니스 스캔|이 보안 스캔 및 스캐너 관리 기능을 제거는 예정-이 기능을 지 원하는 디바이스가 없는 것입니다.|
|구성 요소-Server Core 설치에 대 한 이제 선택적 구성 요소를 인쇄 합니다.|이전 버전의 Windows Server, 인쇄 구성 요소는 Server Core 설치 옵션에는 기본적으로 *사용 하지 않도록 설정* 되었습니다. Windows Server 2016에서는 기본적으로 활성화 하지는 변경 했습니다. Windows Server 2019의 인쇄 해당 구성 요소는 다시 한 번 기본적으로 Server Core에 대 한 비활성화 됩니다. 인쇄 구성 요소를 사용 하도록 설정 해야 할 경우 **설치 WindowsFeature 인쇄 서버** cmdlet을 실행 하 여 하면 됩니다.|
|Server Core 설치의 [원격 데스크톱 연결 브로커 및 원격 데스크톱 가상화 호스트](../remote/remote-desktop-services/desktop-hosting-service.md)|대부분의 원격 데스크톱 서비스 배포는 원격 데스크톱 세션 호스트(RDSH)와 함께 위치하는 역할을 가지며, 이를 위해 데스크톱 환경 포함 서버가 필요합니다. RDSH와 일관성을 유지하기 위해 이러한 역할에 대해서도 데스크톱 환경 포함 서버를 요구하도록 변경하고 있습니다. 이러한 RDS 역할 [Server Core 설치](../administration/server-core/what-is-server-core.md)에 사용 하기 위해 사용할 수 없게 됩니다. [원격 데스크톱 인프라의 일부로 이러한 역할을 배포](../remote/remote-desktop-services/rds-deploy-infrastructure.md)해야 하는 경우 [데스크톱 환경 포함 Windows Server에서 설치할](../get-started/getting-started-with-server-with-desktop-experience.md)수 있습니다. <br/><br/>이러한 역할은 Windows Server 2019의 데스크톱 경험 설치 옵션에도 포함됩니다. |



## <a name="features-were-no-longer-developing"></a>더 이상 개발하지 않는 기능

이러한 기능은 더 이상 적극적으로 개발 중인 하 고 향후 업데이트에서 제거할 수 없습니다. 일부 기능이 다른 기능으로 대체되었으며 일부 기능은 이제 다른 소스에서 사용할 수 있습니다. 

이러한 기능에 대한 교체 제안에 대한 피드백이 있는 경우 [피드백 허브 앱](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)을 사용할 수 있습니다. 

|기능    |대체 기능|
|-----------|---------------------|
|Hyper-v에서 키 저장소 드라이브|Hyper-v에서 키 저장소 드라이브 기능에서 더 이상 노력 합니다. 1 세대 Vm을 사용 하는 경우 앞으로 옵션에 대 한 정보에 대 한 [세대 1 VM 가상화 보안](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v) 아웃 확인 합니다. 만드는 경우 새 Vm 보다 안전한 솔루션에 대 한 TPM 장치와 2 세대 가상 컴퓨터를 사용 합니다. |
|신뢰할 수 있는 플랫폼 모듈 (TPM) 관리 콘솔|TPM 관리 콘솔에서 이전에 제공 되는 정보는 [Windows Defender 보안 센터](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)의 [**장치 보안**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security) 페이지에 출시 되었습니다.|
|호스트 보호 서비스 Active Directory 증명 모드|호스트 보호 서비스 Active Directory 증명 모드 더 이상 개발-대신 [호스트 키 증명](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)을 훨씬 더 간단 하 고 Active Directory 기반 증명으로 호환 동일 하 게 하는 새 증명 모드를 추가 했습니다.  이 새로운 모드 설정 경험, 간단한 관리 및 Active Directory 증명 보다 더 적은 인프라 종속성을 사용 하 여 해당 하는 기능을 제공합니다. 호스트 키 증명에 어떤 Active Directory 증명 필요 이상으로 추가 하드웨어 요구 사항이 없는 모든 기존 시스템 새 모드와 호환 유지 됩니다. 증명 옵션에 대 한 자세한 내용은 [배포 호스트 보호 된](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md) 문서를 참조 하세요.|
|OneSync 서비스|OneSync 서비스는 메일, 일정 및 사용자가 앱에 대 한 데이터를 동기화합니다. Outlook 앱 동일한 동기화를 제공 하는 동기화 엔진을 추가 했습니다.|
|원격 차등 압축 API 지원|원격 차등 압축 API 지원 네트워크를 통해 전송 되는 데이터의 양을 최소화 하는 압축 기술을 사용 하 여 원격 원본 데이터 동기화를 사용할 수 있습니다. 이 지원은 Microsoft 제품에서 현재 사용 하지 않습니다.|
|WFP 경량 필터 스위치 확장|WFP 경량 필터 스위치 확장 사용 하면 [간단한 네트워크 패킷 필터링 확장에 대 한 Hyper-v 가상 스위치](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering)를 만들 수 있습니다. 필터링 하는 전체 확장을 만들어 동일한 기능을 얻을 수 있습니다. 따라서 우리 제거 됩니다이 확장 나중에.|

