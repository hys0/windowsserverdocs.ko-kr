---
title: AD 포리스트 복구-복제 확인
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: f6bee5164849d6643c1744ce121b9ce91b5e7f7f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949047"
---
# <a name="resources-to-verify-replication-is-working"></a>복제가 작동 하는지 확인 하기 위한 리소스 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

모든 Dc를 복원 하거나 다시 설치한 후에는 모든 버전의 Windows Server에서 실행 되는 **repadmin/replsum**를 사용 하 여 AD DS 및 SYSVOL이 올바르게 복구 및 복제 되는지 확인할 수 있습니다.  
  
> [!TIP]
> Dc의 복제 상태를 모니터링 하 고 오류를 보고 하는 무료 도구인 [Active Directory 복제 상태 도구](https://www.microsoft.com/download/details.aspx?id=30005) (adreplstatus)를 다운로드 하 여 실행할 수도 있습니다. ADReplStatus에는 .NET Framework 4가 필요 하며,이는 아직 없는 경우 설치 됩니다.  

SYSVOL이 초기화 되었음을 나타내는 이벤트 ID 4602 (또는 파일 복제 서비스 이벤트 ID 13516)에 대 한 DFS 복제 로그인 이벤트 뷰어를 확인 합니다.  

첫 번째 복구 된 DC가 이벤트 ID 4614 ("도메인 컨트롤러에서 초기 복제를 수행 하려고 대기 중입니다."를 기록 합니다. 복제 된 폴더는 해당 파트너와 함께 복제 될 때까지 초기 동기화 상태로 유지 됩니다. ") DFS 복제 로그에서 이벤트 ID 4602가 표시 되지 않으며 다음 수동 단계를 수행 하 여에서 복제 하는 경우 SYSVOL을 복구 해야 합니다. ACTIVE  

1. 첫 번째 복원 된 DC에 DFSR 이벤트 4612이 표시 되 면 [2218556: dfsr 복제 SYSVOL (예: FRS의 경우 "D4/D2")에 대해 신뢰할 수 있는 동기화와 신뢰할 수 없는 동기화를 강제로 적용 하는 방법](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556) )에 설명 된 대로 수동 신뢰할 수 있는 복원을 수행 합니다.  
2. 947022에 설명 된 대로 **SysvolReady 플래그** 를 수동으로 1로 설정 합니다 .에 설명 [된 대로 새 전체 또는 읽기 전용 Windows Server 2008 기반 도메인 컨트롤러에 Active Directory Domain Services를 설치한 후에는 NETLOGON 공유가 표시 되지](https://support.microsoft.com/kb/947022)않습니다.  

DFS 복제 진단 보고서를 만들 수도 있습니다. 자세한 내용은 [DFS 복제에 대 한 진단 보고서 만들기](https://technet.microsoft.com/library/cc754227.aspx) 및 [Windows Server 2008에 대 한 DFS 단계별 가이드](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx)를 참조 하세요. 서버에서 Windows Server 2008 r 2를 실행 하는 경우에는 [Dfsrdiag ReplicationState 명령줄 스위치](https://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)를 사용할 수 있습니다.  

Dcdiag.exe를 사용 하 여 복제 테스트를 실행 하 여 복제 오류를 확인할 수도 있습니다. 자세한 내용은 기술 자료 [문서 249256](https://support.microsoft.com/kb/249256)를 참조 하십시오.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
