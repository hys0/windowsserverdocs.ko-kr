---
title: 원격 데스크톱 클라이언트 URI 체계
description: 원격 데스크톱 클라이언트의 Uniform Resource Identifier 체계에 대해 알아보기
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 02f970cb2e793c1e342a2818a2bca3900327fa9c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856006"
---
# <a name="remote-desktop-client-universal-resource-identifier-uri-scheme-support"></a>원격 데스크톱 클라이언트 리소스 URI (Universal Identifier) 체계 지원

>적용 대상: Windows Server, 버전 1803, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

URI(Uniform Resource Identifier) 체계를 사용하도록 설정하여 IT 전문가 및 개발자에게 플랫폼 간에 원격 데스크톱 클라이언트 기능을 통합하는 방법을 제공하고 다음을 허용하여 사용자 환경을 강화합니다. 

- 타사 애플리케이션이 Microsoft 원격 데스크톱을 시작하고 URI 문자열의 일부로 제공되는 미리 정의된 설정을 사용하여 원격 세션을 시작할 수 있도록 허용합니다.
- 최종 사용자가 미리 구성된 URL을 사용하여 원격 연결을 시작할 수 있도록 허용합니다.

>[!NOTE]
> URI를 사용하여 RD 클라이언트에 연결하는 방식은 Windows 운영 체제에서 지원되지 않습니다. 따라서 MacOS, iOS 및 Android 디바이스에서는 URI를 사용하도록 합니다.

Microsoft 원격 데스크톱 클라이언트를 시작할 때 사용 되는 미리 구성 된 특성 설정을 저장 하는 URI 구성표 rdp://query_string를 사용 합니다. 쿼리 문자열은 URL로 제공되는 단일 RDP 특성이나 특성 집합을 나타냅니다. 

RDP 특성은 앰퍼샌드 기호(&)로 구분됩니다. 예를 들어 PC에 연결할 경우 문자열은 다음과 같습니다.

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

다음 테이블에서는 iOS, Mac 및 Android 원격 데스크톱 클라이언트에서 사용할 수 있는 지원되는 특성의 전체 목록을 제공합니다. 플랫폼 열의 "x"는 특성이 지원됨을 나타냅니다. 펼침 단추(<>)로 표시된 값은 원격 데스크톱 클라이언트에서 지원되는 값을 나타냅니다.

| **RDP 특성**                                           | **Android** | **Mac** | **iOS** |
|---------------------------------------------------------|---------|-----|-----|
| 바탕 화면 구성 허용 = i:&lt;0 또는 1&gt;                    | x       | x   | x   |
| 글꼴 다듬기 허용 = i: < 0 또는 1&gt;                         | x       | x   | x   |
| 대체 셸 = s:&lt;문자열&gt;                              | x       | x   | x   |
| [audiomode = i:&lt;0, 1 또는 2&gt;](https://technet.microsoft.com/library/ff393707.aspx)                                | x       | x   | x   |
| [인증 수준 = i:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393709.aspx)                         | x       | x   | x   |
| 콘솔에 연결 = i:&lt;0 또는 1&gt;                           | x       | x   | x   |
| 커서 설정 사용 안 함 = i:&lt;0 또는 1&gt;                      | x       | x   | x   |
| 전체 창 끌기를 사용 안 함 = i:&lt;0 또는 1&gt;                     | x       | x   | x   |
| 메뉴 애니메이션 사용 안 함 = i:&lt;0 또는 1&gt;                           | x       | x   | x   |
| 테마 사용 안 함 = i:&lt;0 또는 1&gt;                               | x       | x   | x   |
| 배경 무늬 사용 안 함 = i:&lt;0 또는 1&gt;                            | x       | x   | x   |
| [drivestoredirect = s: *](https://technet.microsoft.com/library/ff393728(v=ws.10).aspx) (이것이 값만 지원된) | x       | x   |     |
| [desktopheight = i:&lt;픽셀 단위 값&gt;](https://technet.microsoft.com/library/ff393702.aspx)                       |         | x   |     |
| [desktopwidth = i:&lt;픽셀 단위 값&gt;](https://technet.microsoft.com/library/ff393697.aspx)                        |         | x   |     |
| [도메인 = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393673.aspx)                           | x | x | x |
| [전체 주소 = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393661.aspx)                     | x | x | x |
| gatewayhostname = s:&lt;문자열&gt;                  | x | x | x |
| [gatewayusagemethod = i:&lt;1 또는 2&gt;](https://msdn.microsoft.com/aa381329.aspx)               | x | x | x |
| [클라이언트에서 자격 증명 확인 = i:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393660(v=ws.10).aspx) |   | x |   |
| [loadbalanceinfo = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393684.aspx)                  | x | x | x |
| [redirectprinters = i:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393671(v=ws.10).aspx)                 |   | x |   |
| remoteapplicationcmdline = s:&lt;문자열&gt;         | x | x | x |
| remoteapplicationmode = i:&lt;0 또는 1&gt;            | x | x | x |
| remoteapplicationprogram = s:&lt;문자열&gt;         | x | x | x |
| 셸 작업 디렉터리 = s:&lt;문자열&gt;          | x | x | x |
| 리디렉션 서버 이름 사용 = i:&lt;0 또는 1&gt;      | x | x | x |
| [사용자 이름 = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393678.aspx)                         | x | x | x |
| [화면 모드 ID = i:&lt;1 또는 2&gt;](https://technet.microsoft.com/library/ff393692.aspx)                   |   | x |   |
| [세션 bpp = i:&lt;8, 15, 16, 24 또는 32&gt;](https://technet.microsoft.com/library/ff393680.aspx)        |   | x |   |
| [멀티 모니터 사용 = i:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393695(v=ws.10).aspx)          |   | x |   |