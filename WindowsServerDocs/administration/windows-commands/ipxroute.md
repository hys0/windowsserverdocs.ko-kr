---
title: ipxroute
description: Ipxroute 명령에 대 한 참조 항목으로, IPX 프로토콜에서 사용 하는 라우팅 테이블에 대 한 정보를 표시 하 고 수정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afcb5064bc8d4eb4a3b4a8920fcfcf71591d7af5
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818323"
---
# <a name="ipxroute"></a>ipxroute

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 하 고 IPX 프로토콜에 의해 사용 되는 라우팅 테이블에 대 한 정보를 수정 합니다. 매개 변수 없이 사용 **ipxroute** 알 수 없음, 브로드캐스트 및 멀티 캐스트 주소로 전송 된 패킷에 대 한 기본 설정을 표시 합니다.

## <a name="syntax"></a>구문

```
ipxroute servers [/type=x]
ipxroute ripout <network>
ipxroute resolve {guid | name} {GUID | <adaptername>}
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]
ipxroute config
```

### <a name="parameters"></a>매개 변수
| 매개 변수 | 설명 |
| ------- | -------- |
| 서버용`[/type=x]` | 지정 된 서버 유형에 대 한 서비스 액세스 지점 (SAP) 테이블을 표시합니다. **x** 는 정수 여야 합니다. 예를 들어는 `/type=4` 모든 파일 서버를 표시 합니다. **/Type**를 지정 하지 않으면에서 서버 `ipxroute servers` 이름을 나열 하는 모든 유형의 서버를 표시 합니다. |
| 해결 `{GUID | name}` 방법`{GUID | adaptername}` | GUID의 이름을 식별 이름으로 하거나 이름을 해당 GUID로 확인 됩니다. |
| 보드 = *n* | 쿼리 또는 매개 변수를 설정 하려는 네트워크 어댑터를 지정 합니다. |
| def | 모든 경로 브로드캐스트 패킷을 전송합니다. 원본 라우팅 테이블에 없는 고유한 미디어 액세스 카드 (MAC) 주소에 패킷이 전송 되는 경우 **ipxroute** 기본적으로 브로드캐스트하는 단일 경로 패킷을 보냅니다. |
| gbr | 모든 경로 브로드캐스트 패킷을 전송합니다. 패킷을 브로드캐스트 주소 (FFFFFFFFFFFF)에 전송 되는 경우 **ipxroute** 기본적으로 브로드캐스트하는 단일 경로 패킷을 보냅니다. |
| mbr | 모든 경로 브로드캐스트 패킷을 전송합니다. 패킷이 멀티 캐스트 주소 (C000xxxxxxxx)로 전송 되는 경우 **ipxroute** 기본적으로 브로드캐스트하는 단일 경로 패킷을 보냅니다. |
| remove =*이상* | 원본 라우팅 테이블에서 지정 된 노드 주소를 제거 합니다. |
| config | 모든 바인딩은 IPX가 구성에 대 한 정보를 표시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

워크스테이션에 연결 된 네트워크 세그먼트, 워크스테이션 노드 주소 및 사용 되는 유형을 프레임을 표시 하려면 다음을 입력 합니다.

```
ipxroute config
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
