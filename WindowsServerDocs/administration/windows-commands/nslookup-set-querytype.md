---
title: nslookup set querytype
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c066277a22325e5db8383f58cda31038aa656e0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838436"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리에 대 한 리소스 레코드 종류를 변경합니다.
## <a name="syntax"></a>구문
```
set querytype=<ResourceRecordtype>
```
### <a name="parameters"></a>매개 변수
<ResourceRecordtype> DNS 리소스 레코드 종류를 지정 합니다. 기본 리소스 레코드 종류는 A입니다. 다음 표에서이 명령에 대 한 유효한 값을 나열합니다.

| 값 |                                                   설명                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   A   |                                      컴퓨터&#39;의 IP 주소를 지정 합니다.                                      |
|  모든  |                                     컴퓨터&#39;의 IP 주소를 지정 합니다.                                      |
| CNAME |                                    별칭에 대 한 정식 이름을 지정합니다.                                     |
|  GID  |                                  그룹 이름의 그룹 식별자를 지정합니다.                                  |
| HINFO |                          컴퓨터&#39;의 CPU 및 운영 체제 유형을 지정 합니다.                           |
|  MB   |                                        사서함 도메인 이름을 지정합니다.                                         |
|  MG   |                                         메일 그룹 구성원을 지정합니다.                                          |
| MINFO |                                   사서함 또는 메일 목록 정보를 지정합니다.                                   |
|  MR   |                                     메일 이름 바꾸기 도메인 이름을 지정합니다.                                      |
|  MX   |                                          메일 교환기를 지정합니다.                                          |
|  NS   |                                 명명 된 영역에 대 한 DNS 이름 서버를 지정합니다.                                 |
|  PTR  | 컴퓨터를 지정 합니다. 경우에 쿼리는 IP 주소, 이름 그렇지 않으면 다른 정보에 대 한 포인터를 지정합니다. |
|  SOA  |                                DNS 영역에 대 한 권한-의-시작을 지정합니다.                                 |
|  TXT  |                                         텍스트 정보를 지정합니다.                                         |
|  UID  |                                         사용자 식별자를 지정합니다.                                          |
| UINFO |                                         사용자 정보를 지정합니다.                                         |
|  WKS  |                                         잘 알려진 서비스를 설명합니다.                                         |
| {도움말 |                                                       ?}                                                        |

간단한 요약이 표시 되며 <strong>nslookup</strong> 하위 명령
## <a name="remarks"></a>주의
- <strong>유형을 설정</strong> 와 동일한 기능을 수행 하는 명령에서 <strong>querytype 설정</strong> 명령입니다.
- 리소스 레코드 종류에 대 한 자세한 내용은 요청 설명 (Rfc) 1035을 참조 하세요.
  ## <a name="additional-references"></a>추가 참조
  href = 명령줄 구문 key.md = [-명령줄 구문 키 > 명령줄](command-line-syntax-key.md)구문 키 <</a> href = nslookup-type.md 데이터-원시-원본 =[nslookup](nslookup-set-type.md)집합 형식 > nslookup 집합 형식</a>를 <
