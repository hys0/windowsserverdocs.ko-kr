---
title: 도메인 이름 공급자 목록 바꾸기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 104d0412-2d77-4cd4-99f7-65a885522850
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e55dc757b93c7e11b29ed4fd579362900e54f909
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819846"
---
# <a name="replace-the-list-of-domain-name-providers"></a>도메인 이름 공급자 목록 바꾸기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 작업을 수행하여 도메인 이름 설정 마법사에 표시되는 도메인 이름 공급자의 목록을 바꿀 수 있습니다.  


-   [조회 서비스 파일 만들기](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  

-   [참조 컴퓨터의 레지스트리에 항목을 추가 합니다.](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [조회 서비스 파일 만들기](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  

-   [참조 컴퓨터의 레지스트리에 항목을 추가 합니다.](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  


###  <a name="create-the-referral-service-files"></a><a name="BKMK_ReferralFiles"></a>조회 서비스 파일 만들기  
 조회 서비스 관리 도구는 도메인 이름 설정 마법사에 표시되는 도메인 이름 공급자 목록을 정의하는 데 사용되는 파일 집합을 만듭니다. 전 세계 각 지역에서 대해 XML으로 형식이 지정된 파일이 만들어지며, 이 파일에는 도구에서 지정하는 도메인 이름 공급자에 대한 정보가 포함됩니다. 도구를 통해 만든 파일은 인터넷에서 관리하는 보안 링크(HTTPS)를 통해 액세스할 수 있는 폴더에 있어야 합니다.  

##### <a name="to-create-the-referral-files"></a>조회 파일을 만들려면  

1.  조회 서비스 관리 도구를 엽니다.  

2.  **추가**를 클릭합니다.  

3.  도메인 이름 공급자 추가 대화 상자에 도메인 이름 공급자 이름을 입력합니다.  

4.  도메인 이름 공급자가 지원하는 최상위 도메인을 추가합니다. **추가**를 클릭하고 최상위 도메인 식별자를 입력한 다음 지원되는 지역을 선택하여 이 작업을 수행합니다. **모든 지역**을 선택할 수 있습니다.  

5.  도메인 이름 공급자에 대한 설명을 입력합니다.  

6.  도메인 이름 공급자와 연결된 모든 웹 사이트의 URL을 추가합니다.  

7.  도메인 이름 공급자에 대한 로고를 사용할 수 있으면 **로고 변경**을 클릭하여 로고를 추가합니다.  

8.  **저장**을 클릭합니다.  

9. 마법사에 나열할 각 도메인 이름 공급자에 대해 2 ~ 8단계를 반복합니다.  

10. 도메인 이름 공급자를 모두 추가한 후 조회 파일을 배치할 폴더를 선택합니다. 폴더를 선택할 때 HTTPS 링크를 통해 조회 파일에 액세스해야 함을 명심하세요.  

11. **파일 시스템에 파일 생성**을 클릭합니다.  

###  <a name="add-an-entry-to-the-registry-on-the-reference-computer"></a><a name="BKMK_AddRegistry"></a>참조 컴퓨터의 레지스트리에 항목을 추가 합니다.  
 운영 체제에서 조회 서비스 파일을 찾을 수 있는 위치를 지정하려면 레지스트리 항목을 추가해야 합니다.  

##### <a name="to-add-a-key-to-the-registry"></a>레지스트리에 키를 추가하려면  

1.  참조 컴퓨터에서 **시작**을 클릭하고 **regedit**을 입력한 다음 **Enter** 키를 누릅니다.  

2.  왼쪽 창에서 **HKEY_LOCAL_MACHINE**, **소프트웨어**, **Microsoft**, **Windows Server**, **도메인 관리자**를 차례로 확장한 다음 **공급자**를 확장합니다.  

3.  **E423C85D-6B1F-4583-95E0-449D8263BAC4** 키를 마우스 오른쪽 단추로 클릭하고 **문자열 값**을 클릭합니다.  

4.  문자열 이름에 **ReferralServerHttpsUri**를 입력한 다음 **Enter** 키를 누릅니다.  

5.  오른쪽 창에서 새 **ReferralServerHttpsUri** 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  


6.  [조회 서비스 파일 만들기](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)에서 만든 조회 파일에 액세스하는 데 사용되는 HTTPS URL을 입력한 다음 **확인**을 클릭합니다.  

6.  [조회 서비스 파일 만들기](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)에서 만든 조회 파일에 액세스하는 데 사용되는 HTTPS URL을 입력한 다음 **확인**을 클릭합니다.  


~~~
> [!IMPORTANT]
>  A slash (/) is required at the end of the URL.  
~~~

###  <a name="domain-name-status-issues"></a><a name="BKMK_ReplaceDomainNameProviders"></a>도메인 이름 상태 문제  
 파트너가 도메인 이름 공급자를 추가 하 고 Windows Server Essentials SDK의 API (응용 프로그래밍 인터페이스)를 사용 하 여 인증서에 대 한 알 수 없음, 실패 및 Certificaterequestnotsubmitted로 설정한 상태를 설정 하는 경우 고객은 잘못 된 정보를 수신 합니다. 메시지 및 구성 결과. 이는 작업이 상태를 반환하는 대신 오류로 처리되기 때문입니다.  

 다음 도메인 상태는 실패를 나타내며 오류로 보고됩니다.  

- 실패  

- PendingCustomerInterventionRequired  

- PurchaseFailed  

- DomainNotFound  

- InRenewalCustomerInterventionRequired  

- RenewalFailed  

  다음 도메인 상태는 성공을 나타내며 성공으로 보고됩니다.  

- 준비  

- 보류 중  

- InRenewal  

## <a name="see-also"></a>관련 항목  

 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [이미지  만들기 및 사용자 지정](../install/Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

