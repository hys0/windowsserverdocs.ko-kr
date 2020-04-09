---
title: ETW를 사용 하 여 LDAP 연결 문제 해결
description: ETW를 설정 하 고 사용 하 여 AD DS 도메인 컨트롤러 간의 LDAP 연결을 추적 하는 방법을 설명 합니다.
author: Teresa-Motiv
manager: dcscontentpm
ms.prod: windows-server-dev
ms.technology: active-directory-lightweight-directory-services
audience: Admin
ms.author: v-tea
ms.topic: article
ms.date: 11/22/2019
ms.openlocfilehash: f7b7df714dbd02b15555fa20c70c1e995e121a48
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822936"
---
# <a name="using-etw-to-troubleshoot-ldap-connections"></a>ETW를 사용 하 여 LDAP 연결 문제 해결

[ETW(Windows용 이벤트 추적) (ETW)](https://docs.microsoft.com/windows/win32/etw/event-tracing-portal) 는 Active Directory Domain Services (AD DS)을 위한 유용한 문제 해결 도구 일 수 있습니다. ETW를 사용 하 여 AD DS 도메인 컨트롤러를 비롯 하 여 Windows 클라이언트와 LDAP 서버 간의[ldap](https://docs.microsoft.com/previous-versions/windows/desktop/ldap/lightweight-directory-access-protocol-ldap-api)(Lightweight Directory Access Protocol) 통신을 추적할 수 있습니다.

## <a name="how-to-turn-on-etw-and-start-a-trace"></a>ETW를 켜고 추적을 시작 하는 방법

**ETW를 켜려면**

1. 레지스트리 편집기를 열고 다음 레지스트리 하위 키를 만듭니다.

   **HKEY\_로컬\_MACHINE\\System\\CurrentControlSet\\서비스\\ldap\\추적\\* ProcessName***

   이 하위 키에서 *ProcessName* 는 확장을 포함 하 여 추적할 프로세스의 전체 이름입니다 (예: "svchost.exe").

1. (**선택 사항**) 이 하위 키 아래에서 **PID**라는 새 항목을 만듭니다. 이 항목을 사용 하려면 프로세스 ID를 DWORD 값으로 할당 합니다.  

   프로세스 ID를 지정 하는 경우 ETW는이 프로세스 ID를 가진 응용 프로그램 인스턴스만 추적 합니다.

**추적 세션을 시작 하려면**

- 명령 프롬프트 창을 열고 다음 명령을 실행 합니다.

   ```cmd
   tracelog.exe -start <SessionName> -guid \#099614a5-5dd7-4788-8bc9-e29f43db28fc -f <FileName> -flag <TraceFlags>
   ```

   이 명령의 자리 표시자는 다음 값을 나타냅니다.

  - \<*세션 이름*>는 추적 세션의 레이블을 나타내는 데 사용 되는 임의의 식별자입니다.  
  > [!NOTE]  
  > 나중에 추적 세션을 중지할 때이 세션 이름을 참조 해야 합니다.
  - \<*파일 이름*> 이벤트를 쓸 로그 파일을 지정 합니다.
  - \<*traceflags*>는 [추적 플래그 테이블](#values-for-trace-flags)에 나열 된 하나 이상의 값 이어야 합니다.

## <a name="how-to-end-a-tracing-session-and-turn-off-event-tracing"></a>추적 세션을 종료 하 고 이벤트 추적을 해제 하는 방법

**추적을 중지 하려면**

- 명령 프롬프트에서 다음 명령을 실행합니다.

   ```cmd
   tracelog.exe -stop <SessionName>
   ```

   이 명령에서 \<*세션*이름 >은 **tracelog .exe-시작** 명령에 사용한 것과 동일한 이름입니다.

**ETW를 해제 하려면**

- 레지스트리 편집기에서 **HKEY\_로컬\_MACHINE\\System\\CurrentControlSet\\Services\\ldap\\추적\\* ProcessName*** 하위 키를 삭제 합니다.

## <a name="values-for-trace-flags"></a>추적 플래그에 대 한 값

플래그를 사용 하려면 **traceflags .exe-start** 명령의 인수에서 <*traceflags*에 대 한 플래그 값 > 자리 표시자로 대체 합니다.

> [!NOTE]  
> 적절 한 플래그 값의 합계를 사용 하 여 여러 플래그를 지정할 수 있습니다. 예를 들어 0x00000001 ( **디버그\_검색** ) 및 0X00000010 ( **debug\_CACHE** ) 플래그를 지정 하려면 적절 한 \<*traceflags*> 값은 **0x00000011**입니다.

|플래그 이름 |플래그 값 |플래그 설명 |
| --- | --- | --- |
|**DEBUG_SEARCH** |0x00000001 |검색 요청 및 해당 요청에 전달 되는 매개 변수를 기록 합니다. 응답은 여기에 기록 되지 않습니다. 검색 요청만 기록 됩니다. ( **DEBUG_SPEWSEARCH** 를 사용 하 여 검색 요청에 대 한 응답을 기록할 수 있습니다.) |
|**DEBUG_WRITE** |0x00000002 |쓰기 요청 및 해당 요청에 전달 되는 매개 변수를 기록 합니다. 쓰기 요청에는 추가, 삭제, 수정 및 확장 작업이 포함 됩니다. |
|**DEBUG_REFCNT** |0x00000004 |연결 및 요청에 대 한 참조를 계산 하는 데이터 및 작업을 기록 합니다. |
|**DEBUG_HEAP** |0x00000008 |모든 메모리 할당과 메모리 릴리스를 기록 합니다. |
|**DEBUG_CACHE** |0x00000010 |로그 캐시 작업입니다. 이 활동에는 추가, 제거, 적중, 누락 등이 포함 됩니다. |
|**DEBUG_SSL** |0x00000020 |SSL 정보 및 오류를 기록 합니다. |
|**DEBUG_SPEWSEARCH** |0x00000040 |검색 요청에 대 한 모든 서버 응답을 기록 합니다. 이러한 응답에는 요청 된 특성과 수신 된 모든 데이터가 포함 됩니다. |
|**DEBUG_SERVERDOWN** |0x00000080 |서버 다운 및 연결 오류를 기록 합니다. |
|**DEBUG_CONNECT** |0x00000100 |연결 설정에 관련 된 데이터를 기록 합니다.<br />**DEBUG_CONNECTION** 를 사용 하 여 연결과 관련 된 다른 데이터를 기록 합니다. |
|**DEBUG_RECONNECT** |0x00000200 |자동 다시 연결 작업을 기록 합니다. 이 동작에는 다시 연결 시도, 오류 및 관련 오류가 포함 됩니다. |
|**DEBUG_RECEIVEDATA** |0x00000400 |서버에서 메시지를 수신 하는 작업과 관련 된 작업을 기록 합니다. 이 동작에는 "서버에서 응답을 기다리는 중" 및 서버에서 받은 응답 등의 이벤트가 포함 됩니다. |
|**DEBUG_BYTES_SENT** |0x00000800 |LDAP 클라이언트가 서버에 보낸 모든 데이터를 기록 합니다. 이 함수는 기본적으로 패킷 로깅 이지만 항상 암호화 되지 않은 데이터를 기록 합니다. (SSL을 통해 패킷을 전송 하는 경우이 함수는 암호화 되지 않은 패킷을 로깅합니다.) 이 로깅은 자세한 정보를 확인할 수 있습니다. 이 플래그는 자체에서 사용 하거나 **DEBUG_BYTES_RECEIVED**와 함께 사용 하는 것이 가장 좋습니다. |
|**DEBUG_EOM** |0x00001000 |메시지 목록의 끝에 도달 하는 것과 관련 된 이벤트를 로깅합니다. 이러한 이벤트에는 "메시지 목록 지우기" 등의 정보가 포함 됩니다. |
|**DEBUG_BER** |0x00002000 |BER (기본 인코딩 규칙)와 관련 된 작업 및 오류를 기록 합니다. 이러한 작업 및 오류에는 인코딩 문제, 버퍼 크기 문제 등이 포함 됩니다. |
|**DEBUG_OUTMEMORY** |0x00004000 |메모리 할당 실패를 기록 합니다. 는 필요한 메모리를 계산 하는 모든 오류 (예: 필요한 버퍼 크기를 계산할 때 발생 하는 오버플로)도 기록 합니다. |
|**DEBUG_CONTROLS** |0x00008000 |컨트롤과 관련 된 데이터를 기록 합니다. 이 데이터에는 삽입 된 컨트롤, 컨트롤에 영향을 주는 문제, 연결에 대 한 필수 컨트롤 등이 포함 됩니다. |
|**DEBUG_BYTES_RECEIVED** |0x00010000 |LDAP 클라이언트에서 수신 하는 모든 데이터를 기록 합니다. 이 동작은 기본적으로 패킷 로깅 이지만 항상 암호화 되지 않은 데이터를 기록 합니다. (SSL을 통해 패킷을 전송 하는 경우이 옵션은 암호화 되지 않은 패킷을 로깅합니다.) 이 유형의 로깅은 자세한 정보를 확인할 수 있습니다. 이 플래그는 자체에서 사용 하거나 **DEBUG_BYTES_SENT**와 함께 사용 하는 것이 가장 좋습니다. |
|**DEBUG_CLDAP** |0x00020000 |UDP 및 연결 없는 LDAP에 해당 하는 이벤트를 기록 합니다. |
|**DEBUG_FILTER** |0x00040000 |검색 필터를 만들 때 발생 하는 이벤트 및 오류를 기록 합니다.<br/>**참고** 이 옵션은 필터 생성 중에만 클라이언트 이벤트를 로깅합니다. 서버에서 필터에 대 한 응답을 기록 하지 않습니다. |
|**DEBUG_BIND** |0x00080000 |바인드 이벤트와 오류를 기록 합니다. 이 데이터에는 협상 정보, 바인드 성공, 바인딩 실패 등이 포함 됩니다. |
|**DEBUG_NETWORK_ERRORS** |0x00100000 |일반 네트워크 오류를 기록 합니다. 이 데이터에는 보내기 및 받기 오류가 포함 됩니다.<br/>**참고** 연결이 끊어졌거나 서버에 연결할 수 없는 경우 **DEBUG_SERVERDOWN** 기본 설정 된 태그입니다. |
|**DEBUG_VERBOSE** |0x00200000 |일반 메시지를 기록 합니다. 많은 양의 출력을 생성 하는 경향이 있는 모든 메시지에 대해이 옵션을 사용 합니다. 예를 들어 "메시지 끝에 도달 했습니다." 라는 메시지를 기록 하 고, "서버는 아직 응답 하지 않았습니다." 등의 메시지를 기록 합니다. 이 옵션은 일반 메시지에도 유용 합니다. |
|**DEBUG_PARSE** |0x00400000 |일반 메시지 이벤트와 오류를 비롯 하 여 패킷 구문 분석 및 인코딩 이벤트와 오류를 기록 합니다. |
|**DEBUG_REFERRALS** |0x00800000 |조회 및 추적 조회에 대 한 데이터를 기록 합니다. |
|**DEBUG_REQUEST** |0x01000000 |요청 추적을 기록 합니다. |
|**DEBUG_CONNECTION** |0x02000000 |일반 연결 데이터 및 오류를 기록 합니다. |
|**DEBUG_INIT_TERM** |0x04000000 |모듈 초기화 및 정리 (DLL 주 등)를 로깅합니다. |
|**DEBUG_API_ERRORS** |0x08000000 |API의 잘못 된 사용 로깅을 지원 합니다. 예를 들어이 옵션은 동일한 연결에서 바인드 작업을 두 번 호출 하는 경우 데이터를 기록 합니다. |
|**DEBUG_ERRORS** |0x10000000 |일반 오류를 기록 합니다. 이러한 오류는 대부분 모듈 초기화 오류, SSL 오류 또는 오버플로 또는 언더플로 오류로 분류 될 수 있습니다. |
|**DEBUG_PERFORMANCE** |0x20000000 |LDAP 요청에 대 한 서버 응답을 받은 후 프로세스-글로벌 LDAP 작업 통계에 대 한 데이터를 기록 합니다. |

## <a name="example"></a>예제

사용자 계정에 대 한 암호를 설정 하는 App1 응용 프로그램을 고려 합니다. App1에서 예기치 않은 오류가 발생 한다고 가정 합니다. ETW를 사용 하 여이 문제를 진단 하려면 다음 단계를 수행 합니다.

1. 레지스트리 편집기에서 다음 레지스트리 항목을 만듭니다.

   **HKEY\_로컬\_MACHINE\\System\\CurrentControlSet\\서비스\\ldap\\추적\\App1**

1. 추적 세션을 시작 하려면 명령 프롬프트 창을 열고 다음 명령을 실행 합니다.

   ```cmd
   tracelog.exe -start ldaptrace -guid \#099614a5-5dd7-4788-8bc9-e29f43db28fc -f .\ldap.etl -flag 0x80000
   ```

   이 명령이 시작 된 후 **\_바인딩 디버그** 를 수행 하면 ETW에서 추적 메시지를에 씁니다. ldap .etl을\\합니다.

1. App1를 시작 하 고 예기치 않은 오류를 재현 합니다.

1. 추적 세션을 중지 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

   ```cmd
    tracelog.exe -stop ldaptrace
   ```

1. 다른 사용자가 응용 프로그램을 추적 하지 못하게 하려면 **HKEY\_로컬\_MACHINE**\\**System**\\**CurrentControlSet**\\**서비스**\\**ldap**\\**추적**\\**App1** 레지스트리 항목을 삭제 합니다.

1. 추적 로그의 정보를 검토 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

   ```cmd
    tracerpt.exe .\ldap.etl -o -report
    ```

   > [!NOTE]  
   > 이 명령에서 **tracerpt** 는 [추적 소비자](https://go.microsoft.com/fwlink/p/?linkid=83876) 도구입니다.
