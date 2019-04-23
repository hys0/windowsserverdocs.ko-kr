---
title: nfsshare
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50df88a3fddbceb1595f328bdd4e3c6f526e3a2c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881694"
---
# <a name="nfsshare"></a>nfsshare



사용할 수 있습니다 **nfsshare** 제어 네트워크 파일 시스템 (NFS)을 공유 합니다.

## <a name="syntax"></a>구문

```
nfsshare <ShareName>=<Drive:Path> [-o <Option=value>...]
nfsshare {<ShareName> | <Drive>:<Path> | * } /delete
```

## <a name="description"></a>설명

인수 없이 **nfsshare** 명령줄 유틸리티는 NFS 용 서버에서 내보낸 모든 네트워크 파일 시스템 (NFS) 공유를 나열 합니다. 와 *ShareName* 을 유일한 인수로 **nfsshare** 로 식별 되는 NFS 공유의 속성을 나열 *ShareName*합니다. 때 *ShareName* 하 고 *드라이브 ***:*** 경로* 제공 됩니다 **nfsshare** 로 식별 되는 폴더를 내보냅니다 *드라이브 ***:*** 경로* 으로 *ShareName*합니다. 경우는 **/삭제** 옵션을 사용 하는 경우 지정된 된 폴더가 더 이상을 사용할 수 있는 NFS 클라이언트입니다.

## <a name="options"></a>변수

**nfsshare** 명령에는 다음 옵션 및 인수:

|용어|정의|
|----|----------|
|-o anon = {예 | no}|익명 (매핑되지 않음된) 사용자가 공유 디렉터리에 액세스할 수 있는지 여부를 지정 합니다. 기본값은 **없는**합니다.|
|-o rw[=\<Host>[:<Host>]...]|그룹으로 지정 된 호스트 또는 클라이언트의 공유 디렉터리에 대 한 읽기 / 쓰기 액세스를 제공 합니다. *호스트*합니다. 호스트 및 그룹 이름에 콜론 구분 (**:**). 경우 *호스트* 을 지정 하지 않으면 모든 호스트 및 클라이언트 그룹 (지정 된 문자를 제외한는 **ro** 옵션) 읽기 / 쓰기 액세스 권한이 있습니다. 모두는 **ro** 또는 **rw** 옵션 설정, 모든 클라이언트가 공유 디렉터리에 대 한 읽기 / 쓰기 액세스 권한이 있습니다.|
|-o ro[=\<Host>[:<Host>]...]|그룹으로 지정 된 호스트 또는 클라이언트의 공유 디렉터리에 대 한 읽기 전용 액세스를 제공 합니다. *호스트*합니다. 호스트 및 그룹 이름에 콜론 구분 (**:**). 경우 *호스트* 을 지정 하지 않으면 모든 클라이언트 (지정 된 문자를 제외한는 **rw** 옵션) 읽기 전용 액세스 권한이 있습니다. 하는 경우는 **ro** 하나 이상의 클라이언트에 대 한 옵션이 설정 되어 있지만 **rw** 옵션을 설정 하지 않으면 클라이언트 에서만 지정 된는 **ro** 옵션에는 공유 디렉터리에 대 한 액세스 권한이 있습니다.|
|-o encoding={big5|euc-jp|euc kr|tw euc|gb2312-80|ksc5601|shift-jis}|기본 인코딩을 파일 및 디렉터리 이름에 사용 되는 지정 하 고 지정을 사용 하는 경우 다음 중 하나를 설정 해야 합니다.</br>-   **big5** (중국어)</br>-   **euc jp** (일본어)</br>-   **euc kr** (한국어)</br>-   **tw euc** (중국어)</br>-   **gb2312 80** (중국어 간체)</br>-   **ksc5601** (한국어)</br>-   **shift jis** (일본어)</br>이 옵션은 하는 경우 기본 인코딩 체계는 ANSI 설정 되지 않은 또는 인코딩 체계 로캘에 대 한 기본 영어가 아닌 로캘의 경우 구성 된 시스템에서. 다음은 지정된 된 로캘에 대 한 기본 인코딩 체계입니다.</br>일본어: SHIFT JIS</br>-한국어: KS_C_5601-1987</br>-중국어 간체: GB2312-80</br>중국어 (번체): BIG5|
|-o anongid=\<gid>|익명 (매핑되지 않음된) 사용자가 사용 하 여 공유 디렉터리를 액세스 하도록 지정 *gid* 를 자신의 그룹 id (GID)로 합니다. 기본값은-2. 익명 GID 익명 액세스를 사용 하지 않도록 설정 하는 경우에 매핑되지 않은 사용자가 소유 하는 파일의 소유자를 보고할 때 사용 됩니다.|
|-o  anonuid=\<uid>|익명 (매핑되지 않음된) 사용자가 사용 하 여 공유 디렉터리를 액세스 하도록 지정 *uid* 를 자신의 사용자 id (UID)로 합니다. 기본값은-2. 익명 UID 익명 액세스를 사용 하지 않도록 설정 하는 경우에 매핑되지 않은 사용자가 소유 하는 파일의 소유자를 보고할 때 사용 됩니다.|
|-o root[=\<Host>[:<Host>]...]|그룹으로 지정 된 호스트 또는 클라이언트의 공유 디렉터리에 대 한 루트 액세스를 제공 합니다. *호스트*합니다. 호스트 및 그룹 이름에 콜론 구분 (**:**). 경우 *호스트* 을 지정 하지 않으면 루트 액세스할 수 있는 모든 클라이언트입니다. 하는 경우는 **루트** 옵션이 설정 되지 않은, 클라이언트가 없습니다. 루트 공유 디렉터리에 액세스할 수 있습니다.|
|/delete|하는 경우 *ShareName* 하거나 *드라이브 ***:*** 경로* 을 지정 하면 지정 된 공유를 삭제 합니다. 경우 *를 지정 하면 모든 NFS 공유를 삭제 합니다.|

> [!NOTE]
> 이 명령의 전체 구문을 보려면 명령 프롬프트에서 다음과 같이 입력합니다.</br>> **nfsshare /?**

##

[네트워크에 대 한 서비스 파일 시스템 명령 참조](services-for-network-file-system-command-reference.md) 참고