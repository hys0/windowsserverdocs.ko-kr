---
title: nslookup root
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d11179ff3cd22acd9df67261e7ab752aa159201a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838646"
---
# <a name="nslookup-root"></a>nslookup root

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

DNS (Domain Name System) 도메인 이름 공간의 루트에 대 한 서버에 기본 서버를 변경 합니다.
## <a name="syntax"></a>구문
```
root 
```
### <a name="parameters"></a>매개 변수

|    매개 변수    |                      설명                      |
|-----------------|-------------------------------------------------------|
| {도움말 및 #124;?} | 간단한 요약이 표시 되며 **nslookup** 하위 명령입니다. |

## <a name="remarks"></a>주의
- 현재, ns.nic.ddn.mil 이름 서버가 사용 됩니다. 이 명령은 lserver ns.nic.ddn.mil에 대 한 동의어입니다. 루트 서버를의 이름을 변경할 수는 **세트 루트** 명령입니다.
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup 루트 설정](nslookup-set-root.md)
