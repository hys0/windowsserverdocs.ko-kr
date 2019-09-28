---
title: manage-bde 상태
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 235db54ef2361c0e95c66b15a15be7f188fb74d9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373860"
---
# <a name="manage-bde-status"></a>manage-bde: 상태



컴퓨터에 모든 드라이브에 대 한 다음 정보를 제공합니다. 여부 BitLocker로 보호 되어 있습니다.
-   Size
-   BitLocker 버전
-   변환 상태
-   암호화 된 비율
-   암호화 방법
-   보호 상태
-   잠금 상태
-   식별 필드
-   키 보호기

이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive >|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|-protectionaserrorlevel|볼륨이; 보호 된 경우 반환 코드는 볼륨을 보호 하는 경우 0과 1을 보낼 manage-bde 명령줄 도구 사용 하면 BitLocker로 보호 되는 드라이브 인지 확인 하려면 일괄 처리 스크립트에 대 한 가장 일반적으로 사용 합니다. 사용할 수도 있습니다 **-p** 이 명령의 축약된 버전으로 합니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **-상태** C 드라이브의 상태를 표시 하는 명령
```
manage-bde –status C:
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)