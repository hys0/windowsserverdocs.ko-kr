---
title: msdt
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c4342cf0fe588f5b41cd98a38a459ac41ca212a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373447"
---
# <a name="msdt"></a>msdt



명령줄에서 또는 자동화 된 스크립트의 일부로 문제 해결 팩을 호출 하 고 사용자 입력 없이 추가 옵션을 활성화 합니다.

## <a name="syntax"></a>구문

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>매개 변수

다음 표에는 msdt에서 지 원하는 매개 변수 및 옵션이 나와 있습니다.


|      매개 변수      |                                                                                            설명                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /id \<패키지 이름 > |        실행할 진단 패키지를 지정 합니다. 사용 가능한 패키지 목록을 보려면이 항목의 뒷부분에 있는 "사용 가능한 문제 해결 팩" 섹션의 문제 해결 팩 ID를 참조 하십시오.         |
|  /path \<디렉터리  |                                                                                           . diagpkg 파일                                                                                            |
|   /dci \<암호 >   |                                        인시던트의은 msdt의 암호 필드입니다. 이 매개 변수는 지원 공급자가 암호를 제공한 경우에만 사용 됩니다.                                         |
|  /dt \<디렉터리 >   | 지정 된 디렉터리에 문제 해결 기록을 표시 합니다. 진단 결과는 사용자의 **%LOCALAPPDATA%\Diagnostics** 또는 **%LOCALAPPDATA%\ElevatedDiagnostics** 디렉터리에 저장 됩니다. |
| /af \<응답 파일 >  |                                               하나 이상의 진단 상호 작용에 대 한 응답을 포함 하는 XML 형식의 응답 파일을 지정 합니다.                                               |

