---
title: 일반 식 NPS 사용
description: 이 항목 패턴 NPS Windows Server 2016에에서 일치에 대 한 일반 표현 사용에 설명 합니다. 이 구문의 조건을의 네트워크 정책 특성 및 RADIUS 영역의 지정을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: bc22d29c-678c-462d-88b3-1c737dceca75
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f84173f1f51be9fd44995dc41f759bbea4fb3539
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-regular-expressions-in-nps"></a>일반 식 NPS 사용

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 패턴 NPS Windows Server 2016에에서 일치에 대 한 일반 표현 사용에 설명 합니다. 이 구문의 조건을의 네트워크 정책 특성 및 RADIUS 영역의 지정을 사용할 수 있습니다.

## <a name="pattern-matching-reference"></a>참조 패턴 검색

다음 표에서 정기적으로 표현 패턴와 일치 하는 구문을 만들 때 참조 원본으로 사용할 수 있습니다.

|문자|설명|예제|
|---------|-----------|-------|
|`\`  |다음 문자 문자를 표시 합니다. |`/n/ matches the character "n". The sequence /\n/ matches a line feed or newline character.`  |
|`^`  |입력 또는 행의 시작 부분을 찾습니다. | &nbsp; |
|`$`  |입력 또는 줄의 끝을 찾습니다. | &nbsp; |
|`*`  |이전 문자 않거나 여러 번을 찾습니다. |`/zo*/ matches either "z" or "zoo."` |
|`+`  |이전 문자를 한 번 이상 찾습니다. |`/zo+/ matches "zoo" but not "z."` |
|`?`  |이전 문자 0 또는 1 개를 찾습니다. |`/a?ve?/ matches the "ve" in "never."` |
|`.`  |새 줄 문자를 제외 하 고 한 문자를 찾습니다.  | &nbsp; |
|`( pattern )`  |일치 하는 기억 하 고 "패턴" 일치 합니다.   |`To match ( ) (parentheses), use "\(" or "\)".`  |
|' x | Y '  |X 또는 y 찾습니다.  |' /z|음식? "동물원" 또는 "음식입니다." 일치 / ` |
|`{ n } `  |찾습니다 정확 하 게 n \ (n non\ 음극 integer\은).  |`/o{2}/ does not match the "o" in "Bob," but matches the first two instances of the letter o in "foooood."`  |
|`{ n ,}`  |적어도 n 찾습니다 \ (n non\ 음극 integer\은).  |`/o{2,}/ does not match the "o" in "Bob" but matches all of the instances of the letter o in "foooood." /o{1,}/ is equivalent to /o+/.`  |
|`{ n , m }`  |적어도 n에서 찾습니다 대부분 m \ (m 및 n는 non\ 음극 integers\).  |`/o{1,3}/ matches the first three instances of the letter o in "fooooood."`  |
|`[ xyz ]`  |포함 된 문자 중 하나를 찾습니다 \(a character set\) 합니다.  |`/[abc]/ matches the "a" in "plain."`  |
|`[^ xyz ]`  |문자에 포함 되지 않는 일치 \ (부정 문자 set\).  |`/[^abc]/ matches the "p" in "plain."`  |
|`\b`  |단어 경계를 찾는 \ (space\ 예).  |`/ea*r\b/ matches the "er" in "never early."`  |
|`\B`  |단어가 아닌 경계를 찾습니다.  |`/ea*r\B/ matches the "ear" in "never early."`  |
|`\d`  |숫자를 찾습니다 \ (와 동일 숫자 0-9\).  | &nbsp; |
|`\D`  |숫자가 아닌 문자 \ (와 동일 `[^0-9]`\).  | &nbsp; |
|`\f`  |양식 피드 문자 일치 합니다.  | &nbsp; |
|`\n`  |일치 줄 피드 문자.  | &nbsp; |
|`\r`  |캐리지 반환 문자를 찾습니다.  | &nbsp; |
|`\s`  |공간, 탭 및 피드 양식을 포함 하 여 임의의 공백 문자 \ (와 동일 `[ \f\n\r\t\v]`\).  | &nbsp; |
|`\S`  |모든 공백이 문자를 \ (와 동일 `[^ \f\n\r\t\v]`\).  | &nbsp; |
|`\t`  |탭 문자를 찾습니다.  | &nbsp; |
|`\v`  |세로 탭 문자를 찾습니다.  | &nbsp; |
|`\w`  |밑줄을 포함 하 여 임의의 word 문자 \ (와 동일 `[A-Za-z0-9_]`\).  | &nbsp; |
|`\W`  |밑줄 제외한 모든 non\ word 문자, \ (와 동일 `[^A-Za-z0-9_]`\).  | &nbsp; |
|`\ num`  |기억된 일치 하는 항목을 나타냅니다 \ (`?num`여기서 num은 긍정적인 integer\,).  이 옵션에만 사용할 수 있는 **교체** 특성 조작을 구성할 때 텍스트 상자 합니다.| `\1` 첫 번째 기억된 일치에 저장 된 바꿉니다.  |
|`/ n / `  |일반 표현 ASCII 코드 삽입할 수 있게 \ (`?n`여기서 n은 8 진, 16 진 또는 소수점 이스케이프 value\,).  | &nbsp; |

