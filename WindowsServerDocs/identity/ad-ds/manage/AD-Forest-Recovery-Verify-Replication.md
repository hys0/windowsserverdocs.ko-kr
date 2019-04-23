---
title: AD 포리스트 복구 복제를 확인 합니다.
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: fb05586f281460dc2c7a1afea4c0423493e3fc46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878314"
---
# <a name="resources-to-verify-replication-is-working"></a>복제가 작동을 확인 하려면 리소스 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

를 다시 모든 Dc를 설치 하거나 복원 후 AD DS 및 SYSVOL는 복구 및 복제 올바르게 사용 하 여 확인할 수 있습니다 **repadmin /replsum**, 모든 버전의 Windows Server에서 실행 되는 합니다.  
  
> [!TIP]
> 또한 다운로드 하 고 실행할 수는 [Active Directory 복제 상태 도구](https://www.microsoft.com/download/details.aspx?id=30005) (ADReplStatus) Dc와 보고서 오류의 복제 상태를 모니터링 하는 무료 도구입니다. ADReplStatus 아직 제공 되지 경우 설치 하는.NET Framework 4 필요 합니다.  

SYSVOL 초기화 되었는지 여부를 나타내는 이벤트 뷰어에서 이벤트 ID 4602 (또는 파일 복제 서비스 이벤트 ID 13516)에 대 한 DFS 복제 로그를 확인 합니다.  

첫 번째 복구 DC가 로그 이벤트 ID 4614 ("도메인 컨트롤러는 대기 중 초기 복제를 수행 합니다. 복제 된 폴더에에서 남아 초기 동기화 상태를 해당 파트너와 복제 될 때 까지")는 DFS 복제 로그에, 이벤트 ID 4602 나타나지 않으면 다음 있고 SYSVOL에 의해 복제 되는 경우 복구 하려면 다음 수동 단계를 수행 해야 DFSR:  

1. DFSR 이벤트 4612 복원된 된 첫 번째 DC에 표시 될 때에 설명 된 대로 수동 정식 복원을 수행 [2218556: DFSR 복제 된 SYSVOL (예: "D4/D2" FRS 용)에 대 한 신뢰할 수 있는 도메인과 신뢰할 수 없는 동기화를 강제 하는 방법](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556)합니다.  
2. 설정할 **SysvolReady 플래그** 1에 설명 된 대로 수동으로 [947022 The NETLOGON 공유 새 전체 또는 읽기 전용 Windows Server 2008 기반 도메인 컨트롤러에서 Active Directory Domain Services를 설치한 후에 나타나지 않습니다. ](https://support.microsoft.com/kb/947022).  

DFS 복제 진단 보고서를 만들 수도 있습니다. 자세한 내용은 [DFS 복제 진단 보고서를 만듭니다](https://technet.microsoft.com/library/cc754227.aspx) 하 고 [DFS 단계별 가이드 Windows Server 2008 용](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx)합니다. 서버는 Windows Server 2008 R2를 실행 하는 경우 사용할 수 있습니다 [dfsrdiag.exe ReplicationState 명령줄 스위치](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)합니다.  

또한 복제 오류를 확인 하 여 dcdiag.exe를 사용 하 여 복제 테스트를 실행할 수 있습니다. 자세한 내용은 기술 자료를 참조 하세요 [249256 문서](https://support.microsoft.com/kb/249256)합니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
