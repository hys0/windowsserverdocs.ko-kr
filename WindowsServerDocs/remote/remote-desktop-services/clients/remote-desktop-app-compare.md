---
title: 원격 데스크톱 - 클라이언트 앱 비교
description: 지원되는 기능과 관련하여 다양한 RD 앱을 비교하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 237bb79fae6460bc3b31fb1753e2d679c8d67512
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404162"
---
# <a name="compare-the-client-apps"></a>클라이언트 앱 비교

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

종종 다양한 원격 데스크톱 클라이언트 앱을 서로 비교하는 방법에 대한 질문을 받습니다. 모두 동일한 작업을 수행하나요? 해당 질문에 대한 답은 다음과 같습니다.

## <a name="redirection-support"></a>리디렉션 지원

다음 표는 원격 데스크톱 연결 앱, 유니버설 앱, Android 앱, iOS 앱, macOS 앱 및 웹 클라이언트에서 디바이스 및 다른 리디렉션에 대한 지원을 비교합니다. 이러한 표는 원격 세션에서 한 번에 액세스할 수 있는 리디렉션을 설명합니다. 

개인 데스크톱에 원격으로 연결하는 경우 세션에 대해 **추가 설정**에서 구성할 수 있는 추가 리디렉션이 있습니다. 조직에서 원격 데스크톱 또는 앱을 관리하는 경우 관리자는 그룹 정책 설정을 통해 리디렉션을 활성화하거나 비활성화할 수 있습니다.

### <a name="input-redirection"></a>입력 리디렉션

| 리디렉션 | 원격 데스크톱<br> 연결 | 범용 | Android | iOS | macOS |          웹 클라이언트           |
|-------------|-------------------------------|-----------|---------|-----|-------|-------------------------------|
|  키보드   |               X               |     X     |    X    |  X  |   X   |               X               |
|    마우스    |               X               |     X     |    X    | X\* |   X   |               X               |
|    터치    |               X               |     X     |    X    |  X  |       | X(Edge 및 IE 지원되지 않음) |
|    기타    |              펜              |           |         |     |       |                               |

*[원격 데스크톱 iOS 베타 클라이언트에 대해 지원되는 입력 디바이스 목록](remote-desktop-ios.md#supported-input-devices)을 보세요.

### <a name="port-redirection"></a>포트 리디렉션   

| 리디렉션 | 원격 데스크톱 <br>연결 | 범용 | Android | iOS | macOS | 웹 클라이언트 |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| 직렬 포트 | X                             |           |         |     |       |            |
| USB         | X                             |           |         |     |       |            |

USB 포트 리디렉션을 활성화하는 경우 USB 포트에 연결된 USB 디바이스는 원격 세션에서 자동으로 인식됩니다.

### <a name="other-redirection-devices-etc"></a>기타 리디렉션(디바이스 등)



| 리디렉션         | 원격 데스크톱 연결 | 범용   | Android | iOS         | macOS                                    | 웹 클라이언트    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| 카메라             | X                         |             |         |             |                                          |               |
| 클립보드           | X                         | 텍스트, 이미지 | text    | 텍스트, 이미지 | X                                        | text          |
| 로컬 드라이브/스토리지 | X                         |             | X       |             | x                                        |               |
| 위치            | X                         |             |         |             |                                          |               |
| 마이크         | X                         |X            |         |             | X                                        |               |
| 프린터            | X                         |             |         |             | X(CUPS에만 해당)                            | PDF 인쇄     |
| 스캐너            | X                         |             |         |             |                                          |               |
| 스마트 카드         | X                         |             |         |             | X(Windows 인증이 지원되지 않음) |               |
| 스피커            | X                         | X           | X       | X           | X                                        | X(IE 제외) |

*프린터 리디렉션의 경우 - macOS 앱은 기본적으로 Publisher Imagesetter 프린터 드라이버를 지원합니다. 기본 프린터 드라이버 리디렉션을 지원하지 않습니다.
