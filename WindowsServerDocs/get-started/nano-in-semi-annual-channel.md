---
title: Windows Server 반기 채널의 Nano 서버 변경 사항
description: 새로운 Windows Server 서비스 모델에서, Nano 서버는 특정 기능이 변경된 컨테이너 운영 체제 역할만 합니다.
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: medium
ms.date: 05/02/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: 7e68d292c32ce58c786a3242203330fcae985913
ms.sourcegitcommit: 4b9b21ca1f366388a78ead7413cb581f2b23d4c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "2711958"
---
# Windows Server 반기 채널의 Nano 서버 변경 사항

>적용 대상: Windows Server, 반기 채널


[Window Server 반기 채널 개요](semi-annual-channel-overview.md)에서 설명한 것처럼, Windows Server 버전 1803은 반기 채널의 최신 릴리스입니다.

이미 Nano 서버를 실행 중인 경우 CBB(비즈니스용 현재 분기) 모델에서 이전에 서비스되었으므로 이 서비스 모델은 친숙할 것입니다. Windows Server의 새로운 반기 채널은 같은 모델의 새 이름일 뿐입니다. 이 모델에서는 Nano 서버의 기능 업데이트 릴리스가 1년에 2~3회로 예상됩니다.

그러나 이 버전의 Windows Server 버전 1803에서 Nano 서버는 **컨테이너 기본 운영 체제 이미지**로만 사용할 수 있습니다. Windows Server의 Server Core 설치와 같은 컨테이너 호스트의 컨테이너로만 Nano 서버를 실행해야 합니다. 이 릴리스에서 Nano 서버를 기반으로 컨테이너를 실행하는 작업은 다음과 같은 방법으로 이전 버전과 다릅니다.

- Nano 서버가 .NET Core 응용 프로그램을 위해 최적화되었습니다.
- Nano 서버가 Windows Server 2016 버전보다도 더 작습니다.
- PowerShell Core, .NET Core 및 WMI가 이제는 기본적으로 포함되지 않지만, 컨테이너를 빌드할 때 [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) 및 [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) 컨테이너 패키지를 포함할 수 있습니다.
- 이제 Nano 서버에 서비스 스택이 포함되지 않습니다. Microsoft는 업데이트된 Nano 컨테이너를 다시 배포할 Docker 허브에 게시합니다.
- Docker를 사용하여 새 Nano 컨테이너의 문제를 해결합니다.
- 이제 IoT Core에서 Nano 컨테이너를 실행할 수 있습니다.

## 관련 항목
참가자 프로그램이 시작되면 [Windows 컨테이너 설명서](http://aka.ms/windowscontainers)에서 자세한 내용을 찾아보세요.
