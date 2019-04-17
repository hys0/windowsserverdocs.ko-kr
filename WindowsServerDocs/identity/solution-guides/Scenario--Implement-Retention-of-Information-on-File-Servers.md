---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: "파일 서버에서 정보가 구현 보존 시나리오"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59fd7f0a0a4d9ed8f5cec57b17be21e1aa4cd592
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>파일 서버에 보유 한 정보를 구현 하는 시나리오:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

보유 기간은 문서 되어야 하는 시간을 만료 되기 전에 유지 합니다. 조직에 따라 보존 기간 다를 수 있습니다. 짧은, 중간 또는 장기 보존 기간 것으로 폴더의 파일을을 분류 하 고 각 기간에 대 한 된 시간을 지정할 수 있습니다. 법률 대기 하 여 파일을 계속 유지 수도 있습니다.  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
파일 분류 인프라와 파일 서버 리소스 관리자 및 사용 하 여 파일 관리 작업 파일 분류 일련의 파일에 대 한 보존 기간을 적용 합니다. 폴더에 고정 기간 지정 하 고 파일 관리 작업을 사용 하 여 마지막에 할당 된 보존 기간은 얼마나 걸리나요 구성할 수 있습니다. 폴더의 파일 만료 되 면 통보 이메일이 해당 파일의 소유자가 받습니다. 파일을 하는 파일 관리 작업 파일을 만료 되지 것입니다 법적 보류 중으로 분류 수도 있습니다.  
  
찾을 수 계획에 보존 구성에 대 한 정보 [파일 서버에 보존의 정보에 대 한 계획](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)합니다.  
  
파일에 대 한 법적 보류 분류 하 고 보존 기간을 구성 단계를 찾을 수 [배포 구현 유지에 대 한 정보 파일 서버 & #40; 데모 단계 & #41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md).  
  
> [!NOTE]  
> 시나리오를 수동으로 법적 길게에 대 한 문서를 분류 하는 방법에 대해서만 설명 합니다. 그러나 법적 길게에 대 한 문서를 자동으로 분류 Windows Server 2012에서 불가능 합니다. 이 작업을 수행 하는 방법은 파일 소유자의 사용자 계정 법적 보류 중인 목록에 비교 하 여 Windows PowerShell 분류자 만드는 것입니다. 파일 소유자의 사용자 계정 목록에서 일부 경우, 해당 파일에 대 한 법적 보류 분류 됩니다.  
  
## <a name="in-this-scenario"></a>이 경우  
이 시나리오는 동적 액세스 제어 시나리오의 일부입니다. 동적 액세스 제어 대 한 자세한 내용은 참조 하십시오.  
  
-   [동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>이 경우에 포함 된 기능  
다음 표에서이 시나리오에 포함 된 기능을 설명 하 고 지 원하는 방법을 설명 합니다.  
  
|기능|이 시나리오를 지 원하는 방법을|  
|-----------|---------------------------------|  
|[파일 서버 리소스 관리자 개요](https://technet.microsoft.com/library/hh831701.aspx)|파일 분류 인프라 파일 서버 리소스 관리자에 포함 된 기능입니다.|  
|[파일 및 저장소 서비스 개요](https://technet.microsoft.com/library/hh831487.aspx)|파일 서버 리소스 관리자 파일 서비스 거부에 포함 된 기능입니다.|  
  
  


