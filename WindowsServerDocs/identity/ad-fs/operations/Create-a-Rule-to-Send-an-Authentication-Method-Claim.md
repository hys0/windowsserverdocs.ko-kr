---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: 인증 방법 클레임을 보내도록 규칙 만들기
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2c011c3b15f6223a6cea2f9c7226d9319641a693
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816584"
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>인증 방법 클레임을 보내도록 규칙 만들기


하나를 사용할 수는 **그룹 구성원을 클레임으로 보내기** 규칙 서식 파일 또는 **들어오는 클레임 변환** 보낼 인증 방법 클레임 규칙 템플릿. 신뢰 당사자 Active Directory Federation Services에서 사용자를 사용 하 여 인증 하 고 얻을 로그온 메커니즘 클레임을 결정 하는 인증 방법 클레임을 사용할 수 \(AD FS\)합니다. Active Directory Federation Services의 인증 메커니즘 보증 기능을 사용할 수도 있습니다 \(AD FS\) Windows Server 2012 r 2의 입력으로를 신뢰 당사자를 스마트 카드 로그온을 기반으로 하는 액세스 수준을 확인 하려고 하는 상황에 대 한 인증 방법 클레임을 생성 합니다. 예를 들어 개발자 신뢰 당사자 애플리케이션의 페더레이션된 사용자에 게 서로 다른 수준의 액세스를 할당할 수 있습니다. 액세스 수준은 기준으로 사용자가 여부 자신의 사용자 이름 및 암호 자격 증명으로가 아니라 스마트 카드 로그온 합니다.  

조직의 요구에 따라 다음 절차 중 하나를 사용 합니다.  

-   이 규칙을 사용 하 여 만들기는 **그룹 구성원을 클레임으로 보내기** 규칙 템플릿 \- 궁극적으로 인증 방법을 결정 하기 위해이 템플릿에 지정할 그룹 클레임 발급 하도록 하려는 경우이 규칙 서식 파일을 사용할 수 있습니다.  

-   이 규칙을 사용 하 여 만들기는 **들어오는 클레임 변환** 규칙 템플릿 \- 표준 AD FS 인증 방법 클레임을 인식 하지 않는 제품을 사용 하는 새 인증 방법으로 기존 인증 방법을 변경 하려는 경우이 규칙 서식 파일을 사용할 수 있습니다.  



## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>신뢰 당사자 트러스트에 Windows Server 2016에 클레임 규칙 템플릿 보내기 그룹 멤버 자격을 사용 하 여 만들기 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) 만들기 ![  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) 만들기 ![   

4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **그룹 구성원 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG) 만들기 ![      

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  

7.  클릭 **찾아보기**, 해당 멤버는이 인증 방법 클레임을 전달 하 고 클릭 한 다음 그룹을 선택 **확인**합니다.  

8.  **보내는 클레임 유형**, 선택, **인증 방법을** 목록에 있습니다.  

9. **보내는 클레임 값**, 기본 uniform resource identifier 중 하나를 입력 \(URI\) 사용자의 기본 인증 방법에 따라 다음 표의 값을 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

|                            실제 인증 방법                             |                                해당 URI                                 |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
|                        사용자 이름 및 암호 인증                        | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                               Windows 인증                                |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| 전송 계층 보안 \(TLS\) X.509 인증서를 사용 하는 상호 인증 | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|                  X.509\-기반 TLS를 사용 하지 않는 인증                  |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)

## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016에서 클레임 공급자 트러스트에 대 한 클레임 규칙 템플릿으로 보내기 그룹 멤버 자격을 사용 하 여 만들기 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) 만들기 ![  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) 만들기 ![   

