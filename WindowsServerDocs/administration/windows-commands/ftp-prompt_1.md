---
title: ftp prompt
description: 프롬프트 모드를 설정 및 해제 하는 ftp 프롬프트 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0859d3989a054d03421f08f5df7823a690dc85c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933115"
---
# <a name="ftp-prompt"></a>ftp prompt

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

프롬프트 모드를 설정 및 해제 합니다. 프롬프트 모드는 기본적으로 설정 되어 있습니다. 프롬프트 모드가 설정 되어 있으면 파일을 선택적으로 검색 하거나 저장할 수 있도록 여러 파일을 전송 하는 동안 ftp 명령이 메시지를 표시 합니다.

> [!NOTE]
> 프롬프트 모드가 꺼져 있는 경우 [ftp mget](ftp-mget.md) 및 [ftp mput](ftp-mput_1.md) 명령을 사용 하 여 모든 파일을 전송할 수 있습니다.

## <a name="syntax"></a>구문

```
prompt
```

### <a name="examples"></a>예

프롬프트 모드를 설정 하거나 해제 하려면 다음을 입력 합니다.

```
prompt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
