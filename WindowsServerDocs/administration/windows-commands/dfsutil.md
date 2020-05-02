---
title: dfsutil
description: DFS 네임 스페이스, 서버 및 클라이언트를 관리 하는 dfsutil에 대 한 참조 항목입니다. dfsutil 명령은 대부분의 명령에 대 한 설명으로 제공 된 업데이트 된 DFS 네임 스페이스 용어를 사용 하 여 원래 분산 파일 시스템 용어를 사용 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 999eef79227d4531ba724c9cac40127297ea38a0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719521"
---
# <a name="dfsutil"></a>dfsutil

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dfsutil 명령은 DFS 네임 스페이스, 서버 및 클라이언트를 관리 합니다.

>[!NOTE]
>**DFS 네임 스페이스 PowerShell 모듈** 은 몇 가지 dfsutil 매개 변수에 대 한 대체를 제공 하지만 다른 일부는 계속 해 서 dfsutil를 사용 해야 합니다. 업데이트 된 PowerShell에 대 한 자세한 내용은 [DFSN](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps)를 참조 하세요.

## <a name="parameters-available-in-powershell"></a>PowerShell에서 사용할 수 있는 매개 변수

PowerShell에서 다음 매개 변수를 사용할 수 있습니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| root | 네임 스페이스 루트를 표시, 생성, 제거, 가져오기 및 내보냅니다. |
| link | 폴더 (링크)를 표시, 생성, 제거 또는 이동 합니다. |
| 대상 | 폴더 대상 또는 네임 스페이스 서버를 표시, 만들기, 제거 합니다. |
| 속성(property) | 표시 하거나 폴더 대상 또는 네임 스페이스 서버를 수정 합니다. |
| 서버 | 네임 스페이스 구성을 표시 하거나 수정 합니다. |
| 도메인 | 도메인의 도메인 기반 네임 스페이스를 모두 표시 합니다. |

## <a name="parameters-only-available-in-dfsutil"></a>Dfsutil 에서만 사용할 수 있는 매개 변수

Dfsutil 에서만 다음 매개 변수를 사용할 수 있습니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| 클라이언트 | 클라이언트 정보 또는 레지스트리 키를 표시 하거나 수정 합니다. |
| diag | 진단을 수행 하거나 dfsdirs/dfspath를 확인 합니다. |
| 캐시 | 클라이언트 캐시를 표시 하거나 플러시합니다. |

이러한 각 명령에 대 한 자세한 내용은 DFS 네임 스페이스 관리 도구가 설치 된 서버에서 명령 프롬프트를 열고, 또는 `dfsutil client /?` `dfsutil diag /?` `dfsutil cache /?`를 입력 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)