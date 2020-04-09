---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: 포리스트에 클레임 배포(데모 단계)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 05ca21f343d2ad3db4ce00b53a66b3cd6dd6de16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861246"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>포리스트에 클레임 배포(데모 단계)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 트러스팅 포리스트와 트러스트 된 포리스트 간에 클레임 변환을 구성 하는 방법을 설명 하는 기본 시나리오를 소개 합니다. 클레임 변환 정책 개체를 만들고 트러스팅 포리스트와 트러스트 된 포리스트의 트러스트에 연결 하는 방법을 알아봅니다. 그런 다음 시나리오의 유효성을 검사 합니다.  

## <a name="scenario-overview"></a>시나리오 개요  
Adatum Corporation에서는 Contoso, l t d .에 금융 서비스를 제공 합니다. Adatum 회계사는 계정 스프레드시트를 Contoso, l t d .의 파일 서버에 있는 폴더에 복사 합니다. Contoso에서 Adatum로 양방향 트러스트 설정이 있습니다. Contoso, l t d .는 Adatum 직원만 원격 공유에 액세스할 수 있도록 공유를 보호 하려고 합니다.  

이 시나리오의 내용:  

1.  [필수 구성 요소 및 테스트 환경 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  

2.  [신뢰할 수 있는 포리스트에서 클레임 변환 설정 (Adatum)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  

3.  [트러스팅 포리스트 (Contoso)에서 클레임 변환 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  

4.  [시나리오 유효성 검사](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  

## <a name="set-up-the-prerequisites-and-the-test-environment"></a><a name="BKMK_1.1"></a>필수 구성 요소 및 테스트 환경 설정  
테스트 구성에는 두 개의 포리스트 (Adatum Corporation 및 Contoso, l t d를 설정 하 고 Contoso와 Adatum 간에 양방향 트러스트 관계가 있음)가 포함 됩니다. "adatum.com"은 트러스트 된 포리스트이 고 "contoso.com"는 트러스팅 포리스트입니다.  

클레임 변환 시나리오에서는 트러스트 된 포리스트의 클레임을 트러스팅 포리스트의 클레임으로 변환 하는 방법을 보여 줍니다. 이렇게 하려면 adatum.com 이라는 새 포리스트를 설정 하 고 회사 값이 ' Adatum ' 인 테스트 사용자로 포리스트를 채워야 합니다. 그런 다음 contoso.com와 adatum.com 간에 양방향 트러스트를 설정 해야 합니다.  

> [!IMPORTANT]  
> Contoso 및 Adatum 포리스트를 설정할 때 클레임 변환이 작동 하려면 두 루트 도메인이 Windows Server 2012 도메인 기능 수준에 있는지 확인 해야 합니다.  

랩에 대해 다음을 설정 해야 합니다. 이러한 절차는 [부록 B: 테스트 환경 설정](Appendix-B--Setting-Up-the-Test-Environment.md) 에 자세히 설명 되어 있습니다.  

이 시나리오에 대 한 랩을 설정 하려면 다음 절차를 구현 해야 합니다.  

1.  [Adatum를 신뢰할 수 있는 포리스트로 Contoso로 설정](Appendix-B--Setting-Up-the-Test-Environment.md)  

2.  [Contoso에서 ' 회사 ' 클레임 유형 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  

3.  [Contoso에서 ' Company ' 리소스 속성을 사용 하도록 설정](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  

4.  [중앙 액세스 규칙 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  

5.  [중앙 액세스 정책 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  

6.  [그룹 정책를 통해 새 정책 게시](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  

7.  [파일 서버에서 소득 폴더 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  

8.  [분류를 설정 하 고 새 폴더에 중앙 액세스 정책을 적용 합니다.](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  

이 시나리오를 완료 하려면 다음 정보를 사용 합니다.  

|개체|세부 정보|  
|-----------|-----------|  
|Users|Jeff Low, Contoso|  
|Adatum 및 Contoso의 사용자 클레임|ID: ad://ext/Company:ContosoAdatum,<p>원본 특성: 회사<p>제안 된 값: Contoso, Adatum **중요:** 클레임 변환이 작동 하려면 Contoso와 Adatum의 ' Company ' 클레임 유형에 대 한 ID를 동일 하 게 설정 해야 합니다.|  
|Contoso의 중앙 액세스 규칙|Adatumemployeeaccessrule이|  
|Contoso의 중앙 액세스 정책|Adatum Only 액세스 정책|  
|Adatum 및 Contoso의 클레임 변환 정책|DenyAllExcept 회사|  
|Contoso의 파일 폴더|D:\EARNINGS|  

## <a name="set-up-claims-transformation-on-trusted-forest-adatum"></a><a name="BKMK_3"></a>신뢰할 수 있는 포리스트에서 클레임 변환 설정 (Adatum)  
이 단계에서는 Adatum에서 ' Company '를 제외한 모든 클레임을 거부 하는 변환 정책을 만들어 Contoso에 전달 합니다.  

Windows PowerShell 용 Active Directory 모듈은 변환 정책에서 지정 된 클레임을 제외한 모든 항목을 삭제 하는 **DenyAllExcept** 인수를 제공 합니다.  

클레임 변환을 설정 하려면 클레임 변환 정책을 만들고 트러스트 된 포리스트와 트러스팅 포리스트 간에 연결 해야 합니다.  

### <a name="create-a-claims-transformation-policy-in-adatum"></a><a name="BKMK_2.2"></a>Adatum에서 클레임 변환 정책 만들기  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>' Company '를 제외한 모든 클레임을 거부 하는 변환 정책 Adatum를 만들려면  

1. 도메인 컨트롤러에 로그인 하 고 adatum.com를 사용 하 여 관리자 권한으로 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except Company"`  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"adatum.com" `  

   ```  

### <a name="set-a-claims-transformation-link-on-adatums-trust-domain-object"></a><a name="BKMK_2.3"></a>Adatum의 트러스트 도메인 개체에 대 한 클레임 변환 링크 설정  
이 단계에서는 Contoso에 대 한 Adatum의 트러스트 도메인 개체에 새로 만든 클레임 변환 정책을 적용 합니다.  

##### <a name="to-apply-the-claims-transformation-policy"></a>클레임 변환 정책을 적용 하려면  

1. 도메인 컨트롤러에 로그인 하 고 adatum.com를 사용 하 여 관리자 권한으로 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  

     Set-ADClaimTransformLink `  
   -Identity:"contoso.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   '"TrustRole:Trusted `  

   ```  

## <a name="set-up-claims-transformation-in-the-trusting-forest-contoso"></a><a name="BKMK_4"></a>트러스팅 포리스트 (Contoso)에서 클레임 변환 설정  
이 단계에서는 Contoso (트러스팅 포리스트)에서 ' Company '를 제외한 모든 클레임을 거부 하는 클레임 변환 정책을 만듭니다. 클레임 변환 정책을 만들어 포리스트 트러스트에 연결 해야 합니다.  

### <a name="create-a-claims-transformation-policy-in-contoso"></a><a name="BKMK_4.1"></a>Contoso에서 클레임 변환 정책 만들기  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>' Company '를 제외한 모든 것을 거부 하는 변환 정책 Adatum를 만들려면  

1. 도메인 컨트롤러에 로그인 하 고 contoso.com를 사용 하 여 관리자 권한으로 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except company" `  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"contoso.com" `  

   ```  

### <a name="set-a-claims-transformation-link-on-contosos-trust-domain-object"></a><a name="BKMK_4.2"></a>Contoso의 트러스트 도메인 개체에 대 한 클레임 변환 링크 설정  
이 단계에서는 Adatum의 contoso.com trust 도메인 개체에 새로 만든 클레임 변환 정책을 적용 하 여 "Company"를 contoso.com로 전달할 수 있습니다. 트러스트 도메인 개체의 이름은 adatum.com입니다.  

##### <a name="to-set-the-claims-transformation-policy"></a>클레임 변환 정책을 설정 하려면  

1. 도메인 컨트롤러에 로그인 하 고 contoso.com를 사용 하 여 관리자 권한으로 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  

     Set-ADClaimTransformLink   
   -Identity:"adatum.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   -TrustRole:Trusting `  

   ```  

## <a name="validate-the-scenario"></a><a name="BKMK_5"></a>시나리오 유효성 검사  
이 단계에서는 파일 서버 FILE1에 설정 된 D:\EARNINGS 폴더에 액세스 하 여 사용자에 게 공유 폴더에 대 한 액세스 권한이 있는지 확인 합니다.  

#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Adatum 사용자가 공유 폴더에 액세스할 수 있도록 하려면  

1. 클라이언트 컴퓨터에 로그인 하 고, c a 1은 암호 <strong>pass@word1</strong>를 사용 합니다.  

2. \FILE1.contoso.com\Earnings. \\폴더로 이동 합니다.  

3. Jeff Low는 폴더에 액세스할 수 있어야 합니다.  

## <a name="additional-scenarios-for-claims-transformation-policies"></a>클레임 변환 정책에 대 한 추가 시나리오  
다음은 클레임 변환의 추가 일반적인 사례 목록입니다.  


|                                                 시나리오                                                 |                                                                                                                                                                                                                                           정책                                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  Adatum에서 제공 하는 모든 클레임이 Contoso Adatum로 이동 하도록 허용 합니다.                  |                                                          코드- <br />ADClaimTransformPolicy \`<br /> -설명: "모든 클레임을 허용 하는 클레임 변환 정책" \`<br />-Name: "AllowAllClaimsPolicy" \`<br />-AllowAll \`<br />-Server:"contoso" \`<br />ADClaimTransformLink \`<br />-Identity:"adatum" \`<br />-Policy: "AllowAllClaimsPolicy" \`<br />-TrustRole: 트러스팅 \`<br />-Server:"contoso" \`                                                          |
|                  Adatum에서 Contoso Adatum로 이동 하는 모든 클레임 거부                   |                                                            코드- <br />ADClaimTransformPolicy \`<br />-설명: "모든 클레임을 거부 하는 클레임 변환 정책" \`<br />-Name: "DenyAllClaimsPolicy" \`<br /> -DenyAll \`<br />-Server:"contoso" \`<br />ADClaimTransformLink \`<br />-Identity:"adatum" \`<br />-Policy: "DenyAllClaimsPolicy" \`<br />-TrustRole: 트러스팅 \`<br />-Server:"contoso"\`                                                             |
| "Company" 및 "학과"를 제외 하 고 Adatum에서 제공 하는 모든 클레임이 Contoso Adatum로 이동 하도록 허용 합니다. | 코드 <br />-ADClaimTransformationPolicy \`<br />-설명: "회사 및 부서를 제외한 모든 클레임을 허용 하는 클레임 변환 정책" \`<br /> -Name: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br />-AllowAllExcept: 회사, 부서 \`<br />-Server:"contoso" \`<br />ADClaimTransformLink \`<br /> -Identity:"adatum" \`<br />-Policy: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br /> -TrustRole: 트러스팅 \`<br />-Server:"contoso" \` |

## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목  

-   클레임 변환에 사용할 수 있는 모든 Windows PowerShell cmdlet 목록은 [Active Directory PowerShell Cmdlet 참조](https://go.microsoft.com/fwlink/?LinkId=243150)를 참조 하세요.  

-   두 포리스트 간에 DAC 구성 정보를 내보내고 가져오는 작업과 관련 된 고급 작업을 수행 하려면 [동적 Access Control PowerShell 참조](https://go.microsoft.com/fwlink/?LinkId=243150) 를 사용 합니다.  

-   [포리스트에 클레임 배포](Deploy-Claims-Across-Forests.md)  

-   [클레임 변환 규칙 언어](Claims-Transformation-Rules-Language.md)  

-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  


