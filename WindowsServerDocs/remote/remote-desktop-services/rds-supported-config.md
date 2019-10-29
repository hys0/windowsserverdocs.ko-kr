---
title: 원격 데스크톱 서비스에 지원되는 구성
description: Windows Server 2016 및 Windows Server 2019에서 RDS에 지원되는 구성 관련 정보를 제공합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/22/2019
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c925c7eb-6880-411f-8e59-bd0f57cc5fc3
author: lizap
manager: dongill
ms.openlocfilehash: 7d4641e2bb40a9a70264c68d0268208a30f36a69
ms.sourcegitcommit: 3262c5c7cece9f2adf2b56f06b7ead38754a451c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72812304"
---
# <a name="supported-configurations-for-remote-desktop-services"></a>원격 데스크톱 서비스에 지원되는 구성

> 적용 대상: Windows Server 2016, Windows Server 2019

원격 데스크톱 서비스 환경에 지원되는 구성에 있어서 가장 큰 문제는 버전 상호 운용성인 경우가 많습니다. 대부분의 환경에는 여러 버전의 Windows Server가 포함되어 있습니다. 예를 들어 기존 Windows Server 2012 R2 RDS 배포가 있지만 새로운 기능(예: OpenGL\OpenCL, 개별 디바이스 할당 또는 스토리지 공간 다이렉트에 대한 지원)을 활용하기 위해 Windows Server 2016으로 업그레이드하려는 경우가 있습니다. 이때 여러 버전과 함께 작동할 수 있는 RDS 구성 요소는 무엇이고, 무엇을 동일하게 유지해야 하는지 궁금해질 것입니다.

이를 고려할 때 Windows Server의 원격 데스크톱 서비스에 지원되는 구성에 대한 기본 지침은 다음과 같습니다.

> [!NOTE]
> [Windows Server 2016의 시스템 요구 사항](../../get-started/system-requirements.md) 및 [Windows Server 2019의 시스템 요구 사항](../../get-started-19/sys-reqs-19.md)을 살펴보세요.

## <a name="best-practices"></a>모범 사례

- 원격 데스크톱 인프라(웹 액세스, 게이트웨이, 연결 브로커 및 라이선스 서버)에 Windows Server 2019를 사용합니다. Windows Server 2019는 이러한 구성 요소와 역호환됩니다. 즉, Windows Server 2016 또는 Windows Server 2012 R2 RD 세션 호스트는 2019 RD 연결 브로커에 연결할 수 있지만 그 반대로는 연결할 수 없습니다.

- RD 세션 호스트의 경우 컬렉션의 모든 세션 호스트가 동일한 수준에 있어야 하지만 여러 컬렉션이 있을 수 있습니다. Windows Server 2016 세션 호스트가 있는 컬렉션과 Windows Server 2019 세션 호스트가 있는 컬렉션이 있을 수 있습니다.

- RD 세션 호스트를 Windows Server 2019로 업그레이드하는 경우 라이선스 서버도 업그레이드하세요. 2019 라이선스 서버는 Windows Server 2003까지 모든 이전 Windows Server 버전의 CAL을 처리할 수 있습니다.

