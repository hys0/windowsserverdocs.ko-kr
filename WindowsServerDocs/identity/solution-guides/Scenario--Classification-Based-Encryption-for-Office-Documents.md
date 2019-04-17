---
ms.assetid: 73542e1c-53ef-4ddb-89b1-bc563b2bfb49
title: "Office 문서에 대 한 분류 기반 암호화 시나리오"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 38e058f36522ba6a2c81694cb883d0946b04adda
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-classification-based-encryption-for-office-documents"></a>Office 문서에 대 한 분류 기반 암호화 시나리오:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

중요 한 정보를 보호 주로 조직에 대 한 위험을 완화입니다. 및 책임 Act (HIPAA) 한 결제 카드 Industry 데이터 보안 표준 (PCI-DSS) 등의 다양 한 규정을 받아쓰게 한 정보를 암호화 되며 비즈니스 중요 한 정보를 암호화 하는 여러 비즈니스 가지 이유가 있습니다. 그러나 듭니다 정보를 암호화 하 고 업무 생산성 손상 될 수 있습니다. 따라서 조직에는 다른 방법 및 우선 순위를 해당 정보를 암호화 하는 경우가 많습니다.  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
 Windows Server 2012 자신의 분류에 따라 중요 한 Microsoft Office 파일을 자동으로 암호화 하는 기능을 제공 합니다. 이 파일 파일 서버에 중요 한 파일 것으로 확인 된 후 몇 초 중요 한 문서에 대 한 Active Directory Rights Management Services (AD RMS) 보호 호출 하는 파일 관리 작업을 통해 수행 됩니다. 이 파일 서버에 연속 파일 관리 작업 하 여 쉽게 처리 됩니다.  
  
AD RMS 암호화 다른 파일에 대 한 보호 계층을 제공합니다. 실수로 중요 한 파일에 액세스할 수 있는 사람의 메일을 통해 해당 파일을 보내는 하는 경우에 해당 파일 AD RMS 암호화에 의해 보호 됩니다. 사용자 파일에 액세스 하는 암호를 해독 키를 받으려면 AD RMS 서버에 자체적으로 인증 먼저 되어야 합니다. 다음 그림에서는이 프로세스를 보여 줍니다.  
  
![해결 방법 가이드](media/Scenario--Classification-Based-Encryption-for-Office-Documents/DynamicAccessControl_RevGuide_6.JPG)  
  
**그림 6** RMS 분류 기반 보호  
  
Microsoft가 아닌 타사 파일 형식에 대 한 지원은 비 Microsoft의 공급 업체를 통해 제공 됩니다. 파일 AD RMS 암호화에 의해 보호 된 후 검색 또는 콘텐츠 기반 분류 등 데이터 관리 기능 해당 파일에 대 한 사용할 수 없게 됩니다.  
  
## <a name="in-this-scenario"></a>이 경우  
다음은 이러한 시나리오 사용할 수 있는 지침입니다.  
  
-   [암호화 Office 문서를 고려 사항](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)  
  
-   [Office 파일 & #40 암호화; 데모 단계 & #41; 배포](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>역할 및이 시나리오에 포함 된 기능  
다음 표에서 역할 및이 시나리오에 포함 된 기능을 나열 하 고 지 원하는 방식에 대해 설명 합니다.  
  
|역할/기능|이 시나리오를 지 원하는 방법을|  
|-----------------|---------------------------------|  
|Active Directory Domain Services 역할 (AD DS)|AD DS 저장 하 고 디렉터리 사용 응용 프로그램에서 특정 응용 프로그램 데이터 및 네트워크 리소스에 대 한 정보를 관리 분산된 데이터베이스를 제공 합니다. 이 경우 Windows Server 2012에서 AD DS 사용자 클레임 및 장치 클레임, 복합 신원을 (사용자와 디바이스가 클레임), 새로운 중앙 액세스 정책 모델 및 인증 결정 파일 분류 정보의 사용 만들 수 있는 승인 클레임 기반 플랫폼을 소개 합니다.|  
|파일 및 저장소 서비스 역할<br /><br />파일 서버 리소스 관리자|파일 및 저장소 서비스 제공 하는 데 도움이 기술을를 설정 하 고 파일을 저장 하 고 사용자와 공유할 수 있는 네트워크를 중앙 위치를 제공 하는 하나 이상의 파일 서버 관리 합니다. 네트워크는 동일한 파일 및 응용 프로그램에 액세스 해야 하는 경우 또는 조직에서 중요 한 경우 백업 및 파일에 대 한 중앙 집중식된 관리 하면으로 설정 해야 하나 이상의 컴퓨터 파일 서버 파일 및 저장소 서비스 역할을 적절 한 역할 서비스 컴퓨터에 추가 하 여 합니다. 이 경우 파일 서버 관리자 파일 중요 한 파일 파일 서버 (연속 파일 서버 관리 작업에는 파일)에 있는 것으로 확인 된 후 몇 초 중요 한 문서에 대 한 AD RMS 보호를 호출 하는 파일 관리 작업 구성할 수 있습니다.|  
|Active Directory Rights Management Services (AD RMS) 역할|AD RMS 사용 하면 개인 관리자가 (관리 IRM (정보 권한) 정책)를 통해 액세스 권한을 문서, 통합, 문서, 프레젠테이션 지정할 수 있습니다. 인쇄 전달 또는 권한이 없는 사람이 복사한 되지 않도록 중요 한 정보를 방지 합니다. IRM를 사용 하 여 파일에 대 한 사용 권한을 제한 자체 문서 파일에 저장 된 파일에 사용 권한을 때문에 대 한 액세스 및 사용 현황 제한을 하 든 어디 정보 적용 됩니다. 이 경우 AD RMS 암호화 다른 파일에 대 한 보호 계층을 제공합니다. 실수로 중요 한 파일에 액세스할 수 있는 사람의 메일을 통해 해당 파일을 보내는 하는 경우에 해당 파일 AD RMS 암호화에 의해 보호 됩니다. 사용자 파일에 액세스 하는 암호를 해독 키를 받으려면 AD RMS 서버에 자체적으로 인증 먼저 되어야 합니다.|  
  


