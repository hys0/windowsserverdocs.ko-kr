---
title: 집합 메타 데이터
description: 한 컴퓨터에서 다른 컴퓨터로 섀도 복사본을 전송 하는 데 사용 되는 섀도 생성 메타 데이터 파일의 이름과 위치를 설정 하는 메타 데이터 집합에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50c9ceebf072db2e7cefada1601accc97b5d0f7f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937090"
---
# <a name="set-metadata"></a>집합 메타 데이터

이름 및 다른 한 컴퓨터에서 섀도 복사본을 전송 하는 데 사용 하는 그림자 만들기 메타 데이터 파일의 위치를 설정 합니다. 매개 변수 없이 사용 하는 경우 **메타 데이터 설정** 명령 프롬프트에서 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<Drive>:][<Path>]|메타 데이터 파일을 만들 위치를 지정 합니다.|
|\<MetaData.cab>|그림자 만들기 메타 데이터를 저장 하는 cab 파일의 이름을 지정 합니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)