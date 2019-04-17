---
title: "Active Directory Domain Services 구성 요소 업데이트"
description: "이 문서에서는 Windows Server 2012 r 2 용 AD DS 구성 요소 업데이트 논의"
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: 52d3dab542b4250670067e927f42ddf1597fc852
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory Domain Services 구성 요소 업데이트

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

이 모듈 부 업데이트 및 신원 공간 디렉터리 서비스에서 받은 구성 요소를 소개 합니다.  
  
|만든이에 대 한|  
|--------------------|  
|**만든이:**|조자룡 Turner|  
|**정보:**|조자룡은 Irving, 텍사스, USA에 따라 디렉터리 서비스 팀과 함께 선임 지원 에스컬레이션 엔지니어입니다.  그가 만들거나 지난 12 년간 Microsoft 기술 자료에 대 한 많은 교육 과정을 KB 문서 기여한 합니다. Microsoft 인증 마스터 (MCM) Microsoft 공인 교육 해 서 MCT ()을 명확 하 고 Microsoft 직원에 새 제품 아키텍처 고객에 설명 그 이며 보유 한 M.S. 컴퓨터 교육 및 Cognitive 시스템 정도입니다.|  
|**참가자**|이 교육 모듈에서가 기여한 사항에 *Michiko 짧은*, *Dean 정*, *앨런 Jowett*, *많습니다 Pushpendran*, *Yashar Bahman*, *Anoosh Saboori*, *Rashmi Jha*, *조자룡 홀* 및 *함부로 Mauerer*|  
|**검토자**|자신의 시간 검토 하 고 피드백을 제공 하는 데 소요 된 다음 개인 덕분에 많은: *저도 Seifert*, *조자룡 홀*|  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.  
  
### <a name="what-you-will-learn"></a>내용  
이 모듈을 완료 한 후에 수 있습니다.  
  
-   Windows Server 2012 r 2에서 디렉터리 서비스 및 신분 기술 영역 내에서 구성 요소 업데이트를 설명 합니다.  
  
    -   [SPN 및 UPN 고유](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  
  
    -   [Winlogon 자동 다시 시작 Sign-on & #40; ARSO & #41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  
  
    -   [TPM 키 대](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  
  
    -   [캘리포니아 백업 및 복원 Windows PowerShell cmdlet](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  
  
    -   [명령줄 프로세스 감사](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)  
  
    -   [자격 증명 보호 및 관리](https://technet.microsoft.com/library/dn408190.aspx)  
  
    -   [디렉터리 서비스 컴포넌트 업데이트](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  
  
        -   [도메인 및 숲 기능 수준](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
        -   [NTFRS의 사용 중단](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
        -   [LDAP 쿼리 최적화 변경](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
        -   [1644 이벤트 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
        -   [Active Directory 복제 처리량 개선](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  


