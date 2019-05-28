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
ms.openlocfilehash: 13969958c9b4e0539993142d680cb6c34dc10750
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190254"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Windows Server 2012 R2 및 Windows Server 2012 AD FS에서 액세스 제어 정책


이 문서에 설명 된 정책을 사용 하면 두 종류의 클레임 사용  
  
1.  클레임을 AD FS에서 AD FS 및 웹 응용 프로그램 프록시를 검사 및 AD FS 또는 WAP에 직접 연결 되는 클라이언트의 IP 주소 확인 수 정보를 기반으로 만듭니다.  
  
2.  AD FS 클레임 HTTP 헤더로 AD FS에 클라이언트에서 전달 하는 정보를 기반으로 만듭니다.  
  
>**중요 한**: 아래 설명 된 대로 정책을 Windows 10 도메인 가입을 차단 되며 다음 추가 끝점에 액세스 해야 하는 시나리오에 로그인

Windows 10 도메인 가입 및 로그인에 필요한 AD FS 끝점
- [페더레이션 서비스 이름] / adfs/services/트러스트/2005/windowstransport
- [페더레이션 서비스 이름] / adfs/services/트러스트/13/windowstransport
- [페더레이션 서비스 이름] / adfs/services/트러스트/2005/usernamemixed
- [페더레이션 서비스 이름] / adfs/services/트러스트/13/usernamemixed 
- [페더레이션 서비스 이름] / adfs/services/트러스트/2005/certificatemixed
- [페더레이션 서비스 이름] / adfs/services/트러스트/13/certificatemixed

를 해결 하려면 위의 끝점에 대 한 예외를 허용 하도록 끝점 클레임을 기준으로 거부 하는 모든 정책을 업데이트 합니다.

예를 들어, 아래 규칙:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

업데이트 됩니다.

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  이 범주에서 클레임을 사용 하 여 비즈니스 정책을 구현할 수만 해야 아니라 네트워크에 대 한 액세스를 보호 하기 위한 보안 정책입니다.  에 액세스 하는 방법으로 잘못 된 정보를 사용 하 여 헤더를 보낼 권한이 없는 클라이언트에 대 한 것 같습니다.  
  
이 문서에 설명 된 정책 이름 및 암호 또는 다중 요소 인증 등의 다른 인증 방법을 사용 하 여 항상 사용 해야 합니다.  
  
## <a name="client-access-policies-scenarios"></a>클라이언트 액세스 정책 시나리오  
  
|**시나리오**|**설명**| 
| --- | --- | 
|시나리오 1: Office 365에 대 한 모든 외부 액세스를 차단 합니다.|Office 365 액세스 내부 회사 네트워크의 모든 클라이언트에서 사용할 수 있지만 외부 클라이언트의 IP 주소를 기반으로 외부 클라이언트에서 요청 거부 됩니다.|  
|시나리오 2: Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 합니다.|Exchange ActiveSync를 사용 하는 스마트폰 등 모든 외부 클라이언트 장치에서 뿐만 아니라 내부 회사 네트워크의 모든 클라이언트에서 office 365 액세스가 허용 됩니다. 다른 모든 외부 클라이언트, Outlook을 사용 하 여 같은 차단 됩니다.|  
|시나리오 3: 브라우저 기반 응용 프로그램을 제외한 Office 365에 모든 외부 액세스를 차단 합니다.|외부 액세스를 차단 Office 365 Outlook Web Access 또는 SharePoint Online과 같은 수동 (브라우저 기반) 응용 프로그램 제외 하 고 있습니다.|  
|시나리오 4: 지정 된 Active Directory 그룹을 제외 하 고 Office 365에 모든 외부 액세스를 차단 합니다.|이 시나리오는 테스트 및 클라이언트 액세스 정책 배포 유효성 검사에 사용 됩니다. 하나 이상의 Active Directory 그룹의 구성원에 대해서만 Office 365에 대 한 외부 액세스를 차단합니다. 그룹의 구성원 에게만 외부 액세스를 제공 하려면 데도 수 있습니다.|  
  
