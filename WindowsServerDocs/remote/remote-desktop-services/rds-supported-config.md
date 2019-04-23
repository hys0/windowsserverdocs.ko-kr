---
title: 원격 데스크톱 서비스에 대 한 지원 되는 구성
description: Windows Server 2016에서 RDS에 대 한 지원 되는 구성에 대 한 정보를 제공합니다.
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
ms.openlocfilehash: 894ea8b134ae5b871a2978e3f72e683c12346fe5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850204"
---
# <a name="supported-configurations-for-remote-desktop-services-in-windows-server-2016"></a>Windows Server 2016에서 원격 데스크톱 서비스에 대 한 지원 되는 구성

> 적용 대상: Windows Server 2016

원격 데스크톱 서비스 환경에 대 한 지원 되는 구성에 있어서 가장 큰 문제를 버전 상호 운용성 경향이 있습니다. Windows Server의 여러 버전을 포함 하는 대부분의 환경-예를 들어 기존 Windows Server 2012 R2 RDS 배포가 수 있지만 새 기능 (예: OpenGL\OpenCL, 불연속에 대 한 지원 활용 하기 위해 Windows Server 2016으로 업그레이드. 장치 할당 또는 저장소 공간 다이렉트). RDS 구성 요소는 서로 다른 버전을 사용 하 여 사용할 수 있으며 동일 해야 하는 다음 질문은?

따라서이 점을 염두에서 다음은 Windows Server 2016에서 원격 데스크톱 서비스의 지원 되는 구성에 대 한 기본 지침입니다.

> [!NOTE]
> 검토 해야 합니다 [Windows Server 2016에 대 한 시스템 요구 사항](../../get-started/system-requirements.md)합니다.

## <a name="best-practices"></a>모범 사례
- 웹 액세스, 게이트웨이, 연결 브로커 및 라이선스 서버 원격 데스크톱 인프라에 대 한 Windows Server 2016을 사용 합니다. Windows Server 2016 이러한 구성 요소에 대 한 이전 버전과 호환 되므로 2012 R2 RD 세션 호스트 2016 RD 연결 브로커에 연결할 수 있지만 반대의 마찬가지입니다.

- RD 세션 호스트-컬렉션의 모든 세션 호스트는 동일한 수준에 있이 필요 하지만 여러 컬렉션을 할 수 있습니다. Windows Server 2012 R2 세션 호스트를 사용 하 여 컬렉션 및 Windows Server 2016 세션 호스트를 사용 하 여 하나를 사용할 수 있습니다.

- RD 세션 호스트 Windows Server 2016으로 업그레이드 하는 경우 라이선스 서버도 업그레이드 합니다. 2016 라이선스 서버에서 모든 이전 버전의 Windows Server, Windows Server 2003까지 Cal을 처리할 수는 기억 합니다.

