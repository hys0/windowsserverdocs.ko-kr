---
title: 원격 데스크톱 클라이언트 URI 체계
description: 원격 데스크톱 클라이언트에 대 한 Uniform Resource Identifier 스키마에 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2934fed43c8f4feec2f321d684cc3593933eb5d
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297472"
---
# 원격 데스크톱 클라이언트 유니버설 URI (Resource Identifier) 체계 지원

>적용 대상: Windows Server, 버전 1803, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

리소스 URI (Uniform Identifier) 체계를 사용 하 고 IT 전문가 개발자 플랫폼 간에 원격 데스크톱 클라이언트의 기능을 통합 하는 방법을 제공 함으로써 사용자 환경을 향상 시킵니다. 

- Microsoft 원격 데스크톱을 실행 (URI 문자열의 일부로 제공 됨)는 미리 정의 된 설정으로 원격 세션을 시작 하는 타사 응용 프로그램.
- 최종 사용자는 미리 구성 된 Url을 사용 하 여 원격 연결을 시작 합니다.

>[!NOTE]
> RD 클라이언트에 연결 하는 URI를 사용 하 여 Windows 운영 체제에 대 한 지원 되지 않습니다-MacOS, iOS 및 Android 디바이스를 사용 하 여 URI를 사용 합니다.

Microsoft 원격 데스크톱 URI 체계 rdp://query_string를 사용 하 여 클라이언트를 시작할 때 사용 되는 미리 구성 된 특성 설정을 저장 합니다. 쿼리 문자열은 단일 또는 URL에서 제공 되는 RDP 특성 집합을 나타냅니다. 

RDP 특성 앰퍼샌드 기호 (&)로 구분 됩니다. 예를 들어 PC에 연결할 때, 문자열은:

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

이 표에서 iOS, Mac 및 Android 원격 데스크톱 클라이언트를 사용 하 여 사용할 수 있는 지원 되는 특성의 전체 목록을 제공 합니다. (플랫폼 열에 "x" 특성이 지원 나타냅니다. 펼침 단추 (<>)으로 표시 하는 값을 나타냅니다 원격 데스크톱 클라이언트에서 지원 되는 값을.)

| **RDP 특성**                                           | **Android** | **Mac** | **iOS** |
|---------------------------------------------------------|---------|-----|-----|
| 바탕 화면 구성 허용 i =:&lt;0 또는 1&gt;                    | x       | x   | x   |
| 글꼴 매끄럽게 i:<0 또는 1 =&gt;                         | x       | x   | x   |
| 대체 셸 = s:&lt;문자열&gt;                              | x       | x   | x   |
| [audiomode i =:&lt;0, 1 또는 2&gt;](https://technet.microsoft.com/library/ff393707.aspx)                                | x       | x   | x   |
| [인증 수준 i =:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393709.aspx)                         | x       | x   | x   |
| 콘솔에 연결 i =:&lt;0 또는 1&gt;                           | x       | x   | x   |
| 커서 설정을 사용 하지 않으면 i =:&lt;0 또는 1&gt;                      | x       | x   | x   |
| 전체 창 끌기 사용 안 함 i =:&lt;0 또는 1&gt;                     | x       | x   | x   |
| 메뉴 anims 사용 안 함 i =:&lt;0 또는 1&gt;                           | x       | x   | x   |
| 테마를 사용 하지 않도록 설정 i =:&lt;0 또는 1&gt;                               | x       | x   | x   |
| 배경 무늬를 사용 하지 않도록 설정 i =:&lt;0 또는 1&gt;                            | x       | x   | x   |
| [drivestoredirect = s: *](https://technet.microsoft.com/library/ff393728(v=ws.10).aspx) (이것이 값만 지원된) | x       | x   |     |
| [desktopheight i =:&lt;픽셀 값&gt;](https://technet.microsoft.com/library/ff393702.aspx)                       |         | x   |     |
| [desktopwidth i =:&lt;픽셀 값&gt;](https://technet.microsoft.com/library/ff393697.aspx)                        |         | x   |     |
| [도메인 = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393673.aspx)                           | x | x | x |
| [주소 전체 = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393661.aspx)                     | x | x | x |
| gatewayhostname = s:&lt;문자열&gt;                  | x | x | x |
| [gatewayusagemethod i =:&lt;1 또는 2&gt;](https://msdn.microsoft.com/aa381329.aspx)               | x | x | x |
| [클라이언트에서 자격 증명을 묻는 i =:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393660(v=ws.10).aspx) |   | x |   |
| [loadbalanceinfo = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393684.aspx)                  | x | x | x |
| [redirectprinters i =:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393671(v=ws.10).aspx)                 |   | x |   |
| remoteapplicationcmdline = s:&lt;문자열&gt;         | x | x | x |
| remoteapplicationmode i =:&lt;0 또는 1&gt;            | x | x | x |
| remoteapplicationprogram = s:&lt;문자열&gt;         | x | x | x |
| 셸 작업 디렉터리 = s:&lt;문자열&gt;          | x | x | x |
| 리디렉션 서버 이름을 사용 하 여 i =:&lt;0 또는 1&gt;      | x | x | x |
| [사용자 이름 = s:&lt;문자열&gt;](https://technet.microsoft.com/library/ff393678.aspx)                         | x | x | x |
| [화면 모드 id i =:&lt;1 또는 2&gt;](https://technet.microsoft.com/library/ff393692.aspx)                   |   | x |   |
| [세션 bpp i =:&lt;8 15, 16, 24, 32&gt;](https://technet.microsoft.com/library/ff393680.aspx)        |   | x |   |
| [멀티 모니터를 사용 하 여 i =:&lt;0 또는 1&gt;](https://technet.microsoft.com/library/ff393695(v=ws.10).aspx)          |   | x |   |