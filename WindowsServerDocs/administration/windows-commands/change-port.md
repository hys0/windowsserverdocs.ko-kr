---
title: change port
description: MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 나열 하거나 변경 하는 포트 변경 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0735c4c21ae8e321da1cfe31c2874f3dcfc540c7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922504"
---
# <a name="change-port"></a>change port

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

나열 하거나 MS-DOS 애플리케이션과 호환 되도록 COM 포트 매핑을 변경 합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

```
change port [<portX>=<portY| /d <portX | /query]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|-----------------|----------------------------------------|
| <portX>=<portY> | COM `<*portX*>` 을에 매핑합니다.`<*portY*>` |
| d<portX> | COM에 대 한 매핑을 삭제 합니다.`<*portX*>` |
| / 쿼리 | 현재 포트 매핑을 표시합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 대부분의 MS-DOS 애플리케이션 COM4 직렬 포트를 통해 c o m 1만 지원합니다. **포트 변경** 명령은 직렬 포트를 다른 포트 번호에 매핑하여, 번호가 매겨진 COM 포트를 지원 하지 않는 앱이 직렬 포트에 액세스할 수 있도록 합니다. 다시 매핑 현재 세션에 대해서만 작동 하며 세션에서 로그 오프 한 다음 다시 로그온 하는 경우 유지 되지 않습니다.

- 사용 하 여 **포트 변경** 대 한 현재 매핑을 사용할 수 있는 COM 포트를 표시 하려면 매개 변수 없이 합니다.

## <a name="examples"></a>예

- COM12 c o m 1을 사용 하기 위해 MS-DOS-기반 애플리케이션을 매핑하려면 다음을 입력 합니다.

  ```
  change port com12=com1
  ```

- 현재 매핑된 포트를 표시 하려면 다음을 입력 합니다.

  ```
  change port /query
  ```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [명령 변경](change.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
