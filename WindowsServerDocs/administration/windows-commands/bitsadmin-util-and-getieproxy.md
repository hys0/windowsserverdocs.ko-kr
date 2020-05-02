---
title: bitsadmin util and getieproxy
description: 지정 된 서비스 계정에 대 한 프록시 사용을 검색 하는 bitsadmin util 및 getieproxy 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 576f308bc7fb9a4e448638d06621f95eebef0cd0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707666"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util and getieproxy

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정한 서비스 계정에 대 한 프록시 사용을 검색합니다. 이 명령은 각 프록시 사용에 대 한 값을 표시 합니다. 뿐만 아니라 프록시 사용에 대해 지정한 서비스 계정. 특정 서비스 계정에 대 한 프록시 사용을 설정 하는 방법에 대 한 자세한 내용은 [bitsadmin util 및 setieproxy](bitsadmin-util-and-setieproxy.md) 명령을 참조 하세요.

## <a name="syntax"></a>구문

```
bitsadmin /util /getieproxy <account> [/conn <connectionname>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| account | 서비스 계정을 검색 하려면 프록시 설정을 지정 합니다. 가능한 값은 다음과 같습니다.<ul><li>LOCALSYSTEM</li><li>   NETWORKSERVICE</li><li>LOCALSERVICE.</li></ul> |
| connectionname | (선택 사항) **/Conn** 매개 변수와 함께 사용 하 여 사용할 모뎀 연결을 지정 합니다. **/Conn** 매개 변수를 지정 하지 않으면 BITS는 LAN 연결을 사용 합니다. |

## <a name="examples"></a>예

네트워크 서비스 계정에 대 한 프록시 사용을 표시 하려면:

```
bitsadmin /util /getieproxy NETWORKSERVICE
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin util 명령](bitsadmin-util.md)

- [bitsadmin 명령](bitsadmin.md)
