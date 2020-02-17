---
title: SYSVOL 복제를 DFS 복제로 마이그레이션
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: d8d9d47ff8f14ce316d2352729247ab2dcf4acbc
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949708"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>SYSVOL 복제를 DFS 복제로 마이그레이션


업데이트됨: 2010년 8월 25일

적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

도메인 컨트롤러는 SYSVOL이라는 특수 공유 폴더를 사용하여 로그온 스크립트와 그룹 정책 개체 파일을 다른 도메인 컨트롤러에 복제합니다. Windows 2000 Server 및 Windows Server 2003에서는 FRS(파일 복제 서비스)를 사용하여 SYSVOL을 복제하는 반면 Windows Server 2008에서는 이전 도메인 기능 수준을 실행하는 도메인을 위해 Windows Server 2008 도메인 기능 수준 및 FRS를 사용하는 도메인에서 최신 DFS 복제 서비스를 사용합니다.

DFS 복제를 사용하여 SYSVOL 폴더를 복제하려면 Windows Server 2008 도메인 기능 수준을 사용하는 새 도메인을 만들거나 이 문서에 설명된 절차를 사용하여 기존 도메인을 업그레이드하고 복제를 DFS 복제로 마이그레이션할 수 있습니다.

이 문서에서는 AD DS(Active Directory Domain Services), FRS 및 DFS 복제(분산 파일 시스템 복제)에 대한 기본적인 지식이 있다고 가정합니다. 자세한 내용은 [Active Directory Domain Services 개요](https://go.microsoft.com/fwlink/?linkid=147787), [FRS 개요](https://go.microsoft.com/fwlink/?linkid=121763) 또는 [DFS 복제 개요](https://go.microsoft.com/fwlink/?linkid=121762)를 참조하세요.


> [!NOTE]
> 이 가이드의 인쇄 가능한 버전을 다운로드하려면 <a href="https://go.microsoft.com/fwlink/?linkid=150375">SYSVOL 복제 마이그레이션: FRS에서 DFS 복제로</a>를 참조하세요(https://go.microsoft.com/fwlink/?LinkId=150375).
<br>


## <a name="in-this-guide"></a>이 가이드의 내용

[SYSVOL 마이그레이션 개념 정보](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL 마이그레이션 상태](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [SYSVOL 마이그레이션 절차 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL 마이그레이션 절차](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [준비된 상태로 마이그레이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [리디렉션된 상태로 마이그레이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [제거된 상태로 마이그레이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[SYSVOL 마이그레이션 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [SYSVOL 마이그레이션 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [안정적인 이전 상태로 SYSVOL 마이그레이션 롤백](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[SYSVOL 애플리케이션 참조 정보](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [지원되는 SYSVOL 마이그레이션 시나리오](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [SYSVOL 마이그레이션 상태 확인](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [Dfsrmig](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [SYSVOL 마이그레이션 도구 작업](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>추가 참조

[SYSVOL 마이그레이션 시리즈: 1부—SYSVOL 마이그레이션 프로세스 소개](https://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL 마이그레이션 시리즈: 2부—Dfsrmig.exe: SYSVOL 마이그레이션 도구](https://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL 마이그레이션 시리즈: 3부—'준비' 상태로 마이그레이션](https://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL 마이그레이션 시리즈: 4부—‘리디렉션' 상태로 마이그레이션](https://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL 마이그레이션 시리즈: 5부—‘제거된' 상태로 마이그레이션](https://go.microsoft.com/fwlink/?linkid=121760)

[Windows Server 2008의 분산 파일 시스템에 대한 단계별 가이드](https://go.microsoft.com/fwlink/?linkid=85231)

[FRS 기술 참조](https://go.microsoft.com/fwlink/?linkid=121764)

