---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: 시나리오 파일 서버의 정보 보존 구현
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59fd7f0a0a4d9ed8f5cec57b17be21e1aa4cd592
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880254"
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>시나리오: 파일 서버에 정보 보존 구현

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

보존 기간은 문서가 만료되기 전에 보관되어야 하는 기간입니다. 조직에 따라 보존 기간이 다를 수 있습니다. 폴더의 파일을 단기, 중기 또는 장기 보존 기간으로 분류한 다음 각 기간의 시간 범위를 할당할 수 있습니다. 파일에 법적 보존을 설정하여 파일을 무기한으로 보관할 수도 있습니다.  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
파일 분류 인프라 및 파일 서버 리소스 관리자는 파일 관리 작업 및 파일 분류를 사용하여 파일 집합의 보존 기간을 적용합니다. 폴더에 보존 기간을 할당한 다음 파일 관리 작업을 사용하여 할당된 보존 기간을 얼마나 오래 유지할지 구성할 수 있습니다. 폴더의 파일이 곧 만료될 경우 파일 소유자에게 알림 메일이 전송됩니다. 또한 파일 관리 작업으로 인해 파일이 만료되지 않도록 파일을 법적 보존이 설정된 것으로 분류할 수도 있습니다.  
  
[Plan for Retention of Information on File Servers](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)에서 보존을 구성하기 위한 계획 정보를 확인할 수 있습니다.  
  
법적 보존을 위해 파일을 분류 하 고의 보존 기간을 구성에 대 한 단계를 찾을 수 있습니다 [배포 구현 정보 보존 파일 서버에 &#40;데모 단계&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)합니다.  
  
> [!NOTE]  
> 이 시나리오에서는 법적 보존할 문서를 수동으로 분류하는 방법에 대해 설명합니다. 그러나 법적 보존을 위해 문서를 자동으로 분류에 Windows Server 2012의 가능성이 있습니다. 예를 들어 법적 보존이 적용되는 사용자 계정 목록과 파일 소유자를 비교하는 Windows PowerShell 분류자를 만들면 됩니다. 파일 소유자가 사용자 계정 목록에 있으면 파일이 법적 보존용으로 분류됩니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
이 시나리오는 동적 Access Control 시나리오의 일부입니다. 동적 액세스 제어에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>이 시나리오에 포함 된 기능  
다음 표에는 이 시나리오에 포함된 기능이 나열되어 있으며, 이 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.  
  
|기능|이 시나리오를 지원하는 방법|  
|-----------|---------------------------------|  
|[파일 서버 리소스 관리자 개요](https://technet.microsoft.com/library/hh831701.aspx)|파일 분류 인프라는 파일 서버 리소스 관리자에 포함되어 있는 기능입니다.|  
|[File and Storage Services 개요](https://technet.microsoft.com/library/hh831487.aspx)|파일 서버 리소스 관리자는 파일 서비스 서버 역할에 포함되어 있는 기능입니다.|  
  
  


