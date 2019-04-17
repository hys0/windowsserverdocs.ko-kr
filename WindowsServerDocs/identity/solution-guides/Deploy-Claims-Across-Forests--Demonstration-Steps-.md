---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: "숲 (데모 단계) 청구 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3bab7a396061ecae8a187cc6986d6d026a9e4b32
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>숲 (데모 단계) 청구 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 기본 시나리오를 신뢰 하 고 신뢰할 수 있는 숲 간의 클레임 변환을 구성 하는 방법에 설명 하겠습니다. 클레임 변환 정책 개체 수 생성 및 숲 신뢰 하 고 신뢰할 수 있는 숲 속의 보안에 연결 된 방법 학습 합니다. 그런 다음 시나리오 여부를 검사 합니다.  
  
## <a name="scenario-overview"></a>시나리오 개요  
Adatum Corporation provides financial services to Contoso, Ltd. Each quarter, Adatum accountants copy their account spreadsheets to a folder on a file server located at Contoso, Ltd. There is a two-way trust set up from Contoso to Adatum. Contoso, Ltd. wants to protect the share so that only Adatum employees can access the remote share.  
  
이 경우:  
  
1.  [테스트 환경 및 필수 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  
  
2.  [신뢰할 수 있는 숲 (Adatum)에 클레임 변환 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  
  
3.  [클레임 변환 신뢰 숲 (Contoso)에서 설정](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  
  
4.  [시나리오의 유효성을 검사합니다](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  
  
## <a name="BKMK_1.1"></a>테스트 환경 및 필수 설정  
테스트 구성에서는 두 개의 숲 설정: Adatum Corporation 및 Ltd Contoso Contoso 사이의 Adatum 양방향 신뢰 하는 데 합니다. "adatum.com" 신뢰할 수 있는 숲 이며 "contoso.com" 신뢰 숲입니다.  
  
클레임 변환 시나리오 신뢰 숲 속의 클레임 신뢰할 수 있는 숲 속의 클레임 변환 보여 줍니다. 이렇게 하려면 adatum.com 라는 새로 숲을 설정 하 고 'Adatum' 회사 값 테스트 사용자와 숲 채웁니다. 그런 다음 contoso.com 사이의 adatum.com 양방향 신뢰를 설정 해야 합니다.  
  
> [!IMPORTANT]  
> Contoso 및 Adatum 숲을 설정할 때 Windows Server 2012 도메인 기능 수준이 클레임 변환에 대 한 작동 하도록 두 루트 도메인 지 확인 해야 합니다.  
  
랩 다음을 설정 해야 합니다. 이 절차에 자세히 설명 된 [부록 b: the 테스트 환경 설정을](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
이 시나리오 랩을 설정 하려면 다음 절차 구현 해야 합니다.  
  
1.  [신뢰할 수 있는 Contoso 숲 Adatum 설정](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
2.  ['회사' 클레임 유형 Contoso에 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  
  
3.  ['회사' 리소스 속성 Contoso 사용 하도록 설정](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  
  
4.  [중앙 액세스 규칙 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  
  
5.  [중앙 액세스 정책 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  
  
6.  [그룹 정책을 통해 새 정책을 게시 합니다.](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  
  
7.  [파일 서버에 수익 폴더 만들기](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  
  
8.  [분류를 설정 하 고 새 폴더에 대 한 중앙 액세스 정책을 적용합니다](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  
  
다음 정보를 사용 하 여이 시나리오를 완료 하려면:  
  
|개체|세부 정보|  
|-----------|-----------|  
|사용자가|Jeff 낮음으로 Contoso|  
|사용자 클레임 Adatum 및 Contoso|ID: 광고: / / 확장/회사: ContosoAdatum<br /><br />원본 특성: 회사<br /><br />추천 값: Contoso, Adatum **중요:** Contoso와 Adatum 클레임 변환에 대 한 동일 하 게 작동 하도록 클레임 유형 회사'에 ID를 설정 해야 합니다.|  
|중앙 액세스 규칙 Contoso에서|AdatumEmployeeAccessRule|  
|중앙 액세스 정책 Contoso에서|Adatum만 액세스 정책|  
|클레임 Adatum 및 Contoso 변환 정책|DenyAllExcept 회사|  
|Contoso 폴더의 파일|D:\EARNINGS|  
  
## <a name="BKMK_3"></a>신뢰할 수 있는 숲 (Adatum)에 클레임 변환 설정  
이 단계에서 Contoso 전달할 '회사' 제외한 모든 클레임 거부 하려면 Adatum에 변환 정책을 만들 수 있습니다.  
  
Windows PowerShell에 대 한 Active Directory 모듈 제공는 **DenyAllExcept** 변환 정책에 지정 된 청구 제외한 모든 항목을 삭제 하는 인수 합니다.  
  
클레임 변환을 설정 하려면 클레임 변환 정책 만들고 신뢰 하 고 신뢰할 수 있는 숲 간에 연결 해야 합니다.  
  
### <a name="BKMK_2.2"></a>클레임 변환 정책 Adatum에서 만들기  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>변환 정책을 '회사' 제외한 모든 클레임 거부 하려면 Adatum 만들려면  
  
1.  도메인 컨트롤러 adatum.com 관리자 권한으로 암호로 로그인 **pass@word1**합니다.  
  
2.  관리자 명령 프롬프트를 Windows PowerShell에서 열고 다음을 입력 합니다.  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except Company"`  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"adatum.com" `  
  
    ```  
  
### <a name="BKMK_2.3"></a>클레임 변환 링크를 신뢰 도메인 개체 Adatum의 설정  
이 단계를 적용 새로 만든된 클레임 변환 정책 Adatum의 신뢰 도메인 개체 contoso.  
  
##### <a name="to-apply-the-claims-transformation-policy"></a>클레임 변환 정책을 적용 하려면  
  
1.  도메인 컨트롤러 adatum.com 관리자 권한으로 암호로 로그인 **pass@word1**합니다.  
  
2.  관리자 명령 프롬프트를 Windows PowerShell에서 열고 다음을 입력 합니다.  
  
    ```  
  
      Set-ADClaimTransformLink `  
    -Identity:"contoso.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    '"TrustRole:Trusted `  
  
    ```  
  
## <a name="BKMK_4"></a>클레임 변환 신뢰 숲 (Contoso)에서 설정  
이 단계에서 클레임 변환 정책을 '회사.' 제외한 모든 클레임 거부 하려면 Contoso (신뢰 숲)에서 만든 클레임 변환 정책 만들고 숲 신뢰를 연결 해야 합니다.  
  
### <a name="BKMK_4.1"></a>클레임 변환 정책에서 Contoso 만들기  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>변환 정책을 '회사' 제외한 모든 거부 하려면 Adatum 만들려면  
  
1.  도메인 컨트롤러 contoso.com 관리자 권한으로 암호로 로그인 **pass@word1**합니다.  
  
2.  Windows PowerShell 관리자 명령 프롬프트를 열고 다음을 입력 합니다.  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except company" `  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"contoso.com" `  
  
    ```  
  
### <a name="BKMK_4.2"></a>클레임 변형 링크 Contoso 신뢰 도메인 개체 설정  
In this step, you apply the newly created claims transformation policy on the contoso.com trust domain object for Adatum to allow "Company" be passed through to contoso.com. The trust domain object is named adatum.com.  
  
##### <a name="to-set-the-claims-transformation-policy"></a>클레임은 변환 정책 설정 하려면  
  
1.  도메인 컨트롤러 contoso.com 관리자 권한으로 암호로 로그인 **pass@word1**합니다.  
  
2.  Windows PowerShell 관리자 명령 프롬프트를 열고 다음을 입력 합니다.  
  
    ```  
  
      Set-ADClaimTransformLink   
    -Identity:"adatum.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    -TrustRole:Trusting `  
  
    ```  
  
## <a name="BKMK_5"></a>시나리오의 유효성을 검사합니다  
이 단계에서 사용자가 공유 폴더에 액세스할 수 있는지 확인 하는 파일 서버 파일 1에 설정 된 D:\EARNINGS 폴더에 액세스 하려고 합니다.  
  
#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Adatum 사용자 공유 된 폴더에 액세스할 수 있는지 확인 하려면  
  
1.  암호를 사용 Jeff 낮게 CLIENT1 클라이언트 컴퓨터에 로그인 **pass@word1**합니다.  
  
2.  폴더 \\\FILE1.contoso.com\Earnings로 이동 합니다.  
  
3.  Jeff 낮은 폴더에 액세스할 수 있어야 합니다.  
  
## <a name="additional-scenarios-for-claims-transformation-policies"></a>클레임 변환 정책에 대 한 추가 시나리오  
다음 청구 변환에서 추가 일반적인 사례의 목록입니다.  
  
|시나리오|정책|  
|------------|----------|  
|Contoso Adatum 거쳐 Adatum에서 제공 하는 모든 클레임 허용|코드- <br />New-ADClaimTransformPolicy \'<br /> 설명: "모든 클레임 수 있도록 변환 정책을 주장" \'<br />-이름: "AllowAllClaimsPolicy" \'<br />-AllowAll \'<br />서버: "contoso.com" \'<br />Set-ADClaimTransformLink \'<br />Id: "adatum.com" \'<br />정책: "AllowAllClaimsPolicy" \'<br />-TrustRole: 신뢰 하는 \'<br />서버: "contoso.com" '|  
|거부 Contoso Adatum 거쳐 Adatum에서 제공 하는 모든 클레임|코드- <br />New-ADClaimTransformPolicy \'<br />설명: "모든 클레임 거부 하려면 변환 정책 주장" \'<br />-이름: "DenyAllClaimsPolicy" \'<br /> -DenyAll \'<br />서버: "contoso.com" \'<br />Set-ADClaimTransformLink \'<br />Id: "adatum.com" \'<br />정책: "DenyAllClaimsPolicy" \'<br />-TrustRole: 신뢰 하는 \'<br />서버: "contoso.com" '|  
|"회사" 및 "부서" Contoso Adatum 통과을 제외 하 고 Adatum에서 제공 하는 모든 클레임 허용|코드 <br />-New-ADClaimTransformationPolicy \'<br />설명: "회사와 부서 제외한 모든 클레임 수 있도록 변환 정책을 주장" \'<br /> -이름: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \'<br />-AllowAllExcept: 회사, 부서 \'<br />서버: "contoso.com" \'<br />Set-ADClaimTransformLink \'<br /> Id: "adatum.com" \'<br />정책: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \'<br /> -TrustRole: 신뢰 하는 \'<br />서버: "contoso.com" '|  
  
## <a name="BKMK_Links"></a>참조 하십시오  
  
-   For a list of all Windows PowerShell cmdlets that are available for claims transformation, see [Active Directory PowerShell Cmdlet Reference](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
-   For advanced tasks that involve export and import of DAC configuration information between two forests, use the [Dynamic Access Control PowerShell Reference](https://go.microsoft.com/fwlink/?LinkId=243150)  
  
-   [숲 클레임 배포](Deploy-Claims-Across-Forests.md)  
  
-   [클레임 변환 규칙 언어](Claims-Transformation-Rules-Language.md)  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

