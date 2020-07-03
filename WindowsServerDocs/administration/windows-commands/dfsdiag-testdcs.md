---
title: dfsdiag testdcs
description: 지정 된 도메인에서 도메인 컨트롤러의 구성을 확인 하는 dfsdiag testdcs 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eca75d233661d51a36b52b79230ad36b704e203
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930665"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag testdcs

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 도메인의 각 도메인 컨트롤러에는 다음과 같은 테스트를 수행 하 여 도메인 컨트롤러의 구성을 확인 합니다.

- 분산 파일 시스템 (DFS) 네임 스페이스 서비스가 실행 중이 고 해당 시작 유형이 **자동**으로 설정 되어 있는지 확인 합니다.

- NETLOGON 및 SYSvol에 대 한 사이트 비용 조회 지원 여부를 확인 합니다.

- 호스트 이름 및 IP 주소 여 사이트 연결의 일관성을 확인합니다.

## <a name="syntax"></a>구문

```
dfsdiag /testdcs [/domain:<domain_name>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /domain`<domain_name>` | 확인할 도메인의 이름입니다. 이 매개 변수는 선택 사항입니다. 기본값은 로컬 호스트가 조인 된 로컬 도메인입니다. |

## <a name="examples"></a>예

*Contoso.com* 도메인에서 도메인 컨트롤러의 구성을 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [dfsdiag 명령](dfsdiag.md)
