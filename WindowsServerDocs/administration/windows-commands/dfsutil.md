---
title: dfsutil
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 1a06806b109bbd324213f935892bbbab415362df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377982"
---
# <a name="dfsutil"></a>dfsutil

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dfsutil 명령은 DFS 네임 스페이스, 서버 및 클라이언트를 관리 합니다. dfsutil 명령은 대부분의 명령에 대 한 설명으로 제공 된 업데이트 된 DFS 네임 스페이스 용어를 사용 하 여 원래 분산 파일 시스템 용어를 사용 합니다.

이 명령을 사용 하는 방법에 대 한 예는를 참조 하십시오. 

## <a name="syntax"></a>구문

```
command </parameter> </param2>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|[dfsutil 루트](dfsutil-root.md)|네임 스페이스 루트를 표시, 생성, 제거, 가져오기 및 내보냅니다.|
|[dfsutil 링크](dfsutil-link.md)|\)링크 \(폴더를 표시, 생성, 제거 또는 이동 합니다.|
|[dfsutil 대상](dfsutil-target.md)|폴더 대상 또는 네임 스페이스 서버를 표시, 만들기, 제거 합니다.|
|[dfsutil 속성](dfsutil-property.md)|표시 하거나 폴더 대상 또는 네임 스페이스 서버를 수정 합니다.|
|[dfsutil 클라이언트](dfsutil-client.md)|클라이언트 정보 또는 레지스트리 키를 표시 하거나 수정 합니다.|
|[dfsutil 서버](dfsutil-server.md)|네임 스페이스 구성을 표시 하거나 수정 합니다.|
|[dfsutil Diag](dfsutil-diag.md)|진단을 수행 하거나 dfsdirs\/dfspath를 확인 합니다.|
|[dfsutil 도메인](dfsutil-domain.md)|도메인의 모든 도메인\-기반 네임 스페이스를 표시 합니다.|
|[dfsutil 캐시](dfsutil-cache.md)|클라이언트 캐시를 표시 하거나 플러시합니다.|
|[dfsutil oldcli](dfsutil-oldcli.md)|Dfsutil \/oldcli 명령을 사용 하 여 원래 dfsutil 구문을 사용 합니다.|

## <a name="remarks-optional-section"></a>설명 <optional section>
명령 끝에 네임 스페이스 서버\)와 같은 개체 \(지정 하면 대부분의 명령에 추가 매개 변수 또는 명령을 요구 하지 않고 개체에 대 한 정보가 표시 됩니다. 예를 들어 dfsutil Root 명령을 사용할 때 네임 스페이스 루트를 명령에 추가 하 여 루트에 대 한 정보를 볼 수 있습니다.

## <a name="BKMK_Examples"></a>예와
여기 &lt;예제에 대 한 자세한 설명을 입력 합니다.&gt;

```
This /is /the /example /of /calling /command /with /parameters
```

여기에서 다른 예제에 대 한 자세한 설명을 입력할 수 있습니다. &lt;&gt;

```
This /is /a:different /example
```

## <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)


