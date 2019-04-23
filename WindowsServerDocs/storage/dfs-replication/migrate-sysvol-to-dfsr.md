---
Title: SYSVOL 복제를 DFS 복제로 마이그레이션
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 7ea883730fcab83d064fa41f610bde4837510276
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836644"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>SYSVOL 복제를 DFS 복제로 마이그레이션


업데이트됨: 2010 년 8 월 25 일

적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

도메인 컨트롤러는 다른 도메인 컨트롤러에 로그온 스크립트와 그룹 정책 개체 파일 복제 SYSVOL 라는 특수 한 공유 폴더를 사용 합니다. Windows 2000 Server 및 Windows Server 2003 복제 서비스 FRS (파일) Windows Server 2008에는 Windows Server 2008 도메인 기능 수준을 사용 하는 도메인에 있을 때 최신 DFS 복제 서비스를 사용 하는 반면 SYSVOL을 복제 하 고 도메인에 대 한 FRS를 사용 하는 이전 도메인 기능 수준을 실행 합니다.

DFS 복제에 SYSVOL 폴더를 복제 하는 데 사용 하려면 Windows Server 2008 도메인 기능 수준을 사용 하는 새 도메인을 만들 수 있습니다. 또는 복제를 마이그레이션하고 기존 도메인을 업그레이드 하려면이 문서에서 설명 하는 절차를 사용할 수 있습니다. DFS 복제 합니다.

이 문서에서는 Active Directory Domain Services (AD DS), FRS, 및 분산 파일 시스템 복제 (DFS 복제)에 대 한 기본적인 지식이 있다고 가정 합니다. 자세한 내용은 [Active Directory Domain Services 개요](http://go.microsoft.com/fwlink/?linkid=147787)를 [FRS 개요](http://go.microsoft.com/fwlink/?linkid=121763), 또는 [DFS 복제 개요](http://go.microsoft.com/fwlink/?linkid=121762)


> [!NOTE]
> 이 가이드의 인쇄 가능한 버전을 다운로드 하려면로 이동 <a href="http://go.microsoft.com/fwlink/?linkid=150375">SYSVOL 복제 마이그레이션 가이드: FRS에서 DFS 복제로</a> (http://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>이 가이드의 내용

[SYSVOL 마이그레이션에 대 한 개념 정보](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL 마이그레이션 상태](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [SYSVOL 마이그레이션 절차의 개요](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL 마이그레이션 절차](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [준비 된 상태 마이그레이션](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [리디렉션된 상태로 마이그레이션](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [제거 상태로 마이그레이션](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[SYSVOL 마이그레이션 문제 해결](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [SYSVOL 마이그레이션 문제 해결](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [이전 안정적인 상태로 SYSVOL 마이그레이션 롤백](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[SYSVOL 마이그레이션 참조 정보](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [지원 되는 SYSVOL 마이그레이션 시나리오](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [SYSVOL 마이그레이션 상태 확인](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [Dfsrmig](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [SYSVOL 마이그레이션 도구 작업](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>추가 참조

[SYSVOL 마이그레이션 시리즈: 1 부-SYSVOL 마이그레이션 소개](http://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL 마이그레이션 시리즈: 2—Dfsrmig.exe 부: SYSVOL 마이그레이션 도구](http://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL 마이그레이션 시리즈: 3 부-'준비' 상태로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL 마이그레이션 시리즈: 4 부-'REDIRECTED' 상태로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL 마이그레이션 시리즈: 5 부-'제거' 상태로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=121760)

[Windows Server 2008의에서 분산된 파일 시스템에 대 한 단계별 가이드](http://go.microsoft.com/fwlink/?linkid=85231)

[FRS 기술 참조](http://go.microsoft.com/fwlink/?linkid=121764)

