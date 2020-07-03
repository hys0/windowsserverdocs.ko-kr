---
title: dfsdiag testdfsconfig
description: 분산 파일 시스템 (DFS) 네임 스페이스의 구성을 확인 하는 dfsdiag testdfs config에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3387b661f454cff089f76f7c9c0d1abe59387010
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930639"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag testdfsconfig

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 작업을 수행 하 여 분산 파일 시스템 (DFS) 네임 스페이스의 구성을 확인 합니다.

- 모든 네임 스페이스 서버에서 DFS 네임 스페이스 서비스가 실행 중이 고 해당 시작 유형이 **자동** 으로 설정 되어 있는지 확인 합니다.

- DFS 레지스트리 구성 네임 스페이스 서버 간에 일관 되는지 확인 합니다.

- 클러스터형 네임 스페이스 서버에 대 한 다음 종속성의 유효성을 검사 합니다.

  - 네임 스페이스 루트 리소스에 대 한 종속성 네트워크 이름 리소스입니다.

  - IP 주소 리소스에 네트워크 이름 리소스 종속성입니다.

  - 실제 디스크 리소스에 네임 스페이스 루트 리소스 종속성입니다.

## <a name="syntax"></a>구문

```
dfsdiag /testdfsconfig /DFSroot:<namespace>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /DFSroot:`<namespace>` | 진단할 네임 스페이스 (DFS 루트)입니다. |

## <a name="examples"></a>예

*Com\MyNamespace*에서 DFS (분산 파일 시스템) 네임 스페이스의 구성을 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testdfsconfig /DFSroot:\contoso.com\MyNamespace
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [dfsdiag 명령](dfsdiag.md)
