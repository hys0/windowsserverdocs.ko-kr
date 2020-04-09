---
title: 새 네임 스페이스
description: 새 네임 스페이스를 만들고 구성 하는 새 네임 스페이스에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6df60703-30bd-4d59-a8d9-9fe3efe96add
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6f616c33525d033827d52925e07764761e7c7b44
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830636"
---
# <a name="new-namespace"></a>새 네임 스페이스

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

만들고 새 네임 스페이스를 구성 합니다. 설치 된 전송 서버 역할 서비스가 있는 경우이 옵션을 사용 해야 합니다. 배포 서버 역할 서비스와 전송 서버 역할 서비스 설치 (즉, 기본값)를 사용 하 여 경우 [MulticastTransmission 새 명령을 사용 하 여](using-the-new-multicasttransmission-command.md)합니다. 참고가이 옵션을 사용 하기 전에 콘텐츠 공급자를 등록 해야 합니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /New-Namespace [/Server:<Server name>]
     /FriendlyName:<Friendly name>
     [/Description:<Description>]
     /Namespace:<Namespace name>
     /ContentProvider:<Name>
     [/ConfigString:<Configuration string>]
     /Namespacetype: {AutoCast | ScheduledCast}
         [/time:<YYYY/MM/DD:hh:mm>]
         [/Clients:<Number of clients>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|/FriendlyName:<Friendly name>|네임 스페이스의 이름을 지정합니다.|
|/Description<Description>]|네임 스페이스에 대 한 설명을 설정합니다.|
|/Namespace:<Namespace name>|네임 스페이스의 이름을 지정합니다. Note 이름, 이것이 하 고 고유 해야 합니다.<p>-   **배포 서버 역할 서비스**:이 옵션에 대 한 구문은/NAMESPACE: WDS:<Image group>/<Image name>/<Index>입니다. 예를 들어: **WDS:ImageGroup1/install.wim/1**<br />-   **전송 서버 역할 서비스**:이 값은 서버에서 네임 스페이스를 만들 때 지정한 이름과 일치 해야 합니다.|
|/ ContentProvider:<Name>]|네임 스페이스에 대 한 콘텐츠를 제공 하는 콘텐츠 공급자의 이름을 지정 합니다.|
|[/ ConfigString:<Configuration string>]|콘텐츠 공급자에 대 한 구성 문자열을 지정합니다.|
|/Namespacetype: {AutoCast &#124; ScheduledCast}|전송에 대 한 설정을 지정합니다. 다음 옵션을 사용 하 여 설정을 지정할 수 있습니다.<p>-[/시간: <time>]-다음 형식 (YYYY/MM/DD: hh: MM 형식)을 사용 하 여 전송이 시작 되어야 하는 시간을 설정 합니다. 예약 된 캐스트 전송에만이 옵션에 적용 됩니다.<br />-[/ 클라이언트: <Number of clients>]-전송이 시작 되기 전에 대기 하는 클라이언트의 최소 수를 설정 합니다. 예약 된 캐스트 전송에만이 옵션에 적용 됩니다.|
## <a name="examples"></a><a name=BKMK_examples></a>예와
자동 캐스트 네임 스페이스를 만들려면 다음을 입력 합니다.
```
wdsutil /New-Namespace /FriendlyName:Custom AutoCast Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider /Namespacetype:AutoCast
```
예약 된 캐스트 네임 스페이스를 만들려면 다음을 입력 합니다.
```
wdsutil /New-Namespace /Server:MyWDSServer /FriendlyName:Custom Scheduled Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider 
/Namespacetype:ScheduledCast /time:2006/11/20:17:00 /Clients:20
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[get AllNamespaces 명령을 사용 하 여](using-the-get-allnamespaces-command.md)
[제거 네임 스페이스 명령을 사용 하 여](using-the-remove-namespace-command.md)
[하위 명령: 시작 네임 스페이스](subcommand-start-namespace.md)
