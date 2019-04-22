---
title: dfsutil
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
robots: noindex,nofollow
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 245f8fb2e6419d22da3e2e76eebd9f801ab90664
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821484"
---
# <a name="dfsutil"></a>dfsutil

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dfsutil 명령 DFS 네임 스페이스, 서버 및 클라이언트를 관리합니다. dfsutil 명령은 대부분의 명령에 대 한 설명으로 제공 하는 업데이트 된 DFS 네임 스페이스 용어를 사용 하 여 원래 분산 파일 시스템 용어를 사용 합니다.

이 명령을 사용할 수 있는 방법을의 예제를 참조 하세요. 

## <a name="syntax"></a>구문

```
command </parameter> </param2>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|[dfsutil Root](dfsutil-root.md)|표시, 만듭니다, 그리고 제거, 가져오기, 네임 스페이스 루트를 내보냅니다.|
|[dfsutil Link](dfsutil-link.md)|표시, 만들고, 제거 하거나 폴더를 이동 \(링크\)합니다.|
|[dfsutil 대상](dfsutil-target.md)|표시를 만들고, 폴더 대상 또는 네임 스페이스 서버를 제거 합니다.|
|[dfsutil 속성](dfsutil-property.md)|표시 하거나 폴더 대상 또는 네임 스페이스 서버를 수정 합니다.|
|[dfsutil 클라이언트](dfsutil-client.md)|표시 하거나 클라이언트 정보 또는 레지스트리 키를 수정 합니다.|
|[dfsutil Server](dfsutil-server.md)|표시 하거나 네임 스페이스 구성을 수정 합니다.|
|[dfsutil Diag](dfsutil-diag.md)|진단을 수행 보거나 dfsdirs\/dfspath 합니다.|
|[dfsutil Domain](dfsutil-domain.md)|모든 도메인 표시\-도메인 네임 스페이스를 기반으로 합니다.|
|[dfsutil Cache](dfsutil-cache.md)|표시 하거나 클라이언트 캐시를 플러시합니다.|
|[dfsutil oldcli](dfsutil-oldcli.md)|Dfsutil를 사용 하 여 \/oldcli 명령에서 원래 dfsutil 구문을 사용 합니다.|

## <a name="remarks-optional-section"></a>설명 <optional section>
개체를 지정 하는 경우 \(네임 스페이스 서버와 같은\) 명령의 끝 대부분의 명령이 표시 됩니다 개체에 대 한 정보 없이 매개 변수 또는 명령입니다. 예를 들어 dfsutil 루트 명령을 사용 하는 경우 네임 스페이스 루트를 루트에 대 한 정보를 보려면 명령에 추가할 수 있습니다.

## <a name="BKMK_Examples"></a>예제
<Here is where you put a detailed description of your example.>

```
This /is /the /example /of /calling /command /with /parameters
```

<Here is where you put a detailed description of another example.>

```
This /is /a:different /example
```

## <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)


