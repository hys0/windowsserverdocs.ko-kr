---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: "Adfs의 Windows Server 2016 대 한 감사 향상"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3d622686a3cc34316f0cf5187839785195c2f104
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Adfs의 Windows Server 2016 대 한 감사 향상

>Windows Server 2016 적용 됩니다.

현재 광고에 FS Windows Server 2012 R2에 대 한 단일 요청 하 고 로그 기능에 대 한 관련 정보에 대해 생성 하는 수많은 감사 이벤트가 이거나 토큰 발급 활동 Adfs의 일부 버전) (에 없는 중 하나 또는 여러 개의 감사 이벤트에서 손가락을 펼치고 합니다. Adfs의 기본적으로 감사 이벤트의 세부 정보 표시 특성으로 인해 꺼져 있습니다.  
    Windows Server 2016에 Adfs의 릴리스를 통해 감사 되 고 더 간소화 되 고 자세 있습니다.  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Windows Server 2016 용 adfs에서 수준 감사합니다.  
기본적으로 Windows Server 2016에 ADFS 기본 감사 사용 하도록 설정에 있습니다.  기본 감사 관리자 단일 요청에 대 한 5 또는 이벤트를 볼 수 있습니다.  중요 한 이벤트 관리자 살펴볼, 단일 요청을 확인 하기 위해 할 수 저하를 표시 합니다.   감사 수준 발생 시킬 수 또는 PowerShell cmdlt 사용 중일: 설정 AdfsProperties AuditLevel 합니다.  아래 표에서 사용 가능한 감사 수준에 설명 합니다.  
  
||||  
|-|-|-|  
|감사 수준|PowerShell 구문|설명|  
|없음|설정-AdfsProperties AuditLevel 없음|감사 비활성화 되 고 없는 이벤트에 기록 됩니다.|  
|기본 (기본)|설정-AdfsProperties AuditLevel 기본|더 이상 5 이벤트 단일 요청에 기록 됩니다.|  
|자세한 정보|설정-AdfsProperties AuditLevel 세부 정보 표시|모든 이벤트 기록 됩니다.  이 상당한 양의 요청에 따라 정보를 기록 합니다.|  
  
현재 감사 수준을 보려면 PowerShell cmdlt 사용할 수 있습니다: AdfsProperties 가져와야 합니다.  
  
![감사 향상 된 기능](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
감사 수준 발생 시킬 수 또는 PowerShell cmdlt 사용 중일: 설정 AdfsProperties AuditLevel 합니다.  
  
![감사 향상 된 기능](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>감사 이벤트 유형  
다양 한 유형의 Adfs에서 처리 요청에 따라 다양 한 종류의 광고 FS 감사 이벤트 될 수 있습니다. 각 유형의 감사 이벤트에 특정 데이터 연결 되어 있습니다.  이벤트 감사 유형의 시스템 요청 (서버 호출 구성 정보 가져오기 등)와 로그인 요청 (즉, 토큰 요청) 간에 구분할 수 있습니다.    
  아래 표에서 기본 유형의 감사 이벤트를 설명합니다.  
  
||||  
|-|-|-|  
|감사 행사 유형|이벤트 ID|설명|  
|신선한 자격 증명 유효성 검사 성공|1202|여기서 신선한 자격 증명 성공적으로 Federation 서비스에 의해 요청 합니다. Ws-trust WS Federation SAML P 포함 됩니다 (SSO 얻기 위해 첫 번째 다리) 및 OAuth 끝점 권한을 부여 합니다.|  
|신선한 자격 증명 유효성 검사 오류|1203|Federation 서비스에서 자격 증명 새로운 유효성 검사가 실패 하는 위치를 요청 합니다. Ws-trust, 포함 WS 급지됨, SAML P (SSO 얻기 위해 첫 번째 다리) 및 OAuth 끝점 권한을 부여 합니다.|  
|토큰 성공 응용 프로그램|1200|보안 토큰 연합 서비스에서 성공적으로 발급이 요청 됩니다. WS 연합, SAML P SSO 유물으로 요청을 처리할 때이 기록 됩니다. (예: SSO 쿠키).|  
|응용 프로그램 토큰 실패|1201|보안 토큰 발급 실패 Federation 서비스에 대 한 위치 요청 합니다. WS 연합, SAML P 요청 SSO 유물을 처리 하는이 기록 됩니다. (예: SSO 쿠키).|  
|암호 변경 요청 성공|1204|암호 변경 요청 거래 성공적으로 Federation 서비스에 의해 처리 합니다.|  
|암호 변경 요청 오류|1205|암호 변경 요청 거래 Federation 서비스에 의해 처리 하지 못했습니다.| 
|로그 아웃 성공|1206|성공적인 로그 아웃 요청에 설명 합니다.|  
|로그 아웃 실패|1207|실패 한 로그 아웃 요청에 설명 합니다.|  

  


