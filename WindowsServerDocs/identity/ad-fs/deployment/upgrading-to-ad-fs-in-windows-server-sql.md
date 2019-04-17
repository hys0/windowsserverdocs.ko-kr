---
title: "Windows server 2016 SQL server Adfs로 업그레이드"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 034d4f1f8d81cf105ba94bff34b180555702acde
ms.sourcegitcommit: 33c1f4965cd2eed7d384a096cfa5c883467b16a4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2017
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>Windows server 2016 SQL server Adfs로 업그레이드

>Windows Server 2016 적용 됩니다.


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 r 2 ADFS 팜에서 Windows Server 2016 ADFS 팜으로 이동  
다음 문서 SQL Server ADFS 데이터베이스에 대 한 사용 중인 경우 Windows Server 2016에 ADFS AD FS Windows Server 2012 r 2 농장 업그레이드 하는 방법을 설명 합니다.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>Windows Server 2016 FBL ADFS 업그레이드  
새로운 Windows Server 2016 용 Adfs의 농장 동작 수준 기능이입니다 (FBL).   이 기능은 농장 다양 한 이며 ADFS 농장 사용할 수 있는 기능을 결정 합니다.   기본적으로 Windows Server 2012 r 2 ADFS 농장의 FBL Windows Server 2012 r 2 FBL입니다.  

Windows Server 2016 ADFS 서버 Windows Server 2012 r 2 그룹에 추가할 수 있으며는 Windows Server 2012 r 2와 같은 FBL에서 작동 합니다.  이러한 방식으로 작동 하는 Windows Server 2016 ADFS 서버를 사용 하는 경우 사용자 농장 "혼합" 이라고 합니다.  그러나 Windows Server 2016에는 FBL 발생 하는 때까지 Windows Server 2016의 새로운 기능을 이용할 수 됩니다.  혼합된 농장 사용:  

-   관리자 새, Windows Server 2016 federation 서버 기존 Windows Server 2012 r 2 농장을 추가할 수 있습니다.  결과적으로, 팜 "혼합 모드"와 Windows Server 2012 r 2 팜 동작 수준 작동 합니다.  그룹에서 일관 된 동작을 위해 Windows Server 2016의 새로운 기능을 구성 하거나이 모드로 사용할 수 수 없습니다.  

-   모든 Windows Server 2012 r 2 federation 서버 운영할 농장에서 제거 하 고 WID 농장의 경우 새 Windows 사용할 2016 federation 서버 중 하나 렸 기본 노드의 역할을 후 관리자 Windows Server 2016에 Windows Server 2012 r 2의 FBL 다음 시킬 수 있습니다.  결과적으로, 만한 새로운 기능은 포함 AD FS Windows Server 2016 다음 구성 및 사용할 수 있습니다.  

-   따라서 혼합된 농장 기능의 광고 FS Windows Server 2012 r 2 조직이 Windows Server 2016로 업그레이드 하는 완전히 새로운 팜 배포 필요가 없습니다 내보내고 구성 데이터.  대신, Windows Server 2016 노드 기존 농장 온라인 상태일 때 추가 고만 간단한 상대적으로 작동 중지 FBL 발생에 포함 된 요금이 수 있습니다.  

혼합된 농장 모드로 ADFS 농장 아닌지 수 있는 새로운 기능 또는 Windows Server 2016에 adfs에서 도입 기능 주의 해야 합니다.  이 새로운 기능을 사용해 하려는 조직에서 FBL 발생 하는 때까지 이렇게 할 수 없는 것을 의미 합니다.  따라서 조직에는 FBL rasing 전에 새로운 기능을 테스트 하 원하는이 작업을 수행 하는 별도 농장 배포 해야 합니다.  

나머지는이 문서에서는 Windows Server 2012 r 2 환경에 Windows Server 2016 federation 서버를 추가 하 고 Windows Server 2016에 FBL 후 발생 하는 단계를 제공 합니다.  아키텍처 다이어그램 아래에 설명 되어 있음 테스트 환경에서 다음이 단계를 수행 했습니다.  

> [!NOTE]  
> Windows Server 2016 FBL에서 Adfs을 이동 하려면 먼저 Windows 2012 r 2 노드가 모두 제거 해야 합니다.  방금 Windows Server 2012 r 2 OS Windows Server 2016로 업그레이드 하 고 2016 노드 될 지도록 할 수 없습니다.  제거 하 고 새 2016 노드 교체 해야 합니다.  

