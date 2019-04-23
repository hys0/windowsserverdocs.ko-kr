---
title: nslookup set type
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5248e314-fac1-413e-81dc-bbe0a0873ba5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: accf8ccbe147a831ee306dd670384b90844ff4fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835954"
---
# <a name="nslookup-set-type"></a>nslookup set type

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리에 대 한 리소스 레코드 종류를 변경합니다.
## <a name="syntax"></a>구문
```
set type=<ResourceRecordtype>
```
## <a name="parameters"></a>매개 변수
<ResourceRecordtype> DNS 리소스 레코드 종류를 지정합니다. 기본 리소스 레코드 종류는 A입니다. 다음 표에서이 명령에 대 한 유효한 값을 나열합니다.
|값|설명|
|-----|--------|
|변수를 잠그기 위한|컴퓨터의 IP 주소를 지정합니다.|
|모든|컴퓨터의 IP 주소를 지정합니다.|
|CNAME|별칭에 대 한 정식 이름을 지정합니다.|
|GID|그룹 이름의 그룹 식별자를 지정합니다.|
|HINFO|컴퓨터의 CPU 및 운영 체제의 유형을 지정합니다.|
|MB|사서함 도메인 이름을 지정합니다.|
|MG|메일 그룹 구성원을 지정합니다.|
|MINFO|사서함 또는 메일 목록 정보를 지정합니다.|
|MR|메일 이름 바꾸기 도메인 이름을 지정합니다.|
|MX|메일 교환기를 지정합니다.|
|NS|명명 된 영역에 대 한 DNS 이름 서버를 지정합니다.|
|PTR|컴퓨터를 지정 합니다. 경우에 쿼리는 IP 주소, 이름 그렇지 않으면 다른 정보에 대 한 포인터를 지정합니다.|
|SOA|DNS 영역에 대 한 권한-의-시작을 지정합니다.|
|TXT|텍스트 정보를 지정합니다.|
|UID|사용자 식별자를 지정합니다.|
|UINFO|사용자 정보를 지정합니다.|
|WKS|잘 알려진 서비스를 설명합니다.|
{도움말 | ?}
간단한 요약이 표시 되며 **nslookup** 하위 명령
## <a name="remarks"></a>설명
-   **유형을 설정** 와 동일한 기능을 수행 하는 명령에서 **querytype 설정** 명령입니다.
-   리소스 레코드 종류에 대 한 자세한 내용은 주석 Rfc 1035에 대 한 요청을 참조 하세요.
## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[nslookup querytype 설정](nslookup-set-querytype.md)
