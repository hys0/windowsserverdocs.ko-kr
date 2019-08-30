---
title: NPS에서 정규식 사용
description: 이 항목에서는 Windows Server에서 NPS의 패턴 일치에 정규식을 사용 하는 방법을 설명 합니다. 이 구문을 사용 하 여 네트워크 정책 특성 및 RADIUS 영역 조건을 지정할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: jgerend
author: jasongerend
msdate: 08/16/2019
ms.openlocfilehash: 76615fcccfe06333a76f872b52d2e88182fd60e5
ms.sourcegitcommit: e58e1646ffd75d4a89576d967b2dbbbb84764303
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "69584793"
---
# <a name="use-regular-expressions-in-nps"></a>NPS에서 정규식 사용

> 적용 대상:  Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

이 항목에서는 Windows Server에서 NPS의 패턴 일치에 정규식을 사용 하는 방법을 설명 합니다. 이 구문을 사용 하 여 네트워크 정책 특성 및 RADIUS 영역 조건을 지정할 수 있습니다.

## <a name="pattern-matching-reference"></a>패턴 일치 참조

패턴 일치 구문을 사용 하 여 정규식을 만들 때 다음 표를 참조 소스로 사용할 수 있습니다. 정규식 패턴은 종종 슬래시 (/)로 둘러싸여 있습니다.