## <a name="examples-for-network-policy-attributes"></a>예 정책 특성 네트워크에 대 한

다음은 패턴와 일치 하는 구문 네트워크 정책 특성을 지정할 사용에 설명 다음과 같습니다.

- 모든 899 지역 번호 전화 번호를 지정 하려면 구문을 다음과 같습니다.

     `899.*`

- 192.168.1로 시작 하는 다양 한 IP 주소를 지정 하려면 구문을 다음과 같습니다.

    `192\.168\.1\..+`

## <a name="examples-for-manipulation-of-the-realm-name-in-the-user-name-attribute"></a>예 조작 영역 이름의 사용자 이름에서

다음은 영역 이름에 있는 사용자 이름 특성을 조작 하는 패턴와 일치 하는 구문을 사용에 설명는 **특성** 연결 요청 정책 속성 탭 합니다.

**사용자 이름 특성 영역 부분을 제거 하려면**

외부 위탁 전화 접속 시나리오는 인터넷 서비스 공급자 \(ISP\) 경로 연결 하도록 요청 조직 NPS 서버 ISP RADIUS 프록시 인증 요청을 라우팅하기 하는 영역 이름이 필요할 수 있습니다. 그러나 NPS 서버 사용자 이름 영역 이름 부분을 인식 하지 될 수 있습니다. 따라서 조직 NPS 서버에 전달 영역 이름은 ISP RADIUS 프록시 제거 해야 합니다.

- 찾고:@microsoft\.com

- 바꿉니다.

**바꾸려면 *user@example.microsoft.com*으로 *example.microsoft.com\user***

- 찾고:`(.*)@(.*)`

- 바꿉니다.`$2\$1`



**바꾸려면 *도메인 \ 사용자* 으로 *specific_domain\user***

- 찾고:`(.*)\\(.*)`

- 바꾸기: *specific_domain*`\$2`



**바꾸려면 *사용자* 와*user@specific_domain***

- 찾고:`$`

- 바꾸기: @*specific_domain*

## <a name="example-for-radius-message-forwarding-by-a-proxy-server"></a>프록시 서버 RADIUS 메시지를 전달 예제

NPS RADIUS 프록시도 사용 되는 경우 RADIUS 서버 집합으로 지정된 영역의 이름의 RADIUS 메시지를 전달 라우팅 규칙 만들 수 있습니다. 다음은 권장된 구문 영역 이름에 따라 요청이 라우팅되지입니다.

- **NetBIOS 이름 **: `WCOAST`
- **패턴 **:      `^wcoast\\`

다음 예제 wcoast.microsoft.com는 wcoast.microsoft.com Active Directory 또는 DNS 도메인에 대 한 고유한 사용자 UPN 계정 이름 () 접미사 합니다. 제공된 된 패턴을 사용 하 여 NPS 프록시 도메인 NetBIOS 이름이 나 upn에 따라 메시지 라우팅하기 수 있습니다.

- **NetBIOS 이름 **: `WCOAST`
- **Upn **:   `wcoast.microsoft.com`
- **패턴 **:      `^wcoast\\|@wcoast\.microsoft\.com$`


NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
