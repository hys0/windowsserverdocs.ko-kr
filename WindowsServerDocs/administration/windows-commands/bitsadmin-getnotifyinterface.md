---
title: bitsadmin getnotifyinterface
description: 다른 프로그램에서 지정 된 작업에 대 한 COM 콜백 인터페이스를 등록 했는지 여부를 확인 하는 **bitsadmin getnotifyinterface**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5eb5aee42446c70f16fd6785a3645f42c1987e4d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850576"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

다른 프로그램에서 지정 된 작업에 대 한 COM 콜백 인터페이스 (알림 인터페이스)를 등록 했는지 여부를 확인 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

#### <a name="output"></a>출력

이 명령의 출력은, **등록** 됨 또는 등록 **취소**됨을 표시 합니다.

> [!NOTE]
> 콜백 인터페이스를 등록 한 프로그램은 확인할 수 없습니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 알림 인터페이스를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)