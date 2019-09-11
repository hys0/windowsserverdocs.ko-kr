---
title: SYSVOL 복제를 DFS 복제로 마이그레이션
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 30222d0737ac3cd2947fc3b2d70a0df77b606299
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871987"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>SYSVOL 복제를 DFS 복제로 마이그레이션


업데이트됨: 2010 년 8 월 25 일

적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

도메인 컨트롤러는 SYSVOL 이라는 특수 공유 폴더를 사용 하 여 로그온 스크립트와 그룹 정책 개체 파일을 다른 도메인 컨트롤러에 복제 합니다. Windows 2000 Server 및 Windows Server 2003에서는 FRS (파일 복제 서비스)를 사용 하 여 SYSVOL을 복제 하는 반면 windows Server 2008에서는 Windows Server 2008 도메인 기능 수준을 사용 하는 도메인에서 최신 DFS 복제 서비스를 사용 하 고 이전 도메인 기능 수준을 실행 합니다.

DFS 복제를 사용 하 여 SYSVOL 폴더를 복제 하려면 Windows Server 2008 도메인 기능 수준을 사용 하는 새 도메인을 만들거나이 문서에 설명 된 절차를 사용 하 여 기존 도메인을 업그레이드 하 고 복제를로 마이그레이션할 수 있습니다. DFS 복제.

이 문서에서는 Active Directory Domain Services (AD DS), FRS 및 분산 파일 시스템 복제 (DFS 복제)에 대 한 기본적인 지식이 있다고 가정 합니다. 자세한 내용은 [Active Directory Domain Services 개요](http://go.microsoft.com/fwlink/?linkid=147787), [FRS 개요](http://go.microsoft.com/fwlink/?linkid=121763)또는 개요를 참조 하세요 [DFS 복제](http://go.microsoft.com/fwlink/?linkid=121762)


> [!NOTE]
> 이 가이드 <a href="http://go.microsoft.com/fwlink/?linkid=150375">의 인쇄 가능한 버전을 다운로드 하려면 SYSVOL 복제 마이그레이션 가이드: FRS를 DFS 복제</a> (http://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>이 가이드의 내용

[SYSVOL 마이그레이션 개념 정보](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL 마이그레이션 상태](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [SYSVOL 마이그레이션 절차 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL 마이그레이션 절차](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [준비 된 상태로 마이그레이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [리디렉션된 상태로 마이그레이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [제거 된 상태로 마이그레이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[SYSVOL 마이그레이션 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [SYSVOL 마이그레이션 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [안정적인 이전 상태로 SYSVOL 마이그레이션 롤백](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[SYSVOL 마이그레이션 참조 정보](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [지원 되는 SYSVOL 마이그레이션 시나리오](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [SYSVOL 마이그레이션 상태를 확인 하는 중](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [Dfsrmig](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [SYSVOL 마이그레이션 도구 작업](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>추가 참조

[SYSVOL 마이그레이션 시리즈: 1 부-SYSVOL 마이그레이션 프로세스 소개](http://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL 마이그레이션 시리즈: 2 부-Dfsrmig: SYSVOL 마이그레이션 도구](http://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL 마이그레이션 시리즈: 3 부-' 준비 ' 상태로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL 마이그레이션 시리즈: 4 부-' 리디렉션 ' 상태로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL 마이그레이션 시리즈: 5 부-' 제거 됨 ' 상태로 마이그레이션](http://go.microsoft.com/fwlink/?linkid=121760)

[Windows Server 2008의 분산 파일 시스템에 대 한 단계별 가이드](http://go.microsoft.com/fwlink/?linkid=85231)

[FRS 기술 참조](http://go.microsoft.com/fwlink/?linkid=121764)

