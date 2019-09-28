---
title: Active Directory 도메인 서비스 구성 요소 업데이트
description: 이 문서에서는 Windows Server 2012 r 2에 대 한 AD DS 구성 요소 업데이트에 대해 설명 합니다.
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: e7bacf4f238144fca26776a729a5e4d5bf3444ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389953"
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory 도메인 서비스 구성 요소 업데이트

>적용 대상: Windows Server 2016, Windows Server 2012 R2

이 모듈에서는 디렉터리 서비스와 ID 공간에서 부분 업데이트를 수신하는 구성 요소를 소개합니다.  


| 작성자 정보 |
|------------------|
|   **작성자:**    |
|     **정보:**     |
| **참가자** |
|  **검토자**   |

> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  

### <a name="what-you-will-learn"></a>학습 내용  
이 모듈을 완료하면 다음을 수행할 수 있습니다.  

-   Windows Server 2012 R2의 디렉터리 서비스 및 ID 기술 영역 내에서 수행된 구성 요소 업데이트에 대해 설명합니다.  

    -   [SPN 및 UPN 고유성](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  

    -   [Winlogon 자동 다시 시작 로그온 &#40;arso&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  

    -   [TPM 키 증명](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  

    -   [CA 백업 및 복원 Windows PowerShell cmdlet](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  

    -   [명령줄 프로세스 감사](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)  

    -   [자격 증명 보호 및 관리](https://technet.microsoft.com/library/dn408190.aspx)  

    -   [디렉터리 서비스 구성 요소 업데이트](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  

        -   [도메인 및 포리스트 기능 수준](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  

        -   [NTFRS의 사용 중단](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  

        -   [LDAP 쿼리 최적화 프로그램 변경 사항](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  

        -   [1644 이벤트 개선 사항](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  

        -   [Active Directory 복제 처리량 개선 사항](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  



