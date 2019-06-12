---
title: klist
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4689b4a9-1740-47dd-9240-02105efca428
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0b77aed5970c74181ba03da5e57e9b230313a15
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438116"
---
# <a name="klist"></a>klist



현재 캐시 된 Kerberos 티켓의 목록을 표시합니다. 이 정보는 Windows Server 2012에 적용 됩니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
klist [-lh <LogonId.HighPart>] [-li <LogonId.LowPart>] tickets | tgt | purge | sessions | kcd_cache | get | add_bind | query_bind | purge_bind
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-lh|16 진수에서 표현 된 사용자의 고유한 로컬 식별자 (LUID)의 상위 부분을 나타냅니다. – Lh 또는 – li 모두 있는 경우이 명령은 현재 로그인 한 사용자의 LUID 기본값은입니다.|
|-li|16 진수에서 표현 된 사용자의 고유한 로컬 식별자 (LUID)의 하위 부분을 나타냅니다. – Lh 또는 – li 모두 있는 경우이 명령은 현재 로그인 한 사용자의 LUID 기본값은입니다.|
|티켓|현재 캐시 된--티켓 (Tgt) 및 지정 된 로그온 세션의 서비스 티켓을 나열합니다. 이 옵션이 기본 옵션입니다.|
|tgt|Kerberos 초기 TGT를 표시합니다.|
|비우기|지정 된 로그온 세션의 모든 티켓을 삭제할 수 있습니다.|
|세션|이 컴퓨터에 로그온 세션의 목록을 표시합니다.|
|kcd_cache|표시는 Kerberos 제한 위임 캐시 정보입니다.|
|get|서비스 주체 이름 (SPN)로 지정 된 대상 컴퓨터에 티켓을 요청할 수 있습니다.|
|add_bind|Kerberos 인증에 대 한 기본 도메인 컨트롤러를 지정할 수 있습니다.|
|query_bind|Kerberos에 연결 된 각 도메인에 대 한 캐시 된 기본 도메인 컨트롤러의 목록을 표시 합니다.|
|purge_bind|제거 캐시 된 기본 설정 지정 된 도메인에 대 한 도메인 컨트롤러입니다.|
|kdcoptions|4120 RFC에에서 지정 된 키 배포 센터 (KDC) 옵션이 표시 됩니다.|
|/?|이 명령에 대 한 도움말을 표시합니다.|

## <a name="remarks"></a>설명

멤버 자격이 **Domain Admins**, 또는 이와 동등한 최소한이이 명령의 모든 매개 변수를 실행 해야 합니다.

매개 변수 없이 제공 하는 경우 Klist 현재 로그온된 한 사용자에 대 한 모든 티켓을 검색 합니다.

매개 변수는 다음 정보를 표시 합니다.
-   **tickets**

    로그온 이후 사용자가 인증 하는 서비스의 현재 캐시 된 티켓을 나열 합니다. 모든 캐시 된 티켓의 다음 특성을 표시 합니다.  
    -   LogonID: LUID를
    -   클라이언트: 클라이언트 이름 및 클라이언트의 도메인 이름 연결
    -   서버: 서비스 이름 및 서비스의 도메인 이름 연결
    -   KerbTicket 암호화 유형: Kerberos 티켓을 암호화 하는 데 사용 되는 암호화 유형
    -   티켓 플래그: Kerberos 티켓 플래그
    -   시작 시간: 티켓을 유효한 됩니다 하는 시간
    -   종료 시간: 티켓이 더 이상 유효 해지는 시간입니다. 티켓을이 시간이 지난 경우 더 이상 사용할 수는 서비스를 인증 하거나 갱신에 사용했습니다
    -   시간을 갱신 합니다. 새 초기 인증에 필요한 시간
    -   세션 키 유형: 세션 키에 사용 되는 암호화 알고리즘
-   **tgt**

    초기 Kerberos TGT 및 현재 캐시 된 티켓의 다음 특성을 나열합니다.  
    -   LogonID: 16 진수 식별
    -   ServiceName: krbtgt
    -   TargetName \<SPN >: krbtgt
    -   도메인 이름: TGT를 발급 하는 도메인의 이름
    -   TargetDomainName: TGT에 발급 된 도메인
    -   AltTargetDomainName: TGT에 발급 된 도메인
    -   티켓 플래그: 주소 및 대상 작업 및 형식
    -   세션 키: 키 길이 및 암호화 알고리즘
    -   StartTime: 티켓 요청 된 로컬 컴퓨터 시간
    -   EndTime: 티켓이 더 이상 유효 해지는 시간입니다. 티켓을이 시간이 지난 경우 더 이상 서비스에 인증을 사용 수 없습니다.
    -   RenewUntil: 티켓 갱신 마감 날짜
    -   TimeSkew: 키 배포 센터 (KDC)를 사용 하 여 시간 차이
    -   EncodedTicket: 인코딩된 티켓
-   **purge**

    특정 티켓을 삭제할 수 있습니다. 캐시 되지 않은 모든 티켓 제거 티켓 제거 되므로 주의 해 서이 특성을 사용 합니다. 리소스에 인증할 수 없도록 하면 중지 될 수 있습니다 것입니다. 이 경우 로그 오프 했다가 다시 로그온 해야 합니다.  
    -   LogonID: 16 진수 식별
