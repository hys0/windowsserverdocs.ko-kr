---
title: nslookup root
description: DNS (Domain Name System) 도메인 이름 공간의 루트에 대해 기본 서버를 서버로 변경 하는 nslookup root 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f1f2bbe3b71660d079a0b7c87f5be487e0ff437
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721656"
---
# <a name="nslookup-root"></a>nslookup root

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 이름 시스템 (DNS) 도메인 네임 스페이스의 루트에 대 한 서버에 기본 서버를 변경합니다. 현재, ns.nic.ddn.mil 이름 서버가 사용 됩니다. [Nslookup root set](nslookup-set-root.md) 명령을 사용 하 여 루트 서버의 이름을 변경할 수 있습니다.

> [!NOTE]
> 이 명령은와 동일 합니다 `lserver ns.nic.ddn.mil` .

## <a name="syntax"></a>구문

```
root
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [nslookup set root](nslookup-set-root.md)
