---
title: DNS 클라이언트에서 DNS 클라이언트 쪽 캐싱을 사용 하지 않도록 설정
description: 이 문서에서는 DNS 클라이언트에서 DNS 클라이언트 쪽 캐싱을 사용 하지 않도록 설정 하는 방법을 소개 합니다.
manager: willchen
ms.prod: ''
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 3aeb7cb06f82b6f2220e42866682ce918389bf1d
ms.sourcegitcommit: b17ccf7f81e58e8f4dd844be8acf784debbb20ae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69023894"
---
# <a name="disable-dns-client-side-caching-on-dns-clients"></a>DNS 클라이언트에서 DNS 클라이언트 쪽 캐싱을 사용 하지 않도록 설정

Windows에는 클라이언트 쪽 DNS 캐시가 포함 되어 있습니다. 클라이언트 쪽 DNS 캐싱 기능은 dns "라운드 로빈" 부하 분산이 DNS 서버에서 Windows 클라이언트 컴퓨터로 발생 하지 않도록 하는 가짜 느낌을 생성할 수 있습니다. Ping 명령을 사용 하 여 동일한 A 레코드 도메인 이름을 검색 하는 경우 클라이언트는 동일한 IP 주소를 사용할 수 있습니다.  

## <a name="how-to-disable-client-side-caching"></a>클라이언트 쪽 캐싱을 사용 하지 않도록 설정 하는 방법

DNS 캐싱을 중지 하려면 다음 명령 중 하나를 실행 합니다.

```cmd
net stop dnscache
```

```cmd
sc servername stop dnscache
```


Windows에서 DNS 캐시를 영구적으로 사용 하지 않도록 설정 하려면 서비스 컨트롤러 도구 또는 서비스 도구를 사용 하 여 DNS 클라이언트 서비스 시작 유형을 사용 **안 함**으로 설정 합니다. Windows DNS 클라이언트 서비스의 이름은 "Dnscache"로 표시 될 수도 있습니다. 

> [!NOTE]
> DNS 확인자 캐시가 비활성화 되 면 클라이언트 컴퓨터의 전반적인 성능이 저하 되 고 DNS 쿼리에 대 한 네트워크 트래픽이 늘어납니다. 

DNS 클라이언트 서비스는 이전에 확인 된 이름을 메모리에 저장 하 여 DNS 이름 확인의 성능을 최적화 합니다. DNS 클라이언트 서비스가 꺼져 있는 경우 컴퓨터는 네트워크의 DNS 서버를 사용 하 여 DNS 이름을 계속 확인할 수 있습니다. 

Windows 확인자는 쿼리에 긍정 또는 부정 응답을 수신 하는 경우 해당 응답을 캐시에 추가 하 여 DNS 리소스 레코드를 만듭니다. 확인자는 DNS 서버를 쿼리 하기 전에 항상 캐시를 확인 합니다. DNS 리소스 레코드가 캐시에 있는 경우 확인자는 서버를 쿼리 하는 대신 캐시의 레코드를 사용 합니다. 이 동작은 쿼리를 신속 하 게 만들고 DNS 쿼리에 대 한 네트워크 트래픽을 감소 시킵니다. 

Ipconfig 도구를 사용 하 여 DNS 확인자 캐시를 보고 플러시할 수 있습니다. DNS 확인자 캐시를 보려면 명령 프롬프트에서 다음 명령을 실행 합니다.

```cmd
ipconfig /displaydns 
```

이 명령은 호스트 파일에서 미리 로드 된 DNS 리소스 레코드와 시스템에서 확인 한 최근에 쿼리 된 이름을 포함 하 여 DNS 확인자 캐시의 내용을 표시 합니다. 잠시 후 확인자는 캐시에서 레코드를 삭제 합니다. 기간은 DNS 리소스 레코드와 연결 된 **TTL (time To Live)** 값으로 지정 됩니다. 캐시를 수동으로 플러시할 수도 있습니다. 캐시를 플러시한 후 컴퓨터에서 이전에 컴퓨터에서 확인 한 DNS 리소스 레코드에 대 한 DNS 서버를 다시 쿼리해야 합니다. DNS 확인자 캐시의 항목을 삭제 하려면 명령 프롬프트에서 `ipconfig /flushdns` 를 실행 합니다.

## <a name="using-the-registry-to-control-the-caching-time"></a>레지스트리를 사용 하 여 캐싱 시간 제어

> [!IMPORTANT]  
> 이 섹션의 단계를 주의 깊게 따르십시오. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있으므로 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)해 두세요.

긍정 또는 부정 응답을 캐시 하는 기간은 다음 레지스트리 키의 항목 값에 따라 달라 집니다.

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNSCache\Parameters**

긍정 응답의 TTL은 다음 값 중 작은 값입니다. 

- 확인자에서 받은 쿼리 응답에 지정 된 시간 (초)입니다.

- **Maxcachettl** 레지스트리 설정의 값입니다.

>[!Note]
>- 긍정 응답의 기본 TTL은 86400 초 (1 일)입니다.
>- 부정 응답의 TTL은 MaxNegativeCacheTtl 레지스트리 설정에 지정 된 시간 (초)입니다.
>- 부정 응답의 기본 TTL은 900 초 (15 분)입니다.
부정 응답을 캐시 하지 않으려면 MaxNegativeCacheTtl 레지스트리 설정을 0으로 설정 합니다.

클라이언트 컴퓨터에서 캐싱 시간을 설정 하려면 다음을 수행 합니다.

1. 레지스트리 편집기 (Regedit.exe)를 시작 합니다.

2. 레지스트리에서 다음 키를 찾아 클릭 합니다.

   **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Dnscache\Parameters**

3. 편집 메뉴에서 새로 만들기를 가리키고 DWORD 값을 클릭 한 후 다음 레지스트리 값을 추가 합니다.

   - 값 이름: MaxCacheTtl

     데이터 형식: REG_DWORD

     방법 2 기본값은 86400 초입니다. 
     
     클라이언트의 DNS 캐시에서 최대 TTL 값을 1 초로 낮추면 클라이언트 쪽 DNS 캐시가 사용 하지 않도록 설정 되었음을 알 수 있습니다.    

   - 값 이름: MaxNegativeCacheTtl

     데이터 형식: REG_DWORD

     방법 2 기본값은 900 초입니다. 
     
     음수 응답이 캐시 되지 않도록 하려면 값을 0으로 설정 합니다.

4. 사용 하려는 값을 입력 한 다음 확인을 클릭 합니다.

5. 레지스트리 편집기를 종료합니다.