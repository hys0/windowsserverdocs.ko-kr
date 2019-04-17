---
title: "광고 포리스트 복구-복제 확인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adfs
ms.openlocfilehash: d85336a10e808755677a99777af8ecf5c07b05ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="resources-to-verify-replication-is-working"></a>복제 작동 하는지 확인 하는 데 리소스 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
 복원 하거나 모든 Dc 다시 설치한 후 AD DS 및 SYSVOL 지 복구 되 고 복제 올바르게를 사용 하 여 확인할 수 있습니다 **repadmin /replsum**, Windows Server의 모든 버전에서 실행 됩니다.  
  
> [!TIP]
>  다운로드 하 고 실행 수도 있습니다는 [Active Directory 복제 상태 도구](https://www.microsoft.com/download/details.aspx?id=30005) (ADReplStatus), 오류 보고서 및 Dc 복제 상태를 모니터링 하는 무료 도구인 합니다. ADReplStatus 존재 없는 경우 설치.NET Framework 4 필요 합니다.  
  
 뷰어에서 이벤트 이벤트 ID 4602 (또는 파일 복제 서비스 이벤트 ID 13516)에 대 한 SYSVOL 초기화 나타내는 DFS 복제 로그를 확인 합니다.  
  
 첫 번째 복구 DC 기록 이벤트 ID 4614 ("은 도메인 컨트롤러 기다리고 초기 복제 수행할 수 있습니다. 복제 폴더에에서 남습니다 초기 동기화 상태와의 파트너 복제가 될 때 까지") Dfs 로그에, 다음 이벤트 ID 4602 표시 되지 않으며 DFSR 복제 SYSVOL 복구할 수동 다음 단계를 수행 해야 합니다.  
  
1.  DFSR 이벤트 4612 첫 번째 복원된 DC에 표시 되 면 수동 정식 복원을에 설명 된 대로 수행 [2218556: DFSR 복제 SYSVOL (예: "d 4/d 2" FRS에 대 한)에 대 한 권한을 보유 하 고 신뢰할 수 없는 동기화 하는 방법을](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556)입니다.  
  
2.  설정 **SysvolReady 플래그** 1을 수동으로에 설명 된 대로 [947022 The NETLOGON 공유 없으면 새 전체 또는 읽기 전용 Windows Server 2008 기반 도메인 컨트롤러에 Active Directory Domain Services를 설치한 후](https://support.microsoft.com/kb/947022)합니다.  
  
 진단 보고서 DFS 복제 만들 수 있습니다. 자세한 내용은 참조 [Dfs 진단 보고서를 만들려면](https://technet.microsoft.com/library/cc754227.aspx) 및 [DFS Step-by-Step Windows Server 2008 가이드](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx)합니다. 서버에서 Windows Server 2008 R2을 실행 하는 경우 사용할 수 있습니다 [dfsrdiag.exe ReplicationState 명령줄 스위치](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)합니다.  
  
 복제 테스트 dcdiag.exe 복제 오류 검사를 사용 하 여 실행할 수 있습니다. 자세한 내용은 참조 기술 자료 [249256 문서](https://support.microsoft.com/kb/249256)합니다.

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
