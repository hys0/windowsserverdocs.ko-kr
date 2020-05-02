---
title: ntbackup
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6bce6b0d-646b-46b6-b833-0ff1d6f082c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba3aaaa192283e0e1dc1777a27fc13973949784b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723480"
---
# <a name="ntbackup"></a>ntbackup



Windows Vista 또는 Windows Server 2008에서는 **ntbackup** 명령을 사용할 수 없습니다. 대신 사용 해야는 **wbadmin** 명령과 subcommands를 백업 하 고 명령 프롬프트에서 컴퓨터 및 파일을 복원 합니다.

사용 하 여 만든 백업을 복구할 수 없습니다 **ntbackup** 를 사용 하 여 **wbadmin**합니다. 그러나 ntbackup을 사용 하 여 만든 백업을 복구 하려는 windows Server 2008 및 Windows Vista 사용자의 경우 버전의 **ntbackup** 을 다운로드할 수 **있습니다.** 이 다운로드 가능한 버전의 **ntbackup** 을 통해 레거시 백업에 대 한 복구만 수행할 수 있으며 windows Server 2008 또는 windows Vista를 실행 하는 컴퓨터에서 새 백업을 만들 수는 없습니다. 이 버전의 **ntbackup**을 다운로드 하려면를 [https://go.microsoft.com/fwlink/?LinkId=82917](https://go.microsoft.com/fwlink/?LinkId=82917)참조 하세요.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

[Wbadmin](wbadmin.md)