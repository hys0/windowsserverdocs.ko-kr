---
title: klist
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4b35069faa835b59f2655262f640ddb18068702f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375312"
---
# <a name="klist"></a>klist



현재 캐시 된 Kerberos 티켓의 목록을 표시 합니다. 이 정보는 Windows Server 2012에 적용 됩니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
klist [-lh <LogonId.HighPart>] [-li <LogonId.LowPart>] tickets | tgt | purge | sessions | kcd_cache | get | add_bind | query_bind | purge_bind
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-lh|사용자의 LUID (로컬 고유 식별자)가 16 진수로 표현 된 상위 부분을 나타냅니다. – Lh 또는 – li가 모두 없는 경우 명령은 현재 로그인 한 사용자의 LUID로 기본 설정 됩니다.|
|-li|사용자의 LUID (로컬 고유 식별자)가 16 진수로 표현 된 하위 부분을 나타냅니다. – Lh 또는 – li가 모두 없는 경우 명령은 현재 로그인 한 사용자의 LUID로 기본 설정 됩니다.|
|종결|지정 된 로그온 세션의 현재 캐시 된 티켓 (Tgt) 및 서비스 티켓을 나열 합니다. 이 옵션이 기본 옵션입니다.|
|tgt|초기 Kerberos TGT를 표시 합니다.|
|비우기|지정 된 로그온 세션의 모든 티켓을 삭제할 수 있습니다.|
|세션|이 컴퓨터의 로그온 세션 목록을 표시 합니다.|
|kcd_cache|Kerberos 제한 위임 캐시 정보를 표시 합니다.|
|get|SPN (서비스 사용자 이름)으로 지정 된 대상 컴퓨터에 대 한 티켓을 요청할 수 있습니다.|
|add_bind|Kerberos 인증에 대 한 기본 설정 도메인 컨트롤러를 지정할 수 있습니다.|
|query_bind|Kerberos에 연결 된 각 도메인에 대해 캐시 된 기본 설정 도메인 컨트롤러 목록을 표시 합니다.|
|purge_bind|지정 된 도메인에 대해 캐시 된 기본 설정 도메인 컨트롤러를 제거 합니다.|
|kdcoptions|RFC 4120에 지정 된 KDC (키 배포 센터) 옵션을 표시 합니다.|
|/?|이 명령에 대 한 도움말을 표시합니다.|

## <a name="remarks"></a>설명

이 명령의 모든 매개 변수를 실행 하려면 최소한 **Domain Admins**의 구성원 이거나 이와 동등한 자격이 필요 합니다.

매개 변수를 제공 하지 않으면 Klist는 현재 로그온 한 사용자에 대 한 모든 티켓을 검색 합니다.

매개 변수는 다음 정보를 표시 합니다.
-   **종결**

    로그온 한 후에 사용자가 인증 한 서비스의 현재 캐시 된 티켓을 나열 합니다. 캐시 된 모든 티켓의 다음 특성을 표시 합니다.  
    -   로그온 id LUID
    -   클라이언트: 클라이언트 이름 및 클라이언트의 도메인 이름 연결
    -   서버: 서비스 이름 및 서비스의 도메인 이름 연결
    -   KerbTicket 암호화 유형: Kerberos 티켓을 암호화 하는 데 사용 되는 암호화 유형입니다.
    -   티켓 플래그: Kerberos 티켓 플래그
    -   시작 시간: 티켓이 유효 해야 하는 시간입니다.
    -   종료 시간: 티켓이 더 이상 유효 하지 않게 되는 시간입니다. 티켓은이 시간을 지난 후에는 더 이상 서비스에 인증 하거나 갱신에 사용 될 수 없습니다.
    -   갱신 시간: 새 초기 인증이 필요한 시간
    -   세션 키 유형: 세션 키에 사용 되는 암호화 알고리즘입니다.
-   **tgt**

    초기 Kerberos TGT 및 현재 캐시 된 티켓의 다음 특성을 나열 합니다.  
    -   로그온 id 16 진수로 식별
    -   ServiceName: krbtgt
    -   TargetName \<SPN >: krbtgt
    -   DomainName TGT를 발급 하는 도메인의 이름
    -   TargetDomainName: TGT가 발급 된 도메인
    -   AltTargetDomainName: TGT가 발급 된 도메인
    -   티켓 플래그: 주소 및 대상 작업 및 형식
    -   세션 키: 키 길이 및 암호화 알고리즘
    -   StartTime 티켓이 요청 된 로컬 컴퓨터 시간
    -   EndTime 티켓이 더 이상 유효 하지 않게 되는 시간입니다. 이 시간을 지난 티켓은 더 이상 서비스에 인증 하는 데 사용할 수 없습니다.
    -   RenewUntil: 티켓 갱신 최종 기한
    -   TimeSkew: 키 배포 센터 (KDC)와의 시간 차이
    -   EncodedTicket: 인코딩된 티켓
-   **제거가**

    특정 티켓을 삭제할 수 있습니다. 티켓을 제거 하면 캐시 된 모든 티켓이 제거 되므로이 특성은 주의 해 서 사용 해야 합니다. 리소스에 인증 하지 못할 수 있습니다. 이 경우에는 로그 오프 했다가 다시 로그온 해야 합니다.  
    -   로그온 id 16 진수로 식별
