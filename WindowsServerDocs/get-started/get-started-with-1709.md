---
title: Windows Server, 버전 1709 소개
description: 구입, 설치 및 정품 인증 방법
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: high
ms.date: 12/5/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cf87597-b15d-4f43-8aa1-91e60367f011
ms.openlocfilehash: 96f098457b9bac4541421c7889aefb030e3d8804
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868804"
---
# <a name="introducing-windows-server-version-1709"></a>Windows Server, 버전 1709 소개

>적용 대상: Windows Server(반기 채널)

**Windows Server 1709 버전은 새 반기 채널의 첫 번째 릴리스입니다.** 

## <a name="what-the-semi-annual-channel-is--and-isnt"></a>반기 채널에 대한 진실과 오해
이 새 채널의 첫 번째 릴리스인 Windows Server, 버전 1709는 Windows Server 2016을 위한 "업데이트" 또는 "서비스 팩"이 *아닙니다*. **새로운 릴리스 트랙**에서 1년에 두 번 출시되는 릴리스의 첫 번째 버전으로서, 개발 주기가 짧은 고객이나 최신 Hyper-V 기술에 계속해서 투자하고 있는 호스터 같이 "클라우드 주기"에서 이동 중인 고객을 위해 개발되었습니다. 이 트랙의 각 릴리스는 최초 릴리스 후 18개월 동안 지원됩니다. 반기 채널에 대한 자세한 내용과 **가입(또는 유지)할 채널을 결정하기 위한 팁**은 [반기 채널 개요](semi-annual-channel-overview.md)를 참조하세요.


