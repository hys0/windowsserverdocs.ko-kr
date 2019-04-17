---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: "시나리오 액세스 거부 지원"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d6b8d8a094aa86fd5be78d2eae13bae50df3fd79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-access-denied-assistance"></a>액세스 거부 Assistance 시나리오:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자가 공유 파일 및 폴더는 하지 권한이 파일 서버에 액세스 하려고 할 때는 액세스 거부 메시지를 받게 됩니다. 관리자는 문제를 해결 하는 것 액세스 문제를 해결 하는 적절 한 상황에 맞는 없는 경우가 많습니다.  
  
## <a name="scenario-description"></a>시나리오 설명  
액세스 거부 지원 관련 된 문제를 해결 하는 다음과 같은 방법으로 제공 하는 Windows Server 2012에서 새로운 기능이 파일 및 폴더에 액세스할 수 있습니다.  
  
-   **자체 지원 합니다.** 사용자가 문제 확인 하 고 요청된 액세스를 받을 수 있도록 문제를 해결 하는 경우 비즈니스에 영향을 낮습니다 및 특별 한 예외 없음 중앙 액세스 정책에 필요한 합니다. 액세스 거부 assistance 액세스 거부 메시지가 파일 서버 관리자 조직에 대 한 정보를 사용자 지정할 수 있는 제공 합니다. 예를 들어, 사용자가 데이터 소유자의 파일 서버 관리자를 않고도 대 한 액세스를 요청할 수 있도록 관리자 메시지를 설정할 수 있습니다.  
  
-   **데이터 소유자가 지원 됩니다.** 공유 폴더에 대 한 메일 그룹 정의 하 고 폴더 소유자가 사용자에 액세스 해야 할 때 전자 메일 알림을 받을 수 있도록 구성할 수 있습니다. 데이터 소유자 액세스는 사용자를 위해 방법을 모릅니다, 소유자 파일 서버 관리자에 게이 정보를 전달할 수 있습니다.  
  
-   **파일 서버 관리자가 지원 됩니다.** 이 유형의 지원은 사용자 수 없는 문제를 해결 하 고 데이터 소유자 수 없는 경우 사용할 수 있습니다.  Windows Server 2012 어디서 파일 서버 관리자 볼 수 유효 사용자에 대 한 사용 권한을 파일 또는 폴더에 쉽게 액세스 문제를 해결 하 않도록 사용자 인터페이스를 제공 합니다.  
  
Windows Server 2012에 대 한 액세스 거부 지원 자녀가 구성을 변경 하 여 액세스 요청 수 있도록 문제를 적절 한 도구를 확인할 수 있습니다 파일 서버 관리자 관련 액세스 세부 정보를 제공 합니다. 예를 들어, 사용자 현재에 대 한 액세스 없는 파일에 액세스 하는이 프로세스를 수행 수 있습니다.  
  
-   사용자가 \\\financeshares 공유 폴더에서 파일을 읽을 수 있지만 서버에 대 한 액세스 거부 메시지가 표시 됩니다.  
  
-    Windows Server 2012 사용자에 게 도움 요청 하는 옵션에 액세스 거부 지원 정보를 표시 합니다.  
  
-   사용자가에서 리소스에 대 한 액세스를 요청 하는 경우 서버 액세스 요청 정보가 포함 된 메일 폴더 소유자에 게 보냅니다.  
  
찾을 수 정보에 액세스 거부 assistance 구성에 대 한 계획 [Access-Denied 지원에 대 한 계획](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)합니다.  
  
단계에서 지원 액세스 거부 구성에 대 한 찾을 수 [Deploy Access-Denied 지원 & #40; 데모 단계 & #41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>이 경우  
이 시나리오는 동적 액세스 제어 시나리오의 일부입니다. 동적 액세스 제어 대 한 자세한 내용은 참조 하십시오.  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>실용적인 응용 프로그램  
사용자 액세스 거부 메시지에서 직접 공유 파일 및 폴더에 대 한 액세스를 요청할 수 있는 기능을 제공 하 여 Windows Server 2012에 대 한 액세스 거부 지원 동적 액세스 제어에 적용 됩니다.  
  
## <a name="BKMK_NEW"></a>이 경우에 포함 된 기능  
다음 표에서이 시나리오에 포함 된 기능을 설명 하 고 지 원하는 방법을 설명 합니다.  
  
|기능|이 시나리오를 지 원하는 방법을|  
|-----------|---------------------------------|  
|[파일 서버 리소스 관리자 개요](https://technet.microsoft.com/library/hh831701.aspx)|파일 서버에서 파일 서버 리소스 관리자 본체를 사용 하 여 액세스 거부 assistance 구성할 수 있습니다.|  
|[파일 및 저장소 서비스 개요](https://technet.microsoft.com/library/hh831487.aspx)|파일 서버 리소스 관리자는는 파일 및 저장소 서비스 역할 서비스 하 고 네트워크에는 파일 서버 관리에 사용할 수 있는 기능 집합으로 구성 됩니다.|  
  


