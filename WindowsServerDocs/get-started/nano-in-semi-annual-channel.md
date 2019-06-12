---
title: Windows Server 반기 채널의 Nano 서버 변경 사항
description: 새로운 Windows Server 서비스 모델에서, Nano 서버는 특정 기능이 변경된 컨테이너 운영 체제 역할만 합니다.
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: c12ca84826a92fa045eb84b55e7406392161280b
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452797"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Windows Server 반기 채널의 Nano 서버 변경 사항

>적용 대상: Windows Server 반기 채널

이미 Nano Server를 실행 하는 경우는 [창의 서버 반기 채널](../get-started-19/servicing-channels-19.md) 서비스 모델도 곧 익숙해질, 이전의 CBB (비즈니스용) 모델에 대 한 현재 분기에서 처리 된 것 이므로 합니다. Windows 서버 반기 채널은 동일한 모델에 대 한 새 이름만입니다. 이 모델에서는 Nano 서버의 기능 업데이트 릴리스가 1년에 2~3회로 예상됩니다.

그러나부터 Windows Server, 버전 1803에서 Nano Server는 보기로 사용할 수는 **컨테이너 기본 OS 이미지가**합니다. Windows Server의 Server Core 설치와 같은 컨테이너 호스트의 컨테이너로만 Nano 서버를 실행해야 합니다. 이 릴리스에서 Nano 서버를 기반으로 컨테이너를 실행하는 작업은 다음과 같은 방법으로 이전 버전과 다릅니다.

- Nano 서버가 .NET Core 응용 프로그램을 위해 최적화되었습니다.
- Nano 서버가 Windows Server 2016 버전보다도 더 작습니다.
- PowerShell Core, .NET Core 및 WMI가 이제는 기본적으로 포함되지 않지만, 컨테이너를 빌드할 때 [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) 및 [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) 컨테이너 패키지를 포함할 수 있습니다.
- 이제 Nano 서버에 서비스 스택이 포함되지 않습니다. Microsoft는 업데이트된 Nano 컨테이너를 다시 배포할 Docker 허브에 게시합니다.
- Docker를 사용하여 새 Nano 컨테이너의 문제를 해결합니다.
- 이제 IoT Core에서 Nano 컨테이너를 실행할 수 있습니다.

## <a name="related-topics"></a>관련 항목

- [Windows 컨테이너 설명서](http://aka.ms/windowscontainers)
- [창 서버 반기 채널 개요](../get-started-19/servicing-channels-19.md)
