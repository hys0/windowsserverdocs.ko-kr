---
title: AD FS 문제 해결-클레임 규칙
description: 이 문서에서는 AD FS 사용 하 여 클레임 규칙 구문 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d0146ba7cfc736f4d37ca66d58d624cc2f7f9a23
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366282"
---
# <a name="ad-fs-troubleshooting---claims-rules-syntax"></a>AD FS 문제 해결-클레임 규칙 구문
클레임은 한 주체가 자신 또는 다른 주체에 대해 수행 하는 문입니다.  클레임은 신뢰 당사자에 의해 발급 되며 하나 이상의 값이 지정 된 다음 AD FS 서버에서 발급 한 보안 토큰에 패키지 됩니다.  이 문서에서는 클레임 구문 및 생성을 다룹니다.  클레임 발급에 대 한 자세한 내용은 [AD FS 문제 해결-클레임 발급](ad-fs-tshoot-claims-issuance.md)을 참조 하세요.

>[!NOTE]  
>[ADFS 도움말](https://adfshelp.microsoft.com) 사이트의 [ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) 를 사용 하 여 클레임 문제 해결에 도움을 받을 수 있습니다.   

## <a name="how-claim-rules-are-processed"></a>클레임 규칙을 처리하는 방법
클레임 규칙은 클레임 [엔진](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)을 사용 하 여 클레임 [파이프라인](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md) 을 통해 처리 됩니다. 클레임 엔진은 사용자로부터의 들어오는 클레임 집합을 검사하고 각 규칙의 논리를 기준으로 클레임의 출력 집합을 생성하는 페더레이션 서비스의 논리적 구성 요소입니다.

## <a name="how-to-create-a-claim-rule"></a>클레임 규칙을 만드는 방법
클레임 규칙은 페더레이션 서비스 내의 각 페더레이션 트러스터 관계에 대해 개별적으로 만들어지며 여러 트러스트 간에 공유되지 않습니다. 클레임 [규칙 템플릿에서](../../ad-fs/technical-reference/determine-the-type-of-claim-rule-template-to-use.md)규칙을 만들거나, [클레임 규칙 언어](../../ad-fs/technical-reference/when-to-use-a-custom-claim-rule.md) 를 사용 하 여 규칙을 작성 하거나, Windows PowerShell을 사용 하 여 규칙을 사용자 지정 하 여 처음부터 시작할 수 있습니다.

## <a name="understanding-the-components-of-the-claim-rule-language"></a>클레임 규칙 언어의 구성 요소 이해
클레임 규칙 언어는 다음과 같은 구성 요소로 구성 됩니다. "= >" 연산자로 구분 됩니다.

- 입력 클레임을 확인 하 고 규칙의 발급 문을 실행 해야 하는지 여부를 결정 하는 데 사용 되는 조건입니다.  규칙 본문 부분을 실행 하려면 true로 평가 되어야 하는 논리 식을 나타냅니다.

- 발급 문

예:

```c:[type == "Name", value == "domain user"] => issue(type = "Role", value = "employee");``` 

다음 클레임에는 다음이 포함 됩니다.
- 조건-`c:[type == "Name", value == "domain user"] `-windows 계정 이름이 도메인 사용자 인지 여부의 입력 클레임을 평가 합니다.
- 발급-`issue(type = "Role", value = "employee")`-조건이 true 이면 employee 역할을 사용 하 여 입력 클레임에 새 클레임을 추가 합니다.

클레임 및 구문에 대 한 자세한 내용은 [클레임 규칙 언어의 역할](../../ad-fs/technical-reference/the-role-of-the-claim-rule-language.md)을 참조 하세요.

## <a name="claims-rule-editor"></a>클레임 규칙 편집기
클레임 규칙 편집기는 클레임을 완료 한 후 **확인**을 클릭 하 여 구문 검사를 수행 합니다.  따라서 잘못 된 구문이 있는 경우 편집기에서 사용자에 게 알려 드리겠습니다.

![클레임](media/ad-fs-tshoot-claims/claims1.png)

## <a name="event-logs"></a>이벤트 로그
로그를 사용 하 여 클레임 문제를 해결 하려는 경우 가장 좋은 방법은 클레임 출력을 찾는 것입니다.  이벤트 로그에서 1000 및 1001 이벤트를 찾을 수 있습니다.

![클레임](media/ad-fs-tshoot-claims/claims2.png)

## <a name="creating-a-sample-application"></a>샘플 응용 프로그램 만들기
또한 클레임을 에코 하는 샘플 응용 프로그램을 만들 수 있습니다.  예를 들어 샘플 응용 프로그램을 사용 하 여 문제 해결을 시도 하는 것과 동일한 클레임을 포함 하는 신뢰 당사자를 만들고 앱이 해당 클레임에 문제가 있는지 확인할 수 있습니다.

![클레임](media/ad-fs-tshoot-claims/claim4.png)

여기에서 좋은 샘플 웹 앱을 사용할 수 있습니다.  이 앱은 신뢰 당사자 로부터 받은 클레임을 다시 에코 하는 간단한 웹 앱입니다.  이를 사용 하려면 다음을 수행 하 여 web.config 앱을 편집 해야 합니다.
- sampapp를 호스트 하는 데 사용 하는 https://app1.contoso.com/sampapp 을 URL로 변경 합니다.
- AD FS 페더레이션 서버를 가리키도록 sts.contoso.com의 모든 인스턴스 변경
- 지문을 지 문으로 바꾸기

![클레임](media/ad-fs-tshoot-claims/claims3.png)

다음 [블로그 문서](https://blogs.technet.microsoft.com/tangent_thoughts/2015/02/20/install-and-configure-a-simple-net-4-5-sample-federated-application-samapp/) 에는이를 설정 하는 데 필요한 매우 뛰어난 지침이 있습니다.

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)