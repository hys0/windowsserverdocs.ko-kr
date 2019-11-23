---
ms.assetid: 22347a94-aeea-44b4-85fb-af2c968f432a
title: 중앙 감사 정책으로 보안 감사 배포(시연 단계)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ecbaa33d83d7b37f376a426571c0d2df89c7695d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407118"
---
# <a name="deploy-security-auditing-with-central-audit-policies-demonstration-steps"></a>중앙 감사 정책으로 보안 감사 배포(시연 단계)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 시나리오에서는 [중앙 액세스 정책 &#40;&#41;데모 단계 배포](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)에서 만든 금융 정책을 사용 하 여 금융 문서 폴더의 파일에 대 한 액세스를 감사 합니다. 폴더에 대한 액세스 권한이 없는 사용자가 이 폴더에 액세스할 경우 이벤트 뷰어에 작업이 캡처됩니다.   
 이 시나리오를 테스트하려면 다음 단계가 필요합니다.  
  
|태스크|설명|  
|--------|---------------|  
|[전역 개체 액세스 구성](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_1)|이 단계에서는 도메인 컨트롤러에서 글로벌 개체 액세스 정책을 구성합니다.|  
|[그룹 정책 설정 업데이트](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_2)|파일 서버에 로그인하고 그룹 정책 업데이트를 적용합니다.|  
|[글로벌 개체 액세스 정책이 적용 되었는지 확인](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_3)|이벤트 뷰어에서 관련 이벤트를 봅니다. 이벤트에는 국가 및 문서 종류에 대한 메타데이터가 포함되어야 합니다.|  
  
## <a name="BKMK_1"></a>전역 개체 액세스 정책 구성  
이 단계에서는 도메인 컨트롤러에서 글로벌 개체 액세스 정책을 구성합니다.  
  
#### <a name="to-configure-a-global-object-access-policy"></a>글로벌 개체 액세스 정책을 구성하려면  
  
1. 암호 <strong>pass@word1</strong>를 사용 하 여 contoso\administrator로 도메인 컨트롤러 d c 1에 로그인 합니다.  
  
2. 서버 관리자에서 **도구**를 가리킨 다음 **그룹 정책 관리**를 클릭합니다.  
  
3. 콘솔 트리에서 **도메인**을 두 번 클릭하고 **contoso.com**을 두 번 클릭한 후 **Contoso**를 클릭하고 **파일 서버**를 두 번 클릭합니다.  
  
4. **FlexibleAccessGPO**를 마우스 오른쪽 단추로 클릭한 후 **편집**을 클릭합니다.  
  
5. **컴퓨터 구성**을 두 번 클릭하고 **정책**을 두 번 클릭한 다음 **Windows 설정**을 두 번 클릭합니다.  
  
6. **보안 설정**을 두 번 클릭하고 **고급 감사 정책 구성**을 두 번 클릭한 다음 **감사 정책**을 두 번 클릭합니다.  
  
7. **개체 액세스**를 두 번 클릭한 후 **파일 시스템 감사**를 두 번 클릭합니다.  
  
8. **다음 이벤트 구성** 확인란을 선택하고 **성공** 및 **실패** 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
9. 탐색 창에서 **글로벌 개체 액세스 감사**를 두 번 클릭한 후 **파일 시스템**을 두 번 클릭합니다.  
  
10. **이 정책 설정 정의** 확인란을 선택하고 **구성**을 클릭합니다.  
  
11. **전역 파일 SACL의 고급 보안 설정** 상자에서 **추가**를 클릭하고 **보안 주체 선택**을 클릭한 후 **모두**를 입력하고 **확인**을 클릭합니다.  
  
12. **전역 파일 SACL 감사 항목** 상자의 **사용 권한** 상자에서 **모든 권한**을 선택합니다.  
  
13. **조건 추가:** 섹션에서 **조건 추가**를 클릭하고 드롭다운 목록에서   
    [**리소스**] [**부서**] [**다음 중 하나**] [**값**] [**금융**]을 선택합니다.  
  
14. **확인** 을 세 번 클릭하여 글로벌 개체 액세스 감사 정책 설정에 대한 구성을 완료합니다.  
  
15. 탐색 창에서 **개체 액세스**를 클릭하고 결과 창에서 **핸들 조작 감사**를 두 번 클릭합니다. **다음 감사 이벤트 구성**, **성공**, **실패**를 클릭하고 **확인**을 클릭한 후 유연한 액세스 GPO를 닫습니다.  
  
## <a name="BKMK_2"></a>그룹 정책 설정 업데이트  
이 단계에서는 감사 정책을 만든 후 그룹 정책 설정을 업데이트합니다.  
  
#### <a name="to-update-group-policy-settings"></a>그룹 정책 설정을 업데이트하려면  
  
1. 암호 <strong>pass@word1</strong>를 사용 하 여 파일 서버 FILE1에 contoso\Administrator로 로그인 합니다.  
  
2. Windows 키+R을 누른 다음 **cmd**를 입력하여 명령 프롬프트 창을 엽니다.  
  
   > [!NOTE]  
   > **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
3. **gpupdate /force**를 입력한 다음 Enter 키를 누릅니다.  
  
## <a name="BKMK_3"></a>글로벌 개체 액세스 정책이 적용 되었는지 확인  
그룹 정책 설정이 적용된 후 감사 정책 설정이 올바르게 적용되었는지 확인할 수 있습니다.  
  
#### <a name="to-verify-that-the-global-object-access-policy-has-been-applied"></a>글로벌 개체 액세스 정책이 적용되었는지 확인하려면  
  
1.  Contoso\MReid로 클라이언트 컴퓨터 CLIENT1에 로그인합니다. HYPERLINK "file:///\\\\\\\ ID_AD_FILE1\\\Finance" \\\ File1\finance documents Documents 폴더로 이동한 다음 Word 문서 2를 수정 합니다.  
  
2.  contoso\administrator로 파일 서버 FILE1에 로그인합니다. 이벤트 뷰어를 열고 **Windows 로그**를 찾은 후 **보안**을 선택하고 만들거나, 수정하거나, 삭제한 파일이나 폴더에 대해 명시적인 감사 SACL을 설정하지 않았더라도 작업을 통해 감사 이벤트 **4656** 및 **4663** 이 생성되었는지 확인합니다.  
  
> [!IMPORTANT]  
> 유효한 액세스를 검사 중인 사용자 대신 리소스가 위치한 컴퓨터에 대해 새 로그온 이벤트가 생성됩니다. 사용자 로그인 작업에 대한 보안 감사 로그 분석 시 유효한 액세스로 인해 생성된 로그온 이벤트와 대화형 네트워크 사용자 로그인으로 인해 생성된 로그온 이벤트를 구별하기 위해 가장 수준 정보가 포함됩니다. 로그온 이벤트가 유효한 액세스로 인해 생성된 경우 가장 수준이 ID가 됩니다. 네트워크 대화형 사용자 로그인에서는 일반적으로 가장 수준이 가장 또는  위임인 로그온 이벤트가 생성됩니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [시나리오: 파일 액세스 감사](Scenario--File-Access-Auditing.md)  
  
-   [파일 액세스 감사 계획](Plan-for-File-Access-Auditing.md)  
  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

