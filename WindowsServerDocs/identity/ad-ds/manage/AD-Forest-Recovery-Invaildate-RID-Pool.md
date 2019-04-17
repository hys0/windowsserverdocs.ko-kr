---
title: "광고 숲 복구-RID 풀 무효화"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adfs
ms.openlocfilehash: cb024356ae5f872e93448d73ea54b271fe3fae4d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>현재 RID 풀 무효화-광고 숲 복구  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 Windows PowerShell 저희에 게 다음 절차를 사용 하 여 도메인 컨트롤러에서 현재 RID 풀 무효화 됩니다. Windows Server 2012와 Windows Server 2008 R2 하지만 위치를 사용 하 여 설치 해야 Windows Server 2008 하지에서 기본적으로 사용 하도록 설정한 Windows PowerShell **기능 추가**합니다. 수 [다운로드](https://www.microsoft.com/download/details.aspx?id=20020) Windows Server 2003에서 실행 됩니다.  
  
 성공적으로 완료 명령을 확인 하려면 16654 이벤트 ID를 확인 (소스 디렉터리-서비스-삼로) Windows Server 2012에서 이벤트 뷰어에서 시스템 로그에 기록 됩니다. 이전 버전의 Windows에서이 행사를 로그 하지 않습니다.  
  
> [!NOTE]
>  RID 풀을 무효화 후 처음 보안 사용자 (사용자를 컴퓨터 또는 그룹) 만드는 하려고 하면 오류가 발생 받습니다. 개체를 트리거하 새로운 RID 풀에 대 한 요청 합니다. 작업을 다시 시도 성공 새 RID 풀 할당 합니다.  
  
## <a name="to-invalidate-the-current-rid-pool"></a>현재에 제거 풀  
  
1.  향상 된 Windows PowerShell 세션을 열고 다음 명령을 실행 ENTER 키를 누릅니다.  
  
    ```  
    $Domain = New-Object System.DirectoryServices.DirectoryEntry  
    $DomainSid = $Domain.objectSid  
    $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")  
    $RootDSE.UsePropertyCache = $false  
    $RootDSE.Put("invalidateRidPool", $DomainSid.Value)  
    $RootDSE.SetInfo()  
    ```  
  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
