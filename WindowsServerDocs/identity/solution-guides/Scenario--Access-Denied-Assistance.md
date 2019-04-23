---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: 액세스 거부 지원 시나리오
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d6b8d8a094aa86fd5be78d2eae13bae50df3fd79
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829094"
---
# <a name="scenario-access-denied-assistance"></a>시나리오: 액세스 거부 지원

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자가 파일 서버에서 권한이 없는 공유 파일 및 폴더에 액세스하려고 하면 액세스 거부 메시지가 표시됩니다. 관리자는 액세스 문제를 해결하는 데 적절한 컨텍스트가 없어 문제 해결에 어려움을 겪는 경우가 많습니다.  
  
## <a name="scenario-description"></a>시나리오 설명  
액세스 거부 지원은 관련 된 문제를 해결 하려면 다음과 같은 방법으로 제공 하는 Windows Server 2012의 새로운 기능에 파일 및 폴더에 액세스 하려면:  
  
-   **자가 지원.** 사용자가 문제를 확인하고 해결하여 요청한 액세스 권한을 얻을 수 있다면 비즈니스에 미치는 영향이 적고 중앙 액세스 정책에 특별한 예외가 필요 없을 것입니다. 액세스 거부 지원은 파일 서버 관리자가 해당 조직에 특정한 정보로 사용자 지정할 수 액세스 거부 메시지를 제공합니다. 예를 들어 관리자는 사용자가 파일 서버 관리자에게 요청하지 않고 데이터 소유자에게 액세스를 요청할 수 있도록 메시지를 설정할 수 있습니다.  
  
-   **데이터 소유자의 지원.** 공유 폴더에 대한 메일 그룹을 정의하여 사용자가 액세스를 요구하는 경우 폴더 소유자에게 메일 알림이 제공되도록 구성할 수 있습니다. 데이터 소유자는 사용자에게 액세스 권한을 부여하는 방법을 모르는 경우 이 정보를 파일 서버 관리자에게 전달할 수 있습니다.  
  
-   **파일 서버 관리자의 지원.** 이 유형의 지원은 사용자가 문제를 해결할 수 없고 데이터 소유자가 도움을 줄 수 없는 경우에 사용할 수 있습니다.  Windows Server 2012 파일 서버 관리자 대 볼 수 있는 사용자에 대 한 유효 사용 권한 파일 또는 폴더를 보다 쉽게 액세스 문제를 해결할 수 있도록 사용자 인터페이스를 제공 합니다.  
  
Windows Server 2012의 액세스 거부 지원 되므로 확인할 수 있는 문제 및 적절 한 도구를 액세스 요청을 충족 하도록 구성을 변경할 수 있도록 관련 액세스 정보 파일 서버 관리자를 제공 합니다. 예를 들어 사용자는 다음 프로세스에 따라 현재 액세스 권한이 없는 파일에 액세스할 수 있습니다.  
  
-   사용자의 파일 읽기를 시도 합니다 \\\financeshares 폴더를 공유 하지만 서버에 대 한 액세스 거부 메시지를 표시 합니다.  
  
-    Windows Server 2012 사용자에 게 지원 요청 옵션과 함께 액세스 거부 지원 정보를 표시 합니다.  
  
-   사용자가 리소스에 대한 액세스를 요청하면 서버에서 폴더 소유자에게 액세스 요청 정보가 포함된 메일을 보냅니다.  
  
액세스 거부 지원 구성을 위한 계획 정보는 [Plan for Access-Denied Assistance](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)에서 확인할 수 있습니다.  
  
액세스 거부 지원을 구성 하는 방법에 대 한 단계를 찾을 수 있습니다 [deploy access-denied Assistance &#40;데모 단계&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)합니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
이 시나리오는 동적 Access Control 시나리오의 일부입니다. 동적 액세스 제어에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>유용한 팁  
Windows Server 2012의 액세스 거부 지원 사용자에 게 액세스 거부 메시지에서 직접 공유 파일 및 폴더에 대 한 액세스를 요청 하는 기능을 제공 하 여 동적 Access Control을 강화 합니다.  
  
## <a name="BKMK_NEW"></a>이 시나리오에 포함 된 기능  
다음 표에는 이 시나리오에 포함된 기능이 나열되어 있으며, 이 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.  
  
|기능|이 시나리오를 지원하는 방법|  
|-----------|---------------------------------|  
|[파일 서버 리소스 관리자 개요](https://technet.microsoft.com/library/hh831701.aspx)|파일 서버에서 파일 서버 리소스 관리자 콘솔을 사용하여 액세스 거부 지원을 구성할 수 있습니다.|  
|[File and Storage Services 개요](https://technet.microsoft.com/library/hh831487.aspx)|파일 서버 리소스 관리자는 파일 및 저장소 서비스 역할 서비스이며, 네트워크의 파일 서버를 관리하는 데 사용할 수 있는 기능 집합으로 구성됩니다.|  
  


