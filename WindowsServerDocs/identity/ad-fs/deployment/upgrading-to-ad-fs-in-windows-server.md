---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: "Windows Server 2016에에서 Adfs로 업그레이드"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ce07398a2d624a1e9b004cd35eb9228d59dc2b5b
ms.sourcegitcommit: 76e57a5453d6ee9a04dcff6a8cca087132cb1d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>Adfs의 Windows Server 2016 WID 데이터베이스를 사용 하 여 업그레이드

>Windows Server 2016 적용 됩니다.


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 r 2 ADFS 팜에서 Windows Server 2016 ADFS 팜으로 이동  
다음 문서 WID 데이터베이스를 사용 하는 경우 Windows Server 2016에 ADFS AD FS Windows Server 2012 r 2 농장 업그레이드 하는 방법을 설명 합니다.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>Windows Server 2016 FBL ADFS 업그레이드  
새로운 Windows Server 2016 용 Adfs의 농장 동작 수준 기능이입니다 (FBL).   이 기능은 농장 다양 한 이며 ADFS 농장 사용할 수 있는 기능을 결정 합니다.   기본적으로 Windows Server 2012 r 2 ADFS 농장의 FBL Windows Server 2012 r 2 FBL입니다.  

Windows Server 2016 ADFS 서버 Windows Server 2012 r 2 그룹에 추가할 수 있으며는 Windows Server 2012 r 2와 같은 FBL에서 작동 합니다.  이러한 방식으로 작동 하는 Windows Server 2016 ADFS 서버를 사용 하는 경우 사용자 농장 "혼합" 이라고 합니다.  그러나 Windows Server 2016에는 FBL 발생 하는 때까지 Windows Server 2016의 새로운 기능을 이용할 수 됩니다.  혼합된 농장 사용:  

-   관리자 새, Windows Server 2016 federation 서버 기존 Windows Server 2012 r 2 농장을 추가할 수 있습니다.  결과적으로, 팜 "혼합 모드"와 Windows Server 2012 r 2 팜 동작 수준 작동 합니다.  그룹에서 일관 된 동작을 위해 Windows Server 2016의 새로운 기능을 구성 하거나이 모드로 사용할 수 수 없습니다.  

-   모든 Windows Server 2012 r 2 federation 서버 운영할 농장에서 제거 하 고 WID 농장의 경우 새 Windows Server 2016 federation 서버 중 하나 렸 기본 노드의 역할을 후 관리자 Windows Server 2016에 Windows Server 2012 r 2의 FBL 다음 시킬 수 있습니다.  결과적으로, 만한 새로운 기능은 포함 AD FS Windows Server 2016 다음 구성 및 사용할 수 있습니다.  

-   따라서 혼합된 농장 기능의 광고 FS Windows Server 2012 r 2 조직이 Windows Server 2016로 업그레이드 하는 완전히 새로운 팜 배포 필요가 없습니다 내보내고 구성 데이터.  대신, Windows Server 2016 노드 기존 농장 온라인 상태일 때 추가 고만 간단한 상대적으로 작동 중지 FBL 발생에 포함 된 요금이 수 있습니다.  

혼합된 농장 모드로 ADFS 농장 아닌지 수 있는 새로운 기능 또는 Windows Server 2016에 adfs에서 도입 기능 주의 해야 합니다.  이 새로운 기능을 사용해 하려는 조직에서 FBL 발생 하는 때까지 이렇게 할 수 없는 것을 의미 합니다.  따라서 조직에는 FBL rasing 전에 새로운 기능을 테스트 하 원하는이 작업을 수행 하는 별도 농장 배포 해야 합니다.  

나머지는이 문서에서는 Windows Server 2012 r 2 환경에 Windows Server 2016 federation 서버를 추가 하 고 Windows Server 2016에 FBL 후 발생 하는 단계를 제공 합니다.  아키텍처 다이어그램 아래에 설명 되어 있음 테스트 환경에서 다음이 단계를 수행 했습니다.  

> [!NOTE]  
> Windows Server 2016 FBL에서 Adfs을 이동 하려면 먼저 Windows 2012 r 2 노드가 모두 제거 해야 합니다.  방금 Windows Server 2012 r 2 OS Windows Server 2016로 업그레이드 하 고 2016 노드 될 지도록 할 수 없습니다.  제거 하 고 새 2016 노드 교체 해야 합니다.
>
> SQL를 사용 하 여 저장소 ADFS 구성 하 고 FBL 업그레이드 "AdfsConfigurationV3" 새로운 관리 데이터베이스를 만듭니다지 않습니다.

##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2016-farm-behavior-level"></a>Windows Server 2016 팜 동작 수준 ADFS 농장 업그레이드 하려면  

1.  Windows Server 2016에 서버 관리자 설치 Active Directory Federation Services 역할을 사용 하 여  

2.  새 Windows Server 2016 서버 기존 ADFS 농장을에 가입 AD FS 구성 마법사를 사용 합니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)  

3.  Windows Server 2016 federation 서버에서 ADFS 관리를 엽니다.    Note는 아무는 대로 표시이 federation 서버 주 서버는 아닙니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)  

4.  연결 Windows Server 2016 서버에 완료 되 면 PowerShell 열고 다음 cmdlt 실행: 설정 AdfsSyncProperties-역할 PrimaryComputer  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)  

5.  원래 AD FS Windows Server 2012 r 2 서버의 PowerShell 열고 다음 cmdlt 실행: 설정 AdfsSyncProperties-역할 SecondaryComputer PrimaryComputerName {FQDN}  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)  

6.  웹 응용 프로그램 프록시에서 PowerShell 열고 followoing cmdlt 실행: WebApplicationProxy 설치-CertificateThumbprint {SSLCert}-fsname fsname-TrustCred $trustcred  

7.  이제 Windows Server 2016 federation 서버에서 광고 FS 관리를 엽니다.  기본 역할로이 서버에 전송 된 때문에 표시 하는 모든 노드 이제는 note 합니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)  

8.  Windows Server 2016 설치 미디어를 사용 명령 프롬프트를 열고 support\adprep 디렉터리에 이동 합니다.  다음을 실행할: adprep /forestprep 합니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)  

9. 완료 되 면 실행 adprep/도메인 준비  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)  

10. 이제 Windows Server 2016 서버에 PowerShell 열고 실행 다음 cmdlt: 호출 AdfsFarmBehaviorLevelRaise  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)  

11. 메시지가 표시 되 면 Y 입력 합니다. 이 수준 올리기 시작 됩니다.  다운로드가 완료 되 고 FBL를 성공적으로 발생 했습니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)  

> [!NOTE]  
> ADFS 서버 SQL 구성에 대 한를 사용 "AdfsConfiguraionV3" 이름의 이제 새 manamgement 데이터베이스를 만들었습니다. 

12. 이제 AD FS 관리로 이동 하는 경우 나타납니다 adfs Windows Server 2016에 추가 된 새 노드에서  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)  

13. 마찬가지로, PowerShell cmdlt 사용할 수 있습니다: 다운로드 AdfsFarmInformation 현재 FBL 표시 됩니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)  
