---
title: klist
description: Klist 명령에 대 한 참조 문서로, 현재 캐시 된 Kerberos 티켓 목록을 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4689b4a9-1740-47dd-9240-02105efca428
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1a8d3d18cbf008efab203bfcef39179da39e109
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931420"
---
# <a name="klist"></a>klist

현재 캐시 된 Kerberos 티켓의 목록을 표시 합니다.

> [!IMPORTANT]
> 이 명령의 모든 매개 변수를 실행 하려면 적어도 **도메인 관리자**또는 이와 동등한 자격이 있어야 합니다.

## <a name="syntax"></a>구문

```
klist [-lh <logonID.highpart>] [-li <logonID.lowpart>] tickets | tgt | purge | sessions | kcd_cache | get | add_bind | query_bind | purge_bind
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -lh | 사용자의 LUID (로컬 고유 식별자)가 16 진수로 표현 된 상위 부분을 나타냅니다. **– Lh** 와 **– li** 모두 표시 되지 않는 경우이 명령은 현재 로그인 한 사용자의 LUID로 설정 됩니다. |
| -li | 사용자의 LUID (로컬 고유 식별자)가 16 진수로 표현 된 하위 부분을 나타냅니다. **– Lh** 와 **– li** 모두 표시 되지 않는 경우이 명령은 현재 로그인 한 사용자의 LUID로 설정 됩니다. |
| 티켓 | 지정 된 로그온 세션의 현재 캐시 된 티켓 (Tgt) 및 서비스 티켓을 나열 합니다. 기본 옵션입니다. |
| tgt | 초기 Kerberos TGT를 표시 합니다. |
| 제거가 | 지정 된 로그온 세션의 모든 티켓을 삭제할 수 있습니다. |
| 세션 | 이 컴퓨터의 로그온 세션 목록을 표시 합니다. |
| kcd_cache | Kerberos 제한 위임 캐시 정보를 표시 합니다. |
| Get | SPN (서비스 사용자 이름)으로 지정 된 대상 컴퓨터에 대 한 티켓을 요청할 수 있습니다. |
| add_bind | Kerberos 인증에 대 한 기본 설정 도메인 컨트롤러를 지정할 수 있습니다. |
| query_bind | Kerberos에 연결 된 각 도메인에 대해 캐시 된 기본 설정 도메인 컨트롤러 목록을 표시 합니다. |
| purge_bind | 지정 된 도메인에 대해 캐시 된 기본 설정 도메인 컨트롤러를 제거 합니다. |
| kdcoptions | RFC 4120에 지정 된 KDC (키 배포 센터) 옵션을 표시 합니다. |
| /? | 이 명령에 대 한 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 매개 변수를 제공 하지 않으면 **klist** 는 현재 로그온 한 사용자에 대 한 모든 티켓을 검색 합니다.

- 매개 변수는 다음 정보를 표시 합니다.

  - **티켓** -로그온 한 후에 인증 한 서비스의 현재 캐시 된 티켓을 나열 합니다. 캐시 된 모든 티켓의 다음 특성을 표시 합니다.

    - **로그온 id:** LUID입니다.

    - **클라이언트:** 클라이언트 이름 및 클라이언트의 도메인 이름 연결입니다.

    - **서버:** 서비스 이름 및 서비스의 도메인 이름 연결입니다.

    - **Kerbticket 암호화 유형:** Kerberos 티켓을 암호화 하는 데 사용 되는 암호화 유형입니다.

    - **티켓 플래그:** Kerberos 티켓 플래그입니다.

    - **시작 시간:** 티켓이 유효한 시간입니다.

    - **종료 시간:** 티켓이 더 이상 유효 하지 않게 되는 시간입니다. 이 시간을 지난 티켓은 더 이상 서비스에 인증 하거나 갱신 하는 데 사용 될 수 없습니다.

    - **갱신 시간:** 새 초기 인증이 필요한 시간입니다.

    - **세션 키 유형:** 세션 키에 사용 되는 암호화 알고리즘입니다.

  - **tgt** -초기 Kerberos tgt 및 현재 캐시 된 티켓의 다음 특성을 나열 합니다.

    - **로그온 id:** 16 진수로 식별 됩니다.

    - **ServiceName:** krbtgt

    - **TargetName `<SPN>` :** krbtgt

    - **도메인 이름:** TGT를 발급 하는 도메인의 이름입니다.

    - **Targetdomainname:** TGT가 발급 된 도메인입니다.

    - **Alttargetdomainname:** TGT가 발급 된 도메인입니다.

    - **티켓 플래그:** 주소 및 대상 작업 및 형식.

    - **세션 키:** 키 길이 및 암호화 알고리즘입니다.

    - **StartTime:** 티켓이 요청 된 로컬 컴퓨터 시간입니다.

    - **EndTime:** 티켓이 더 이상 유효 하지 않게 되는 시간입니다. 이 시간을 지난 티켓은 더 이상 서비스에 인증 하는 데 사용할 수 없습니다.

    - **RenewUntil:** 티켓 갱신에 대 한 최종 기한입니다.

    - **Timeskew:** 키 배포 센터 (KDC)와의 시간 차이입니다.

    - **EncodedTicket:** 인코딩된 티켓입니다.

  - **제거** -특정 티켓을 삭제할 수 있습니다. 티켓을 제거 하면 캐시 된 모든 티켓이 제거 되므로이 특성은 주의 해 서 사용 해야 합니다. 리소스에 인증 하지 못할 수 있습니다. 이 경우 로그 오프 한 후 다시 로그온 해야 합니다.

    - **로그온 id:** 16 진수로 식별 됩니다.

  - **세션** -이 컴퓨터의 모든 로그온 세션에 대 한 정보를 나열 하 고 표시할 수 있습니다.

    - **로그온 id:** 지정 된 경우 지정 된 값 으로만 로그온 세션을 표시 합니다. 지정 하지 않으면이 컴퓨터의 모든 로그온 세션을 표시 합니다.

  - **kcd_cache** -Kerberos 제한 위임 캐시 정보를 표시할 수 있습니다.

    - **로그온 id:** 지정 된 경우 지정 된 값으로 로그온 세션에 대 한 캐시 정보를 표시 합니다. 지정 하지 않으면 현재 사용자의 로그온 세션에 대 한 캐시 정보를 표시 합니다.

  - **get** -SPN으로 지정 된 대상에 대 한 티켓을 요청할 수 있습니다.

    - **로그온 id:** 지정 된 경우 지정 된 값으로 로그온 세션을 사용 하 여 티켓을 요청 합니다. 지정 하지 않으면는 현재 사용자의 로그온 세션을 사용 하 여 티켓을 요청 합니다.

    - **kdcoptions:** 지정 된 KDC 옵션으로 티켓을 요청 합니다.

  - **add_bind** -Kerberos 인증에 대 한 기본 설정 도메인 컨트롤러를 지정할 수 있습니다.

  - **query_bind** -도메인에 대해 캐시 된 기본 도메인 컨트롤러를 표시할 수 있습니다.

  - **purge_bind** -도메인에 대해 캐시 된 기본 설정 도메인 컨트롤러를 제거할 수 있습니다.

  - **kdcoptions** -현재 옵션 목록과 해당 설명을 보려면 [RFC 4120](http://www.ietf.org/rfc/rfc4120.txt)을 참조 하세요.

### <a name="examples"></a>예

Kerberos 티켓 캐시를 쿼리하여 티켓이 누락 되었는지 확인 하거나, 대상 서버 또는 계정에 오류가 있거나, 이벤트 ID 27 오류로 인해 암호화 형식이 지원 되지 않는 경우 다음을 입력 합니다.

```
klist
```

```
klist –li 0x3e7
```

로그온 세션을 위해 컴퓨터에 캐시 되는 각 티켓 허용 티켓의 세부 정보에 대해 알아보려면 다음을 입력 합니다.

```
klist tgt
```

Kerberos 티켓 캐시를 제거 하 고 로그 오프 한 다음 다시 로그인 하려면 다음을 입력 합니다.

```
klist purge
```

```
klist purge –li 0x3e7
```

로그온 세션을 진단 하 고 사용자 또는 서비스에 대 한 로그온 id을 찾으려면 다음을 입력 합니다.

```
klist sessions
```

Kerberos 제한 위임 오류를 진단 하 고 마지막으로 발생 한 오류를 찾으려면 다음을 입력 합니다.

```
klist kcd_cache
```

사용자 또는 서비스가 서버에 대 한 티켓을 가져올 수 있는지 진단 하거나 특정 SPN에 대 한 티켓을 요청 하려면 다음을 입력 합니다.

```
klist get host/%computername%
```

도메인 컨트롤러에서 복제 문제를 진단 하려면 일반적으로 특정 도메인 컨트롤러를 대상으로 하는 클라이언트 컴퓨터가 필요 합니다. 특정 도메인 컨트롤러에 대 한 클라이언트 컴퓨터를 대상으로 지정 하려면 다음을 입력 합니다.

```
klist add_bind CONTOSO KDC.CONTOSO.COM
```

```
klist add_bind CONTOSO.COM KDC.CONTOSO.COM
```

이 컴퓨터에서 최근에 연결 된 도메인 컨트롤러를 쿼리하려면 다음을 입력 합니다.

```
klist query_bind
```

도메인 컨트롤러를 다시 검색 하거나를 사용 하 여 새 도메인 컨트롤러 바인딩을 만들기 전에 캐시를 플러시하려면 `klist add_bind` 다음과 같이 입력 합니다.

```
klist purge_bind
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)