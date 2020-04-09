---
title: nslookup set domain
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa433383e23fd19779960348e0af88e0a405ff83
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838466"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 DNS (Domain Name System) 도메인 이름을 지정 된 이름으로 변경 합니다.
## <a name="syntax"></a>구문
```
set domain=<DomainName>
```
### <a name="parameters"></a>매개 변수

|    매개 변수    |                                           설명                                           |
|-----------------|-------------------------------------------------------------------------------------------------|
|  <DomainName>   | 기본 DNS 도메인 이름에 대 한 새 이름을 지정합니다. 기본 도메인 이름은 호스트 이름입니다. |
| {도움말 및 #124;?} |                      간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.                      |

## <a name="remarks"></a>주의
- 기본 DNS 도메인 이름 상태에 따라 조회 요청에 추가 됩니다는 **defname** 및 **검색** 옵션입니다. DNS 도메인 검색 목록 두 개 이상의 구성 요소 이름에 있으면 기본 DNS 도메인의 부모를 포함 합니다. 예를 들어, 기본 DNS 도메인이 mfg.widgets.com 이면 mfg.widgets.com와 widgets.com 검색 목록 이름은입니다. 사용 하 여는 **srchlist 설정** 다른 목록을 지정 하는 명령 및 **모두 설정** 목록을 표시 하는 명령입니다.
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md)
  [nslookup set srchlist](nslookup-set-srchlist.md)
  nslookup set [all](nslookup-set-all.md)
