---
title: nfsstat
description: NFS (네트워크 파일 시스템) 및 RPC (원격 프로시저 호출) 호출에 대 한 통계 정보를 표시 하는 nfsstat 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 833081baa3ae9a0c2493623a7d015334087ee26d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934789"
---
# <a name="nfsstat"></a>nfsstat

NFS (네트워크 파일 시스템) 및 RPC (원격 프로시저 호출) 호출에 대 한 통계 정보를 표시 하는 명령줄 유틸리티입니다. 매개 변수 없이 사용 하는 경우이 명령은 모든 통계를 다시 설정 하지 않고 모든 통계 데이터를 표시 합니다.

## <a name="syntax"></a>구문

```
nfsstat [-c][-s][-n][-r][-z][-m]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -c | 클라이언트에서 보내고 거부 한 클라이언트 쪽 NFS 및 RPC 및 NFS 호출만 표시 합니다. NFS 또는 RPC 정보만 표시 하려면이 플래그를 **-n** 또는 **-r** 매개 변수와 결합 합니다. |
| -S | 서버에서 보내고 거부 한 서버 쪽 NFS 및 RPC 및 NFS 호출만 표시 합니다. NFS 또는 RPC 정보만 표시 하려면이 플래그를 **-n** 또는 **-r** 매개 변수와 결합 합니다. |
| -M | 탑재 옵션에 의해 설정 된 탑재 플래그, 시스템 내부에 있는 탑재 플래그 및 기타 탑재 정보를 표시 합니다. |
| -n | 클라이언트와 서버 모두에 대 한 NFS 정보를 표시 합니다. NFS 클라이언트나 서버 정보만 표시 하려면이 플래그를 **-c** 또는 **-s** 매개 변수와 결합 합니다. |
| -r | 클라이언트와 서버 모두에 대 한 RPC 정보를 표시 합니다. RPC 클라이언트나 서버 정보만 표시 하려면이 플래그를 **-c** 또는 **-s** 매개 변수와 결합 합니다. |
| -Z | 호출 통계를 다시 설정 합니다. 이 플래그는 루트 사용자만 사용할 수 있으며 다른 매개 변수와 결합 하 여 특정 통계 집합을 표시 한 후 다시 설정할 수 있습니다. |

### <a name="examples"></a>예

클라이언트에서 보내고 거부 한 RPC 및 NFS 호출 수에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
nfsstat -c
```

클라이언트 NFS 호출 관련 정보를 표시 하 고 인쇄 하려면 다음을 입력 합니다.

```
nfsstat -cn
```

클라이언트와 서버 모두에 대 한 RPC 호출 관련 정보를 표시 하려면 다음을 입력 합니다.

```
nfsstat -r
```

서버에서 받아서 거부 한 RPC 및 NFS 호출 수에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
nfsstat -s
```

클라이언트와 서버에서 모든 호출 관련 정보를 0으로 다시 설정 하려면 다음을 입력 합니다.

```
nfsstat -z
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [네트워크 파일 시스템 서비스 명령 참조](services-for-network-file-system-command-reference.md)

- [NFS cmdlet 참조](https://docs.microsoft.com/powershell/module/nfs)
