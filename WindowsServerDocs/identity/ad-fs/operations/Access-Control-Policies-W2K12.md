---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: AD FS의 액세스 제어 정책
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 610d2f9f2a159751b86782a07b3474469253aa2c
ms.sourcegitcommit: f6503e503d8f08ba8000db9c5eda890551d4db37
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68523930"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Windows Server 2012 R2 및 Windows Server 2012의 Access Control 정책 AD FS


이 문서에 설명 된 정책은 두 가지 종류의 클레임을 활용 합니다.  

1.  클레임 AD FS는 AD FS 및 웹 응용 프로그램 프록시가 AD FS 또는 WAP에 직접 연결 하는 클라이언트의 IP 주소와 같이 검사 하 고 확인할 수 있는 정보를 기반으로 만듭니다.  

2.  클라이언트에서 HTTP 헤더로 AD FS에 전달 된 정보에 따라 클레임 AD FS 생성 됩니다.  

>**중요**: 아래에 설명 된 정책은 다음 추가 끝점에 액세스 해야 하는 Windows 10 도메인 가입 및 로그온 시나리오를 차단 합니다.

Windows 10 도메인 가입 및 로그온에 필요한 AD FS 끝점
- [페더레이션 서비스 이름]/adfs/services/trust/2005/windowstransport
- [페더레이션 서비스 이름]/adfs/services/trust/13/windowstransport
- [페더레이션 서비스 이름]/adfs/services/trust/2005/usernamemixed
- [페더레이션 서비스 이름]/adfs/services/trust/13/usernamemixed 
- [페더레이션 서비스 이름]/adfs/services/trust/2005/certificatemixed
- [페더레이션 서비스 이름]/adfs/services/trust/13/certificatemixed

>**중요**:/adfs/services/trust/2005/windowstransport 및/adfs/services/trust/13/windowstransport 끝점은 HTTPS에서 WIA 바인딩을 사용 하는 인트라넷 연결 끝점 이므로 인트라넷 액세스에 대해서만 사용 하도록 설정 해야 합니다. 이러한 끝점에 대 한 요청이 이러한 끝점에 대 한 요청을 허용 하 여 잠금 보호를 우회할 수 있습니다. AD 계정 잠금을 보호 하려면 프록시 (예: 엑스트라넷에서 사용 안 함)에서 이러한 끝점을 사용 하지 않도록 설정 해야 합니다. 

해결 하려면 끝점 클레임을 기반으로 거부 하는 모든 정책을 업데이트 하 여 위의 끝점에 대 한 예외를 허용 합니다.

예를 들어 다음과 같은 규칙이 있습니다.

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

다음과 같이 업데이트 됩니다.

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  이 범주의 클레임은 네트워크에 대 한 액세스를 보호 하기 위해 보안 정책이 아닌 비즈니스 정책을 구현 하는 데만 사용 해야 합니다.  권한이 없는 클라이언트는 액세스 권한을 얻는 방법으로 잘못 된 정보를 포함 하는 헤더를 보낼 수 있습니다.  

이 문서에 설명 된 정책은 항상 사용자 이름 및 암호 또는 다단계 인증과 같은 다른 인증 방법과 함께 사용 해야 합니다.  

## <a name="client-access-policies-scenarios"></a>클라이언트 액세스 정책 시나리오  

