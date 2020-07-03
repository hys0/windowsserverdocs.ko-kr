---
title: bitsadmin util and setieproxy
description: Service 계정을 사용 하 여 파일을 전송할 때 사용할 프록시 설정을 설정 하는 bitsadmin util 및 setieproxy 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 018e9400dd2463b61f053d37338740090670f51a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927317"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util and setieproxy

서비스 계정을 사용 하 여 파일을 전송할 때 사용할 프록시 설정을 설정 합니다. 성공적으로 완료 하려면 관리자 권한 명령 프롬프트에서이 명령을 실행 해야 합니다.

> [!NOTE]
> 이 명령은 BITS 1.5 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /util /setieproxy <account> <usage> [/conn <connectionname>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ---------- |
| account | 프록시 설정이 정의 하려는 서비스 계정을 지정 합니다. 가능한 값은 다음과 같습니다.<ul><li>LOCALSYSTEM</li><li>   NETWORKSERVICE</li><li>LOCALSERVICE.</li></ul> |
| usage | 프록시 검색을 사용 하 여 폼을 지정 합니다. 가능한 값은 다음과 같습니다.<ul><li>**NO_PROXY.** 프록시 서버를 사용 하지 마세요.</li><li>**자동 검색.** 프록시 설정을 자동으로 검색 합니다.</li><li>**MANUAL_PROXY.** 지정 된 프록시 목록 및 바이패스 목록을 사용 합니다. 사용 태그 바로 다음에 목록을 지정 해야 합니다. 예: `MANUAL_PROXY proxy1,proxy2 NULL`.<ul><li>**프록시 목록.** 사용할 프록시 서버를 쉼표로 구분한 목록입니다.</li><li>**바이패스 목록입니다.** 전송을 프록시를 통해 라우팅되지 않는 호스트 이름 또는 IP 주소 또는 둘 다의 공백으로 구분 된 목록입니다. 이 수 \<local> 동일한 LAN에 있는 모든 서버를 가리키도록 합니다. NULL 또는 값은 빈 프록시 무시 목록에 사용할 수 있습니다.</li></ul><li>**AUTOSCRIPT.** 자동 **검색**과 동일 합니다. 단, 스크립트도 실행 합니다. 사용 태그 바로 뒤에 스크립트 URL을 지정 해야 합니다. 예: `AUTOSCRIPT http://server/proxy.js`.</li><li>**다시 설정.** **NO_PROXY**와 동일 합니다. 단, 수동 프록시 url (지정 된 경우) 및 자동 검색을 사용 하 여 검색 된 url은 제거 합니다.</li></ul> |
| connectionname | 선택 사항입니다. **/Conn** 매개 변수와 함께 사용 하 여 사용할 모뎀 연결을 지정 합니다. **/Conn** 매개 변수를 지정 하지 않으면 BITS는 LAN 연결을 사용 합니다. |

### <a name="remarks"></a>설명

이 스위치를 사용 하 여 연속 된 각 호출은 이전에 정의 된 사용을 대체 하지만 이전에 정의 된 사용의 매개 변수는 대체 하지 않습니다. 예를 들어 별도의 호출에서 **NO_PROXY**, 자동 **검색**및 **MANUAL_PROXY** 를 지정 하는 경우 BITS는 마지막으로 제공 된 사용을 사용 하지만 이전에 정의 된 사용의 매개 변수를 유지 합니다.

## <a name="examples"></a>예

LOCALSYSTEM 계정에 대 한 프록시 사용을 설정 하려면:

```
bitsadmin /util /setieproxy localsystem AUTODETECT
```

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
```

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin util 명령](bitsadmin-util.md)

- [bitsadmin 명령](bitsadmin.md)