|  문자  |  설명  |   예제                                                                 |
| ----------- | ------------- | ------------------------------------------------------------------------  |
|     `\ `     | 뒤에 오는 문자가 특수 문자 이거나 리터럴로 해석 되어야 함을 나타냅니다.  | `/n/ matches the character "n" while the sequence /\n/ matches a line feed or newline character.`  |
|     `^`     |                                                                 입력 또는 줄의 시작 부분을 찾습니다.                                                                  |                                                                 &nbsp;                                                                  |
|     `$`     |                                                                    입력 또는 줄의 끝을 찾습니다.                                                                     |                                                                 &nbsp;                                                                  |
|     `*`     |                                                             이전 문자를 0 번 이상 찾습니다.                                                              |                                                  `/zo*/ matches either "z" or "zoo."`                                                   |
|     `+`     |                                                              이전 문자를 한 번 이상 찾습니다.                                                              |                                                   `/zo+/ matches "zoo" but not "z."`                                                    |
|     `?`     |                                                              이전 문자를 0 번 또는 한 번 찾습니다.                                                              |                                                 `/a?ve?/ matches the "ve" in "never."`                                                  |
|     `.`     |                                                           줄 바꿈 문자를 제외한 모든 단일 문자를 찾습니다.                                                           |                                                                 &nbsp;                                                                  |
| `(pattern)` |                         "Pattern"과 일치 하 고 일치 항목을 기억 합니다.<br />`(` 리터럴 문자와 `)` (괄호)를 일치 시키려면 또는 `\)`를 사용 `\(` 합니다.                         |                                                                 &nbsp;                                                                  |
|   `x | y `  |                                                                               X 또는 y와 일치 합니다.                                                          |
|   `{n} `    |                                                          정확히 n 번 \(일치 n은 음수가 아닌\-정수\)입니다.                                                           |               `/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`               |
|   `{n,}`    |                                                          적어도 n 번 \(일치 n n은 음수가 아닌\-정수\)입니다.                                                          | `/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.` |
|   `{n,m}`   |                                                는 적어도 n ~ m 번 \(이상 일치 하며 n은 음수가 아닌\-정수\)입니다.                                                |                               `/o{1,3}/ matches the first three instances of the letter o in "fooooood."`                               |
|   `[xyz]`   |                                                       문자 집합 \(\)에서 포함 된 문자 중 하나를 찾습니다.                                                        |                                                  `/[abc]/ matches the "a" in "plain."`                                                  |
|  `[^xyz]`   |                                                  음수 문자 집합 \(\)으로 묶지 않은 모든 문자를 찾습니다.                                                  |                                                 `/[^abc]/ matches the "p" in "plain."`                                                  |
|    `\b`     |                                                              단어 경계 \((예: 공백\))를 찾습니다.                                                               |                                              `/ea*r\b/ matches the "er" in "never early."`                                              |
|    `\B`     |                                                                         단어가 아닌 경계와 일치 합니다.                                                                          |                                             `/ea*r\B/ matches the "ear" in "never early."`                                              |
|    `\d`     |                                                       0에서 9\)까지의 \(숫자에 해당 하는 숫자 문자를 찾습니다.                                                        |                                                                 &nbsp;                                                                  |
|    `\D`     |                                                           에 \( 해당하는\)nondigit 문자를 찾습니다. `[^0-9]`                                                           |                                                                 &nbsp;                                                                  |
|    `\f`     |                                                                        양식 피드 문자를 찾습니다.                                                                        |                                                                 &nbsp;                                                                  |
|    `\n`     |                                                                        줄 바꿈 문자를 찾습니다.                                                                        |                                                                 &nbsp;                                                                  |
|    `\r`     |                                                                     캐리지 리턴 문자를 찾습니다.                                                                     |                                                                 &nbsp;                                                                  |
|    `\s`     |                                   에 \( 해당하는\)공백, 탭 및 폼 피드를 포함 하는 공백 문자를 찾습니다. `[ \f\n\r\t\v]`                                   |                                                                 &nbsp;                                                                  |
|    `\S`     |                                                  에 해당 하는 공백이 아닌 문자 \(를 `[^ \f\n\r\t\v]` \)찾습니다.                                                   |                                                                 &nbsp;                                                                  |
|    `\t`     |                                                                           탭 문자를 찾습니다.                                                                           |                                                                 &nbsp;                                                                  |
|    `\v`     |                                                                      세로 탭 문자를 찾습니다.                                                                       |                                                                 &nbsp;                                                                  |
|    `\w`     |                                              에 \( 해당하는\)밑줄을 포함 하 여 모든 단어 문자를 찾습니다. `[A-Za-z0-9_]`                                              |                                                                 &nbsp;                                                                  |
|    `\W`     |                                           에 해당 하\- \( 는밑줄을\)제외한 모든 단어가 아닌 문자를 찾습니다. `[^A-Za-z0-9_]`                                           |                                                                 &nbsp;                                                                  |
|   `\num`    | 는 기억 된 일치 \(항목 `?num`을 참조 합니다. 여기서 num\)은 양의 정수입니다.  이 옵션은 특성 조작을 구성할 때 **바꾸기** 텍스트 상자 에서만 사용할 수 있습니다. |                                       `\1`는 기억 된 첫 번째 일치 항목에 저장 된 항목을 바꿉니다.                                       |
|   `/n/ `    |                      정규식 \(\)에 ASCII 코드를 삽입할 수 있습니다. 여기서 n은 8 진수, 16 진수 또는 10 진수 이스케이프 값입니다. `?n`                       |                                                                 &nbsp;                                                                  |

## <a name="examples-for-network-policy-attributes"></a>네트워크 정책 특성에 대 한 예제

다음 예에서는 패턴 일치 구문을 사용 하 여 네트워크 정책 특성을 지정 하는 방법을 설명 합니다.

- 899 지역 코드 내에 모든 전화 번호를 지정 하려면 구문은 다음과 같습니다.

     `899.*`

- 192.168.1로 시작 하는 IP 주소 범위를 지정 하려면 구문은 다음과 같습니다.

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>사용자 이름 특성에서 영역 이름을 조작 하는 예

다음 예에서는 패턴 일치 구문을 사용 하 여 연결 요청 정책 속성의 **특성** 탭에 있는 사용자 이름 특성의 영역 이름을 조작 하는 방법을 설명 합니다.

**사용자 이름 특성의 영역 부분을 제거 하려면**

인터넷 서비스 공급자 \(isp\) 가 연결 요청을 조직 NPS로 라우팅하는 아웃소싱 전화 접속 시나리오에서는 isp RADIUS 프록시에 인증 요청을 라우팅하는 영역 이름이 필요할 수 있습니다. 그러나 NPS는 사용자 이름의 영역 이름 부분을 인식 하지 못할 수 있습니다. 따라서 NPS를 조직에 전달 하기 전에 ISP RADIUS 프록시를 통해 영역 이름이 제거 되어야 합니다.

- Find: @microsoft \.com

- 바꿀 대상:

**바꾸려는 <em>user@example.microsoft.com</em> _경우 example._**

- 찾아낼`(.*)@(.*)`

- 바꾸십시오`$2\$1`



**_Domain\user_ 를 _specific_domain\user_ 로 바꾸려면**

- 찾아낼`(.*)\\(.*)`

- Replace: *specific_domain*`\$2`



<strong>*사용자* 를로 바꾸려면 *user@specific_domain</strong>*

- 찾아낼`$`

- Replace: @*specific_domain*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>프록시 서버에서 RADIUS 메시지를 전달 하는 예제

NPS를 RADIUS 프록시로 사용 하는 경우 지정 된 영역 이름을 가진 RADIUS 메시지를 RADIUS 서버 집합에 전달 하는 라우팅 규칙을 만들 수 있습니다. 다음은 영역 이름에 따라 요청을 라우팅하는 권장 구문입니다.

- **NetBIOS 이름**:`WCOAST`
- **패턴**:`^wcoast\\`

다음 예제에서 wcoast.microsoft.com은 DNS 또는 Active Directory 도메인 wcoast.microsoft.com에 대 한 고유한 UPN (사용자 계정 이름) 접미사입니다. 제공 된 패턴을 사용 하 여 NPS 프록시는 도메인 NetBIOS 이름 또는 UPN 접미사를 기반으로 메시지를 라우팅할 수 있습니다.

- **NetBIOS 이름**:`WCOAST`
- **UPN 접미사**:`wcoast.microsoft.com`
- **패턴**:`^wcoast\\|@wcoast\.microsoft\.com$`


NPS를 관리 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 관리](nps-manage-top.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
