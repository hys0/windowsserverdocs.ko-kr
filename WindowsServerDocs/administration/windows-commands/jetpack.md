---
title: jetpack
description: WINS (Windows Internet Name Service) 또는 DHCP (Dynamic Host Configuration Protocol) 데이터베이스를 압축 하는 jetpack 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d77f9c964f5820fc7a44b803bb765e94cb35637
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818253"
---
# <a name="jetpack"></a>jetpack

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

WINS (Windows Internet Name Service) 또는 DHCP (Dynamic Host Configuration Protocol) 데이터베이스를 압축 합니다. 30 MB에 도달할 때까지 WINS 데이터베이스를 압축 하는 것이 좋습니다.

Jetpack는 다음을 수행 하 여 데이터베이스를 압축 합니다.

1. 임시 데이터베이스 파일에 데이터베이스 정보를 복사 하는 중입니다.

2. 원래 데이터베이스 파일을 삭제 합니다. 즉, WINS 또는 DHCP를 삭제 합니다.

3. 임시 데이터베이스 파일의 이름을 원래 파일 이름으로 바꿉니다.

## <a name="syntax"></a>구문

```
jetpack.exe <database_name> <temp_database_name>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| `<database_name>` | 원본 데이터베이스 파일의 이름을 지정 합니다. |
| `<temp_database_name>` | Jetpack에서 만들 임시 데이터베이스 파일의 이름을 지정 합니다.<p>참고:이 임시 파일은 compact 프로세스가 완료 되 면 제거 됩니다. 이 명령이 제대로 작동 하려면 임시 파일 이름이 고유 하 고 해당 이름을 가진 파일이 이미 존재 하지 않는지 확인 해야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

WINS 데이터베이스를 압축 하는 경우 (예: **.tmp. mdb** 는 임시 데이터베이스이 고, WINS-A는 wins 데이터베이스) 다음을 입력 **합니다** .

```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack Wins.mdb Tmp.mdb
NET start WINS
```

DHCP 데이터베이스를 압축 하는 경우. 여기서 **Tmp** 는 임시 데이터베이스이 고 **dhcp** 데이터베이스는 다음과 같이 입력 합니다.

```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERVER
jetpack Dhcp.mdb Tmp.mdb
NET start DHCPSERVER
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
