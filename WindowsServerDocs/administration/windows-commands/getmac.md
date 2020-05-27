---
title: getmac
description: Getmac 명령에 대 한 참조 항목으로, MAC (미디어 액세스 제어) 주소와 각 로컬 또는 네트워크를 통해 연결 된 네트워크 프로토콜 목록을 반환 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a749a348-7cd1-4336-9f33-bb42dd0e31e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b84218b5506770bbefd5af8c89801547cc658f88
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819093"
---
# <a name="getmac"></a>getmac

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

반환 미디어 제어 (MAC) 주소 및 네트워크 프로토콜에 연결 된 각 컴퓨터에 모든 네트워크 카드에 대 한 각 주소 하거나 로컬 또는 네트워크를 통해 목록에 액세스 합니다. 이 명령은 네트워크 분석기에 MAC 주소를 입력 하려는 경우 또는 컴퓨터의 각 네트워크 어댑터에서 현재 사용 중인 프로토콜을 알아야 할 때 특히 유용 합니다.

## <a name="syntax"></a>구문

```
getmac[.exe][/s <computer> [/u <domain\<user> [/p <password>]]][/fo {table | list | csv}][/nh][/v]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| /s`<computer>` | 이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다. |
| /u`<domain>\<user>` | *사용자* 또는 *도메인 \*사용자가 지정한 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| /p`<password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| /fo {테이블 | list | csv | 쿼리 출력에 사용할 형식을 지정 합니다. 유효한 값은 **테이블**, **목록**, 및 **csv**합니다. 출력에 대 한 기본 형식은 **테이블**합니다. |
| /nh | 출력에서 열 머리글을 표시 하지 않습니다. **/Fo** 매개 변수가 **table** 또는 **csv**로 설정 된 경우에 유효 합니다. |
| /v | 출력이 자세한 정보를 표시 하도록 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

다음 예제에서는 사용 하는 방법을 보여는 **getmac** 명령:

```
getmac /fo table /nh /v
```

```
getmac /s srvmain
```

```
getmac /s srvmain /u maindom\hiropln
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo list /v
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo table /nh
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