|**시나리오**|**설명**| 
| --- | --- | 
|시나리오 1: Office 365에 대 한 모든 외부 액세스 차단|Office 365는 내부 회사 네트워크의 모든 클라이언트에서 액세스할 수 있지만 외부 클라이언트의 요청은 외부 클라이언트의 IP 주소를 기준으로 거부 됩니다.|  
|시나리오 2: Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스 차단|Office 365는 Exchange ActiveSync를 사용 하는 모든 외부 클라이언트 장치 (예: 스마트폰) 뿐만 아니라 내부 회사 네트워크의 모든 클라이언트에서 액세스할 수 있습니다. Outlook을 사용 하는 다른 모든 외부 클라이언트는 차단 됩니다.|  
|시나리오 3: 브라우저 기반 응용 프로그램을 제외한 Office 365에 대 한 모든 외부 액세스 차단|Outlook 웹 액세스 또는 SharePoint Online과 같은 수동 (브라우저 기반) 응용 프로그램을 제외 하 고 Office 365에 대 한 외부 액세스를 차단 합니다.|  
|시나리오 4: 지정 된 Active Directory 그룹을 제외 하 고 Office 365에 대 한 모든 외부 액세스 차단|이 시나리오는 클라이언트 액세스 정책 배포를 테스트 하 고 유효성을 검사 하는 데 사용 됩니다. 하나 이상의 Active Directory 그룹 멤버에 대해서만 Office 365에 대 한 외부 액세스를 차단 합니다. 또한 그룹의 멤버에만 외부 액세스를 제공 하는 데 사용할 수 있습니다.|  

## <a name="enabling-client-access-policy"></a>클라이언트 액세스 정책 사용  
 Windows Server 2012 r 2에서 AD FS의 클라이언트 액세스 정책을 사용 하도록 설정 하려면 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트를 업데이트 해야 합니다. 조직의 요구에 가장 부합 하는 **Microsoft Office 365 Id 플랫폼** 신뢰 당사자 트러스트에 대 한 클레임 규칙을 구성 하려면 아래 예제 시나리오 중 하나를 선택 합니다.  

###  <a name="scenario1"></a>시나리오 1: Office 365에 대 한 모든 외부 액세스 차단  
 이 클라이언트 액세스 정책 시나리오에서는 모든 내부 클라이언트의 액세스를 허용 하 고 외부 클라이언트의 IP 주소에 따라 모든 외부 클라이언트를 차단 합니다. 다음 절차를 사용 하 여 선택한 시나리오에 대 한 Office 365 신뢰 당사자 트러스트에 올바른 발급 권한 부여 규칙을 추가할 수 있습니다.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면  

1.  **서버 관리자**에서 **도구**를 클릭 한 다음 **AD FS 관리**를 클릭 합니다.  

2.  콘솔 트리의 **AD FS\Trust 관계**에서 **신뢰 당사자 트러스트**를 클릭 하 **Microsoft Office 365 id 플랫폼** 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 **클레임 규칙 편집**을 클릭 합니다.  

3.  **클레임 규칙 편집** 대화 상자에서 **발급 권한 부여 규칙** 탭을 선택한 다음 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.  

4.  **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