- [원격 데스크톱 서비스 환경 업그레이드](upgrade-to-rds.md#flow-for-deployment-upgrades)에서 권장되는 업그레이드 순서를 따르세요.

- 고가용성 환경을 만드는 경우 모든 연결 브로커가 동일한 OS 수준에 있어야 합니다.

## <a name="rd-connection-brokers"></a>RD 연결 브로커

Windows Server 2016은 Windows Server 2016을 실행하는 RDSH(원격 데스크톱 세션 호스트) 및 RDVH(원격 데스크톱 가상화 호스트) 사용 시 배포에 있는 연결 브로커 수에 대한 제한을 제거합니다. 다음 표는 3개 이상의 연결 브로커가 있는 고가용성 배포에서 연결 브로커의 2016 및 2012 R2 버전과 함께 작동하는 RDS 구성 요소 버전을 보여줍니다.

|HA의 연결 브로커 3개 이상|RDSH 또는 RDVH 2019|RDSH 또는 RDVH 2016|RDSH 또는 RDVH 2012 R2|
|---|---|---|---|
 |Windows Server 2019 연결 브로커|지원함|지원함|지원함|
 |Windows Server 2016 연결 브로커|해당 없음|지원함|지원함|
 |Windows Server 2012 R2 연결 브로커|해당 없음|해당 없음|지원되지 않음|

## <a name="support-for-graphics-processing-unit-gpu-acceleration"></a>GPU(그래픽 처리 장치) 가속 지원

원격 데스크톱 서비스는 GPU가 장착된 시스템을 지원합니다. 원격 연결을 통해 GPU가 필요한 애플리케이션을 사용할 수 있습니다. 또한 GPU 가속 렌더링 및 인코딩을 활성화하면 앱 성능과 확장성을 향상시킬 수 있습니다.

단독 세션 클라이언트 운영 체제인 원격 데스크톱 서비스 세션 호스트는 [Azure GPU 최적화된 가상 머신 크기](/en-us/azure/virtual-machines/windows/sizes-gpu), 실제 RDSH 서버에 사용할 수 있는 GPU, RemoteFX vGPU(Windows Server 2016) 및 지원되는 하이퍼바이저를 통해 VM에 제공된 GPU 등 다양한 방식으로 운영 체제에 제공되는 실제 또는 가상 GPU를 활용할 수 있습니다.

[나에게 적합한 그래픽 가상화 기술은 무엇일까요?](rds-graphics-virtualization.md)를 참조하여 필요한 것을 알아보세요. DDA에 대한 자세한 내용은 [개별 디바이스 할당 배포를 위한 계획](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)을 확인하세요.

GPU 공급업체는 RDSH 시나리오에 대해 별도의 라이선싱 체계를 갖거나 서버 OS에서 GPU 사용을 제한할 수 있으므로, 선호하는 공급업체와 요구 사항을 확인하세요.

타사 하이퍼바이저 또는 클라우드 플랫폼에서 제공하는 GPU에는 WHQL에서 디지털 서명되고, GPU 공급업체에서 제공되는 드라이버가 있어야 합니다.

### <a name="remote-desktop-session-host-support-for-gpus"></a>GPU를 위한 원격 데스크톱 세션 호스트 지원

다음 표는 다양한 버전의 RDSH 호스트에서 지원되는 시나리오를 보여줍니다.

|기능|Windows Server 2008 R2|Windows Server 2012 R2|Windows Server 2016|Windows Server 2019|
|---|---|---|---|---|
|모든 RDP 세션에 하드웨어 GPU 사용|아니오|예|예|예|
|H.264/AVC 하드웨어 인코딩(GPU에서 지원되는 경우)|아니오|아니오|예|예|
|OS에 제공되는 여러 GPU 간의 부하 분산|아니오|아니오|아니오|예|
|대역폭 사용을 최소화하기 위한 H.264/AVC 인코딩 최적화|아니오|아니오|아니오|예|
|4K 해상도를 위한 H.264/AVC 지원|아니오|아니오|아니오|예|

### <a name="vdi-support-for-gpus"></a>GPU를 위한 VDI 지원

다음 표는 클라이언트 OS의 GPU 시나리오에 대한 지원을 보여줍니다.

|기능|Windows 7 SP1|Windows 8.1|Windows 10|
|---|---|---|---|
|모든 RDP 세션에 하드웨어 GPU 사용|아니오|예|예|
|H.264/AVC 하드웨어 인코딩(GPU에서 지원되는 경우)|아니오|아니오|Windows 10 1703 이상|
|OS에 제공되는 여러 GPU 간의 부하 분산|아니오|아니오|Windows 10 1803 이상|
|대역폭 사용을 최소화하기 위한 H.264/AVC 인코딩 최적화|아니오|아니오|Windows 10 1803 이상|
|4K 해상도를 위한 H.264/AVC 지원|아니오|아니오|Windows 10 1803 이상|

### <a name="remotefx-3d-video-adapter-vgpu-support"></a>RemoteFX 3D 비디오 어댑터(vGPU) 지원

VM이 Windows Server 2012 R2 또는 Windows Server 2016에서 Hyper-V 게스트로 실행되는 경우 원격 데스크톱 서비스는 RemoteFX vGPU를 지원합니다. 다음 게스트 운영 체제는 RemoteFX vGPU를 지원합니다.

- Windows 7 SP1
- Windows 8.1
- Windows 10 1703 이상
- 단일 세션 배포에서만 Windows Server 2016
- 단일 세션 배포에서만 Windows Server 2019

### <a name="discrete-device-assignment-support"></a>개별 디바이스 할당 지원

원격 데스크톱 서비스는 Windows Server 2016 또는 Windows Server 2019 Hyper-V 호스트의 개별 디바이스 할당과 함께 제공되는 실제 GPU를 지원합니다. 자세한 내용은 [개별 디바이스 할당 배포 계획](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)을 참조하세요.


## <a name="vdi-deployment--supported-guest-oses"></a>VDI 배포 - 지원되는 게스트 OS

Windows Server 2016 및 Windows Server 2019 RD 가상화 호스트 서버는 다음과 같은 게스트 OS를 지원합니다.

- Windows 10 Enterprise
- Windows 8.1 Enterprise
- Windows 7 SP1 Enterprise

> [!NOTE]
> - 원격 데스크톱 서비스는 이기종 세션 컬렉션을 지원하지 않습니다. 컬렉션에 있는 모든 VM의 OS는 버전이 동일해야 합니다.
> - 게스트 OS 버전이 다른 개별 이기종 컬렉션을 동일한 호스트에서 사용할 수 있습니다.
> - VM을 실행하는 데 사용된 Hyper-V 호스트는 원래 VM 템플릿을 만드는 데 사용된 Hyper-V 호스트와 동일한 버전이어야 합니다.

## <a name="single-sign-on"></a>Single Sign-On

Windows Server 2016 및 Windows Server 2019 RDS는 두 가지 기본 SSO 환경을 지원합니다.

- 앱 내(Windows, iOS, Android 및 Mac의 원격 데스크톱 애플리케이션)
- 웹 SSO

원격 데스크톱 애플리케이션을 사용하면 각 OS에 고유한 메커니즘을 통해 자격 증명을 연결 정보의 일부([Mac](clients/remote-desktop-mac.md)) 또는 관리형 계정의 일부([iOS](clients/remote-desktop-ios.md#manage-your-user-accounts), [Android](clients/remote-desktop-android.md#manage-your-user-accounts), Windows)로 안전하게 저장할 수 있습니다.

Windows의 받은 편지함 원격 데스크톱 연결 클라이언트를 통해 SSO를 사용하여 데스크톱 및 RemoteApps에 연결하려면 Internet Explorer를 통해 RD 웹 페이지에 연결해야 합니다. 다음 구성 옵션은 서버 쪽에서 필요합니다. 다른 구성은 웹 SSO에 지원되지 않습니다.

- 양식 기반 인증으로 설정된 RD 웹(기본값)
- 암호 인증으로 설정된 RD 게이트웨이(기본값)
- RD 게이트웨이 속성에 "원격 컴퓨터에 대해 RD 게이트웨이 자격 증명 사용"(기본값)으로 설정된 RDS 배포

> [!NOTE]
> 필요한 구성 옵션으로 인해 스마트카드에는 웹 SSO가 지원되지 않습니다. 스마트카드를 통해 로그인하는 사용자에게는 로그인 메시지가 여러 개 표시될 수 있습니다.

원격 데스크톱 서비스의 VDI 배포를 만드는 방법에 대한 자세한 내용은 [원격 데스크톱 서비스 VDI에 지원되는 Windows 10 보안 구성](rds-vdi-supported-config.md)을 확인하세요.

## <a name="using-remote-desktop-services-with-application-proxy-services"></a>애플리케이션 프록시 서비스와 원격 데스크톱 서비스 사용

웹 클라이언트를 제외한 원격 데스크톱 서비스를 [Azure AD 애플리케이션](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-remote-desktop) 프록시와 함께 사용할 수 있습니다. 원격 데스크톱 서비스는 Windows Server 2016 이하 버전에 포함된 [웹 애플리케이션 프록시](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server) 사용을 지원하지 않습니다.
