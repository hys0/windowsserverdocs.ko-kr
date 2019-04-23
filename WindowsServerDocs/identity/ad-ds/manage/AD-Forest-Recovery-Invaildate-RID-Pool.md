---
title: AD 포리스트 복구-RID 풀 무효화
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adds
ms.openlocfilehash: 46115991e48da301a8a739009bac27415ebe73df
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842514"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD 포리스트 복구-현재 RID 풀 무효화  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

Windows PowerShell에 다음 절차를 사용 하 여 도메인 컨트롤러에 현재 RID 풀을 무효화 합니다. Windows PowerShell은 Windows Server 2012 및 Windows Server 2008 R2를 사용 하 여 설치 해야 Windows Server 2008 하지에서 기본값으로 사용 가능 **기능 추가**합니다. 하기란 [다운로드](https://www.microsoft.com/download/details.aspx?id=20020) Windows Server 2003에서 실행 되도록 합니다.  

명령이 성공적으로 완료를 확인 하려면 이벤트 id 16654 확인 (원본이 디렉터리-서비스-SAM) Windows Server 2012의 이벤트 뷰어에서 시스템 로그에 있습니다. 이전 버전의 Windows에서이 이벤트를 기록 하지 않습니다.  
  
> [!NOTE]
> RID 풀을 무효화 면 먼저 보안 주체 (사용자, 컴퓨터 또는 그룹)을 생성 하려는 경우는 오류가 발생 합니다. 개체를 만드는 데 새 RID 풀 요청을 트리거합니다. 새 RID 풀을 할당할 성공할 수 작업을 다시 시도 합니다.  
  
## <a name="to-invalidate-the-current-rid-pool"></a>현재 RID 풀 무효화  
  
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
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
