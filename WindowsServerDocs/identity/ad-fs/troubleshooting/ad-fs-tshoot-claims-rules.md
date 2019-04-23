---
title: AD FS 문제 해결-클레임 규칙
description: 이 문서에서는 AD FS 사용 하 여 클레임 규칙 구문 문제를 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 027b2afc9e580253ec820e7e5be14419387ddd44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837924"
---
# <a name="ad-fs-troubleshooting---claims-rules-syntax"></a>구문 규칙 클레임을 AD FS 문제 해결-
클레임은 문을 하나의 주제는 자신 또는 다른 방법에 대 한 제목입니다.  클레임을 신뢰 당사자가 발급 한와 하나 이상의 값을 지정 하 고 AD FS 서버에서 발급 한 보안 토큰에 패키지화 합니다.  이 문서에서는 클레임 구문 및 생성을 사용 하 여 처리합니다.  발급 클레임에 대 한 정보에 대 한 참조 [AD FS 문제 해결-클레임 발급](ad-fs-tshoot-claims-issuance.md)합니다.

>[!NOTE]  
>사용할 수 있습니다 [ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) 에 [ADFS 도움말](https://adfshelp.microsoft.com) 문제를 해결 하는 데 도움이 되는 사이트 문제를 클레임 합니다.   

## <a name="how-claim-rules-are-processed"></a>클레임 규칙을 처리하는 방법
클레임 규칙을 통해 처리 되는 [클레임 파이프라인](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md) 사용 하 여는 [클레임 엔진](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)합니다. 클레임 엔진은 사용자로부터의 들어오는 클레임 집합을 검사하고 각 규칙의 논리를 기준으로 클레임의 출력 집합을 생성하는 페더레이션 서비스의 논리적 구성 요소입니다.

## <a name="how-to-create-a-claim-rule"></a>클레임 규칙을 만드는 방법
클레임 규칙은 페더레이션 서비스 내의 각 페더레이션 트러스터 관계에 대해 개별적으로 만들어지며 여러 트러스트 간에 공유되지 않습니다. 규칙을 만들 수 있습니다는 [클레임 규칙 템플릿](../../ad-fs/technical-reference/determine-the-type-of-claim-rule-template-to-use.md)를 사용 하 여 규칙을 작성 하 여 처음부터 시작 합니다 [클레임 규칙 언어](../../ad-fs/technical-reference/when-to-use-a-custom-claim-rule.md) 또는 Windows PowerShell을 사용 하 여 규칙을 사용자 지정할 합니다.

## <a name="understanding-the-components-of-the-claim-rule-language"></a>클레임 규칙 언어의 구성 요소 이해
구분 하 여, 다음 구성 요소로 이루어져 있습니다 클레임 규칙 언어는 "= >" 연산자:

- 조건-입력된 클레임을 확인 하 고 규칙의 발급 문을 실행할지 여부를 결정 하는 데 사용 합니다.  평가 되어야 하는 논리 식을 나타내는 규칙 본문 부분을 실행할 때 true로 합니다.

- 발급 문

예:

```c:[type == "Name", value == "domain user"] => issue(type = "Role", value = "employee");``` 

다음 클레임에는 다음 있습니다.
- 조건- `c:[type == "Name", value == "domain user"] ` -windows 계정 이름을 인지 도메인 사용자의 입력된 클레임을 평가 합니다.
- 발급- `issue(type = "Role", value = "employee")` 조건이 true 인 경우-새 직원의 역할을 사용 하 여 입력된 클레임을 클레임을 추가 합니다.

클레임 및 구문에 대 한 자세한 내용은 참조 하세요 [클레임 규칙 언어의 역할](../../ad-fs/technical-reference/the-role-of-the-claim-rule-language.md)입니다.

## <a name="claims-rule-editor"></a>클레임 규칙 편집기
구문 검사 수행 하는 클레임 규칙 편집기에서 클레임을 완료 하 고 클릭 **확인**합니다.  따라서 잘못 된 구문이 있는 경우 다음 편집기 알 수 있습니다.

![클레임](media/ad-fs-tshoot-claims/claims1.png)

## <a name="event-logs"></a>이벤트 로그
로그를 사용 하 여 클레임의 문제를 해결 하는 동안 볼 때 클레임 출력에 대 한 확인 하는 것이 좋습니다.  이벤트 로그에 1000 및 1001 이벤트를 검색할 수 있습니다.

![클레임](media/ad-fs-tshoot-claims/claims2.png)

## <a name="creating-a-sample-application"></a>샘플 응용 프로그램 만들기
만들 수도 있습니다는 샘플 응용 프로그램 에코 사용자 클레임입니다.  예를 들어 샘플 응용 프로그램을 사용 하 고 문제를 해결 하 고 앱에 클레임 된 문제가 있는지 확인 하려는 동일한 클레임을 신뢰 당사자를 만들 수 있습니다.

![클레임](media/ad-fs-tshoot-claims/claim4.png)

좋은 샘플 웹 앱은 여기에 사용할 수 있습니다.  이 앱은 신뢰 당사자 로부터 받은 클레임을 에코 하는 간단한 웹 앱.  이 사용 하려면 web.config 앱에서 편집 해야 합니다.
- 변경 https://app1.contoso.com/sampapp URL에는 사용할는 sampapp 호스팅용
- AD FS 페더레이션 서버를 가리키도록 sts.contoso.com의 모든 인스턴스를 변경 합니다.
- 에 지 문으로 지문 대체

![클레임](media/ad-fs-tshoot-claims/claims3.png)

다음 [블로그 문서](https://blogs.technet.microsoft.com/tangent_thoughts/2015/02/20/install-and-configure-a-simple-net-4-5-sample-federated-application-samapp/) 이 설정에 대 한 뛰어난, 자세한 지침이 포함 되어 있습니다.

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)