5.  **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다 (예: "원하는 범위 밖에 있는 IP 클레임이 있는 경우 거부"). **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. "x m-------ip"의 경우 위의 값을 유효한 ip 식으로 바꿉니다.  
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  **마침**을 클릭합니다. 기본적으로 **모든 사용자에 대 한 액세스 허용** 규칙에 앞서 발급 권한 부여 규칙 목록에 새 규칙이 표시 되는지 확인 합니다 (목록에서 이전에 표시 된 경우에도 거부 규칙이 우선적으로 적용 됨).  기본 허용 액세스 규칙이 없는 경우 다음과 같이 클레임 규칙 언어를 사용 하 여 목록의 끝에 하나를 추가할 수 있습니다.  </br>

    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  새 규칙을 저장 하려면 **클레임 규칙 편집** 대화 상자에서 **확인**을 클릭 합니다. 결과 목록은 다음과 같습니다.  

     ![발급 인증 규칙](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  

###  <a name="scenario2"></a>시나리오 2: Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스 차단  
 다음 예에서는 Outlook을 포함 하 여 내부 클라이언트에서 Exchange Online을 비롯 한 모든 Office 365 응용 프로그램에 액세스할 수 있습니다. 클라이언트 IP 주소에 표시 되는 것 처럼 회사 네트워크 외부에 있는 클라이언트의 액세스를 차단 합니다. 단, 스마트 휴대폰과 같은 Exchange ActiveSync 클라이언트의 경우는 예외입니다.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면  

1.  **서버 관리자**에서 **도구**를 클릭 한 다음 **AD FS 관리**를 클릭 합니다.  

2.  콘솔 트리의 **AD FS\Trust 관계**에서 **신뢰 당사자 트러스트**를 클릭 하 **Microsoft Office 365 id 플랫폼** 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 **클레임 규칙 편집**을 클릭 합니다.  

3.  **클레임 규칙 편집** 대화 상자에서 **발급 권한 부여 규칙** 탭을 선택한 다음 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.  

4.  **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

5.  **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다. 예를 들어 원하는 범위 밖에 있는 IP 클레임이 있는 경우 ipoutsiderange 클레임을 발급 합니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. "x m-------ip"의 경우 위의 값을 유효한 ip 식으로 바꿉니다.  

    `c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  **마침**을 클릭합니다. 새 규칙이 **발급 권한 부여 규칙** 목록에 나타나는지 확인 합니다.  

7.  그런 다음 **클레임 규칙 편집** 대화 상자의 **발급 권한 부여 규칙** 탭에서 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 다시 시작 합니다.  

8.  **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

9. **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다. 예를 들어, 원하는 범위 밖에 있는 IP가 있고 EAS에서 비 EAS (거부) 인 경우에는이 규칙에 대 한 표시 이름을 입력 합니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다.  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
~~~

10. **마침**을 클릭합니다. 새 규칙이 **발급 권한 부여 규칙** 목록에 나타나는지 확인 합니다.  

11. 그런 다음 **클레임 규칙 편집** 대화 상자의 **발급 권한 부여 규칙** 탭에서 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 다시 시작 합니다.  

12. **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

13. **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름 (예: "응용 프로그램 클레임이 있는지 확인")을 입력 합니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다.  

   ```  
   NOT EXISTS([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
   ```  

14. **마침**을 클릭합니다. 새 규칙이 **발급 권한 부여 규칙** 목록에 나타나는지 확인 합니다.  

15. 그런 다음 **클레임 규칙 편집** 대화 상자의 **발급 권한 부여 규칙** 탭에서 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 다시 시작 합니다.  

16. **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

17. **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다 (예: "ipoutsiderange true 및 응용 프로그램을 사용 하지 않는 사용자 거부"). **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다.  

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. **마침**을 클릭합니다. 새 규칙이 이전 규칙 바로 아래에 표시 되 고, 발급 권한 부여 규칙 목록의 모든 사용자에 게 기본적으로 액세스 허용 규칙 이전에 표시 되는지 확인 합니다 (목록에서 이전에 표시 되는 경우에도 거부 규칙이 우선적으로 적용 됨).  </br>기본 허용 액세스 규칙이 없는 경우 다음과 같이 클레임 규칙 언어를 사용 하 여 목록의 끝에 하나를 추가할 수 있습니다.</br></br>      `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. 새 규칙을 저장 하려면 **클레임 규칙 편집** 대화 상자에서 확인을 클릭 합니다. 결과 목록은 다음과 같습니다.  

    ![발급 권한 부여 규칙](media/Access-Control-Policies-W2K12/clientaccess2.png )  

###  <a name="scenario3"></a>시나리오 3: 브라우저 기반 응용 프로그램을 제외한 Office 365에 대 한 모든 외부 액세스 차단  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외한 Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면  

1.  **서버 관리자**에서 **도구**를 클릭 한 다음 **AD FS 관리**를 클릭 합니다.  

2.  콘솔 트리의 **AD FS\Trust 관계**에서 **신뢰 당사자 트러스트**를 클릭 하 **Microsoft Office 365 id 플랫폼** 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 **클레임 규칙 편집**을 클릭 합니다.  

3.  **클레임 규칙 편집** 대화 상자에서 **발급 권한 부여 규칙** 탭을 선택한 다음 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.  

4.  **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

5.  **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다. 예를 들어 원하는 범위 밖에 있는 IP 클레임이 있는 경우 ipoutsiderange 클레임을 발급 합니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. "x m-------ip"의 경우 위의 값을 유효한 ip 식으로 바꿉니다.  </br>
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  **마침**을 클릭합니다. 새 규칙이 **발급 권한 부여 규칙** 목록에 나타나는지 확인 합니다.  

7.  그런 다음 **클레임 규칙 편집** 대화 상자의 **발급 권한 부여 규칙** 탭에서 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 다시 시작 합니다.  

8.  **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

9. **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다. 예를 들어 원하는 범위 밖에 있는 IP가 있고 끝점은/adfs/ls이 아닌 경우 거부 됩니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다.  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
~~~

10. **마침**을 클릭합니다. 기본적으로 **모든 사용자에 대 한 액세스 허용** 규칙에 앞서 발급 권한 부여 규칙 목록에 새 규칙이 표시 되는지 확인 합니다 (목록에서 이전에 표시 된 경우에도 거부 규칙이 우선적으로 적용 됨).  </br></br> 기본 허용 액세스 규칙이 없는 경우 다음과 같이 클레임 규칙 언어를 사용 하 여 목록의 끝에 하나를 추가할 수 있습니다.  

   `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`

11. 새 규칙을 저장 하려면 **클레임 규칙 편집** 대화 상자에서 **확인**을 클릭 합니다. 결과 목록은 다음과 같습니다.  

    ![발급](media/Access-Control-Policies-W2K12/clientaccess3.png)  

###  <a name="scenario4"></a>시나리오 4: 지정 된 Active Directory 그룹을 제외 하 고 Office 365에 대 한 모든 외부 액세스 차단  
 다음 예제에서는 IP 주소를 기반으로 하는 내부 클라이언트에서 액세스할 수 있도록 합니다. 지정 된 Active Directory 그룹의 개인을 제외 하 고 외부 클라이언트 IP 주소가 있는 회사 네트워크 외부에 있는 클라이언트의 액세스를 차단 합니다. 다음 단계를 사용 하 여에 올바른 발급 권한 부여 규칙 **을 추가 하십시오. Microsoft Office 365** 클레임 규칙 마법사를 사용 하 여 Id 플랫폼 신뢰 당사자 트러스트:  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>지정 된 Active Directory 그룹을 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 하는 규칙을 만들려면  

1.  **서버 관리자**에서 **도구**를 클릭 한 다음 **AD FS 관리**를 클릭 합니다.  

2.  콘솔 트리의 **AD FS\Trust 관계**에서 **신뢰 당사자 트러스트**를 클릭 하 **Microsoft Office 365 id 플랫폼** 트러스트를 마우스 오른쪽 단추로 클릭 한 다음 **클레임 규칙 편집**을 클릭 합니다.  

3.  **클레임 규칙 편집** 대화 상자에서 **발급 권한 부여 규칙** 탭을 선택한 다음 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 시작 합니다.  

4.  **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

5.  **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다. 예를 들어 원하는 범위 밖에 있는 IP 클레임이 있는 경우 ipoutsiderange 클레임이 발급 됩니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다. "x m-------ip"의 경우 위의 값을 유효한 ip 식으로 바꿉니다.  


~~~
`c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  
~~~

6. **마침**을 클릭합니다. 새 규칙이 **발급 권한 부여 규칙** 목록에 나타나는지 확인 합니다.  

7. 그런 다음 **클레임 규칙 편집** 대화 상자의 **발급 권한 부여 규칙** 탭에서 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 다시 시작 합니다.  

8. **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

9. **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름 (예: "확인 그룹 SID")을 입력 합니다. **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다 ("groupsid"를 사용 중인 AD 그룹의 실제 SID로 바꿈).  

    `NOT EXISTS([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. **마침**을 클릭합니다. 새 규칙이 **발급 권한 부여 규칙** 목록에 나타나는지 확인 합니다.  

11. 그런 다음 **클레임 규칙 편집** 대화 상자의 **발급 권한 부여 규칙** 탭에서 **규칙 추가** 를 클릭 하 여 클레임 규칙 마법사를 다시 시작 합니다.  

12. **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 에서 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 선택 하 고 **다음**을 클릭 합니다.  

13. **규칙 구성** 페이지의 **클레임 규칙 이름**에이 규칙에 대 한 표시 이름을 입력 합니다 (예: "ipoutsiderange true 및 groupsid가 있는 사용자 거부"). **사용자 지정 규칙**에서 다음 클레임 규칙 언어 구문을 입력 하거나 붙여 넣습니다.  

   `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. **마침**을 클릭합니다. 새 규칙이 이전 규칙 바로 아래에 표시 되 고, 발급 권한 부여 규칙 목록의 모든 사용자에 게 기본적으로 액세스 허용 규칙 이전에 표시 되는지 확인 합니다 (목록에서 이전에 표시 되는 경우에도 거부 규칙이 우선적으로 적용 됨).  </br></br>기본 허용 액세스 규칙이 없는 경우 다음과 같이 클레임 규칙 언어를 사용 하 여 목록의 끝에 하나를 추가할 수 있습니다.  

   `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. 새 규칙을 저장 하려면 **클레임 규칙 편집** 대화 상자에서 확인을 클릭 합니다. 결과 목록은 다음과 같습니다.  

     ![발급](media/Access-Control-Policies-W2K12/clientaccess4.png)  

##  <a name="buildingip"></a>IP 주소 범위 식 작성  
 X AD FS--------------------------------------------------- 클레임의 값은 다음 중 하나일 수 있습니다.  

> [!NOTE]
>  Exchange Online은 현재 IPV4 및 IPV6 주소만 지원 합니다.  

-   단일 IP 주소: Exchange Online에 직접 연결 된 클라이언트의 IP 주소  

> [!NOTE]
> - 회사 네트워크에 있는 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.  
>   -   Vpn 또는 da의 구성에 따라 VPN 또는 Microsoft DirectAccess (DA)를 통해 회사 네트워크에 연결 된 클라이언트는 내부 회사 클라이언트나 외부 클라이언트로 표시 될 수 있습니다.  

-   하나 이상의 IP 주소: Exchange Online에서 연결 하는 클라이언트의 IP 주소를 확인할 수 없는 경우에는 HTTP 기반 요청에 포함 될 수 있고 많은 클라이언트, 부하 분산 장치에서 지원 되는 비표준 헤더 인 x 전달-헤더의 값을 기반으로 값을 설정 합니다. 시장에 대 한 및 프록시.  

> [!NOTE]
> 1. 클라이언트 IP 주소와 요청을 전달한 각 프록시의 주소를 나타내는 여러 IP 주소가 쉼표로 구분 됩니다.  
>    2. Exchange Online 인프라와 관련 된 IP 주소는 목록에 없습니다.  

### <a name="regular-expressions"></a>정규식  
 IP 주소 범위와 일치 해야 하는 경우 비교를 수행 하는 정규식을 생성 해야 합니다. 다음 일련의 단계에서는 다음 주소 범위와 일치 하도록 이러한 식을 구성 하는 방법에 대 한 예제를 제공 합니다. 공용 IP 범위와 일치 하도록 이러한 예제를 변경 해야 합니다.  

- 192.168.1.1 – 192.168.1.25  

- 10.0.0.1 – 10.0.0.14  

  첫째, 단일 IP 주소와 일치 하는 기본 패턴은 \b # # #\\.\\\\# # #. # # #. # # \b와 같습니다.  

  이를 확장 하 여 두 개의 서로 다른 IP 주소를 또는 식과 일치 시킬 수 있습니다. \b\\# # #.\\# # #.\\# # #. #&#124;# # \b \b\\#\\# #.\\# # #. # # #. # # #. # # #. # # #. # # # \b  

  따라서 두 개의 주소 (예: 192.168.1.1 또는 10.0.0.1)만 일치 하는 예제는\\\b192입니다.\\168\\1. \ b&#124;\b10\\.0 .0\\\\  

  이렇게 하면 원하는 수의 주소를 입력할 수 있는 방법이 제공 됩니다. 주소 범위 (예: 192.168.1.1 – 192.168.1.25)를 허용 해야 하는 경우 일치 하는 문자는 \b192\\.\\168\\. ( [1-9] &#124;1 [0-9]&#124;2 [0-5]) \b  

  다음 사항에 유의하세요.  

- IP 주소는 숫자가 아니라 문자열로 처리 됩니다.  

- 이 규칙은 \b192\\.\\168\\1과 같이 세분화 되어 있습니다.  

- 이 값은 192.168.1로 시작 하는 모든 값과 일치 합니다.  

- 다음은 마지막 소수점 뒤의 주소 부분에 필요한 범위와 일치 합니다.  

  -   ([1-9] 1-9로 끝나는 주소와 일치  

  -   &#124;1 [0-9] 10-19로 끝나는 주소와 일치 합니다.  

  -   &#124;2 [0-5]) 20-25로 끝나는 주소와 일치  

- IP 주소의 다른 부분 일치를 시작 하지 않도록 괄호를 올바르게 배치 해야 합니다.  

- 192 블록 일치를 사용 하 여 10 개의 블록 (\b10\\.0\\.0\\)에 대 한 유사한 식을 작성할 수 있습니다. [1-9] &#124;1 [0-4]) \b  

- 다음 식은 "192.168.1.1 ~ 25" 및 "10.0.0.1 ~ 14": \b192.\\\\168\\1. ( [1-9] &#124;1 [0-9]&#124;2 [0-5]) \b&#124;\b10\\.0\\.0\\. ( [1-9] &#124;1 [0-4]) \b  

### <a name="testing-the-expression"></a>식 테스트  
 Regex 식이 매우 복잡할 수 있으므로 regex 확인 도구를 사용 하는 것이 좋습니다. "온라인 regex 식 작성기"에 대해 인터넷 검색을 수행 하는 경우 샘플 데이터에 대해 식을 사용해 볼 수 있도록 하는 몇 가지 좋은 온라인 유틸리티를 찾을 수 있습니다.  

 식을 테스트할 때 일치 해야 할 것으로 예측 해야 하는 사항을 이해 하는 것이 중요 합니다. Exchange online 시스템은 쉼표로 구분 된 많은 IP 주소를 보낼 수 있습니다. 위에서 제공한 식이이 작업에 대해 작동 합니다. 그러나 regex 식을 테스트할 때이에 대해 생각 하는 것이 중요 합니다. 예를 들어 다음 샘플 입력을 사용 하 여 위의 예제를 확인할 수 있습니다.  

 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  

 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10, 0.0.1  

## <a name="claim-types"></a>클레임 유형  
 Windows Server 2012 r 2의 AD FS는 다음 클레임 유형을 사용 하 여 요청 컨텍스트 정보를 제공 합니다.  

### <a name="x-ms-forwarded-client-ip"></a>X-MS 전달-클라이언트-IP  
 클레임 유형:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  

 이 AD FS 클레임은 요청을 수행 하는 사용자의 IP 주소 (예: Outlook 클라이언트)를 확인의 "최상의 시도"를 나타냅니다. 이 클레임은 요청을 전달한 모든 프록시의 주소를 포함 하 여 여러 IP 주소를 포함할 수 있습니다.  이 클레임은 HTTP에서 채워집니다. 클레임의 값은 다음 중 하나일 수 있습니다.  

-   단일 IP 주소-Exchange Online에 직접 연결 되는 클라이언트의 IP 주소  

> [!NOTE]
>  회사 네트워크에 있는 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.  

-   하나 이상의 IP 주소  

    -   Exchange Online에서 연결 하는 클라이언트의 IP 주소를 확인할 수 없는 경우에는 HTTP 기반 요청에 포함 될 수 있고 많은 클라이언트, 부하 분산 장치에서 지원 되는 비표준 헤더 인 x 전달-헤더의 값을 기반으로 값을 설정 합니다. 시장에서 프록시를 설정 합니다.  

    -   클라이언트 IP 주소와 요청을 전달한 각 프록시의 주소를 나타내는 여러 IP 주소가 쉼표로 구분 됩니다.  

> [!NOTE]
>  Exchange Online 인프라와 관련 된 IP 주소는 목록에 표시 되지 않습니다.  

> [!WARNING]
>  Exchange Online은 현재 IPV4 주소만 지원 합니다. IPV6 주소는 지원 하지 않습니다.  

### <a name="x-ms-client-application"></a>X-y-클라이언트 응용 프로그램  
 클레임 유형:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  

 이 AD FS 클레임은 사용 중인 응용 프로그램에 느슨하게 해당 하는 최종 클라이언트에서 사용 하는 프로토콜을 나타냅니다.  이 클레임은 현재 Exchange Online 에서만 설정 되는 HTTP 헤더에서 채워지며, AD FS에 인증 요청을 전달할 때 헤더를 채웁니다. 응용 프로그램에 따라이 클레임의 값은 다음 중 하나가 됩니다.  

-   Exchange Active Sync를 사용 하는 장치의 경우 값은 Microsoft. Exchange.  

-   Microsoft Outlook 클라이언트를 사용 하면 다음 값 중 하나가 발생할 수 있습니다.  

    -   Microsoft에서 자동 검색  

    -   OfflineAddressBook  

    -   WebServices (영문)  

    -   WebServices (영문)  

-   이 헤더에 사용할 수 있는 다른 값은 다음과 같습니다.  

    -   Microsoft. Exchange Powershell  

    -   Microsoft Exchange. SMTP  

    -   Microsoft Exchange Pop  

    -   Microsoft Exchange. Imap  

### <a name="x-ms-client-user-agent"></a>X-y-사용자-에이전트  
 클레임 유형:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  

 이 AD FS 클레임은 클라이언트에서 서비스에 액세스 하는 데 사용 하는 장치 유형을 나타내는 문자열을 제공 합니다. 고객이 특정 유형의 스마트폰 등 특정 장치에 대 한 액세스를 차단 하려는 경우에 사용할 수 있습니다.  이 클레임에 대 한 값 예에는 아래 값이 포함 됩니다 (이에 국한 되지 않음).  

 다음은 x-m s-응용 프로그램이 "Microsoft. s s. m s. m s. m s s" 인 클라이언트에 대해 x-y (사용자 에이전트) 값이 포함 될 수 있는 예입니다.  

- 소용돌이/1.0  

- IPad1C1/812.1  

- IPhone3C1/811.2  

- Apple-iPhone/704.11  

- Moto-DROID2/4.5.1  

- SAMSUNGSPHD700/100.202  

- Android/0.3  

  이 값이 비어 있을 수도 있습니다.  

### <a name="x-ms-proxy"></a>X-MS 프록시  
 클레임 유형:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  

 이 AD FS 클레임은 요청이 웹 응용 프로그램 프록시를 통해 전달 되었음을 나타냅니다.  이 클레임은 페더레이션 서비스 백 엔드에 인증 요청을 전달할 때 헤더를 채우는 웹 응용 프로그램 프록시를 통해 채워집니다. 그런 다음 AD FS 클레임으로 변환 합니다.  

 클레임의 값은 요청을 전달 하는 웹 응용 프로그램 프록시의 DNS 이름입니다.  

### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 클레임 유형:`http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  

 위의 x-ms 프록시 클레임 형식과 마찬가지로이 클레임 유형은 요청이 웹 응용 프로그램 프록시를 통과 했는지 여부를 나타냅니다. Insidecorporatenetwork은 x-y와 달리, 회사 네트워크 내부에서 페더레이션 서비스에 직접 요청을 나타내는 True를 포함 하는 부울 값입니다.  

### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-y-절대 경로 (활성 vs 수동)  
 클레임 유형:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  

 이 클레임 유형은 "active" (리치) 클라이언트와 "passive" (웹 브라우저 기반) 클라이언트에서 시작 되는 요청을 확인 하는 데 사용할 수 있습니다. 이렇게 하면 Microsoft Outlook과 같은 리치 클라이언트에서 들어오는 요청이 차단 되는 동안 Outlook 웹 액세스, SharePoint Online 또는 Office 365 포털과 같은 브라우저 기반 응용 프로그램의 외부 요청이 허용 됩니다.  

 클레임의 값은 요청을 받은 AD FS 서비스의 이름입니다.  

## <a name="see-also"></a>관련 항목  
 [AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
