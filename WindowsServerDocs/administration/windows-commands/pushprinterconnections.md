---
title: pushprinterconnections
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe25a29af34f78ebe161dc0d07c5edf64257f5c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371961"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



그룹 정책에서 배포 된 프린터 연결 설정을 읽고 필요에 따라 프린터 연결을 배포/제거 합니다.

## <a name="syntax"></a>구문

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|<-로그 >|작성 한 %temp 또는 쓰기를 디버그 로그 파일을 사용자 당는 windir%\temp에 디버그 로그를 컴퓨터 별로 합니다.|
|<-? >|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

이 유틸리티는 컴퓨터 시작 또는 사용자 로그온 스크립트에 사용 하기 위한 하 고 명령줄에서 실행 되지 않아야 합니다.

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [그룹 정책를 사용 하 여 프린터 배포](https://go.microsoft.com/fwlink/?LinkId=230627)