## <a name="enabling-client-access-policy"></a>클라이언트 액세스 정책 사용  
 클라이언트 액세스 정책에서 Windows Server 2012 R2에서 AD FS 사용 하려면 Microsoft Office 365 Id 플랫폼 신뢰 당사자 트러스트를 업데이트 해야 합니다. 예제 시나리오에서 클레임 규칙을 구성 하려면 다음 중 하나를 선택 합니다 **Microsoft Office 365 Id 플랫폼** 조직의 요구에 가장 잘 부합 하는 신뢰 당사자 트러스트 합니다.  
  
###  <a name="scenario1"></a> 시나리오 1: Office 365에 대 한 모든 외부 액세스를 차단 합니다.  
 이 클라이언트 액세스 정책 시나리오는 외부 클라이언트의 IP 주소를 기반으로 하는 모든 외부 클라이언트가 모든 내부 클라이언트 및 블록에서 액세스를 허용 합니다. 신뢰 당사자 트러스트에 선택한 시나리오에 대 한 Office 365에 올바른 발급 권한 부여 규칙을 추가 하려면 다음 절차를 사용할 수 있습니다.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 액세스를 차단 하도록 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD f s \ 트러스트 관계**, 클릭 **신뢰 당사자 트러스트**를 마우스 오른쪽 단추로 클릭 합니다 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 **클레임 규칙 편집**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자에서를 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**를 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
