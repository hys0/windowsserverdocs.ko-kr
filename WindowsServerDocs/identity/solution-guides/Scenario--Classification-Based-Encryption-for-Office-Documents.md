---
ms.assetid: 73542e1c-53ef-4ddb-89b1-bc563b2bfb49
title: Office 문서에 대 한 분류 기반 암호화 시나리오
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 38e058f36522ba6a2c81694cb883d0946b04adda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865184"
---
# <a name="scenario-classification-based-encryption-for-office-documents"></a>시나리오: Office 문서에 대한 분류 기반 암호화

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

중요한 정보를 보호하는 가장 큰 이유는 조직의 위험을 완화하기 위함입니다. HIPAA(Health Insurance Portability and Accountability Act) 및 PCI-DSS(Payment Card Industry Data Security Standard)와 같은 다양한 규정에 정보의 암호화가 명시되어 있고, 비즈니스 측면에서 중요한 비즈니스 정보를 암호화해야 하는 이유는 다양합니다. 그러나 정보 암호화는 비용이 많이 들고 비즈니스 생산성을 저하시킬 수 있습니다. 따라서 조직마다 정보 암호화의 접근 방식과 우선 순위가 다양한 편입니다.  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
 Windows Server 2012 분류에 따라 중요 한 Microsoft Office 파일을 자동으로 암호화 하는 기능을 제공 합니다. 이 기능은 파일이 파일 서버에서 중요한 파일로 식별되고 몇 초 후 중요한 문서에 대한 AD RMS(Active Directory Rights Management Services) 보호를 호출하는 파일 관리 작업을 통해 수행됩니다. 파일 서버의 연속적인 파일 관리 작업이 이를 용이하게 해줍니다.  
  
AD RMS 암호화는 또 다른 파일 보호 계층을 제공합니다. 중요한 파일에 대한 액세스 권한이 있는 사용자가 해당 파일을 실수로 전자 메일을 통해 보낸 경우에도 AD RMS 암호화에 의해 파일이 보호됩니다. 파일에 액세스하려는 사용자는 먼저 AD RMS 서버의 인증을 통해 암호 해독 키를 받아야 합니다. 다음 그림에서는 이 프로세스를 보여줍니다.  
  
![솔루션 가이드](media/Scenario--Classification-Based-Encryption-for-Office-Documents/DynamicAccessControl_RevGuide_6.JPG)  
  
**그림 6** 분류 기반 RMS 보호  
  
타사 파일 형식에 대한 지원은 해당 공급업체를 통해 받을 수 있습니다. 파일이 AD RMS 암호화로 보호된 후에는 검색 또는 콘텐츠 기반 분류와 같은 데이터 관리 기능을 해당 파일에 사용할 수 없습니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
다음은 이 시나리오에 사용할 수 있는 지침입니다.  
  
-   [Office 문서 암호화에 대 한 계획 고려 사항](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)  
  
-   [Office 파일 암호화 배포 &#40;데모 단계&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)  
  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>역할과이 시나리오에 포함 된 기능  
다음 표에는 이 시나리오에 포함된 역할 및 기능이 나열되어 있으며, 이러한 역할 및 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|-----------------|---------------------------------|  
|AD DS(Active Directory 도메인 서비스) 역할|AD DS에서는 디렉터리 사용 응용 프로그램의 네트워크 리소스와 응용 프로그램별 데이터에 대한 정보를 저장하고 관리하는 분산 데이터베이스를 제공합니다. 이 시나리오에서는 Windows Server 2012의 AD DS는 사용자 클레임 및 장치 클레임, 복합 id (사용자 + 장치 클레임), 새로운 중앙 액세스 정책 모델 및 권한 부여 결정에 파일 분류 정보 사용을 만들 수 있도록 하는 클레임 기반 권한 부여 플랫폼을 소개 합니다.|  
|파일 및 저장소 서비스 역할<br /><br />파일 서버 리소스 관리자|파일 및 저장소 서비스는 파일을 저장하고 다른 사용자와 공유할 수 있는 네트워크의 중앙 위치를 제공하는 하나 이상의 파일 서버를 설정 및 관리할 수 있는 기술을 제공합니다. 네트워크 사용자에게 동일한 파일 및 응용 프로그램에 대한 액세스 권한이 필요하거나 조직에서 중앙 집중 방식의 백업 및 파일 관리가 필요한 경우, 파일 및 저장소 서비스 역할과 해당 역할 서비스를 컴퓨터에 추가하여 하나 이상의 컴퓨터를 파일 서버로 설정해야 합니다. 이 시나리오에서 파일 서버 관리자는 파일이 파일 서버에서 중요한 파일로 식별되고 몇 초 후 중요한 문서에 대한 AD RMS 보호를 호출하는 파일 관리 작업을 구성할 수 있습니다(파일 서버의 연속적인 파일 관리 작업).|  
|AD RMS(Active Directory Rights Management Services) 역할|AD RMS는 개별 사용자와 관리자가 IRM(정보 권한 관리) 정책을 통해 문서, 통합 문서 및 프레젠테이션에 대한 액세스 권한을 지정할 수 있도록 허용합니다. 따라서 중요한 정보가 권한 없는 사용자에 의해 인쇄, 전달 또는 복사되는 것을 방지할 수 있습니다. IRM을 사용하여 파일에 대한 권한을 제한하고 나면 해당 파일에 대한 권한이 문서 파일 자체에 저장되므로 정보에 관계없이 액세스 및 사용 제한이 적용됩니다. 이 시나리오에서 AD RMS 암호화는 또 다른 파일 보호 계층을 제공합니다. 중요한 파일에 대한 액세스 권한이 있는 사용자가 해당 파일을 실수로 전자 메일을 통해 보낸 경우에도 AD RMS 암호화에 의해 파일이 보호됩니다. 파일에 액세스하려는 사용자는 먼저 AD RMS 서버의 인증을 통해 암호 해독 키를 받아야 합니다.|  
  


