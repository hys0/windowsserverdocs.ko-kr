---
title: ftp 프롬프트
description: 프롬프트 모드를 설정 및 해제 하는 ftp 프롬프트 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57f0e1eead36665c19845944bf22325b1aecebbb
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820383"
---
# <a name="ftp-prompt"></a>ftp 프롬프트

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
