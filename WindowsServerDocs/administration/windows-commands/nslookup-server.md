---
title: nslookup server
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8de2d8a801d57a9197d5e8ec7d3b6adb2d00dd04
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838686"
---
# <a name="nslookup-server"></a>nslookup server

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 도메인 이름 시스템 (DNS) 도메인에 기본 서버를 변경합니다.
## <a name="syntax"></a>구문
```
server <DNSDomain>
```
### <a name="parameters"></a>매개 변수

|    매개 변수    |                          설명                           |
|-----------------|----------------------------------------------------------------|
|   <DNSDomain>   | 필수입니다. 기본 서버에 대 한 새 DNS 도메인을 지정합니다. |
| {도움말 및 #124;?} |     간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.      |

## <a name="remarks"></a>주의
- **서버** 명령은 현재의 기본 서버를 사용 하 여 지정된 된 DNS 도메인에 대 한 정보를 조회 합니다. 이 달리는 **lserver** 초기 서버를 사용 하는 명령입니다.
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup lserver](nslookup-lserver.md)