-   **sessions**

    나열 하 고이 컴퓨터에 모든 로그온 세션에 대 한 정보를 표시할 수 있습니다.  
    -   LogonID: 를 지정 하는 경우 지정된 된 값에 의해서만 로그온 세션을 표시 합니다. 지정 하지 않으면이 컴퓨터에서 모든 로그온 세션을 표시 합니다.
-   **kcd_cache**

    Kerberos 제한 위임 캐시 정보를 표시할 수 있습니다.  
    -   LogonID: 를 지정 하는 경우 지정된 된 값에서 로그온 세션에 대 한 캐시 정보를 표시 합니다. 지정 하지 않으면 현재 사용자의 로그온 세션에 대 한 캐시 정보를 표시 합니다.
-   **get**

    SPN 지정 된 대상에 티켓을 요청할 수 있습니다.  
    -   LogonID: 를 지정 하는 경우 지정된 된 값에서 로그온 세션을 사용 하 여 티켓을 요청 합니다. 지정 하지 않으면 현재 사용자의 로그온 세션을 사용 하 여 티켓을 요청 합니다.
    -   kdcoptions: 지정된 된 KDC 옵션을 사용 하 여 티켓을 요청
-   **add_bind**

    Kerberos 인증에 대 한 기본 도메인 컨트롤러를 지정할 수 있습니다.
-   **query_bind**

    도메인에 대 한 캐시 된 기본 도메인 컨트롤러를 표시할 수 있습니다.
-   **purge_bind**

    도메인에 대 한 캐시 된 기본 도메인 컨트롤러를 제거할 수 있습니다.
-   **kdcoptions**

    옵션 및 해당 설명의 현재 목록에 대 한 참조 [RFC 4120](http://www.ietf.org/rfc/rfc4120.txt)합니다.

**기타 고려 사항**
-   Klist.exe는 Windows Server 2012 및 Windows 8에서 사용할 수 있는 하며 특수 설치할 필요가 없습니다.

## <a name="BKMK_Examples"></a>예제

1. 처리 하는 동안 이벤트 ID 27을 진단 하는 경우 티켓 부여 서비스 (TGS) 요청 대상 서버에 대 한 계정에 Kerberos 티켓을 생성 하는 적합 한 키 없었습니다. Klist Kerberos 티켓 캐시 계정을 확인 하는 대상 서버 오류를 반환 하는 경우 모든 티켓, 누락 된 경우 또는 암호화 유형이 지원 되지 않는 경우를 확인 하려면 쿼리를 사용할 수 있습니다.  
   ```
   klist 
   ```  
   ```
   klist –li 0x3e7
   ```  
2. 오류를 진단 하는 경우 각 티켓--티켓 로그온 세션에 대 한 컴퓨터에 캐시 되는 세부 사항을 알 하려는 Klist TGT 정보를 표시 하려면 사용할 수 있습니다.  
   ```
   klist tgt
   ```  
3. 에 연결할 수 없는 경우 진단 너무 오래 걸릴 수 있습니다 Kerberos 티켓 캐시 제거 수, 로그 오프 한 다음 다시 로그온 합니다.  
   ```
   klist purge
   ```  
   ```
   klist purge –li 0x3e7
   ```  
4. 사용자 또는 서비스에 대 한 로그온 세션을 진단 하려는 경우 다른 Klist 명령에서 사용 되는 로그온 Id를 찾으려면 다음 명령을 사용할 수 있습니다.  
   ```
   klist sessions
   ```  
5. Kerberos 제한 위임 실패를 진단 하려는 경우에 발생 한 마지막 오류를 찾으려면 다음 명령을 사용할 수 있습니다.  
   ```
   klist kcd_cache
   ```  
6. 사용자가 진단 하려는 때나 서비스 서버에 티켓을 가져올 수 특정 SPN에 대 한 티켓을 요청 하려면이 명령을 사용할 수 있습니다.  
   ```
   klist get host/%computername%
   ```  
7. 도메인 컨트롤러에서 복제 문제를 진단할 때 특정 도메인 컨트롤러를 대상으로 클라이언트 컴퓨터를 일반적으로 필요 합니다. 이러한 경우에는 특정 도메인 컨트롤러에 클라이언트 컴퓨터를 대상으로 다음 명령을 사용할 수 있습니다.  
   ```
   klist add_bind CONTOSO KDC.CONTOSO.COM
   ```  
   ```
   klist add_bind CONTOSO.COM KDC.CONTOSO.COM
   ```  
8. 어떤 도메인 컨트롤러에 연결할 최근에이 컴퓨터를 쿼리하려면 다음 명령을 사용할 수 있습니다.  
   ```
   klist query_bind
   ```  
9. 도메인 컨트롤러를 다시 검색 하는 Kerberos를 하려는 경우 다음 명령을 사용할 수 있습니다. 이 명령은 klist add_bind를 사용 하 여 새 도메인 컨트롤러 바인딩을 만들기 전에 캐시를 플러시하려면 데도 사용할 수 있습니다.  
   ```
   klist purge_bind
   ```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)