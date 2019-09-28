---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Windows Server 2016 AD FS의 향상된 감사 기능
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4eb93513d12b2bba2620ff16be24f62ace5dee85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407250"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Windows Server 2016 AD FS의 향상된 감사 기능


현재 AD FS Windows Server 2012 R2에 대 한 단일 요청 및 로그인에 대 한 관련 정보에 대해 생성 된 다양 한 감사 이벤트는 또는 토큰 발급 활동은 없는 (AD FS의 일부 버전)에서 또는 여러 감사 이벤트에 걸쳐 있습니다. AD FS 기본적으로 감사 이벤트의 자세한 특성으로 인해 해제 됩니다.  
    Windows Server 2016에서 AD FS의 릴리스부터 감사 되었습니다 더 효율적이 고 상대적으로 간단 합니다.  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Windows Server 2016 용 AD FS의 감사 수준  
기본적으로 Windows Server 2016에서 AD FS 감사가 기본 사용 합니다.  기본 감사 관리자는 단일 요청에 대 한 이벤트 5 개 이하로 표시 됩니다.  이 관찰, 단일 요청을 확인 하기 위해 관리자는 이벤트 수가 크게 감소 되는 표시 됩니다.   PowerShell cmdlt를 사용 하 여 감사 수준을 발생 하거나 낮출 수 있습니다.  Set-adfsproperties-AuditLevel을 설정 합니다.  아래 표에서 사용할 수 있는 감사 수준을 설명합니다.  
  
||||  
|-|-|-|  
|감사 수준|PowerShell 구문|설명|  
|없음|Set-adfsproperties-AuditLevel 없음|감사 사용 하지 않도록 설정 하 고 이벤트가 기록 됩니다.|  
|Basic (기본값)|Set-adfsproperties-AuditLevel Basic|단일 요청에 대 한 5 개 이하의 이벤트가 기록 됩니다.|  
|자세히|Set-adfsproperties-AuditLevel 세부 정보 표시|모든 이벤트가 기록 됩니다.  이 상당한 양의 요청당 정보를 기록 합니다.|  
  
현재 감사 수준을 보려면 PowerShell cmdlt를 사용 하면 됩니다.  Set-adfsproperties.  
  
![감사 기능 향상](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
PowerShell cmdlt를 사용 하 여 감사 수준을 발생 하거나 낮출 수 있습니다.  Set-adfsproperties-AuditLevel을 설정 합니다.  
  
![감사 기능 향상](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>감사 이벤트 유형  
AD FS 감사 이벤트는 다양 한 유형의 AD FS에서 처리 된 요청에 따라 서로 다른 형식의 수 있습니다. 각 유형의 감사 이벤트는 연관 된 특정 데이터에 있습니다.  감사 이벤트의 유형 시스템 요청 (페칭 (fetching) 구성 정보를 포함 하는 서버 호출)와 로그인 요청 (즉, 토큰 요청) 간의 구분할 수 있습니다.    
  아래 표에서 기본 유형의 감사 이벤트를 설명합니다.  
  
||||  
|-|-|-|  
|감사 이벤트 유형|이벤트 ID|설명|  
|새 자격 증명 유효성 검사 성공|1202|여기서 새 자격 증명의 유효성을 검사 성공적으로 페더레이션 서비스는 요청입니다. Saml-p, Ws-federation, Ws-trust, 여기에 포함 됩니다 (SSO를 생성 하려면 첫 번째 구간) 및 OAuth 권한 부여 끝점입니다.|  
|새 자격 증명 유효성 검사 오류|1203|새 자격 증명 유효성 검사는 페더레이션 서비스에는 실패 한 요청입니다. Ws-trust, 이때 Ws-fed, Saml-p (SSO를 생성 하려면 첫 번째 구간) 및 OAuth 권한 부여 끝점입니다.|  
|응용 프로그램 토큰 성공|1200|보안 토큰을 페더레이션 서비스에서 성공적으로 실행 되는 요청입니다. Ws-federation, SAML-P이 이벤트는 SSO 아티팩트가 요청이 처리 될 때 기록 됩니다. (예: SSO 쿠키).|  
|응용 프로그램 토큰 실패|1201|페더레이션 서비스에서 보안 토큰 발급 실패 하는 위치는 요청입니다. Ws-federation, SAML-P SSO 아티팩트가 요청이 처리 된이 기록 됩니다. (예: SSO 쿠키).|  
|암호 변경 요청 성공|1204|페더레이션 서비스에서 암호 변경 요청에는 트랜잭션이 처리 되었습니다.|  
|암호 변경 요청 오류|1205|페더레이션 서비스에서 처리할 수 있는 암호 변경 요청 트랜잭션이 실패 했습니다.| 
|로그 아웃 성공|1206|로그 아웃 요청이 성공적으로 실행에 대해 설명 합니다.|  
|로그 아웃 실패|1207|실패 한 로그 아웃 요청에 설명 합니다.|  

  


