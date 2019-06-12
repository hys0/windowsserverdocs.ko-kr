---
title: nslookup root
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47a26be99a5eee510970d3eee6b486331a98b159
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436901"
---
# <a name="nslookup-root"></a>nslookup root

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 이름 시스템 (DNS) 도메인 네임 스페이스의 루트에 대 한 서버에 기본 서버를 변경합니다.
## <a name="syntax"></a>구문
```
root 
```
## <a name="parameters"></a>매개 변수

|    매개 변수    |                      설명                      |
|-----------------|-------------------------------------------------------|
| {도움말 및 #124;?} | 간단한 요약이 표시 되며 **nslookup** 하위 명령입니다. |

## <a name="remarks"></a>설명
- 현재, ns.nic.ddn.mil 이름 서버가 사용 됩니다. 이 명령은 lserver ns.nic.ddn.mil에 대 한 동의어입니다. 루트 서버를의 이름을 변경할 수는 **세트 루트** 명령입니다.
  ## <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup 루트 설정](nslookup-set-root.md)
