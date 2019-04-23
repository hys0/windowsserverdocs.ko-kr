---
title: NPS에서 정규식 사용
description: 이 항목에서는 Windows Server 2016에서 NPS의 패턴 일치에 대 한 정규식 사용에 설명 합니다. 네트워크 정책 특성 및 RADIUS 영역 조건을 지정 하려면이 구문을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a985df9fea31e5ee180caef4e69899ae8468ff71
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865264"
---
# <a name="use-regular-expressions-in-nps"></a>NPS에서 정규식 사용

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016에서 NPS의 패턴 일치에 대 한 정규식 사용에 설명 합니다. 네트워크 정책 특성 및 RADIUS 영역 조건을 지정 하려면이 구문을 사용할 수 있습니다.

## <a name="pattern-matching-reference"></a>패턴 일치 하는 참조

패턴 일치 구문을 사용 하 여 정규식을 만들면 다음 표에서 참조 원본으로 사용할 수 있습니다.

|문자|설명|예제|
|---------|-----------|-------|
|`\`  |일치 하는 문자 다음 문자를 표시 합니다. |`/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`  |
|`^`  |입력 또는 줄의 시작과 일치 합니다. | &nbsp; |
|`$`  |입력 또는 줄의 끝 부분과 일치 합니다. | &nbsp; |
|`*`  |선행 문자 0 회 이상 일치 합니다. |`/zo*/ matches either "z" or "zoo."` |
|`+`  |이전 문자를 한 번 이상 찾습니다. |`/zo+/ matches "zoo" but not "z."` |
|`?`  |이전 문자 0 회 또는 1 개 찾습니다. |`/a?ve?/ matches the "ve" in "never."` |
|`.`  |줄 바꿈 문자를 제외 하 고 단일 문자를 찾습니다.  | &nbsp; |
|`(pattern)`  |일치 하는 기억 하 고 "패턴"과 일치 합니다.<br />리터럴 문자를 일치 하도록 `(` 하 고 `)` (괄호)를 사용 하 여 `\(` 또는 `\)`합니다.   | &nbsp;  |
|`x|y `  |X 또는 y와 일치합니다.  |`/z|food?/ matches "zoo" or "food."` |
|`{n} `  |정확히 n 번 일치 \(n은 비\-음의 정수\)합니다.  |`/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`  |
|`{n,}`  |적어도 n 번 일치 \(n은 비\-음의 정수\)합니다.  |`/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.`  |
|`{n,m}`  |적어도 n이 고 최대 m 개 일치 \(m과 n은 비\-음수\)합니다.  |`/o{1,3}/ matches the first three instances of the letter o in "fooooood."`  |
|`[xyz]`  |대괄호로 묶은 문자 중 하 나와 일치 \(문자 집합을\)입니다.  |`/[abc]/ matches the "a" in "plain."`  |
|`[^xyz]`  |묶이지 않은 모든 문자를 찾습니다 \(부정 문자 집합을\)입니다.  |`/[^abc]/ matches the "p" in "plain."`  |
|`\b`  |단어 경계와 일치 \(예를 들어 공백을\)합니다.  |`/ea*r\b/ matches the "er" in "never early."`  |
|`\B`  |비단어 경계와 일치 합니다.  |`/ea*r\B/ matches the "ear" in "never early."`  |
|`\d`  |숫자를 찾습니다 \(0-9의 숫자에 해당\)합니다.  | &nbsp; |
|`\D`  |숫자가 아닌 문자를 찾습니다 \(같음 `[^0-9]` \)합니다.  | &nbsp; |
|`\f`  |용지 공급 문자를 일치 합니다.  | &nbsp; |
|`\n`  |일치 하는 줄 바꿈 문자입니다.  | &nbsp; |
|`\r`  |캐리지 리턴 문자를 찾습니다.  | &nbsp; |
|`\s`  |공백, 탭 및 용지 공급을 비롯 한 모든 공백 문자를 찾습니다 \(같음 `[ \f\n\r\t\v]` \)합니다.  | &nbsp; |
|`\S`  |공백이 아닌 문자를 찾습니다 \(같음 `[^ \f\n\r\t\v]` \)합니다.  | &nbsp; |
|`\t`  |탭 문자를 찾습니다.  | &nbsp; |
|`\v`  |세로 탭 문자를 찾습니다.  | &nbsp; |
|`\w`  |밑줄을 비롯 한 모든 단어 문자와 일치 \(같음 `[A-Za-z0-9_]` \)합니다.  | &nbsp; |
|`\W`  |이 아닌 모든 일치\-단어 문자를 밑줄을 제외한 \(같음 `[^A-Za-z0-9_]` \)합니다.  | &nbsp; |
|`\num`  |기억 된 일치 항목을 가리킵니다 \( `?num`, 여기서 숫자는 양의 정수\)합니다.  이 옵션을 에서만 사용할 수는 **대체** 특성 조작을 구성 하는 경우 텍스트 상자입니다.| `\1` 첫 번째 저장 된 일치 항목에 저장 된 것으로 바꿉니다.  |
|`/n/ `  |정규식 ASCII 코드 삽입을 허용 \( `?n`, 여기서 n은 8 진수, 16 진수 또는 10 진수 이스케이프 값을\)입니다.  | &nbsp; |

## <a name="examples-for-network-policy-attributes"></a>네트워크 정책 특성에 대 한 예제

다음 예제에서는 네트워크 정책 특성을 지정 하는 패턴 일치 구문은 사용에 설명 합니다.

- 899 영역 코드 내에서 모든 전화 번호를 지정 하려면 구문은 다음과 같습니다.

     `899.*`

- 192.168.1로 시작 하는 일정 범위의 IP 주소를 지정 하려면 구문은 다음과 같습니다.

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>사용자 이름 특성에 영역 이름 조작에 대 한 예제

다음 예제에 있는 사용자 이름 특성에 대 한 영역 이름을 조작 하는 패턴 일치 구문은 사용에 설명 합니다 **특성** 연결 요청 정책 속성 탭 합니다.

**사용자 이름 특성의 영역 부분을 제거 하려면**

아웃소싱 된 전화 접속 시나리오는 인터넷 서비스 공급자 \(ISP\) 조직을 NPS 연결 요청을 라우팅하, ISP RADIUS 프록시가 요청을 라우팅하는 인증 영역 이름 필요할 수 있습니다. 그러나 NPS 사용자 이름의 영역 이름 부분을 인식 하지 않을 수 있습니다. 따라서 조직 NPS에 전달 되기 전에 영역 이름은 ISP RADIUS 프록시에 의해 제거 해야 합니다.

- 찾기: @microsoft \.com

- 바꿀 대상:

**바꾸려면 *user@example.microsoft.com* 사용 하 여 *example.microsoft.com\user***

- 찾기:`(.*)@(.*)`

- 으로 바꿉니다.`$2\$1`



**바꾸려면 *domain\user* 사용 하 여 *specific_domain\user***

- 찾기:`(.*)\\(.*)`

- 바꾸기: *specific_domain*`\$2`



**바꾸려면 *사용자* 사용 하 여 *user@specific_domain***

- 찾기:`$`

- 바꾸기: @*specific_domain*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>프록시 서버에서 RADIUS 메시지 전달에 대 한 예제

NPS를 RADIUS 프록시로 사용 되는 경우 RADIUS 서버의 집합에 지정 된 영역 이름을 사용 하 여 RADIUS 메시지를 전달 하는 라우팅 규칙을 만들 수 있습니다. 다음은 영역 이름을 기반으로 하는 라우팅 요청에 대 한 권장 되는 구문입니다.

- **NetBIOS 이름**: `WCOAST`
- **패턴**:      `^wcoast\\`

다음 예제에서는 wcoast.microsoft.com에서는 DNS 또는 Active Directory 도메인 wcoast.microsoft.com에 대 한 고유한 사용자 계정 이름 (UPN) 접미사. 제공 된 패턴을 사용 하는 NPS 프록시 도메인 NetBIOS 이름 또는 UPN 접미사에 따라 메시지를 라우팅할 수 있습니다.

- **NetBIOS 이름**: `WCOAST`
- **UPN 접미사**:   `wcoast.microsoft.com`
- **패턴**:      `^wcoast\\|@wcoast\.microsoft\.com$`


NPS를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
