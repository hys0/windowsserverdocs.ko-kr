---
title: AD 포리스트 복구-RID 풀을 무효화 합니다.
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adds
ms.openlocfilehash: 9e693f6f30fb721897eaaac89b3d146c57e0e63f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823926"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD 포리스트 복구-현재 RID 풀을 무효화 합니다.  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

다음 절차를 사용 하 여 Windows PowerShell에서 도메인 컨트롤러의 현재 RID 풀을 무효화 합니다. Windows PowerShell은 windows server 2012 및 Windows server 2008 r 2에서 기본적으로 사용 되지만 **기능 추가**를 사용 하 여 설치 해야 하는 windows server 2008에서는 사용 되지 않습니다. [다운로드](https://www.microsoft.com/download/details.aspx?id=20020) 하 여 Windows Server 2003에서 실행할 수 있습니다.  

명령이 성공적으로 완료 되었는지 확인 하려면 Windows Server 2012의 이벤트 뷰어 시스템 로그에서 이벤트 ID 16654 (원본 디렉터리-서비스-SAM)를 확인 합니다. 이전 버전의 Windows에서는이 이벤트를 기록 하지 않습니다.  
  
> [!NOTE]
> RID 풀을 무효화 한 후에는 보안 주체 (사용자, 컴퓨터 또는 그룹)를 처음 만들 때 오류가 표시 됩니다. 개체를 만들려고 할 때 새 RID 풀에 대 한 요청이 트리거됩니다. 새 RID 풀이 할당 되므로 작업을 다시 시도할 수 있습니다.  
  
## <a name="to-invalidate-the-current-rid-pool"></a>현재 RID 풀을 무효화 하려면  
  
- 관리자 권한 Windows PowerShell 세션을 열고 다음 명령을 실행 하 고 ENTER 키를 누릅니다.  

   ```powershell
   $Domain = New-Object System.DirectoryServices.DirectoryEntry  
   $DomainSid = $Domain.objectSid  
   $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")  
   $RootDSE.UsePropertyCache = $false  
   $RootDSE.Put("invalidateRidPool", $DomainSid.Value)  
   $RootDSE.SetInfo()  
   ```  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
