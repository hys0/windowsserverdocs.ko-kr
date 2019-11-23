---
title: nslookup set retry
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 306bcc4f5e7ac98767c3c2e274100cf917874a8e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372863"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

재시도 횟수를 설정합니다.
## <a name="syntax"></a>구문
```
set retry=<Number>
```
## <a name="parameters"></a>매개 변수

|    매개 변수    |                                      설명                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | 재시도 횟수에 대 한 새 값을 지정합니다. 재시도 횟수 기본값은 4입니다. |
| {도움말 및 #124;?} |                 간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.                  |

## <a name="remarks"></a>설명
- 요청에 회신 하는 특정 시간 내에 수신 되지 않으면, 제한 시간을 두 배로 증가 하 고는 요청을 다시 보냅니다. 다시 시도 값을 포기 하기 전에 다시는 요청을 보내는 횟수를 제어 합니다. 와 제한 시간을 변경할 수는 **제한 시간 설정** 하위 명령.
  ## <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup 설정 시간 제한](nslookup-set-timeout.md)
