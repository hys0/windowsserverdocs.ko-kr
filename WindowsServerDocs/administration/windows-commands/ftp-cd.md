---
title: ftp cd
description: 원격 컴퓨터의 작업 디렉터리를 변경 하는 ftp cd 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbeff9c2fca654120347f0f616325b700f5c9be3
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820003"
---
# <a name="ftp-cd"></a>ftp cd

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터의 작업 디렉터리를 변경 합니다.

## <a name="syntax"></a>구문

```
cd <remotedirectory>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| <remotedirectory> | 변경 하려는 원격 컴퓨터의 디렉터리를 지정 합니다. |

### <a name="examples"></a>예

*문서*에 대 한 원격 컴퓨터의 디렉터리를 변경 하려면 다음을 입력 합니다.

```
cd Docs
```

원격 컴퓨터의 디렉터리를 *동영상*으로 변경 하려면 다음을 입력 합니다.

```
cd  May Videos
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