5.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 예를 들어가이 규칙에 대 한 표시 이름 "원하는 범위를 벗어나는 IP 클레임 경우 거부" 형식입니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문을 ("x-ms-전달-클라이언트-ip"를 유효한 IP 식으로 위의 값으로 대체):  
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  **마침**을 클릭합니다. 새 규칙을 기본값으로 하기 전에 발급 권한 부여 규칙 목록에 나타나는지 확인 **모든 사용자에 게 액세스 허용** 규칙 (거부 규칙이 우선 적용 됩니다는 목록에서 앞에 표시 되어 있다 하더라도).  액세스 규칙을 허용 하는 기본 없으면 같이 클레임 규칙 언어를 사용 하 여 목록 끝에 추가할 수 있습니다.  </br>
    
    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  새 규칙을 저장 하는 **클레임 규칙 편집** 대화 상자, 클릭 **확인**합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급 인증 규칙](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  
  
###  <a name="scenario2"></a> 시나리오 2: Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 합니다.  
 다음 예제에는 Outlook을 비롯 한 내부 클라이언트에서 Exchange Online을 비롯 한 모든 Office 365 응용 프로그램에 액세스할 수 있습니다. 클라이언트 IP 주소를 제외 하 고 스마트폰 등의 Exchange ActiveSync 클라이언트에 표시 된 대로 회사 네트워크 외부에 상주 하는 클라이언트에서 액세스를 차단 합니다.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Exchange ActiveSync를 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 하도록 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD f s \ 트러스트 관계**, 클릭 **신뢰 당사자 트러스트**를 마우스 오른쪽 단추로 클릭 합니다 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 **클레임 규칙 편집**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자에서를 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**를 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
5.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 예제에서는 "원하는 범위를 벗어나는 IP 클레임 있으면 ipoutsiderange 클레임 발급"에 대 한이 규칙에 대 한 표시 이름을 입력 합니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문을 ("x-ms-전달-클라이언트-ip"를 유효한 IP 식으로 위의 값으로 대체):  
    
    `c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  **마침**을 클릭합니다. 새 규칙에 표시 되는지 확인 합니다 **발급 권한 부여 규칙** 목록입니다.  
  
7.  다음으로 **클레임 규칙 편집** 대화 상자의 합니다 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
8.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**를 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
9. 에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 예를 들어가이 규칙에 대 한 표시 이름 "원하는 범위 밖에 있는 IP는 되어 비-EAS x-ms-클라이언트 응용 프로그램 클레임을 거부 하는 형식 ". 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문:  
  

    `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
  
10. **마침**을 클릭합니다. 새 규칙에 표시 되는지 확인 합니다 **발급 권한 부여 규칙** 목록입니다.  
  
11. 다음으로 **클레임 규칙 편집** 대화 상자의 합니다 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
12. 에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
13. 에 **규칙 구성** 페이지의 **클레임 규칙 이름**이 규칙에 대 한 표시 이름을 입력 하 고 예를 들어 "응용 프로그램 클레임 있는지 확인" 합니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문:  
  
    ```  
    NOT EXISTS([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
    ```  
  
14. **마침**을 클릭합니다. 새 규칙에 표시 되는지 확인 합니다 **발급 권한 부여 규칙** 목록입니다.  
  
15. 다음으로 **클레임 규칙 편집** 대화 상자의 합니다 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
16. 에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
17. 에 **규칙 구성** 페이지의 **클레임 규칙 이름**이 규칙에 대 한 표시 이름을 입력 하 고 예를 들어 "거부" ipoutsiderange true이 고 응용 프로그램을 사용 하 여 사용자가 실패 합니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문:  
  
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. **마침**을 클릭합니다. 새 규칙을 바로 아래에 나타나고 이전 규칙을 확인 하 고 전에 모든 사용자에 게 액세스 허용 기본값으로 (거부 규칙이 우선 적용 됩니다는 목록에서 앞에 표시 되더라도) 발급 권한 부여 규칙 목록에서 규칙.  </br>액세스 규칙을 허용 하는 기본 없으면 같이 클레임 규칙 언어를 사용 하 여 목록 끝에 추가할 수 있습니다.</br></br>      `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. 새 규칙을 저장 하는 **클레임 규칙 편집** 대화 상자에서 확인을 클릭 합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급 권한 부여 규칙](media/Access-Control-Policies-W2K12/clientaccess2.png )  
  
###  <a name="scenario3"></a> 시나리오 3: 브라우저 기반 응용 프로그램을 제외한 Office 365에 모든 외부 액세스를 차단 합니다.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외한 Office 365에 모든 외부 액세스를 차단 하도록 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD f s \ 트러스트 관계**, 클릭 **신뢰 당사자 트러스트**를 마우스 오른쪽 단추로 클릭 합니다 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 **클레임 규칙 편집**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자에서를 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**를 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
5.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 예제에서는 "원하는 범위를 벗어나는 IP 클레임 있으면 ipoutsiderange 클레임 발급"에 대 한이 규칙에 대 한 표시 이름을 입력 합니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문을 ("x-ms-전달-클라이언트-ip"를 유효한 IP 식으로 위의 값으로 대체):  </br>
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  **마침**을 클릭합니다. 새 규칙에 표시 되는지 확인 합니다 **발급 권한 부여 규칙** 목록입니다.  
  
7.  다음으로 **클레임 규칙 편집** 대화 상자의 합니다 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
8.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
9. 에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 예를 들어가이 규칙에 대 한 표시 이름 "는 원하는 범위 밖에 있는 IP를 사용할 수 없으면/adf/ls 끝점 거부" 형식입니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문:  
  
 
    `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
  
10. **마침**을 클릭합니다. 새 규칙을 기본값으로 하기 전에 발급 권한 부여 규칙 목록에 나타나는지 확인 **모든 사용자에 게 액세스 허용** 규칙 (거부 규칙이 우선 적용 됩니다는 목록에서 앞에 표시 되어 있다 하더라도).  </br></br> 액세스 규칙을 허용 하는 기본 없으면 같이 클레임 규칙 언어를 사용 하 여 목록 끝에 추가할 수 있습니다.  
  
    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`
  
11. 새 규칙을 저장 하는 **클레임 규칙 편집** 대화 상자, 클릭 **확인**합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급](media/Access-Control-Policies-W2K12/clientaccess3.png)  
  
###  <a name="scenario4"></a> 시나리오 4: 지정 된 Active Directory 그룹을 제외 하 고 Office 365에 모든 외부 액세스를 차단 합니다.  
 다음 예제에서는 IP 주소를 기반으로 하는 내부 클라이언트에서 액세스할 수 있도록 합니다. 외부 클라이언트 IP 주소를 포함 하는 회사 네트워크 외부에 상주 하는 클라이언트에서 액세스를 차단, 지정 된 Active Directory Group.Use에서 개별 제외 하 고 올바른 발급 권한 부여를 추가 하려면 다음 단계를 규칙 합니다  **Microsoft Office 365 Id 플랫폼** 신뢰 당사자 트러스트 클레임 규칙 마법사를 사용 하 여:  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>지정 된 Active Directory 그룹을 제외 하 고 Office 365에 대 한 모든 외부 액세스를 차단 하도록 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래 **AD f s \ 트러스트 관계**, 클릭 **신뢰 당사자 트러스트**를 마우스 오른쪽 단추로 클릭 합니다 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 **클레임 규칙 편집**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자에서를 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**를 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
5.  에 **규칙 구성** 페이지의 **클레임 규칙 이름**, 예제에서는 "원하는 범위를 벗어나는 IP 클레임 있으면 ipoutsiderange 클레임 발급 합니다."에 대 한이 규칙에 대 한 표시 이름 입력 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문을 ("x-ms-전달-클라이언트-ip"를 유효한 IP 식으로 위의 값으로 대체):  
  
      
    `c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  **마침**을 클릭합니다. 새 규칙에 표시 되는지 확인 합니다 **발급 권한 부여 규칙** 목록입니다.  
  
7.  다음으로 **클레임 규칙 편집** 대화 상자의 합니다 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
8.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
9. 에 **규칙 구성** 페이지의 **클레임 규칙 이름**이 규칙에 대 한 표시 이름을 입력 하 고 예를 들어 "check 그룹 SID"입니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문을 (replace "groupsid" AD 그룹을 사용 하는 실제 SID 사용 하 여):  
   
    `NOT EXISTS([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. **마침**을 클릭합니다. 새 규칙에 표시 되는지 확인 합니다 **발급 권한 부여 규칙** 목록입니다.  
  
11. 다음으로 **클레임 규칙 편집** 대화 상자의 합니다 **발급 권한 부여 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
12. 에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿** 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기**를 클릭 하 고 **다음**합니다.  
  
13. 에 **규칙 구성** 페이지의 **클레임 규칙 이름**이 규칙에 대 한 표시 이름을 입력 하 고 예를 들어 "거부" groupsid ipoutsiderange true와 사용자가 실패 합니다. 아래 **사용자 지정 규칙**입력 하거나 붙여넣은 다음 클레임 규칙 언어 구문:  
   
    `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. **마침**을 클릭합니다. 새 규칙을 바로 아래에 나타나고 이전 규칙을 확인 하 고 전에 모든 사용자에 게 액세스 허용 기본값으로 (거부 규칙이 우선 적용 됩니다는 목록에서 앞에 표시 되더라도) 발급 권한 부여 규칙 목록에서 규칙.  </br></br>액세스 규칙을 허용 하는 기본 없으면 같이 클레임 규칙 언어를 사용 하 여 목록 끝에 추가할 수 있습니다.  
   
    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. 새 규칙을 저장 하는 **클레임 규칙 편집** 대화 상자에서 확인을 클릭 합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급](media/Access-Control-Policies-W2K12/clientaccess4.png)  
  
