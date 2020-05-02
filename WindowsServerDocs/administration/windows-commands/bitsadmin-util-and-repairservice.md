---
title: bitsadmin util and repairservice
description: BITS 서비스의 여러 버전에서 알려진 문제를 해결 하는 bitsadmin util 및 repairservice 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0104a3f2ace972821151bf5083f9b0795e427ff1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707651"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util and repairservice

BITS가 시작 되지 않으면이 스위치는 잘못 된 서비스 구성과 Windows 서비스 (예: LANManworkstation) 및 네트워크 디렉터리에 대 한 종속성과 관련 된 오류를 해결 하려고 합니다. 이 스위치는 해결 된 문제가 있는지 여부를 나타내는 출력도 생성 합니다.

> [!NOTE]
> 이 명령은 BITS 1.5 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /util /repairservice [/force]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /force | (선택 사항) 서비스를 삭제 하 고 다시 만듭니다.|

> [!NOTE]
> BITS가 서비스를 다시 만들 경우 지역화 된 시스템 에서도 서비스 설명 문자열을 영어로 설정할 수 있습니다.

## <a name="examples"></a>예

BITS 서비스 구성을 복구 하려면:

```
bitsadmin /util /repairservice
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin util 명령](bitsadmin-util.md)

- [bitsadmin 명령](bitsadmin.md)
