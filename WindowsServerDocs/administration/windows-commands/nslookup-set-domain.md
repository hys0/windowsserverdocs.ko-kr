---
title: nslookup set domain
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9019893d92201079fb60b820a14dda3763bafd6b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886644"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 이름과 기본 도메인 이름 시스템 (DNS) 도메인 이름을 변경 합니다.
## <a name="syntax"></a>구문
```
set domain=<DomainName>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<DomainName>|기본 DNS 도메인 이름에 대 한 새 이름을 지정합니다. 기본 도메인 이름은 호스트 이름입니다.|
|{도움말 및 #124;?}|간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.|
## <a name="remarks"></a>설명
-   기본 DNS 도메인 이름 상태에 따라 조회 요청에 추가 됩니다는 **defname** 및 **검색** 옵션입니다. DNS 도메인 검색 목록 두 개 이상의 구성 요소 이름에 있으면 기본 DNS 도메인의 부모를 포함 합니다. 예를 들어, 기본 DNS 도메인이 mfg.widgets.com 이면 mfg.widgets.com와 widgets.com 검색 목록 이름은입니다. 사용 하 여는 **srchlist 설정** 다른 목록을 지정 하는 명령 및 **모두 설정** 목록을 표시 하는 명령입니다.
## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[nslookup 설정 srchlist](nslookup-set-srchlist.md)
[nslookup 모두 설정](nslookup-set-all.md)