4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **그룹 구성원 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG) 만들기 ![     

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  

7.  클릭 **찾아보기**, 해당 멤버는이 인증 방법 클레임을 전달 하 고 클릭 한 다음 그룹을 선택 **확인**합니다.  

8.  **보내는 클레임 유형**, 선택, **인증 방법을** 목록에 있습니다.  

9. **보내는 클레임 값**, 기본 uniform resource identifier 중 하나를 입력 \(URI\) 사용자의 기본 인증 방법에 따라 다음 표의 값을 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

|                            실제 인증 방법                             |                                해당 URI                                 |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
|                        사용자 이름 및 암호 인증                        | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                               Windows 인증                                |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| 전송 계층 보안 \(TLS\) X.509 인증서를 사용 하는 상호 인증 | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|                  X.509\-기반 TLS를 사용 하지 않는 인증                  |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>들어오는 클레임을 신뢰 당사자 트러스트에 Windows Server 2016 규칙 템플릿 변환을 사용 하 여이 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  콘솔 트리에서 아래 **AD FS**, 클릭 **신뢰 당사자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) 만들기 ![  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 발급 정책 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) 만들기 ![   

4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **들어오는 클레임 변환** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG) 만들기 ![      

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  

7.  **들어오는 클레임 유형**,  **인증 방법을** 목록에 있습니다.  

8.  **보내는 클레임 유형**, 선택, **인증 방법을** 목록에 있습니다.  

9. 선택 **들어오는 클레임 값을 다른 나가는 클레임 값을 바꿉니다**, 다음을 수행 합니다.  

    1.  **들어오는 클레임 값**, 실제 인증 방법을 원래 사용 된 URI 기반으로 하는 다음 URI 값 중 하나를 입력, 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

    2.  **보내는 클레임 값**, 새 기본 설정된 인증 방법 선택에 따라 달라 지는 다음 표에 기본 URI 값 중 하나를 입력, 클릭 **완료**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

|              실제 인증 방법              |                                해당 URI                                 |
|--------------------------------------------------------|----------------------------------------------------------------------------------|
|         사용자 이름 및 암호 인증          | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                 Windows 인증                 |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| X.509 인증서를 사용 하는 TLS 상호 인증 | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|   X.509\-기반 TLS를 사용 하지 않는 인증    |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)