##  <a name="buildingip"></a> IP 주소 범위 식 작성  
 클레임 x-ms-전달-클라이언트-ip는 현재 Exchange Online을 AD fs 인증 요청을 전달 하는 경우 헤더를 채우는 의해서만 설정 된 HTTP 헤더에서 채워집니다. 클레임의 값 중 하나일 수 있습니다.  
  
> [!NOTE]
>  현재 Exchange Online는 IPV4 및 IPV6 하지 주소만 지원합니다.  
  
-   단일 IP 주소: Exchange Online에 직접 연결 된 클라이언트의 IP 주소  
  
> [!NOTE]
>  -   회사 네트워크에서 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.  
> -   클라이언트는 VPN을 통해 또는에서 Microsoft DA (DirectAccess) 회사 네트워크에 연결 된 VPN 또는 da. 구성에 따라 외부 클라이언트 또는 내부 회사 클라이언트로 나타날 수 있습니다.  
  
-   하나 이상의 IP 주소: Exchange Online는 연결 중인 클라이언트의 IP 주소를 확인할 수 없습니다, 하는 경우 x-전달 기능에 대 한 헤더의 HTTP 기반 요청에 포함 될 수 있으며 많은 클라이언트에 부하 분산 장치에서 사용할 수 있는 비표준 헤더 값을 기반으로 하는 값 설정 및 시장에서 프록시입니다.  
  
