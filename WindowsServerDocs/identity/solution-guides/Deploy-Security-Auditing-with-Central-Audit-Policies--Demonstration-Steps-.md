---
ms.assetid: 22347a94-aeea-44b4-85fb-af2c968f432a
title: "보안와 중앙 감사 정책 (데모 단계) 감사 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac2b1643ed151e94c3815abca9a57eb3706c845a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-security-auditing-with-central-audit-policies-demonstration-steps"></a>보안와 중앙 감사 정책 (데모 단계) 감사 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 시나리오에서 만든 금융 정책을 사용 하 여 금융 문서 폴더의에서 파일에 대 한 액세스를 감사 됩니다 [중앙 액세스 정책 & #40; 데모 단계 & #41; 배포 ](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md). 하지 않을 폴더에 액세스할 수 없는 권한이 있는 사용자가에 대 한 액세스를 경우 이벤트 뷰어에 활동이 캡처됩니다.   
 다음 단계를 테스트이 시나리오 필요 합니다.  
  
|작업|설명|  
|--------|---------------|  
|[전 세계 개체 액세스 구성](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_1)|이 단계에서 도메인 컨트롤러에서 전 세계 개체 액세스 정책을 구성 합니다.|  
|[업데이트를 그룹 정책 설정](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_2)|파일 서버에 로그인 하 고 그룹 정책 업데이트를 적용 합니다.|  
|[전 세계 개체 액세스 정책이 적용 되어 있는지 확인](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_3)|이벤트 뷰어에 관련 이벤트를 봅니다. 이벤트 국가 및 문서 형식의 메타 데이터를 포함 해야 합니다.|  
  
## <a name="BKMK_1"></a>전 세계 개체 액세스 정책을 구성합니다  
이 단계에서 도메인 컨트롤러의 글로벌 개체 액세스 정책을 구성할 수 있습니다.  
  
#### <a name="to-configure-a-global-object-access-policy"></a>전 세계 개체 액세스 정책을 구성 하려면  
  
1.  암호를 사용 contoso\administrator로 d c 1 도메인 컨트롤러에 로그인 **pass@word1**합니다.  
  
2.  서버 관리자 가리킨 **도구**을 차례로 클릭 하 고 **그룹 정책 관리**합니다.  
  
3.  콘솔 트리에서 두 번 클릭 **도메인**를 두 번 클릭 **contoso.com**, 클릭 **Contoso**, 다음 두 번 클릭 하 고 **파일 서버**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **FlexibleAccessGPO**를 클릭 하 고 **편집**합니다.  
  
5.  두 번 클릭 **컴퓨터 구성**를 두 번 클릭 **정책**, 다음 두 번 클릭 하 고 **Windows 설정**합니다.  
  
6.  두 번 클릭 **보안 설정**를 두 번 클릭 **감사 정책 구성 고급**, 다음 두 번 클릭 하 고 **감사 정책**합니다.  
  
7.  두 번 클릭 **개체 액세스**, 다음 두 번 클릭 하 고 **감사 파일 시스템**합니다.  
  
8.  선택는 **다음과 같은 이벤트를 구성** 확인란을 선택는 **성공** 및 **오류** 확인란을 선택한 다음 클릭 **확인**합니다.  
  
9. 탐색 창에서 두 번 클릭 **글로벌 개체 액세스 감사**, 다음 두 번 클릭 하 고 **파일 시스템**합니다.  
  
10. 선택는 **정책 설정을 정의** 확인란을 클릭 하 고 **구성**합니다.  
  
11. **파일 SACL 전 세계에 대 한 고급 보안 설정을** 상자를 클릭 **추가**, 클릭 한 다음 **주체 선택**, 입력 **모든**, 클릭 한 다음 **확인**합니다.  
  
12. 에 **글로벌 파일 SACL 감사 항목** 상자를 선택 하 고 **모든 권한** 에 **권한을** 상자 합니다.  
  
13. 에 **조건을 추가:** 섹션에서 클릭 **조건을 추가** 목록 드롭다운 목록에서 선택 하 고   
    [**리소스**] [**부서**] [**Any of**] [**Value**] [**금융**] 합니다.  
  
14. 클릭 **확인** 글로벌 개체 액세스 구성을 완료 하기 위해 세 번 정책 설정을 감사 합니다.  
  
15. 탐색 창에서 클릭 **개체 액세스**, 결과 창에서 두 번 클릭 하 고 **감사 처리 조작**합니다. 클릭 **다음 감사 이벤트 구성**, **성공**, 및 **오류**, 클릭 **확인**, GPO 유연한 액세스를 닫습니다.  
  
## <a name="BKMK_2"></a>그룹 정책 설정 업데이트  
이 단계 감사 정책 만든 후 그룹 정책 설정을 업데이트 합니다.  
  
#### <a name="to-update-group-policy-settings"></a>그룹 정책 설정 업데이트  
  
1.  암호를 사용 contoso\Administrator로 파일 1 파일 서버에에 로그인 **pass@word1**합니다.  
  
2.  Windows 키 + r 다음 입력 **cmd** 명령 프롬프트 창을 엽니다.  
  
    > [!NOTE]  
    > 하는 경우는 **사용자 계정 컨트롤** 무엇을 누르고 원하는 다음 작업이 표시 되는지 확인 대화 상자가 나타나면 **예**합니다.  
  
3.  입력 **gpupdate /force** ENTER 키를 누릅니다.  
  
## <a name="BKMK_3"></a>전 세계 개체 액세스 정책이 적용 되어 있는지 확인  
그룹 정책 설정을 적용 한 후 감사 정책 설정이 올바르게 적용 된 것을 확인할 수 있습니다.  
  
#### <a name="to-verify-that-the-global-object-access-policy-has-been-applied"></a>전 세계 개체 액세스 정책이 적용 되어 있는지 확인 하려면  
  
1.  가지의로 Contoso\MReid CLIENT1에 로그인 합니다. Word 문서 2 수정 및 문서, 하이퍼링크 "file:///\\\ID_AD_FILE1\\\Finance" \\\ FILE1\Finance 폴더를 찾습니다.  
  
2.  파일 1 contoso\administrator로 파일 서버에 로그인 합니다. 이벤트 뷰어 열고를 찾은 **Windows 로그**선택 **보안**, 사용자의 활동 결과 이벤트 감사 있는지 확인 하 고 **4656** 및 **4663** (명시적 감사 Sacl 파일 또는 폴더를 만든을 설정 하지 않은 경우에, 수정 및 삭제 됨).  
  
> [!IMPORTANT]  
> 새 로그온 이벤트에서이 리소스는 위치에 유효한 액세스 체크 되 고 사용자를 대신 하 여 컴퓨터에서 생성 됩니다. 활동에 대 한 사용자의 로그인, 로그온 생성 되는 이벤트 때문에 유효한 액세스 하 고 때문에 생성 된 구분할 수 보안 감사 로그 분석 대화형 네트워크 사용자가 로그인, 가장 수준을 정보가 포함 됩니다. 유효한 액세스 있어서 로그온 이벤트 생성 되 면 가장 수준을 Id가 됩니다. 가장 수준으로 로그온 이벤트를에서는 일반적으로 발생 하는 네트워크 대화형 사용자 로그인에 가장 또는 위임 = 합니다.  
  
## <a name="BKMK_Links"></a>참조 하십시오  
  
-   [시나리오가: 감사 액세스 파일](Scenario--File-Access-Auditing.md)  
  
-   [파일에 대 한 계획 액세스 감사](Plan-for-File-Access-Auditing.md)  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  