> [!NOTE]  
> 다른 URI 값은 테이블의 값 외에도 사용할 수 있습니다. 이온 표시 되어 있는 URI 값 앞의 표에 기본적으로 신뢰 당사자를 허용 하는 Uri를 반영 합니다.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>들어오는 클레임 Windows Server 2016에서 클레임 공급자 트러스트에 규칙 템플릿 변환을 사용 하 여이 규칙을 만들려면 

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  콘솔 트리에서 아래 **AD FS**, 클릭 **클레임 공급자 트러스트**합니다. 
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) 만들기 ![  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) 만들기 ![   

4.  에 **클레임 규칙 편집** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) 만들기 ![    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **들어오는 클레임 변환** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG) 만들기 ![      

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  

7.  **들어오는 클레임 유형**,  **인증 방법을** 목록에 있습니다.  

8.  **보내는 클레임 유형**, 선택, **인증 방법을** 목록에 있습니다.  

9. 선택 **들어오는 클레임 값을 다른 나가는 클레임 값을 바꿉니다**, 다음을 수행 합니다.  

    1.  **들어오는 클레임 값**, 실제 인증 방법을 원래 사용 된 URI 기반으로 하는 다음 URI 값 중 하나를 입력, 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

    2.  **보내는 클레임 값**, 새 기본 설정된 인증 방법 선택에 따라 달라 지는 다음 표에 기본 URI 값 중 하나를 입력, 클릭 **완료**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

|              실제 인증 방법              |                                해당 URI                                 |
|--------------------------------------------------------|----------------------------------------------------------------------------------|
|         사용자 이름 및 암호 인증          | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                 Windows 인증                 |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| X.509 인증서를 사용 하는 TLS 상호 인증 | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|   X.509\-기반 TLS를 사용 하지 않는 인증    |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 클레임 규칙 템플릿으로 보내기 그룹 멤버 자격을 사용 하 여이 규칙을 만들려면  

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  

2.  콘솔 트리에서 **AD FS\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 만들기 ![  

4.  에 **클레임 규칙 편집** 대화 상자는 다음과 같은 탭 하나를 선택, 편집 하는 하는 규칙 집합을 신뢰에 따라,이 규칙을 만들려고 할 및 클릭 한 다음 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  

    -   **수락 변환 규칙**  

    -   **발급 변환 규칙**  

    -   **발급 권한 부여 규칙**  

    -   **위임 권한 부여 규칙**  
규칙](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 만들기 ![

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **그룹 구성원을 클레임으로 보내기** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG) 만들기 ![

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  

7.  클릭 **찾아보기**, 해당 멤버는이 인증 방법 클레임을 전달 하 고 클릭 한 다음 그룹을 선택 **확인**합니다.  

8.  **보내는 클레임 유형**, 선택, **인증 방법을** 목록에 있습니다.  

9. **보내는 클레임 값**, 기본 uniform resource identifier 중 하나를 입력 \(URI\) 사용자의 기본 인증 방법에 따라 다음 표의 값을 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

|                            실제 인증 방법                             |                                해당 URI                                 |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
|                        사용자 이름 및 암호 인증                        | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                               Windows 인증                                |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| 전송 계층 보안 \(TLS\) X.509 인증서를 사용 하는 상호 인증 | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|                  X.509\-기반 TLS를 사용 하지 않는 인증                  |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)

> [!NOTE]  
> 다른 URI 값은 테이블의 값 외에도 사용할 수 있습니다. 위의 표에 나와 있는 URI 값 신뢰 당사자를 기본적으로 허용 하는 Uri를 반영 합니다.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>이 규칙을 만들려면이 변환을 사용 하 여 들어오는 클레임 규칙 템플릿은 Windows Server 2012 r2  



1.  서버 관리자에서 클릭 **도구**, 를 클릭 하 고 **AD FS 관리**합니다.  

2.  콘솔 트리에서 **AD FS\\트러스트 관계**, 클릭 **클레임 공급자 트러스트** 또는 **신뢰 당사자 트러스트**, 이 규칙을 만드는 목록에서 특정 트러스트를 클릭 하 고 있습니다.  

3.  오른쪽\-선택한 트러스트를 클릭 한 다음 클릭 **클레임 규칙 편집**합니다.  
규칙](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 만들기 ![ 

4.  에 **클레임 규칙 편집** 대화 상자에서 하나를 선택 했는지에 따라 편집 하는 규칙 수를 설정 하는 신뢰 하는 다음과 같은 탭이이 규칙을 만들고 연결할 클릭 **규칙 추가** 해당 규칙 집합에 연관 된 규칙 마법사를 시작 합니다.  

    -   **수락 변환 규칙**  

    -   **발급 변환 규칙**  

    -   **발급 권한 부여 규칙**  

    -   **위임 권한 부여 규칙**  
규칙](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 만들기 ![

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 템플릿**, 선택, **들어오는 클레임 변환** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다.  
규칙](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG) 만들기 ![    

6.  에 **규칙 구성** 페이지에서 클레임 규칙 이름을 입력 합니다.  

7.  **들어오는 클레임 유형**,  **인증 방법을** 목록에 있습니다.  

8.  **보내는 클레임 유형**, 선택, **인증 방법을** 목록에 있습니다.  

9. 선택 **들어오는 클레임 값을 다른 나가는 클레임 값을 바꿉니다**, 다음을 수행 합니다.  

    1.  **들어오는 클레임 값**, 실제 인증 방법을 원래 사용 된 URI 기반으로 하는 다음 URI 값 중 하나를 입력, 클릭 **마침**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

    2.  **보내는 클레임 값**, 새 기본 설정된 인증 방법 선택에 따라 달라 지는 다음 표에 기본 URI 값 중 하나를 입력, 클릭 **완료**, 클릭 하 고 **확인** 여 규칙을 저장 합니다.  

|              실제 인증 방법              |                                해당 URI                                 |
|--------------------------------------------------------|----------------------------------------------------------------------------------|
|         사용자 이름 및 암호 인증          | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                 Windows 인증                 |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| X.509 인증서를 사용 하는 TLS 상호 인증 | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|   X.509\-기반 TLS를 사용 하지 않는 인증    |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)

> [!NOTE]  
> 다른 URI 값은 테이블의 값 외에도 사용할 수 있습니다. 이온 표시 되어 있는 URI 값 앞의 표에 기본적으로 신뢰 당사자를 허용 하는 Uri를 반영 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임 규칙 구성](Configure-Claim-Rules.md)  

[검사 목록: 신뢰 당사자 트러스트에 대 한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[검사 목록: 클레임 공급자 트러스트에 대 한 클레임 규칙 만들기](https://technet.microsoft.com/library/ee913564.aspx)  

[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  

[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
