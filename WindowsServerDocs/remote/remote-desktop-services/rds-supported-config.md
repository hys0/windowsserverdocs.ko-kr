---
title: 원격 데스크톱 서비스에 지원되는 구성
description: Windows Server 2016에서 RDS에 지원되는 구성 관련 정보를 제공합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 12/20/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c925c7eb-6880-411f-8e59-bd0f57cc5fc3
author: lizap
manager: dongill
ms.openlocfilehash: 8571c2220f804a27e4e1a6b744e8e15e38bd53a3
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66453077"
---
# <a name="supported-configurations-for-remote-desktop-services-in-windows-server-2016"></a>Windows Server 2016의 원격 데스크톱 서비스에 지원되는 구성

> 적용 대상: Windows Server 2016

원격 데스크톱 서비스 환경에 지원되는 구성에 있어서 가장 큰 문제는 버전 상호 운용성인 경우가 많습니다. 대부분의 환경에는 여러 버전의 Windows Server가 포함되어 있습니다. 예를 들어 기존 Windows Server 2012 R2 RDS 배포가 있지만 새로운 기능(예: OpenGL\OpenCL, 개별 디바이스 할당 또는 스토리지 공간 다이렉트에 대한 지원)을 활용하기 위해 Windows Server 2016으로 업그레이드하려는 경우가 있습니다. 이때 여러 버전과 함께 작동할 수 있는 RDS 구성 요소는 무엇이고, 무엇을 동일하게 유지해야 하는지 궁금해질 것입니다.

이를 고려할 때 Windows Server 2016의 원격 데스크톱 서비스에 지원되는 구성에 대한 기본 지침은 다음과 같습니다.

> [!NOTE]
> [Windows Server 2016의 시스템 요구 사항](../../get-started/system-requirements.md)을 살펴보세요.

## <a name="best-practices"></a>모범 사례
- 원격 데스크톱 인프라(웹 액세스, 게이트웨이, 연결 브로커 및 라이선스 서버)에 Windows Server 2016을 사용합니다. Windows Server 2016은 이러한 구성 요소의 이전 버전과 호환되므로 2012 R2 RD 세션 호스트는 2016 RD 연결 브로커에 연결할 수 있지만 반대로는 불가능합니다.

- RD 세션 호스트의 경우 컬렉션의 모든 세션 호스트가 동일한 수준에 있어야 하지만 여러 컬렉션이 있을 수 있습니다. Windows Server 2012 R2 세션 호스트가 있는 컬렉션과 Windows Server 2016 세션 호스트가 있는 컬렉션이 있을 수 있습니다.

- RD 세션 호스트를 Windows Server 2016으로 업그레이드하는 경우 라이선스 서버도 업그레이드하세요. 2016 라이선스 서버는 Windows Server 2003까지 모든 이전 Windows Server 버전의 CAL을 처리할 수 있습니다.

- [원격 데스크톱 서비스 환경 업그레이드](upgrade-to-rds.md#flow-for-deployment-upgrades)에서 권장되는 업그레이드 순서를 따르세요. 

- 고가용성 환경을 만드는 경우 모든 연결 브로커가 동일한 OS 수준에 있어야 합니다.

## <a name="rd-connection-brokers"></a>RD 연결 브로커

Windows Server 2016은 Windows Server 2016을 실행하는 RDSH(원격 데스크톱 세션 호스트) 및 RDVH(원격 데스크톱 가상화 호스트) 사용 시 배포에 있는 연결 브로커 수에 대한 제한을 제거합니다. 다음 표는 3개 이상의 연결 브로커가 있는 고가용성 배포에서 연결 브로커의 2016 및 2012 R2 버전과 함께 작동하는 RDS 구성 요소 버전을 보여줍니다.

| HA의 연결 브로커 3개 이상              | RDSH 2016 | RDVH 2016 | RDSH 2012 R2  | RDVH 2012 R2  |
|------------------------------------------|-----------|-----------|---------------|---------------|
| Windows Server 2016 연결 브로커    | 지원함 | 지원함 | 지원함     | 지원함     |
| Windows Server 2012 R2 연결 브로커 | 해당 없음       | 해당 없음       | 지원함     | 지원함     |

## <a name="support-for-gpu-acceleration-with-hyper-v"></a>Hyper-V를 사용하여 GPU 가속화 지원
다음 표에서는 가상 머신의 GPU 가속화 지원을 자세히 설명합니다. [나에게 적합한 그래픽 가상화 기술은 무엇일까요?](rds-graphics-virtualization.md)를 참조하여 필요한 것을 알아보세요. DDA에 대한 자세한 내용은 [개별 디바이스 할당 배포를 위한 계획](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)을 확인하세요.

|VM 게스트 OS  |Windows Server 2012 R2 또는 Windows Server 2016<br> Hyper-V RemoteFX vGPU(1세대 VM) |  Windows Server 2016  Hyper-V RemoteFX vGPU(2세대 VM) |  Windows Server 2016  Hyper-V 개별 디바이스 할당(2세대 VM) |
|-----------------------------|------------------------------------------------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| Windows 7 SP1               | 예                                                        | 아니오                                                     | 아니오                                                                  |
| Windows 8.1                 | 예                                                        | 아니오                                                     | 아니오                                                                  |
| Windows 10 1511 업데이트      | 예                                                        | 예                                                    | 예                                                                 |
| Windows Server 2012 R2      | 예                                                        | 아니오                                                     | 예(KB 3133690 필요)                                           |
| Windows Server 2016         | 예                                                        | 예                                                    | 예                                                                 |
| Windows Server 2012 R2 RDSH | 아니오                                                         | 아니오                                                     | 예(KB 3133690 필요)                                           |
| Windows Server 2016 RDSH    | 아니오                                                         | 아니오                                                     | 예                                                                 |
## <a name="vdi-deployment--supported-guest-oss"></a>VDI 배포 - 지원되는 게스트 OS 
Windows Server 2016 RD 가상화 호스트 서버는 다음과 같은 게스트 OS를 지원합니다.

- Windows 10 Enterprise
- Windows 8.1 Enterprise 
- Windows 8 Enterprise 
- Windows 7 SP1 Enterprise 

아래 표는 지원되는 RD 가상화 호스트 운영 체제 및 게스트 운영 체제 조합을 보여줍니다.

| RDVH OS 버전        | 게스트 OS 버전           |
| ------------- |-------------|
| Windows Server 2016      | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012 R2   | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012      | Windows 7 SP1, Windows 8, Windows 8.1 |

> [!NOTE]  
> - Windows Server 2016 원격 데스크톱 서비스는 이기종 컬렉션을 지원하지 않습니다. 컬렉션의 모든 VM은 OS 버전이 동일해야 합니다. 
> - 게스트 OS 버전이 다른 개별 이기종 컬렉션을 동일한 호스트에서 사용할 수 있습니다. 
> - VM 템플릿은 Windows Server 2016 Hyper-V 호스트에서 게스트 OS로 사용되는 Windows Server 2016 Hyper-V 호스트에 만들어야 합니다.

## <a name="single-sign-on-sso"></a>SSO(Single Sign-On)
Windows Server 2016 RDS는 두 가지 기본 SSO 환경을 지원합니다.

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
