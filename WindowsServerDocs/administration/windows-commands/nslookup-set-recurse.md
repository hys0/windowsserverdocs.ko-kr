---
title: nslookup set recurse
description: 지정 된 서버에서 정보를 찾을 수 없는 경우 다른 서버를 쿼리하도록 DNS (Domain Name System) 이름 서버에 지시 하는 nslookup set 재귀 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 082ba3bd926d1f47be5510c2340804b1b92991f1
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721622"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse

지정 된 서버에서 정보를 찾을 수 없는 경우 다른 서버를 쿼리하도록 DNS (Domain Name System) 이름 서버에 지시 합니다.

## <a name="syntax"></a>구문

```
set [no]recurse
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ---------- | ---------- |
| norecurse | 지정 된 서버에서 정보를 찾을 수 없는 경우 DNS (Domain Name System) 이름 서버에서 다른 서버를 쿼리하지 못하게 합니다. |
| recurse | 지정 된 서버에서 정보를 찾을 수 없는 경우 다른 서버를 쿼리하도록 DNS (Domain Name System) 이름 서버에 지시 합니다. 이것은 기본값입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
