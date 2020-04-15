---
title: 원격 데스크톱 - 클라이언트 앱 비교
description: 지원되는 기능과 관련하여 다양한 RD 앱을 비교하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 04/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8c41d2691f22e7feb89518a02736f3607940a2f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856226"
---
# <a name="compare-the-clients"></a>클라이언트 비교

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

종종 다양한 원격 데스크톱 클라이언트를 서로 비교하는 방법에 대한 질문을 받습니다. 모두 동일한 작업을 수행하나요? 해당 질문에 대한 답은 다음과 같습니다.

## <a name="redirection-support"></a>리디렉션 지원

다음 표는 서로 다른 클라이언트에서 디바이스 및 기타 리디렉션에 대한 지원을 비교합니다. 이러한 표는 원격 세션에서 한 번에 액세스할 수 있는 리디렉션을 설명합니다.

개인 데스크톱에 원격으로 연결하는 경우 세션에 대해 **추가 설정**에서 구성할 수 있는 추가 리디렉션이 있습니다. 조직에서 원격 데스크톱 또는 앱을 관리하는 경우 관리자는 그룹 정책 설정 또는 RDP 속성을 통해 리디렉션을 활성화하거나 비활성화할 수 있습니다.

### <a name="input-redirection"></a>입력 리디렉션

| 리디렉션 | Windows Inbox</br>(MSTSC) | Windows 데스크톱</br>(MSRDC) | Windows 스토어 | Android | iOS | macOS | 웹 클라이언트    |
|-------------|---------------------------|-----------------------------|---------------|---------|-----|-------|---------------|
| Keyboard    | X                         | X                           | X             | X       | X   | X     | X             |
| 마우스       | X                         | X                           | X             | X       | X\* | X     | X             |
| 터치       | X                         | X                           | X             | X       | X   |       | X(IE 제외) |
| 펜         | X                         | X                           |               |         |     |       |               |

*[원격 데스크톱 iOS 클라이언트에 대해 지원되는 입력 디바이스 목록](remote-desktop-ios.md#supported-input-devices)을 보세요.

### <a name="port-redirection"></a>포트 리디렉션

| 리디렉션 | Windows Inbox</br>(MSTSC) | Windows 데스크톱</br>(MSRDC) | Windows 스토어 | Android | iOS | macOS | 웹 클라이언트 |
|-------------|---------------------------|-----------------------------|---------------|---------|-----|-------|------------|
| 직렬 포트 | X                         | X                           |               |         |     |       |            |
| USB         | X                         | X                           |               |         |     |       |            |

USB 포트 리디렉션을 활성화하는 경우 USB 포트에 연결된 USB 디바이스는 원격 세션에서 자동으로 인식됩니다.

### <a name="other-redirection-devices-etc"></a>기타 리디렉션(디바이스 등)

| 리디렉션         | Windows Inbox</br>(MSTSC) | Windows 데스크톱</br>(MSRDC) | Windows 스토어 | Android | iOS         | macOS                           | 웹 클라이언트    |
|---------------------|---------------------------|-----------------------------|---------------|---------|-------------|---------------------------------|---------------|
| 카메라             | X                         | X                           |               |         |   X         | X                               |               |
| 클립보드           | X                         | X                           | X             | 텍스트    | 텍스트, 이미지 | X                               | text          |
| 로컬 드라이브/스토리지 | X                         | X                           |               | X       |   X        | X                               |               |
| 위치            | X                         | X                           |               |         |             |                                 |               |
| 마이크         | X                         | X                           | X             |         |  X          | X                               |               |
| 프린터            | X                         | X                           |               |         |             | X(CUPS에만 해당)                   | PDF 인쇄     |
| 스캐너            | X                         | X                           |               |         |             |                                 |               |
| Smart Cards         | X                         | X                           |               |         |             | X(Windows 로그온은 지원되지 않음) |               |
| 스피커            | X                         | X                           | X             | X       | X           | X                               | X(IE 제외) |

*프린터 리디렉션의 경우 - macOS 앱은 기본적으로 Publisher Imagesetter 프린터 드라이버를 지원합니다. 기본 프린터 드라이버 리디렉션을 지원하지 않습니다.
