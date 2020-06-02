---
title: 원격 데스크톱 URI 체계
description: 원격 데스크톱 클라이언트의 Uniform Resource Identifier 체계에 대해 알아보기
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 06/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: aadb115c68108125abdaf980c12eac951d798bba
ms.sourcegitcommit: df94dac422d13566c32e1cdb8c6e7a4e82747947
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84205614"
---
# <a name="remote-desktop-uri-scheme"></a>원격 데스크톱 URI 체계

> 적용 대상: Windows Server, 버전 1803, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

이 문서에서는 원격 데스크톱용 URI(Uniform Resource Identifier)의 형식을 정의합니다. 이러한 URI 구성을 통해 원격 데스크톱 클라이언트를 다양한 명령으로 호출할 수 있습니다.

## <a name="ms-rd-uri-scheme"></a>ms-rd URI 스키마

>[!NOTE]
> ms-rd URI 스키마는 현재 Windows 데스크톱 클라이언트(MSRDC)에서만 지원됩니다.

ms-rd URI는 클라이언트에 대한 명령과 다음 형식을 사용하여 명령에 고유한 매개 변수 세트를 지정하는 옵션을 제공합니다.

```
ms-rd:command?parameters
```

매개 변수는 &로 구분된 key=value 쌍의 쿼리 문자열 형식을 사용하여 지정된 명령에 대한 추가 정보를 제공합니다.

```
param1=value1&param2=value2&…
```

### <a name="commands-and-parameters"></a>함수 및 매개 변수

다음은 현재 지원되는 명령 및 해당 매개 변수의 목록입니다.

명령 없이 `ms-rd:`를 사용하면 클라이언트가 시작됩니다.

#### <a name="subscribe"></a>구독

이 명령은 클라이언트를 시작하고 구독 프로세스를 시작합니다.

**명령 이름:** 구독

**명령 매개 변수:**

| 매개 변수 | 설명                  | 값 |
|-----------|------------------------------|--------|
| url       | 작업 영역 URL을 지정합니다. | <https://contoso.com>과 같은 유효한 URL입니다. |

**예:** ms-rd:subscribe?url=https://contoso.com

## <a name="legacy-rdp-uri-scheme"></a>레거시 rdp URI 스키마

>[!NOTE]
> 다음 URI 스키마는 macOS, iOS 및 Android 디바이스에 대한 클라이언트에서만 지원됩니다. 이는 위의 새로운 ms-rd URI로 대체됩니다.

Microsoft 원격 데스크톱 클라이언트를 시작할 때 사용되는 미리 구성된 특성 설정을 저장하는 URI 스키마 rdp://query_string을 사용합니다. 쿼리 문자열은 URL로 제공되는 단일 RDP 특성이나 특성 집합을 나타냅니다.

RDP 특성은 앰퍼샌드 기호(&)로 구분됩니다. 예를 들어 PC에 연결할 경우 문자열은 다음과 같습니다.

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

다음 테이블에서는 iOS, Mac 및 Android 원격 데스크톱 클라이언트에서 사용할 수 있는 지원되는 특성의 전체 목록을 제공합니다. 플랫폼 열의 "x"는 특성이 지원됨을 나타냅니다. 펼침 단추(<>)로 표시된 값은 원격 데스크톱 클라이언트에서 지원되는 값을 나타냅니다.

| RDP 특성                                           | Android | Mac | iOS |
|---------------------------------------------------------|---------|-----|-----|
| 바탕 화면 구성 허용 = i:&lt;0 또는 1&gt;              | x       | x   | x   |
| 글꼴 다듬기 허용 = i: < 0 또는 1&gt;                      | x       | x   | x   |
| 대체 셸 = s:&lt;문자열&gt;                        | x       | x   | x   |
| [audiomode = i:&lt;0, 1 또는 2&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393707(v=ws.10)) | x       | x   | x   |
| [인증 수준 = i:&lt;0 또는 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393709(v=ws.10)) | x       | x   | x   |
| 콘솔에 연결 = i:&lt;0 또는 1&gt;                     | x       | x   | x   |
| 커서 설정 사용 안 함 = i:&lt;0 또는 1&gt;                | x       | x   | x   |
| 전체 창 끌기를 사용 안 함 = i:&lt;0 또는 1&gt;               | x       | x   | x   |
| 메뉴 애니메이션 사용 안 함 = i:&lt;0 또는 1&gt;                     | x       | x   | x   |
| 테마 사용 안 함 = i:&lt;0 또는 1&gt;                         | x       | x   | x   |
| 배경 무늬 사용 안 함 = i:&lt;0 또는 1&gt;                      | x       | x   | x   |
| [drivestoredirect = s: *](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393728(v=ws.10)) (이것이 값만 지원된) | x       | x   |     |
| [desktopheight = i:&lt;픽셀 단위 값&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393702(v=ws.10)) |         | x   |     |
| [desktopwidth = i:&lt;픽셀 단위 값&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393697(v=ws.10))  |         | x   |     |
| [도메인 = s:&lt;문자열&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393673(v=ws.10))                 | x | x | x |
| [전체 주소 = s:&lt;문자열&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393661(v=ws.10))           | x | x | x |
| gatewayhostname = s:&lt;문자열&gt;                  | x | x | x |
| [gatewayusagemethod = i:&lt;1 또는 2&gt;](https://docs.microsoft.com/windows/win32/termserv/imsrdpclienttransportsettings-gatewayusagemethod)                | x | x | x |
| [클라이언트에서 자격 증명 확인 = i:&lt;0 또는 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393660(v=ws.10)) |   | x |   |
| [loadbalanceinfo = s:&lt;문자열&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393684(v=ws.10))                  | x | x | x |
| [redirectprinters = i:&lt;0 또는 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393671(v=ws.10))                 |   | x |   |
| remoteapplicationcmdline = s:&lt;문자열&gt;         | x | x | x |
| remoteapplicationmode = i:&lt;0 또는 1&gt;            | x | x | x |
| remoteapplicationprogram = s:&lt;문자열&gt;         | x | x | x |
| 셸 작업 디렉터리 = s:&lt;문자열&gt;          | x | x | x |
| 리디렉션 서버 이름 사용 = i:&lt;0 또는 1&gt;      | x | x | x |
| [사용자 이름 = s:&lt;문자열&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393678(v=ws.10))                  | x | x | x |
| [화면 모드 ID = i:&lt;1 또는 2&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393692(v=ws.10))            |   | x |   |
| [세션 bpp = i:&lt;8, 15, 16, 24 또는 32&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393680(v=ws.10)) |   | x |   |
| [멀티 모니터 사용 = i:&lt;0 또는 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393695(v=ws.10))              |   | x |   |