다음 아키텍처 다이어그램을 확인 하 고 다음 단계를 녹화 하는 데 사용 된 설정 보여 줍니다.

![건축물](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png) 


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Windows 2016 광고 FS 서버 ADFS 농장 가입

1.  Windows Server 2016에 서버 관리자 설치 Active Directory Federation Services 역할을 사용 하 여  

2.  새 Windows Server 2016 서버 기존 ADFS 농장을에 가입 AD FS 구성 마법사를 사용 합니다.  에 **시작** 화면 클릭 **다음**합니다.
 ![농장 가입](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  에 **Active Directory 도메인 서비스에 연결** 화면, s**관리자 계정으로 지정** federation services 구성을 수행 및 클릭 수 있는 권한이 있는 **다음**합니다.
4.  에 **지정 농장** 화면 고 SQL server 인스턴스의 이름을 입력 하 고 클릭 한 다음 **다음**합니다.
![농장 가입](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  에 **SSL 인증서를 지정** 화면 인증서를 지정 하 고 클릭 **다음**합니다.
![농장 가입](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  에 **서비스 계정 지정** 화면 서비스 계정을 지정 하 고 클릭 **다음**합니다. 
7.  에 **옵션 검토** 화면에서 옵션을 검토 한 클릭 **다음**합니다. 
8.  에 **필수 검사** 화면에서 모든 전 필수 조건 검사를 통과 및 클릭 수 있도록 **구성**합니다.
9.  에 **결과** 화면 서버를 성공적으로 구성 있는지 확인 하 고 클릭 **닫기**합니다.
 
   
#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 r 2 ADFS 서버 제거

>[!NOTE]
>AdfsSyncProperties 집합을 사용 하 여 기본 ADFS 서버를 설정할 필요는 없습니다-데이터베이스 SQL 사용할 경우 어떤 역할을 맡고 있습니다.  이 구성 기본 간주 모든 노드 하기 때문입니다.

1.  Windows Server 2012 r 2 ADFS 서버 관리자 사용 하는 서버에서 **역할 제거 및 기능** 아래 **관리**합니다. 
![서버를 제거](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  에 **시작 하기 전에** 화면에서 클릭 **다음**합니다.
3.  에 **서버 선택** 화면 클릭 **다음**합니다.
4.  에 **서버 역할** 화면에서 옆에 있는 확인란의 선택을 취소 **Active Directory Federation Services** 클릭 **다음**합니다.
![서버를 제거](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  에 **기능** 화면 클릭 **다음**합니다.
6.  에 **확인** 화면 클릭 **제거**합니다.
7.  이 완료 되 면 서버를 다시 시작 합니다.
     
#### <a name="raise-the-farm-behavior-level-fbl"></a>(FBL) 농장 동작 수준 높이기
이 단계 전에 forestprep 및 도메인 준비 Active Directory 환경에서 실행 하 고 Active Directory에 Windows Server 2016 스키마 있는지 확인 해야 합니다.  이 문서는 Windows 2016 도메인 컨트롤러를 시작 하 고 광고를 설치할 때 실행 하는 것이 실행 필요 하지 않았습니다.

1. Windows Server 2016 서버에서 이제 PowerShell 열고 다음을 실행할: **$cred Get 자격 증명 =** 시작 하 고 입력 하 고 있습니다.
2. SQL Server에서 관리자 권한이 있는 자격 증명을 입력 합니다.
3. PowerShell의 다음 입력할: **호출 AdfsFarmBehaviorLevelRaise-$cred 자격 증명**
2. 메시지가 표시 되 면 입력 **Y**합니다. 이 수준 올리기 시작 됩니다.  다운로드가 완료 되 고 FBL를 성공적으로 발생 했습니다.  
![업데이트를 완료 합니다.](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. 이제 AD FS 관리로 이동 하는 경우 나타납니다 adfs Windows Server 2016에 추가 된 새 노드에서  
4. 마찬가지로, PowerShell cmdlt 사용할 수 있습니다: 다운로드 AdfsFarmInformation 현재 FBL 표시 됩니다.  
![업데이트를 완료 합니다.](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)
