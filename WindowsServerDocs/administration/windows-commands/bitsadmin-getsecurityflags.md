---
title: bitsadmin getsecurityflags
description: '**Bitsadmin getsecurityflags**에 대 한 Windows 명령 항목으로, 전송 하는 동안 서버 인증서에서 수행 되는 URL 리디렉션 및 검사에 대 한 HTTP 보안 플래그를 보고 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 360f8d5514e5251dd9e4a6a6b60335dc34fe4415
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850476"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

URL 리디렉션 및 검사에 대 한 보안 플래그 보고서 HTTP 전송 하는 동안 서버 인증서에서 수행 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 *Mydownloadjob*이라는 작업에서 보안 플래그를 검색 합니다.

```
C:\>bitsadmin /getsecurityflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)