- 권장 업그레이드 순서를 따릅니다 [원격 데스크톱 서비스 환경 업그레이드](upgrade-to-rds.md#flow-for-deployment-upgrades)합니다. 

- 항상 사용 가능한 환경에서 만드는 경우 모든 사용자 연결 브로커 같은 OS 수준에서 되도록 해야 합니다.

## <a name="rd-connection-brokers"></a>RD 연결 브로커

Windows Server 2016 세션 호스트 RDSH (원격 데스크톱) 및 원격 데스크톱 가상화 호스트 (RDVH)도 Windows Server 2016을 실행 하는 사용 하 여 배포에서 있습니다 연결 브로커 수에 대 한 제한을 제거 합니다. 다음 표에서 세 개 이상의 연결 브로커를 사용 하 여 항상 사용 가능한 배포에 연결 브로커의 2016 및 2012 R2 버전을 사용 하 여 RDS 구성 요소 작업의 버전을 보여 줍니다.

| Ha에서 3 + 연결 브로커              | RDSH 2016 | RDVH 2016 | RDSH 2012 R2  | RDVH 2012 R2  |
|------------------------------------------|-----------|-----------|---------------|---------------|
| Windows Server 2016 연결 브로커    | 지원됨 | 지원됨 | 지원됨     | 지원됨     |
| Windows Server 2012 R2 Connection Broker | 해당 사항 없음       | 해당 사항 없음       | 지원됨     | 지원됨     |

## <a name="support-for-gpu-acceleration-with-hyper-v"></a>Hyper-v가 설치 된 GPU 가속에 대 한 지원
다음 표에서 가상 머신에서 GPU 가속에 대 한 지원을 자세히 설명합니다. 참조 [그래픽 가상화 기술을 적합 한?](rds-graphics-virtualization.md) 에 대 한 도움말을 확인 해야 합니다. DDA에 대 한 특정 내용은 체크 아웃 [불연속 장치 할당을 배포 하기 위한 계획](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)합니다.

|VM 게스트 OS  |Windows Server 2012 R2 또는 Windows Server 2016<br> Hyper-v가 RemoteFX vGPU (Gen 1 VM) |  Windows Server 2016 Hyper-v RemoteFX vGPU (Gen 2 VM) |  Windows Server 2016 Hyper-v 불연속 장치 할당 (Gen 2 VM) |
|-----------------------------|------------------------------------------------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| Windows 7 SP1               | 예                                                        | 아니오                                                     | 아니오                                                                  |
| Windows 8.1                 | 예                                                        | 아니오                                                     | 아니요                                                                  |
| Windows 10 1511 업데이트      | 예                                                        | 예                                                    | 예                                                                 |
| Windows Server 2012 R2      | 예                                                        | 아니요                                                     | 예 (KB 3133690 필요)                                           |
| Windows Server 2016         | 예                                                        | 예                                                    | 예                                                                 |
| Windows Server 2012 R2 RDSH | 아니오                                                         | 아니요                                                     | 예 (KB 3133690 필요)                                           |
| Windows Server 2016 RDSH    | 아니요                                                         | 아니요                                                     | 예                                                                 |
## <a name="vdi-deployment--supported-guest-oss"></a>VDI 배포-지원 되는 게스트 Os 
Windows Server 2016 RD 가상화 호스트 서버는 다음 게스트 Os를 지원합니다.

- Windows 10 Enterprise
- Windows 8.1 Enterprise 
- Windows 8 Enterprise 
- Windows 7 SP1 Enterprise 

아래 표에서 지원 되는 RD 가상화 호스트 운영 체제 및 게스트 운영 체제 조합을 보여 줍니다.

| RDVH OS 버전        | 게스트 OS 버전           |
| ------------- |-------------|
| Windows Server 2016      | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012 R2   | Windows 7 SP1, Windows 8, Windows 8.1, Windows 10 |
| Windows Server 2012      | Windows 7 SP1, Windows 8, Windows 8.1 |

> [!NOTE]  
> - Windows Server 2016 원격 데스크톱 서비스는 유형이 다른 컬렉션을 지원 하지 않습니다. 컬렉션의 모든 Vm에는 동일한 OS 버전 이어야 합니다. 
> - 동일한 호스트에서 별도 유형이 같은 컬렉션과 다른 게스트 OS 버전을 사용할 수 있습니다. 
> - Windows Server 2016 Hyper-v 호스트에서 게스트 OS로 사용 되는 Windows Server 2016 Hyper-v 호스트에 VM 템플릿은 만들어야 합니다.

## <a name="single-sign-on-sso"></a>Single Sign-on (SSO)
Windows Server 2016 RDS는 두 가지 주요 SSO 환경을 지원합니다.

 - 앱 (Windows, iOS, Android 및 Mac에서 원격 데스크톱 응용 프로그램)
 - 웹 SSO
 
원격 데스크톱 응용 프로그램을 사용 수 자격 증명을 저장 하거나 연결 정보의 일부로 ([Mac](clients\remote-desktop-mac.md)) 또는 관리 되는 계정의 일부로 ([iOS](clients\remote-desktop-ios.md#manage-your-user-accounts)하십시오 [Android](clients\remote-desktop-android.md#manage-your-user-accounts), Windows) 각 OS에 고유 메커니즘을 통해 안전 하 게

에 연결 하려면 SSO 사용 하 여 데스크톱과 Windows에서 받은 편지함 원격 데스크톱 연결 클라이언트를 통해 Internet Explorer를 통해 RD 웹 페이지에 연결 해야 합니다. 다음 구성 옵션은 서버 쪽에서 필요 합니다. 웹 SSO에 대 한 다른 구성이 지원 됩니다.

 - RD 웹 폼 기반 인증 (기본값)로 설정
 - 암호 인증 (기본값)로 설정 하는 RD 게이트웨이
 - RDS 배포 "원격 컴퓨터에 사용 하 여 RD 게이트웨이 자격 증명"으로 설정 (기본값) RD 게이트웨이 속성

> [!NOTE]
> 필요한 구성 옵션으로 인해 웹 SSO 스마트 카드를 사용 하 여 지원 되지 않습니다. 스마트 카드를 통해 로그인에 로그인 하는 여러 것인지 발생할 수 있는 사용자입니다.

원격 데스크톱 서비스의 VDI 배포를 만드는 방법에 대 한 자세한 내용은 체크 아웃 [원격 데스크톱 서비스 VDI에 대 한 지원 되는 Windows 10 보안 구성을](rds-vdi-supported-config.md)합니다.

## <a name="using-remote-desktop-services-with-application-proxy-services"></a>원격 데스크톱 서비스를 사용 하 여 응용 프로그램 프록시 서비스

원격 데스크톱 서비스를 사용 하 여 웹 클라이언트를 제외 하 고 사용할 수 있습니다 [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-remote-desktop)합니다. 원격 데스크톱 서비스를 사용 하 여 지원 하지 않습니다 [웹 응용 프로그램 프록시](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server), Windows Server 2016 및 이전 버전에 포함 되어 있는 합니다.
