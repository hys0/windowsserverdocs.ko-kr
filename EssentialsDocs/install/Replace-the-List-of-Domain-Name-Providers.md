---
title: "도메인 이름 공급자 목록이 바꾸기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 104d0412-2d77-4cd4-99f7-65a885522850
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ebaef0f88456f61fa229c9a18ee8014987fe7fa7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="replace-the-list-of-domain-name-providers"></a>도메인 이름 공급자 목록이 바꾸기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음과 같은 작업을 완료 하 여 설정 도메인 이름 마법사에 표시 되는 도메인 이름 공급자 목록을 바꿀 수 있습니다.  
  

-   [조회 서비스 파일을 만듭니다.](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [참조 컴퓨터의 레지스트리에 항목 추가](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [조회 서비스 파일을 만듭니다.](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [참조 컴퓨터의 레지스트리에 항목 추가](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

  
###  <a name="BKMK_ReferralFiles"></a>조회 서비스 파일을 만듭니다.  
 추천 서비스 관리 도구 집합 설정 도메인 이름 마법사에 표시 되는 도메인 이름 공급자 목록 정의 하는 데 사용 하는 파일을 만듭니다. XML 된 형식의 파일은 전 세계 각 영역에 대 한 만들고 도구에 지정 되는 도메인 이름 공급자에 대 한 정보를 포함 합니다. 도구에서 생성 된 파일은 인터넷에서 관리 하는 보안 링크 (HTTPS)를 통해 액세스할 수 있는 폴더에 있어야 합니다.  
  
##### <a name="to-create-the-referral-files"></a>추천 파일을 만들려면  
  
1.  추천 서비스 관리 도구를 엽니다.  
  
2.  클릭 **추가**합니다.  
  
3.  추가 도메인 이름 공급자 대화 상자에서 도메인 이름 공급자의 이름을 입력 합니다.  
  
4.  최상위 도메인 도메인 이름 공급자에서 지원 되는 추가 합니다. 클릭 하 여이 작업을 수행 **추가**, 최상위 도메인 식별자를 입력 하 고 지원 되는 영역을 선택 합니다. 선택할 수 **일부 지역**합니다.  
  
5.  도메인 이름 공급자에 대 한 설명을 입력 합니다.  
  
6.  도메인 이름 공급자와 관련 된 모든 웹 사이트의 Url을 추가 합니다.  
  
7.  클릭 하 여 로고 도메인 이름 공급자를 사용할 수 있는 경우 추가 로고 **변경 로고**합니다.  
  
8.  클릭 **저장**합니다.  
  
9. 마법사에서 목록을 하려는 각 도메인 이름 공급자에 2-8 단계를 반복 합니다.  
  
10. 모든 도메인 이름 공급자를 추가한 후 추천 파일 찾을 수는 폴더를 선택 합니다. 폴더를 선택할 때 점을 명심에서 추천 파일 HTTPS 링크를 통해 액세스할 수 있어야 합니다.  
  
11. 클릭 **파일 파일 시스템을 생성**합니다.  
  
###  <a name="BKMK_AddRegistry"></a>참조 컴퓨터의 레지스트리에 항목 추가  
 레지스트리 항목이 지정 되는 운영 체제 파일을 찾을 수 조회 서비스에 추가 해야 합니다.  
  
##### <a name="to-add-a-key-to-the-registry"></a>레지스트리 키를 추가 하려면  
  
1.  참조 컴퓨터에서 클릭 **시작**, 입력 **regedit**를 누른 다음 **Enter**합니다.  
  
2.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**, 확장 **도메인 관리자**를 확장 한 다음 **공급자**합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **E423C85D-6B1F-4583-95E0-449D8263BAC4** 키를 클릭 한 다음 **문자열 값**합니다.  
  
4.  입력 **ReferralServerHttpsUri** 문자열을 차례로 누르기 이름을 **Enter**합니다.  
  
5.  새을 마우스 오른쪽 단추로 클릭 **ReferralServerHttpsUri** 오른쪽 창에는 문자열와 클릭 한 다음 **수정**합니다.  
  

6.  만든 추천 파일에 액세스 하는 데 사용 되는 HTTPS URL을 입력 [조회 서비스 파일을 만들어](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)을 차례로 클릭 하 고 **확인**합니다.  

6.  만든 추천 파일에 액세스 하는 데 사용 되는 HTTPS URL을 입력 [조회 서비스 파일을 만들어](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)을 차례로 클릭 하 고 **확인**합니다.  

  
    > [!IMPORTANT]
    >  슬래시 (/) URL 끝 필요 합니다.  
  
###  <a name="BKMK_ReplaceDomainNameProviders"></a>도메인 이름 상태 문제  
 파트너 도메인 이름 공급자를 추가 하 고 Windows Server Essentials SDK의 응용 프로그램 프로그래밍 인터페이스 (API)를 사용 하 여 알 수 없는, 실패 및 CertificateRequestNotSubmitted 상태 인증서에 대 한 설정, 경우 고객 잘못 메시지 및 구성 결과 받습니다. 하는 경우는 예외에 의해 처리 하기 때문에 상태를 반환 하지 않고 합니다.  
  
 다음 도메인 상태 오류가 발생 하는 하 고 오류가으로 보고 합니다.  
  
-   실패  
  
-   PendingCustomerInterventionRequired  
  
-   PurchaseFailed  
  
-   DomainNotFound  
  
-   InRenewalCustomerInterventionRequired  
  
-   RenewalFailed  
  
 다음 도메인 상태 성공 중 이며를 성공적으로 보고 합니다.  
  
-   준비  
  
-   보류 중인  
  
-   InRenewal  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