> [!NOTE]
>  1.  클라이언트 IP 주소 및 요청을 전달 하는 각 프록시 주소를 나타내는 여러 IP 주소를 쉼표로 구분 됩니다.  
> 2.  Exchange Online 인프라와 관련 된 IP 주소 목록에 없는 됩니다.  
  
### <a name="regular-expressions"></a>정규식  
 범위의 IP 주소와 일치 하는 경우에 비교를 수행 하는 정규식을 생성 하는 데 필요한 됩니다. 다음 일련의 단계에서 다음 주소 범위 (공용 IP 범위를 일치 하도록 이러한 예제를 변경 해야 하는 참고)에 맞게 이러한 식을 구성 하는 방법에 대 한 예제가 제공 됩니다.  
  
-   192.168.1.1 – 192.168.1.25  
  
-   10.0.0.1 – 10.0.0.14  
  
 먼저 단일 IP 주소를 일치 하는 기본적인 패턴은 다음과 같습니다: \b###\\합니다. # # #\\합니다. # # #\\. # # # \b  
  
 이 확장을 일치 시킬 수는 OR 식으로 서로 다른 두 IP 주소 다음과 같이: \b###\\. # # #\\. # # #\\. # # # \b&#124;\b###\\합니다. # # #\\합니다. # # #\\. # # # \b  
  
 따라서 두 주소 (예: 192.168.1.1 또는 10.0.0.1)와 일치 하는 예제는 것: \b192\\.168\\.1\\. 1\b&#124;\b10\\.0\\.0\\. 1\b  
  
 이는 임의 개수의 주소를 입력할 수 있습니다 하는 기술을 제공 합니다. 주소 범위 수, 예: 192.168.1.1 – 192.168.1.25를 해야 하는 경우 일치 하는 수행 해야 문자로 문자: \b192\\.168\\.1\\. ( [1-9] &#124;1 [0-9]&#124;2 [0-5]) \b  
  
 다음 사항에 유의하세요.  
  
-   IP 주소 문자열 및 숫자가 아닌로 처리 됩니다.  
  
-   규칙은 다음과 같이 세분화: \b192\\.168\\.1\\합니다.  
  
-   이 모든 값부터 192.168.1 일치합니다.  
  
-   다음은 마지막 소수점 뒤의 주소 부분에 필요한 범위 일치 합니다.  
  
    -   1-9로 끝나는 ([1-9] 일치 주소  
  
    -   &#124;[0-9] 1 10-19로 끝나는 주소와 일치  
  
    -   &#124;20-25 끝나는 2[0-5]) 일치 주소  
  
-   일치 하는 다른 부분 IP 주소를 시작 하지는 괄호 올바르게 배치 해야, note 합니다.  
  
-   일치 하는 192 블록을 사용 하 여 10 개 블록에 대 한 유사한 식을 작성할 수 있습니다: \b10\\.0\\.0\\. ( [1-9] &#124;[0-4] 1) \b  
  
-   와 함께 배치 하, 다음 식은 같아야 "192.168.1.1~25" 및 "10.0.0.1~14"에 대 한 모든 주소: \b192\\.168\\.1\\. ( [1-9] &#124;1 [0-9]&#124;2 [0-5]) \b&#124;\b10\\.0\\.0\\합니다. ( [1-9] &#124;[0-4] 1) \b  
  
### <a name="testing-the-expression"></a>식 테스트  
 Regex 식을 상당히 까다로운 될 수 있으므로 regex 확인 도구를 사용 하는 것이 좋습니다. "온라인 regex 식 작성기"에 대 한 인터넷을 검색 하면 샘플 데이터에 대 한 식을 실행 해 볼 수 있도록 몇 가지 좋은 온라인 유틸리티를 찾을 수 있습니다.  
  
 식을 테스트 하는 경우는 일치 하는 데 예상 되는 상황을 파악 하는 것입니다. Exchange 온라인 시스템에는 쉼표로 구분 하 여 여러 IP 주소를 보낼 수 있습니다. 위에 제공 된 식이이 작동 합니다. 그러나 regex 식을 테스트 하는 경우이 대해 생각 하는 것이 반드시 합니다. 예를 들어 위의 예제를 확인 하려면 입력 다음 샘플을 사용할 수 있습니다 하나.  
  
 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  
  
 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1  
  
## <a name="claim-types"></a>클레임 유형  
 Windows Server 2012 R2에서 AD FS는 다음 클레임 유형을 사용 하 여 요청 컨텍스트 정보를 제공 합니다.  
  
### <a name="x-ms-forwarded-client-ip"></a>X-MS-전달-클라이언트-IP  
 클레임 유형: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  
  
 이 AD FS 클레임에서 요청을 만드는 사용자 (예: Outlook 클라이언트)의 IP 주소를 부분도 "최상의 시도를"를 나타냅니다. 이 클레임 요청을 전달 하는 모든 프록시의 주소를 포함 하 여 여러 IP 주소를 포함할 수 있습니다.  이 클레임은 HTTP에서 채워집니다. 클레임의 값 중 하나일 수 있습니다.  
  
-   단일 IP 주소-Exchange Online에 직접 연결 된 클라이언트의 IP 주소  
  
> [!NOTE]
>  회사 네트워크에서 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.  
  
-   하나 이상의 IP 주소  
  
    -   Exchange Online는 연결 중인 클라이언트의 IP 주소를 확인할 수 없으면, HTTP 기반에 포함 될 수 있는 비표준 헤더를 요청 하 고 많은 클라이언트, 부하 분산 장치에서 지원 되는 x-전달 기능에 대 한 헤더의 값에 따라 값을 설정 하 고 시장에서 프록시를 제공 합니다.  
  
    -   클라이언트 IP 주소 및 요청을 전달 하는 각 프록시 주소를 나타내는 여러 IP 주소를 쉼표로 구분 됩니다.  
  
> [!NOTE]
>  Exchange Online 인프라와 관련 된 IP 주소 목록에 표시 되지 않습니다.  
  
> [!WARNING]
>  Exchange Online만 IPV4 주소는 현재 지원 IPV6 주소를 지원 하지 않습니다.  
  
### <a name="x-ms-client-application"></a>X-MS-Client-Application  
 클레임 유형: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  
  
 이 AD FS 클레임 느슨하게 사용 중인 응용 프로그램에 해당 하는 최종 클라이언트에 의해 사용 된 프로토콜을 나타냅니다.  현재 HTTP 헤더에서이 클레임 채워집니다만 설정한 Exchange Online을 AD fs 인증 요청을 전달 하는 경우 헤더를 채웁니다. 응용 프로그램에 따라이 클레임의 값 중 하나로 설정 됩니다.  
  
-   Exchange Active Sync를 사용 하는 장치의 경우 Microsoft.Exchange.ActiveSync 가치가 있습니다.  
  
-   다음 값 중 하나에서 Microsoft Outlook 클라이언트 사용 될 수 있습니다.  
  
    -   Microsoft.Exchange.Autodiscover  
  
    -   Microsoft.Exchange.OfflineAddressBook  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
-   이 헤더에 대 한 다른 가능한 값은 다음과 같습니다.  
  
    -   Microsoft.Exchange.Powershell  
  
    -   Microsoft.Exchange.SMTP  
  
    -   Microsoft.Exchange.Pop  
  
    -   Microsoft.Exchange.Imap  
  
### <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent  
 클레임 유형: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  
  
 이 AD FS 클레임에는 클라이언트는 서비스에 액세스 하는 데 사용 하는 장치 유형을 나타내는 문자열을 제공 합니다. 이 고객은 특정 장치 (예: 스마트폰의 특정 유형)에 대 한 액세스를 방지 하려는 경우 사용할 수 있습니다.  포함 (하지만에 제한 되지 않습니다)이이 클레임에 대 한 예제 값 아래의 값입니다.  
  
 다음은 x ms-사용자 에이전트 값을 해당 x-ms-클라이언트 응용 프로그램은 "Microsoft.Exchange.ActiveSync" 클라이언트에 대 한 포함 될 수 있습니다의 예  
  
-   소용돌이/1.0  
  
-   Apple-iPad1C1/812.1  
  
-   Apple-iPhone3C1/811.2  
  
-   Apple-iPhone/704.11  
  
-   Moto-DROID2/4.5.1  
  
-   SAMSUNGSPHD700/100.202  
  
-   Android/0.3  
  
 이 값은 비워 둘 수 이기도 합니다.  
  
### <a name="x-ms-proxy"></a>X-MS-Proxy  
 클레임 유형: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  
  
 이 AD FS 클레임 요청에 웹 응용 프로그램 프록시를 통해 전달 되는 것을 나타냅니다.  이 클레임은 페더레이션 서비스를 백 엔드로 인증 요청을 전달 하는 경우 헤더를 채우는 웹 응용 프로그램 프록시에 의해 채워집니다. AD FS이 클레임을 다음 변환합니다.  
  
 클레임의 값에는 요청을 전달 하는 웹 응용 프로그램 프록시의 DNS 이름입니다.  
  
### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 클레임 유형: `http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  
  
 위의 x-ms-프록시 비슷하게 클레임 유형, 클레임 유형을이 웹 응용 프로그램 프록시를 통해 요청에 전달 하는지 여부를 나타냅니다. X-ms-프록시 달리 insidecorporatenetwork 사용 하 여 회사 네트워크 내부에서 페더레이션 서비스에 직접 요청을 나타내는 True 부울 값입니다.  
  
### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-끝점-절대 경로 (활성 및 수동)  
 클레임 유형: `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  
  
 이 클레임 유형이 "수동" (웹 브라우저 기반) 클라이언트와 "활성" (진한) 클라이언트에서 시작 된 요청을 결정 하는 데 사용할 수 있습니다. 따라서 Outlook Web Access, SharePoint Online 또는 Office 365 포털에서 Microsoft Outlook 등의 다양 한 클라이언트에서 보내는 요청을 차단 하는 동안 수와 같은 브라우저 기반 응용 프로그램에서 외부 요청을 수 있습니다.  
  
 클레임의 값에는 요청을 수신 하는 AD FS 서비스의 이름입니다.  
  
## <a name="see-also"></a>관련 항목  
 [AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
