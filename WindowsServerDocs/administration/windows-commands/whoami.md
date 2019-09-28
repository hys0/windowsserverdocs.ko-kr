---
title: whoami
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3f4d5c-f1f5-4429-b602-afad2b3488bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9731ba3be3983eb53ade88fceaee863800229084
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362138"
---
# <a name="whoami"></a>whoami



로컬 시스템에 현재 로그온 사용자에 대 한 사용자, 그룹 및 권한 정보를 표시 합니다. 매개 변수 없이 사용 하는 경우 **whoami** 현재 도메인 및 사용자 이름을 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
whoami [/upn | /fqdn | /logonid]
whoami {[/user] [/groups] [/priv]} [/fo <Format>] [/nh]
whoami /all [/fo <Format>] [/nh]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/upn|사용자 계정 이름 (UPN) 형식으로 사용자 이름을 표시 합니다.|
|/fqdn|정규화 된 도메인 이름 (FQDN) 형식으로 사용자 이름을 표시 합니다.|
|/logonid|현재 사용자의 로그온 ID를 표시합니다.|
|/user|현재 도메인 및 사용자 이름 및 보안 식별자 (SID)를 표시합니다.|
|/ 그룹|현재 사용자가 속해 있는 사용자 그룹을 표시 합니다.|
|여|현재 사용자의 보안 권한을 표시합니다.|
|/fo \<Format >|출력 형식을 지정합니다. 유효한 값은 다음과 같습니다.</br>**테이블** 테이블에 출력을 표시 합니다. 기본값입니다.</br>**목록** 출력을 목록에 표시 합니다.</br>**csv** 쉼표로 구분 된 값 (CSV) 형식으로 출력을 표시 합니다.|
|/all|현재 사용자 이름, SID (보안 식별자), 권한 및 현재 사용자가 속한 그룹을 포함 하 여 현재 액세스 토큰의 모든 정보를 표시 합니다.|
|/nh|열 머리글을 출력에 표시할를 지정 합니다. 테이블 및 CSV 형식에 대해서만 유효합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_examples"></a>예와

표시 하려면이 컴퓨터에 현재 로그온 한 사용자의 도메인과 사용자 이름을 입력 합니다.
```
whoami
```
다음과 유사한 출력이 표시 됩니다.
```
DOMAIN1\administrator
```
모든 정보를 현재 액세스 토큰에 표시 하려면 다음을 입력 합니다.
```
whoami /all
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)