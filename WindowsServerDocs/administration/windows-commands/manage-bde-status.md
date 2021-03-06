---
title: manage-bde 상태
description: BitLocker로 보호 되는지 여부와 관계 없이 컴퓨터의 모든 드라이브에 대 한 정보를 제공 하는 manage-bde status 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20430899b8259207f228219cf0d2ac516866714a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922211"
---
# <a name="manage-bde-status"></a>manage-bde 상태

컴퓨터의 모든 드라이브에 대 한 정보를 제공 합니다. 다음을 포함 하 여 BitLocker로 보호 되는지 여부

- 크기

- BitLocker 버전

- 변환 상태

- 암호화 된 비율

- 암호화 방법

- 보호 상태

- 잠금 상태

- 식별 필드

- 키 보호기

## <a name="syntax"></a>구문

```
manage-bde -status [<drive>] [-protectionaserrorlevel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -protectionaserrorlevel | 볼륨이 보호 되 면 manage-bde 명령줄 도구에서 반환 코드 **0** 을 보내고 볼륨이 보호 되지 않는 경우 **1** 을 보냅니다. 드라이브가 BitLocker로 보호 되 고 있는지 여부를 확인 하기 위해 일괄 처리 스크립트에 가장 일반적으로 사용 됩니다. 사용할 수도 있습니다 **-p** 이 명령의 축약된 버전으로 합니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

C 드라이브의 상태를 표시 하려면 다음을 입력 합니다.

```
manage-bde –status C:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)