**장기 서비스 채널(LTSC) 제품의 최신 버전은 Windows Server 2016**입니다. LTSC는 기존의 워크로드 및 응용 프로그램을 지원하기 위해 서버 운영 체제에서 장기적인 안정성과 예측 가능성이 필요한 경우에 가장 적합합니다. LTSC를 계속 사용하고 싶다면 Server Core 모드나 데스크톱 환경 포함 서버 모드에서 설치가 가능한 Windows Server 2016을 설치하거나 계속 사용해야 합니다. 자세한 내용은 [Windows Server 2016 시작](https://docs.microsoft.com/windows-server/get-started/server-basics)을 참조하십시오.


## <a name="whats-different-about-1709"></a>1709의 차이점은 무엇입니까?

Windows Server, 버전 1709는 Server Core 모드로 실행됩니다. 즉, GUI가 없으므로 원격으로 관리합니다. 하지만 하드웨어 요구 사항이 적고, 공격 노출 영역이 작으며, 업데이트가 적게 필요하다는 장점이 있습니다. Server Core를 처음 사용하는 경우 [Server Core 서버 관리](../administration/server-core/server-core-manage.md)가 이 환경에 익숙해지는 데 도움이 됩니다. [Windows Server 2016 관리](../administration/manage-windows-server.md)는 원격 서버 관리를 위한 다양한 옵션을 보여줍니다.

[Windows Server, 버전 1709의 새로운 기능](whats-new-in-windows-server-1709.md)은 Windows Server, 버전 1709에 추가된 새 기능을 소개합니다.

### <a name="why-does-windows-server-version-1709-offer-only-the-server-core-installation-option"></a>Windows Server, 버전 1709가 Server Core 설치 옵션만을 제공하는 이유는 무엇인가요?
Windows Server의 각 릴리스를 계획할 때 중요한 단계 중 하나는 고객의 피드백을 듣는 것입니다. Windows Server를 어떻게 사용하고 계신가요? Windows Server 배포, 그리고 더 나아가 일상적인 비즈니스에 가장 큰 영향을 미치는 새 기능은 무엇인가요? 고객 피드백에 따르면 새로운 혁신 기술을 가급적 빠르고 효율적으로 제공하는 것이 최우선 과제입니다. 동시에 가장 빠르게 혁신을 수행하는 고객의 경우 주로 PowerShell을 통한 명령줄 스크립팅을 사용하여 데이터 센터를 관리하고, 데스크톱 환경 포함 Windows Server 설치 시 이용 가능한 데스크톱 GUI를 강력하게 요구하지 않습니다. Server Core 설치 옵션에 집중함으로써 기존 Windows Server 플랫폼 기능 및 응용 프로그램 호환성을 유지하면서 더 많은 리소스를 새로운 혁신에 쏟을 수 있습니다. 이에 관한 문제 또는 Windows Server 및 향후 릴리스에 관한 다른 피드백이 있는 경우 [피드백 허브](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)를 통해 의견이나 제안 사항을 보낼 수 있습니다.


### <a name="what-about-nano-server"></a>Nano 서버는 어떤가요?
Nano 서버는 컨테이너 운영 체제로 이용 가능합니다. 자세한 내용은 [Windows Server 반기 채널 내 Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 참조하세요.

## <a name="additional-information-about-this-release"></a>이 릴리스에 대한 추가 정보
Windows Server, 버전 1709에 관한 핵심 정보를 포괄적으로 알아보려면 설치 전 다음 항목을 검토해야 합니다.

- 실행하려면 어떤 하드웨어가 필요한가요? [시스템 요구 사항](system-requirements.md)을 참조하세요. 이 릴리스에 대한 시스템 요구 사항은 Windows Server 2016에서와 동일합니다.
- 어떤 새로운 기능이 추가되었나요? [Windows Server, 버전 1709의 새로운 기능](whats-new-in-windows-server-1709.md) 참조
- 무엇이 제거되었나요? [Windows Server(버전 1709)부터 제거되었거나 교체될 예정인 기능](Removed-Features-1709.md) 참조
- 반드시 해결이 필요한 이 버전의 고유한 문제는 무엇입니까? [릴리스 정보--Windows Server, 버전 1709의 중요한 문제](server-1709-relnotes.md) 참조


## <a name="where-to-obtain-windows-server-version-1709"></a>Windows Server, 버전 1709 얻을 수 있는 곳

이 릴리스는 새로 설치되어야 합니다.

- VLSC: 볼륨 라이선스 고객에 게 [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx) 로 이동 하 여이 릴리스를 가져올 수 있습니다 합니다 [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx) 를 클릭 하 고 **로그인**. 그런 다음 **다운로드 및 키**를 클릭하고 이 릴리스를 검색합니다. 

- Windows Server, 버전 1709는 [Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.WindowsServer?tab=Overview)에서도 사용할 수 있습니다.

- 참가자 **Visual Studio 구독:** Visual Studio 구독에 이미 참여 하는 경우 Windows Server 1709 버전으로 이동 하 여 얻을 수 있습니다 합니다 [Visual Studio 구독자 다운로드 페이지](https://my.visualstudio.com/downloads?pid=2347) 있습니다 제공 되는 다운로드를 완료 합니다. 이미 구독자가 아닌 경우 [Visual Studio 구독](https://www.visualstudio.com/subscriptions/) 페이지로 이동하고 로그인한 다음 위와 같이 [Visual Studio 구독자 다운로드 페이지](https://my.visualstudio.com/downloads?pid=2347)로 이동합니다. Visual Studio 구독을 통해 얻은 릴리스는 개발 및 테스트용으로만 사용됩니다.




## <a name="activating-windows-server-version-1709"></a>Windows Server, 버전 1709 정품 인증

- 볼륨 라이선싱 서비스 센터에서 이 릴리스를 얻었다면 Windows Server 2016 정품 인증 키를 사용하여 정품 인증할 수 있습니다.
- Microsoft Azure를 사용하고 있는 경우에는 이 릴리스가 자동으로 정품 인증됩니다.
- Visual Studio 구독을 통해 이 릴리스를 얻은 경우 자동으로 정품 인증됩니다.