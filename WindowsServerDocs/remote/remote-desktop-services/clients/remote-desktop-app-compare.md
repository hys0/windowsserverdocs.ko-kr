---
title: 원격 데스크톱-클라이언트 앱 비교
description: 지원 되는 기능에 있어 다양 한 RD 앱 비교 하는 방법에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 79a6b264c38b4b843c2887c6a3eb6f236480243d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828964"
---
# <a name="compare-the-client-apps"></a>클라이언트 앱 비교

>적용 대상: Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2016

다양 한 원격 데스크톱 클라이언트 앱을 서로 비교 하는 것은 많습니다는 합니다. 모두 동일한 작업을 수행 하나요? 다음은 이러한 질문에 대 한 답변입니다.

## <a name="redirection-support"></a>리디렉션 지원

다음 표에 장치 및 원격 데스크톱 연결 앱, Universal 앱, Android 앱, iOS 앱을 macOS 앱 및 웹 클라이언트에서 다른 리디렉션에 대 한 지원을 비교합니다. 이러한 테이블에는 원격 세션에서 한 번에 액세스할 수 있는 리디렉션을 설명 합니다. 

경우 있습니다 개인 데스크톱에 원격 가지에서 구성할 수 있는 추가 리디렉션 합니다 **추가 설정** 세션에 대 한 합니다. 원격 데스크톱 또는 앱이 관리 하는 조직의 관리자에 게 사용 하도록 설정 하거나 그룹 정책 설정을 통해 리디렉션 사용 안 함 수 있습니다.

### <a name="input-redirection"></a>입력된 리디렉션

| 리디렉션 | 원격 데스크톱<br> 연결 | 범용 | Android | iOS | macOS | 웹 클라이언트 |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| 키보드    | X                             | X         | X       | X   | X     | X          |
| 마우스       | X                             | X         | X       | X*    | X     | X          |
| 터치       | X                             | X         | X       | X   |       |            |
| 기타       | 펜                           |           |         |     |       |            |
* 보기의 [원격 데스크톱 iOS 베타 클라이언트에 대 한 지원 되는 입력된 장치 목록이](remote-desktop-ios.md#supported-input-devices)합니다.

### <a name="port-redirection"></a>포트 리디렉션   

| 리디렉션 | 원격 데스크톱 <br>연결 | 범용 | Android | iOS | macOS | 웹 클라이언트 |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| 직렬 포트 | X                             |           |         |     |       |            |
| USB         | X                             |           |         |     |       |            |

USB 포트 리디렉션을 사용 하도록 설정 하면 USB 포트에 연결 된 USB 장치 원격 세션에서 자동으로 인식 됩니다.

### <a name="other-redirection-devices-etc"></a>기타 리디렉션 (장치 등)



| 리디렉션         | 원격 데스크톱 연결 | 범용   | Android | iOS         | macOS                                    | 웹 클라이언트    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| 카메라             | X                         |             |         |             |                                          |               |
| 클립보드           | X                         | 텍스트, 이미지 | text    | 텍스트, 이미지 | X                                        | text          |
| 로컬 드라이브/저장소 | X                         |             | X       |             | x                                        |               |
| Location            | X                         |             |         |             |                                          |               |
| 마이크         | X                         |X            |         |             | X                                        |               |
| 프린터            | X                         |             |         |             | X (CUP에만 해당)                            | PDF 인쇄     |
| 스캐너            | X                         |             |         |             |                                          |               |
| 스마트 카드         | X                         |             |         |             | X (Windows 인증을 지원 되지 않습니다.) |               |
| 스피커            | X                         | X           | X       | X           | X                                        | X (IE) 제외 |

* MacOS 앱을 대 한 프린터 리디렉션-기본적으로 게시자 세터 프린터 드라이버를 지원합니다. 기본 프린터 드라이버 리디렉션을 지원 하지 않습니다.
