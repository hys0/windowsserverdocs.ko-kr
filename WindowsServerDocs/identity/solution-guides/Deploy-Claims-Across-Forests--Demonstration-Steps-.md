---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: 포리스트에 클레임 배포(데모 단계)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a6f2e5d3a227384b20735ab99ee1ab5ea77bd913
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445840"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>포리스트에 클레임 배포(데모 단계)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 트러스팅 포리스트와 트러스트 된 포리스트 간 클레임 변환을 구성 하는 방법에 설명 하는 기본 시나리오를 설명 합니다. 어떻게 클레임 변환 정책 개체를 작성 및 트러스트에서 트러스팅 포리스트와 트러스트 된 포리스트의 연결할 배웁니다. 다음 시나리오를 확인 합니다.  

## <a name="scenario-overview"></a>시나리오 개요  
Adatum Corporation Contoso, Ltd.를 금융 서비스 제공 각 분기 마다 Adatum accountants 계정 스프레드시트 Contoso, Ltd.에 있는 파일 서버의 폴더에 복사 Adatum Contoso에서 설정 양방향 트러스트가 있습니다. Contoso, Ltd. Adatum 직원만 원격 공유에 액세스할 수 있도록 공유를 보호 하려고 합니다.  

이 시나리오의 내용:  

1.  [필수 구성 요소 및 테스트 환경 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  

2.  [신뢰할 수 있는 포리스트 (Adatum)에서 클레임 변환을 설정합니다](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  

3.  [(Contoso) 트러스팅 포리스트에 클레임 변환 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  

4.  [시나리오의 유효성을 검사합니다](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  

## <a name="BKMK_1.1"></a>필수 구성 요소 및 테스트 환경 설정  
테스트 구성에는 두 포리스트 설정 포함 됩니다. Adatum Corporation Contoso, Ltd 이면 및 Contoso 및 Adatum 간에 양방향 트러스트가 필요 합니다. "adatum.com" 신뢰할 수 있는 포리스트 이며 "contoso.com" 트러스팅 포리스트에 있습니다.  

클레임 변환 시나리오는 트러스팅 포리스트에 클레임에 트러스트 된 포리스트에서 클레임 변환 방법을 보여 줍니다. 이렇게 하려면 'Adatum' 회사 값을 사용 하 여 테스트 사용자를 사용 하 여 포리스트를 우 adatum.com 이라는 새 포리스트를 설정 해야 합니다. 그런 다음 contoso.com을 adatum.com 간에 양방향 트러스트를 설정 해야 합니다.  

> [!IMPORTANT]  
> Contoso와 Adatum 포리스트를 설정할 때 두 루트 도메인의 Windows Server 2012 도메인 기능 수준을 클레임 변환에 대 한 작업에 확인 해야 합니다.  

랩에 대해 다음을 설정 해야 합니다. 이러한 절차에서 자세히 설명 되어 [부록 b: 테스트 환경 설정](Appendix-B--Setting-Up-the-Test-Environment.md)  

이 시나리오에 랩을 설정 하려면 다음 절차를 구현 해야 합니다.  

1.  [신뢰할 수 있는 포리스트 Contoso Adatum로](Appendix-B--Setting-Up-the-Test-Environment.md)  

2.  [Contoso에서 '회사' 클레임 유형 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  

3.  [Contoso에서 '회사' 리소스 속성을 사용 하도록 설정](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  

4.  [중앙 액세스 규칙 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  

5.  [중앙 액세스 정책 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  

6.  [그룹 정책을 통해 새 정책 게시](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  

7.  [파일 서버에서 Earnings 폴더 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  

8.  [분류를 설정 하 고 새 폴더에 중앙 액세스 정책을 적용 합니다.](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  

이 시나리오를 완료 하려면 다음 정보를 사용 합니다.  

|개체|설명|  
|-----------|-----------|  
|사용자|Jeff Low를 Contoso|  
|Contoso 및 Adatum 사용자 클레임|ID: ad: / / ext/회사: ContosoAdatum<br /><br />원본 특성: 회사<br /><br />제안 된 값: Contoso를 Adatum **중요 합니다.** Contoso와 Adatum 클레임 변환에 대 한 동일 하도록 하려면 클레임 유형을 '회사'의 ID를 설정 해야 합니다.|  
|Contoso에서 중앙 액세스 규칙|AdatumEmployeeAccessRule|  
|Contoso에서 중앙 액세스 정책|Adatum 전용 액세스 정책|  
|Contoso 및 Adatum 클레임 변환 정책|DenyAllExcept 회사|  
|Contoso의 파일 폴더|D:\EARNINGS|  

## <a name="BKMK_3"></a>신뢰할 수 있는 포리스트 (Adatum)에서 클레임 변환을 설정합니다  
이 단계에서는 Adatum Contoso 전달할 '회사'를 제외한 모든 클레임을 거부 하에 변환 정책을 만들 수 있습니다.  

Windows PowerShell 용 Active Directory 모듈을 제공 합니다 **DenyAllExcept** 변환 정책에 지정된 된 클레임을 제외한 모든 항목을 삭제 하는 인수입니다.  

클레임 변환을 설정 하려면 클레임 변환 정책 만들기 및 신뢰할 수 있고 트러스팅 포리스트 사이 연결 해야 합니다.  

### <a name="BKMK_2.2"></a>Adatum에서 클레임 변환 정책 만들기  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>'회사'를 제외한 모든 클레임을 거부 하도록 Adatum 변환 정책을 만들려면  

1. 도메인 컨트롤러에 암호를 사용 하 여 관리자로 adatum.com에 로그인 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except Company"`  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"adatum.com" `  

   ```  

### <a name="BKMK_2.3"></a>Adatum의 트러스트 도메인 개체에는 클레임 변환 링크 설정  
이 단계에서는 Contoso에 대 한 Adatum의 트러스트 도메인 개체에 새로 만든된 클레임 변환 정책을 적용 합니다.  

##### <a name="to-apply-the-claims-transformation-policy"></a>클레임 변환 정책 적용  

1. 도메인 컨트롤러에 암호를 사용 하 여 관리자로 adatum.com에 로그인 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  

     Set-ADClaimTransformLink `  
   -Identity:"contoso.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   '"TrustRole:Trusted `  

   ```  

## <a name="BKMK_4"></a>(Contoso) 트러스팅 포리스트에 클레임 변환 설정  
이 단계에서는 contoso (트러스팅 포리스트) '회사입니다.'를 제외한 모든 클레임을 거부 하는 클레임 변환 정책을 만듭니다. 클레임 변환 정책 만들기 및 포리스트 트러스트에 연결 해야 합니다.  

### <a name="BKMK_4.1"></a>Contoso에서 클레임 변환 정책 만들기  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>'회사'를 제외한 모든 거부 Adatum 변환 정책을 만들려면  

1. 도메인 컨트롤러에 암호를 사용 하 여 관리자로 contoso.com에 로그인 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except company" `  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"contoso.com" `  

   ```  

### <a name="BKMK_4.2"></a>Contoso 트러스트 도메인 개체에는 클레임 변환 링크 설정  
새로 만든 적용이 단계에서는 Adatum "회사" 있도록 contoso.com 트러스트 도메인 개체에 클레임 변환 정책 contoso.com으로 전달 하도록 합니다. 트러스트 도메인 개체 adatum.com을 라고 합니다.  

##### <a name="to-set-the-claims-transformation-policy"></a>클레임 변환 정책 설정  

1. 도메인 컨트롤러에 암호를 사용 하 여 관리자로 contoso.com에 로그인 <strong>pass@word1</strong>합니다.  

2. Windows PowerShell에서 관리자 권한 명령 프롬프트를 열고 다음을 입력 합니다.  

   ```  

     Set-ADClaimTransformLink   
   -Identity:"adatum.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   -TrustRole:Trusting `  

   ```  

## <a name="BKMK_5"></a>시나리오의 유효성을 검사합니다  
이 단계에서는 사용자 공유 폴더에 대 한 액세스 권한이 있는지 유효성을 검사 하는 파일 서버 FILE1에 설정 된 D:\EARNINGS 폴더에 액세스 하려고 합니다.  

#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Adatum 사용자 공유 폴더에 액세스할 수 있는지 확인 합니다.  

1. 컴퓨터 클라이언트에 로그인을 암호를 사용 하 여 Jeff Low를 CLIENT1 <strong>pass@word1</strong>합니다.  

2. 폴더로 이동 \\\FILE1.contoso.com\Earnings 합니다.  

3. Jeff Low 폴더에 액세스할 수 있어야 합니다.  

## <a name="additional-scenarios-for-claims-transformation-policies"></a>클레임 변환 정책에 대 한 추가 시나리오  
다음은 추가 일반적인 사례는 클레임 변환의 목록입니다.  


|                                                 시나리오                                                 |                                                                                                                                                                                                                                           정책                                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  Contoso를 Adatum 하기 위해 거쳐야 Adatum에서 제공 하는 모든 클레임을 허용                  |                                                          코드- <br />New-ADClaimTransformPolicy \`<br /> 설명: "클레임 변환 정책 모든 클레임을 허용 하려면" \`<br />-Name:"AllowAllClaimsPolicy" \`<br />-AllowAll \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsPolicy" \`<br />-TrustRole:Trusting \`<br />-Server:"contoso.com" \`                                                          |
|                  Contoso를 Adatum 하기 위해 거쳐야 Adatum에서 제공 하는 모든 클레임을 거부                   |                                                            코드- <br />New-ADClaimTransformPolicy \`<br />설명: "클레임 변환 정책 모든 클레임을 거부 하려면" \`<br />-Name:"DenyAllClaimsPolicy" \`<br /> -DenyAll \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"DenyAllClaimsPolicy" \`<br />-TrustRole:Trusting \`<br />-Server:"contoso.com"\`                                                             |
| "회사" 및 "Department" Contoso Adatum 하기 위해 거쳐야 제외한 Adatum에서 제공 하는 모든 클레임을 허용 | 코드 <br />-새-ADClaimTransformationPolicy \`<br />설명: "클레임 변환 정책 회사 및 부서를 제외한 모든 클레임을 허용 하려면" \`<br /> -Name:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br />-AllowAllExcept:company,department \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br /> -Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br /> -TrustRole:Trusting \`<br />-Server:"contoso.com" \` |

## <a name="BKMK_Links"></a>참고 항목  

-   클레임 변환에 사용할 수 있는 모든 Windows PowerShell cmdlet 목록은 참조 하세요 [Active Directory PowerShell Cmdlet 참조](https://go.microsoft.com/fwlink/?LinkId=243150)합니다.  

-   내보내기 및 가져오기 두 포리스트 간에 DAC 구성 정보를 포함 하는 고급 작업을 사용 합니다 [동적 액세스 제어 PowerShell 참조](https://go.microsoft.com/fwlink/?LinkId=243150)  

-   [포리스트에 클레임 배포](Deploy-Claims-Across-Forests.md)  

-   [클레임 변환 규칙 언어](Claims-Transformation-Rules-Language.md)  

-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  