-   **세션**

    이 컴퓨터의 모든 로그온 세션에 대 한 정보를 나열 하 고 표시할 수 있습니다.  
    -   로그온 id 지정 된 경우 지정 된 값 으로만 로그온 세션을 표시 합니다. 지정 하지 않으면이 컴퓨터의 모든 로그온 세션을 표시 합니다.
-   **kcd_cache**

    Kerberos 제한 위임 캐시 정보를 표시할 수 있습니다.  
    -   로그온 id 지정 된 경우 지정 된 값으로 로그온 세션에 대 한 캐시 정보를 표시 합니다. 지정 하지 않으면 현재 사용자의 로그온 세션에 대 한 캐시 정보를 표시 합니다.
-   **get**

    SPN으로 지정 된 대상에 대 한 티켓을 요청할 수 있습니다.  
    -   로그온 id 지정 된 경우 지정 된 값으로 로그온 세션을 사용 하 여 티켓을 요청 합니다. 지정 하지 않으면는 현재 사용자의 로그온 세션을 사용 하 여 티켓을 요청 합니다.
    -   kdcoptions: 지정 된 KDC 옵션으로 티켓을 요청 합니다.
-   **add_bind**

    Kerberos 인증에 대 한 기본 설정 도메인 컨트롤러를 지정할 수 있습니다.
-   **query_bind**

    도메인에 대 한 캐시 된 기본 도메인 컨트롤러를 표시할 수 있습니다.
-   **purge_bind**

    도메인에 대 한 캐시 된 기본 도메인 컨트롤러를 제거할 수 있습니다.
-   **kdcoptions**

    현재 옵션 목록과 해당 설명을 보려면 [RFC 4120](http://www.ietf.org/rfc/rfc4120.txt)을 참조 하세요.

**기타 고려 사항**
-   Klist는 Windows Server 2012 및 Windows 8에서 사용할 수 있으며 특별 한 설치는 필요 하지 않습니다.

## <a name="BKMK_Examples"></a>예와

1. 대상 서버에 대 한 TGS (티켓 부여 서비스) 요청을 처리 하는 동안 이벤트 ID 27을 진단할 때이 계정에는 Kerberos 티켓을 생성 하는 데 적합 한 키가 없습니다. Klist를 사용 하 여 Kerberos 티켓 캐시를 쿼리하면 대상 서버 또는 계정에 오류가 있거나 암호화 형식이 지원 되지 않는 경우에는 티켓이 없는지 확인할 수 있습니다.  
   ```
   klist 
   ```  
   ```
   klist –li 0x3e7
   ```  
2. 오류를 진단 하 고 로그온 세션을 위해 컴퓨터에 캐시 된 각 티켓 허용 티켓의 세부 정보를 알고 싶으면 Klist를 사용 하 여 TGT 정보를 표시할 수 있습니다.  
   ```
   klist tgt
   ```  
3. 연결을 설정할 수 없고 진단이 너무 오래 걸릴 수 있는 경우 Kerberos 티켓 캐시를 제거 하 고 로그 오프 한 다음 다시 로그온 하면 됩니다.  
   ```
   klist purge
   ```  
   ```
   klist purge –li 0x3e7
   ```  
4. 사용자 또는 서비스에 대 한 로그온 세션을 진단 하려는 경우 다음 명령을 사용 하 여 다른 Klist 명령에 사용 되는 로그온 id를 찾을 수 있습니다.  
   ```
   klist sessions
   ```  
5. Kerberos 제한 위임 실패를 진단 하려는 경우 다음 명령을 사용 하 여 마지막으로 발생 한 오류를 찾을 수 있습니다.  
   ```
   klist kcd_cache
   ```  
6. 사용자 또는 서비스가 서버에 대 한 티켓을 가져올 수 있는지를 진단 하려는 경우이 명령을 사용 하 여 특정 SPN에 대 한 티켓을 요청할 수 있습니다.  
   ```
   klist get host/%computername%
   ```  
7. 도메인 컨트롤러에서 복제 문제를 진단할 때는 일반적으로 특정 도메인 컨트롤러를 대상으로 하는 클라이언트 컴퓨터가 필요 합니다. 이러한 경우 다음 명령을 사용 하 여 해당 특정 도메인 컨트롤러에 대 한 클라이언트 컴퓨터를 대상으로 지정할 수 있습니다.  
   ```
   klist add_bind CONTOSO KDC.CONTOSO.COM
   ```  
   ```
   klist add_bind CONTOSO.COM KDC.CONTOSO.COM
   ```  
8. 이 컴퓨터에 가장 최근에 연결한 도메인 컨트롤러를 쿼리하려면 다음 명령을 사용 하면 됩니다.  
   ```
   klist query_bind
   ```  
9. Kerberos에서 도메인 컨트롤러를 다시 검색 하도록 하려면 다음 명령을 사용할 수 있습니다. Klist add_bind를 사용 하 여 새 도메인 컨트롤러 바인딩을 만들기 전에이 명령을 사용 하 여 캐시를 플러시할 수도 있습니다.  
   ```
   klist purge_bind
   ```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)