---
ms.assetid: ad3f0480-99f7-428a-ab33-6d165a440840
title: 시나리오 분류를 사용 하 여 데이터에 대 한 통찰력 얻기
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cd6a6e9d3cb452a2cd0a48c6207aea181d85dc7b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357451"
---
# <a name="scenario-get-insight-into-your-data-by-using-classification"></a>시나리오: 분류를 사용하여 데이터 이해

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

대부분의 조직에서 데이터 및 저장소 리소스에 대한 의존도가 점점 높아지고 있습니다. IT 관리자는 점점 커지고 복잡해지는 저장소 인프라를 관리하는 동시에 총 소유 비용을 합리적인 수준으로 유지해야 하는 과제에 직면했습니다. 저장소 리소스 관리는 더 이상 데이터의 볼륨이나 가용성에만 국한되지 않습니다. 회사 정책을 적용하고 저장소가 어떻게 소비되고 있는지 파악하여 효율성을 높이고 규정 준수를 강화함으로써 위험을 완화하는 방법까지 고려해야 합니다. 파일 분류 인프라는 데이터를 보다 효율적으로 관리할 수 있도록 분류 프로세스를 자동화함으로써 데이터에 대한 정보를 제공합니다. 파일 분류 인프라에서는 수동, 프로그래밍 및 자동과 같은 분류 방법을 사용할 수 있습니다. 이 항목에서는 자동 파일 분류 방법에 중점을 둡니다.  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
파일 분류 인프라에서는 분류 규칙을 사용하여 자동으로 파일을 검사하고 파일의 내용에 따라 파일을 분류합니다. 분류 속성은 조직의 파일 서버에서 공유할 수 있도록 중앙의 Active Directory에서 정의됩니다. 파일에서 표준 문자열 또는 패턴(정규식)과 일치하는 문자열을 검사하는 분류 규칙을 만들 수 있습니다. 구성된 분류 매개 변수가 파일에서 발견되면 해당 파일은 분류 규칙에 구성된 대로 분류됩니다. 분류 규칙의 몇 가지 예를 들면 다음과 같습니다.  
  
-   "Contoso 기밀" 문자열이 포함 된 모든 파일을 높은 비즈니스 영향을 가진 것으로 분류 합니다.  
  
-   주민 등록 번호가 10개 이상 포함된 파일을 개인 식별 가능한 정보가 담긴 파일로 분류합니다.  
  
파일이 분류되면 파일 관리 작업을 사용하여 특정 방식으로 분류된 파일에 대한 작업을 수행할 수 있습니다. 파일 관리 작업의 작업에는 파일과 연관된 권한 보호, 파일 만료 및 사용자 지정 작업(예: 웹 서비스에 정보 게시) 실행이 포함됩니다.  
  
자동 파일 분류 구성을 위한 계획 정보는 [자동 파일 분류 계획](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)에서 확인할 수 있습니다.  
  
자동 [파일 분류 &#40;데모 단계&#41;배포](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)에서 자동으로 파일을 분류 하는 방법에 대 한 단계를 찾을 수 있습니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
이 시나리오는 동적 Access Control 시나리오의 일부입니다. 동적 액세스 제어에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_APP"></a>실용적인 응용 프로그램  
Windows Server 2012의 파일 분류 인프라는 비즈니스 데이터 소유자가 데이터를 쉽게 분류 하 고 레이블을 설정할 수 있도록 하 여 동적 Access Control에 기여 합니다. 중앙 액세스 정책에 저장된 분류 정보를 사용하여 비즈니스에 중요한 데이터 클래스에 대한 액세스 정책을 정의할 수 있습니다.  
  
## <a name="BKMK_NEW"></a>이 시나리오에 포함 된 기능  
다음 표에는 이 시나리오에 포함된 기능이 나열되어 있으며, 이 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.  
  
|기능|이 시나리오를 지원하는 방법|  
|-----------|---------------------------------|  
|[파일 서버 리소스 관리자 개요](https://technet.microsoft.com/library/hh831701.aspx)|파일 분류 인프라는 파일 서버 리소스 관리자에 포함되어 있는 기능입니다.|  
|[파일 및 스토리지 서비스 개요](https://technet.microsoft.com/library/hh831487.aspx)|파일 서버 리소스 관리자는 파일 서비스 서버 역할에 포함되어 있는 기능입니다.|  
  


