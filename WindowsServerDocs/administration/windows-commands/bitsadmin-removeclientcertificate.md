---
title: bitsadmin removeclientcertificate
description: '**Bitsadmin removeclientcertificate**에 대 한 Windows 명령 항목-작업에서 클라이언트 인증서를 제거 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38cf00dc48ff036e7d710fb7436f00fd9381dd0b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849876"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

작업에서 클라이언트 인증서를 제거합니다.

## <a name="syntax"></a>구문

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 *Mydownloadjob*이라는 작업에서 클라이언트 인증서를 제거 합니다.

```
C:\>bitsadmin /removeclientcertificate myDownloadJob 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)