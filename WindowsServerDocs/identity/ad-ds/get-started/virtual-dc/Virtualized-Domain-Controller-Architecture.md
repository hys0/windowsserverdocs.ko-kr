---
ms.assetid: 341614c6-72c2-444f-8b92-d2663aab7070
title: "가상화 도메인 컨트롤러 아키텍처"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac8b190df065547d82aa431761eb5c00c94a2ad6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-architecture"></a>가상화 도메인 컨트롤러 아키텍처

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목의 아키텍처 가상화 도메인 컨트롤러 복제와 안전 복원이 설명 합니다. 프로세스 복제와 순서도 안전 복원이 표시 하 고 각 단계 프로세스에 대 한 자세한 내용은 다음 제공 합니다.  
  
-   [아키텍처 복제 가상화 도메인 컨트롤러](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)  
  
-   [가상화 도메인 컨트롤러 안전 복원이 건축물](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)  
  
## <a name="BKMK_CloneArch"></a>아키텍처 복제 가상화 도메인 컨트롤러  
  
### <a name="overview"></a>개요  
하이퍼바이저 플랫폼 이라는 식별자를 사용 하 여 가상화 도메인 컨트롤러 복제 **VM 세대 ID** 생성 가상 컴퓨터의 검색. AD DS 값이이 식별자 (NTDS 데이터베이스에 처음 저장. DIT) 도메인 컨트롤러 프로 모션 중입니다. 가상 컴퓨터가 부팅 VM 세대 ID에서 가상 컴퓨터의 현재 값 데이터베이스에 값 비교 됩니다. 두 개의 값 다른 경우 도메인 컨트롤러 호출 ID를 다시 설정 하 고 USN 다시 사용 하거나 중복 보안 사용자의 잠재적 생성 차단 RID 풀 삭제 합니다. 도메인 컨트롤러 다음 위치에 DCCloneConfig.xml 파일을 찾습니다에 3 단계에서에서 호출 [자세한 처리 복제](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneProcessDetails)합니다. DCCloneConfig.xml 파일을 찾을 경우 다시 상태 올리기 기존 NTDS를 사용 하 여 복제 구축 자체 추가 도메인 컨트롤러를 시작 되므로 복제본이으로 배포 되는 종료 합니다. 원본 미디어에서 DIT 및 SYSVOL 콘텐츠 복사 됩니다.  
  
일부 하이퍼바이저 VM GenerationID를 지원 하지 않는 경우도 장소와 혼합된 환경, 복제 미디어를 실수로 VM GenerationID 지원 하지 않는 하이퍼바이저에 배포할 수는 있습니다. DCCloneConfig.xml 파일이 있는지 관리 의도 DC 복제를 나타냅니다. 따라서 DCCloneConfig.xml 파일 부팅 하지만 VM GenerationID 중 발견 되 면 제공 되지 않습니다 호스트, DC 복제에 DSRM 디렉터리 서비스 복원 모드 () 환경의 나머지 부분에 어떤 영향을 방지 하기 위해 부팅할. 복제 미디어를 지 원하는 VM GenerationID 하이퍼바이저 이후에 이동할 수 있으며 복제 다음 다시 시도할 수 있습니다.  
  
복제 미디어를 지 원하는 VM GenerationID 하이퍼바이저에 배포 될 한다면 DCCloneConfig.xml 파일 제공 되지 않은 DC 감지 해당 DIT 새 VM에서 하나 사이의 VM GenerationID 변경 보호 USN 다시 사용 하 여 예방 하 고 Sid 중복 방지 하는 모두 합니다. 그러나 복제는 시작 되지, 계속 보조 DC 원본 DC 같은 id 아래에서 실행 하도록 합니다. 이 보조 DC 환경에서 일치 하지 않는 부분을 방지 하려면 가능한 한 빠른 시간에는 네트워크에서 제거 해야 합니다. 이 보조 DC 업데이트 아웃 바운드 복제, Microsoft KB 표시 하면서 확보 하는 방법에 대 한 자세한 내용은 문서 [2742970](https://support.microsoft.com/kb/2742970)합니다.  
  
### <a name="BKMK_CloneProcessDetails"></a>자세한 처리 복제  
다음 그림 아키텍처 복제 다시 시도 하는 및 초기 복제 작업에 대 한 보여 줍니다. 자세한 내용은이 항목 뒷부분에서에이 프로세스를 설명 되어 있습니다.  
  
**초기 복제 작업**  
  
![DC 가상화 건축물](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_InitialCloningProcess.png)  
  
**다시 시도 복제**  
  
![DC 가상화 건축물](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_CloningRetryProcess.png)  
  
다음 단계에 과정을 자세히 설명합니다.  
  
1.  기존 가상 컴퓨터 도메인 컨트롤러에서 지 원하는 VM 세대 id입니다. 하이퍼바이저 부팅  
  
    1.  이 VM이 프로 모션 후 AD DS 컴퓨터 개체의 기존 VM 세대 ID 값 설정 없음에 있습니다.  
  
    2.  것 된 경우에 다음 컴퓨터 만들기는 의미 여전히 복제에서으로 새 VM 세대-ID와 일치 하지 것입니다.  
  
    3.  VM 세대 ID는 dc 다시 부팅 설정 되 고 복제 하지 않습니다.  
  
2.  가상 컴퓨터 다음 VMGenerationCounter 드라이버에서 제공 하 고 VM 세대 ID를 읽습니다. 두 개의 VM 세대 Id를 비교합니다.  
  
    1.  Id 일치 이것은 새 가상 컴퓨터 및 복제 진행 되지 않습니다. DCCloneConfig.xml 파일이 있는 경우 도메인 컨트롤러 복제 방지 하기 위해 날짜 타임 스탬프에 있는 파일을 이름을 바꿉니다. 서버는 정상적으로 부팅 계속 합니다. 가상 도메인 컨트롤러의 재부팅할 Windows Server 2012에서 작동 하는 방법입니다.  
  
    2.  두 개의 Id 일치 하지 않는 경우는 NTDS 포함 된 새 가상 컴퓨터를 수 있습니다. 이전 도메인 컨트롤러에서 DIT (또는 것이 복원된 스냅숏을). DCCloneConfig.xml 파일이 있는 경우 도메인 컨트롤러 복제 작업으로 진행 됩니다. 그렇지 않으면 스냅숏 복원 작업을 계속 합니다. 참조 [도메인 컨트롤러 안전 복원이 아키텍처 가상화](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)합니다.  
  
    3.  하이퍼바이저 비교 VM 세대 ID를 제공 하지는 않지만 DCCloneConfig.xml 파일이, 게스트 파일의 이름을 바꿉니다 한 DSRM 으로부터 보호 하기 위해 네트워크 중복 도메인 컨트롤러에 부팅 합니다. Dccloneconfig.xml 파일이 없는 경우 일반적으로 (가능성이 있는 네트워크에서 중복 된 도메인 컨트롤러) 게스트 부팅 됩니다. 이 중복 도메인 컨트롤러 참조 Microsoft 기술 자료 문서 확보 하는 방법에 대 한 자세한 내용은 [2742970](https://support.microsoft.com/kb/2742970)합니다.  
  
3.  NTDS 서비스 (아래에서 찾아) 레지스트리 값 VDCisCloning DWORD 이름 값을 확인 합니다.  
  
    1.  존재 하지 않는 경우이 가상 컴퓨터에 대 한 복제는 최초의 시도 수 있습니다. 로컬 RID 풀 무효화 고 도메인 컨트롤러에 대 한 새 복제 호출 ID를 설정 하는 VDC 개체 중복 보호 기능을 구현 게스트  
  
    2.  이미 0x1 설정 된 것을 경우이 "다시 시도 하는" 시도 복제 이전 복제 작업이 실패 했습니다. 이미 완료 되기 전에 실행 하 고 불필요 변경 게스트 여러 번 VDC 개체 중복 위한 안전 적용 되지 않도록 합니다.  
  
4.  IsClone DWORD 레지스트리 값 이름을 작성 되었습니다 (찾아)  
  
5.  NTDS 서비스는 더 이상 다시 부팅 한 후에 대 한 DS 복구 모드로 시작 하도록 게스트 부팅 플래그를 변경 합니다.  
  
6.  NTDS 서비스 (DSA 작업 디렉터리, %windir%\NTDS 또는 읽기/쓰기 이동식 미디어 루트 드라이브의 드라이브 문자가의 순서로 나열) 세 허용된 위치 중 하나에 DcCloneConfig.xml 읽기 하려고 합니다.  
  
    1.  유효한 어느 위치에 파일이 없으면 게스트 중복 IP 주소를 확인 합니다. IP 주소에서 중복 되지 경우 서버를 정상적으로 부팅 합니다. 중복 IP 주소를 이면 컴퓨터 DSRM 으로부터 보호 하기 위해 네트워크 중복 도메인 컨트롤러에 부팅 됩니다.  
  
    2.  유효한 위치에 파일이, 경우 NTDS 서비스 해당 설정을 확인 합니다. 비어 있는 파일 (또는 모든 특정 설정은 빈) 하는 경우 NTDS 이러한 설정에 대 한 자동 값을 구성 합니다.  
  
    3.  에 DSRM 디렉터리 서비스 복원 모드 () 부팅 하 여 DcCloneConfig.xml 하지만 잘못 된 항목에 포함 되어 있거나를 읽을 수, 경우 실패 하 고 게스트 복제 합니다.  
  
7.  게스트 모든 DNS 자동 등록 실수로 가로채기 소스 컴퓨터 이름을 및 IP 주소를 방지 하기 위해 사용할 수 없습니다.  
  
8.  게스트는 Netlogon 서비스는 광고 또는 클라이언트의 광고 네트워크 DS 요청에 응답 하지 않으려면 중지 합니다.  
  
9. NTDS는 DefaultDCCloneAllowList.xml 또는 CustomDCCloneAllowList.xml에 속하지 않는 설치 프로그램이 없거나 서비스는 유효성 검사  
  
    1.  서비스는 또는 기본 제외에 설치 된 프로그램 목록을 허용 또는 사용자 지정 제외 목록에서 허용 하는 경우 DSRM 으로부터 보호 하기 위해 네트워크 중복 도메인 컨트롤러에 부팅 실패 하 고 게스트 복제 됩니다.  
  
    2.  사항이 없음 호환성 문제를 복제 계속 합니다.  
  
10. 빈 DCCloneConfig.xml 네트워크 설정으로 인해 사용 되 면 자동 IP 주소, 게스트 DHCP에 네트워크 어댑터는 IP 주소 임대, 네트워크 경로 및 이름 확인 정보를 얻을 수 있습니다.  
  
11. 게스트 찾아 도메인 컨트롤러 역할 FSMO PDC 에뮬레이터를 실행 합니다. DNS 및 DCLocator 프로토콜을 사용합니다. RPC 연결 하 고 도메인 컨트롤러 컴퓨터 개체 복제 IDL_DRSAddCloneDC 메서드를 호출 있습니다.  
  
    1.  게스트의 소스 컴퓨터 개체 도메인 머리의 확장된 사용 권한을 보유 "' DC 자체 복제를 만들 수 있도록" 진행 복제 합니다.  
  
    2.  게스트의 소스 컴퓨터 개체 실패 하 고 게스트 복제 확장된 사용 권한을 DSRM 으로부터 보호 하기 위해 네트워크 중복 도메인 컨트롤러에 부팅을 유지 하지 않으면 합니다.  
  
12. AD DS 컴퓨터 개체 이름은 PDCE에 자동으로 생성가 있는 경우에 DCCloneConfig.xml 지정 된 이름이 맞게 설정 됩니다. NTDS 적절 한 Active Directory 논리 사이트에 대 한 정확한 NTDS 설정을 개체를 만듭니다.  
  
    1.  PDC 하는 경우 복제, 다음 게스트 바꾸고 로컬 컴퓨터를 다시 부팅 합니다. 다시 부팅 한 후 다시을 1 ~ 10 단계를 거칩니다 다음 13 단계로 이동 합니다.  
  
    2.  DC 복제 하는 경우이 단계에서 부팅은 복제, 합니다.  
  
13. 게스트 프로 모션 설정을 프로 모션 시작할 DS 역할 서버 서비스를 제공 합니다.  
  
14. DS 역할 서버 서비스 AD DS 관련 서비스 (NTDS, NTFRS/DFSR, KDC, DNS)의 모든 중지 합니다.  
  
15. 게스트 NT5DS 사용 하면 다른 도메인 컨트롤러의 (Windows NTP) 시간 동기화 (기본 Windows 시간 서비스 계층에서 즉 PDCE 사용). 게스트 pdce 합니다. 모든 기존 Kerberos 티켓 플러시입니다.  
  
16. 게스트는 DFSR 또는 NTFRS 서비스 자동으로 실행 되도록 구성 됩니다. 게스트 파일을 삭제 기존 DFSR 및 NTFRS 데이터베이스 (기본: c:\windows\ntfrs 및 c:\system 볼륨 information\dfsr\\*< database_GUID >*) 다음 서비스를 시작할 때의 SYSVOL 신뢰할 수 없는 동기화 하기 위해, 합니다. 게스트는 동기화 나중에 시작 되 면 SYSVOL 미리 시드하기 SYSVOL 파일 내용의 삭제 되지 않습니다.  
  
17. 게스트가 바뀝니다. 게스트 DS 역할 서버 서비스 AD DS 구성 (프로 모션) 기존 NTDS를 사용 하 여 시작 합니다. 프로 모션 일반적으로 비슷함 c:\windows\system32에 포함 된 템플릿 데이터베이스 아니라 소스, DIT 데이터베이스 파일.  
  
18. 게스트 연락처를 새 RID 풀 할당 마스터 FSMO 제거 역할 소유자 합니다.  
  
19. 프로 모션 프로세스는 새로운 호출 ID 만들고 복제 도메인 컨트롤러에 대 한 NTDS 설정을 개체 다시 (복제에 관계 없이 프로 모션 도메인의 일부 기존 NTDS를 사용 하는 경우. DIT 데이터베이스)입니다.  
  
20. 개체 양은 참 누락 된 최신, 또는 파트너 도메인 컨트롤러에서 더 높은 버전에 복제 NTDS 됩니다. NTDS 합니다. DIT 원본 도메인 컨트롤러에, 오프 라인 시간부터 개체에 이미 개인정보와 이용 사용자는 가능한 복제 교통량을 최소화 하려면 인바인드 합니다. 드 파티션은 채워집니다.  
  
21. DFSR 또는 FRS 서비스 시작 하 고 있기 때문 없는 데이터베이스 SYSVOL 비 정식으로 인바인드 복제가 파트너 로부터 동기화 합니다. 이 프로세스는 다시 네트워크 복제 교통량을 최소화 하려면 SYSVOL 폴더의 기존 데이터를 사용 합니다.  
  
22. 게스트 고유 하 게 이름을 지정 하 고 네트워크에 연결 되는 컴퓨터는 이제 DNS 클라이언트 등록을 다시 설정 합니다.  
  
23. 게스트 실행는 DefaultDCCloneAllowList.xml에 지정 된 SYSPREP 모듈 <SysprepInformation> 참조 이전 컴퓨터 이름과 SID를 이동 하려면 요소입니다.  
  
24. 프로 모션 복제 완료 되었습니다.  
  
    1.  게스트는 재부팅할 일반 하므로 DSRM 부팅 플래그를 제거 합니다.  
  
    2.  게스트 읽지 다시 다음 부팅 시 하는 추가 날짜 타임 스탬프도 DCCloneConfig.xml의 이름을 바꿉니다.  
  
    3.  게스트는 VdcIsCloning DWORD 레지스트리 값 이름을 찾아 아래에서 제거 됩니다.  
  
    4.  게스트 설정 "VdcCloningDone" DWORD 0x1 찾아 아래 레지스트리 값 이름입니다. Windows이이 값을 사용 하지 않지만 대신 제 3 자에 대 한 마커로 제공 합니다.  
  
25. 게스트 업데이트에 자체 복제 도메인 컨트롤러 개체 VM 세대 id입니다. 현재 게스트에 맞게를 GenerationID 특성  
  
26. 게스트 다시 시작합니다. 도메인 컨트롤러 광고 일반, 됩니다.  
  
## <a name="BKMK_SafeRestoreArch"></a>가상화 도메인 컨트롤러 안전 복원이 건축물  
  
### <a name="overview"></a>개요  
하이퍼바이저 플랫폼 이라는 식별자를 사용 하 여 광고 DS **VM 세대 ID** 스냅숏을 복원 가상 컴퓨터의 검색. AD DS 값이이 식별자 (NTDS 데이터베이스에 처음 저장. DIT) 도메인 컨트롤러 프로 모션 중입니다. 관리자가 이전 스냅숏을에서 가상 컴퓨터를 복원, VM 세대 ID에서 가상 컴퓨터의 현재 값 데이터베이스에 값 비교 됩니다. 두 개의 값 다른 경우 도메인 컨트롤러 호출 ID를 다시 설정 하 고 USN 다시 사용 하거나 중복 보안 사용자의 잠재적 생성 차단 RID 풀 삭제 합니다. 두 가지 시나리오 안전 복원이 발생할 수 있습니다.  
  
-   종료 되는 동안 스냅숏을 복원 된 후 가상 도메인 컨트롤러를 시작 될 때  
  
-   실행 중인 가상 도메인 컨트롤러에서 스냅숏은 복원 될 때  
  
    가상화 도메인 컨트롤러의 스냅숏 종료 아닌 일시 중단 된 경우 새 RID 풀 요청을 시작 하려면 AD DS 서비스 다시 시작 해야 합니다. 서비스 스냅인를 사용 하 여 Windows PowerShell를 사용 하 여 광고 DS 서비스를 다시 시작할 수 있습니다 (다시 서비스 NTDS-강제로).  
  
다음 섹션 안전 복원이 각 시나리오에 대해 자세히 설명 합니다.  
  
### <a name="safe-restore-detailed-processing"></a>안전 복원이 자세한 처리  
다음 순서도 얼마나 안전 복원이 표시 종료 되는 동안 스냅숏을 복원 된 후 가상 도메인 컨트롤러를 시작 될 때 발생 합니다.  
  
![DC 가상화 건축물](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringNormalBoot.png)  
  
1.  가상 컴퓨터가 부팅 스냅숏 복구 후 때 스냅숏 복원 때문 하이퍼바이저 호스트가 제공 하는 새로운 세대 VM ID 해야 합니다.  
  
2.  가상 컴퓨터에서 새 VM 세대 ID VM 세대 ID 데이터베이스에서 비교 됩니다. 두 개의 Id 일치 하지 않으므로 (이전 섹션에 3 단계 참조) virtualization 보호 기능이 포함 됩니다. 새와 일치 하도록 AD DS 컴퓨터 개체 그에 대 한 설정 VM GenerationID이 업데이트 적용 복원이 완료 한 후 하이퍼바이저 호스트 하 여 ID를 제공 합니다.  
  
3.  게스트 사용 하 여 virtualization 보호:  
  
    1.  로컬 RID 풀을 무효화 됩니다.  
  
    2.  도메인 컨트롤러 데이터베이스에 대 한 새로운 호출 ID로 설정합니다.  
  
> [!NOTE]  
> 안전 복원이의이 부분 겹치는 복제 프로세스입니다. 이 과정 가상 도메인 컨트롤러의 안전 복원이 대 한 되어도 스냅숏을 복원을 수행를 부팅 한 후 복제 프로세스 중 단계를 그대로 수행 합니다.  
  
다음 그림 virtualization 보호 기능 스냅샷을 실행 가상 도메인 컨트롤러에서 복원 될 때 USN 롤백 자가 제시 확산을 방지 하는 방법입니다.  
  
![DC 가상화 건축물](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringSnapShotRestore.png)  
  
> [!NOTE]  
> 위 그림 개념 설명 간단해 집니다.  
  
1.  T 1 시간에 하이퍼바이저 관리자의 스냅숏을 가상 d c 1. 이 이번에 d c 1 USN 값이 (**highestCommittedUsn** 실제로) A의 100, (위의 다이어그램에 ID로 표시 됨) InvocationId 가치 (실제로이 없었다면 GUID). SavedVMGID 값이 dc DIT 파일에 VM GenerationID (이라는 특성에서 DC의 컴퓨터 목표에 대해 저장 **를 GenerationId**). VMGID 지정 된 VM GenerationId 가상 컴퓨터에서 드라이버를 사용할 수입니다. 이 값은 하이퍼바이저 제공 됩니다.  
  
2.  T 2, 나중에이 DC에 100 사용자를 추가 (것이 좋습니다이 DC 사이 수행 수 있는 업데이트가 예를 들어 사용자가 t 1과 t 2 시간, 사용자 작품, 그룹 작품, 암호 업데이트, 특성 업데이트 등과 함께 이러한 업데이트 되지 실제로)입니다. 여기에서 각 업데이트 (하지만 실제로 사용자 작성 개 이상의 USN 소비 수도 있습니다) 고유한 USN 하나를 사용 합니다. 이러한 업데이트를 설정 하기 전에 d c 1 VM GenerationID 값 데이터베이스 (savedVMGID)에서 지정 된 드라이버 (VMGID)에서 사용할 수 있는 것과 동일한 인지 확인 합니다. 어떤 롤백 USN 최대 200는 다음 업데이트가 USN 201 사용 하 여 나타내는으로 이동 하 고 업데이트는 앞으로 아직 발생 했습니다.으로 동일한, 됩니다. 여기은 InvocationId, savedVMGID, 또는 VMGID 변경 되지 않습니다. 이러한 업데이트 d c 2에는 다음 복제 주기 복제 합니다. D c 2 높은 워터 업데이트 (와 **UptoDatenessVector**) 표현 DC1(A)로 간단 하 게 @USN = 200 합니다. 즉, d c 2은 A USN 200부터 InvocationId 컨텍스트가의 d c 1에서 모든 업데이트에 알고 있습니다.  
  
3.  시 T3 t 1 시간 찍은 스냅숏은 d c 1에 적용 됩니다. D c 1 롤백 되었습니다, 그 USN 롤백됩니다 100, 나타내는 101에서 Usn 후속 업데이트와 연결을 사용 하도록 합니다. 그러나이 시점 VMGID 값이 마다 다를 수 VM GenerationID 지원 하이퍼바이저 합니다.  
  
4.  그런 다음, d c 1 모든 업데이트를 수행할 때 수 있는지 확인 (savedVMGID) 데이터베이스에는 VM GenerationId 값 가상 컴퓨터 드라이버 (VMGID)에서 값과 같은 합니다. 이 경우 것 같지 않습니다, d c 1 유추로 롤백, 것이 고; virtualization 세이프 가드를 트리거하 즉, 그 InvocationId을 다시 설정 (ID = B) 하 고 (위의 다이어그램에 표시 되지 않음) RID 풀 삭제 합니다. 그런 다음 새 VMGID 값 데이터베이스에 저장 하 고 새 InvocationId B. 컨텍스트가에서 이러한 업데이트 (USN 101-250) 커밋합니다. 다음 복제 주기 d c 2 알고 아무것도 d c 1에서 InvocationId B의 컨텍스트에서 하므로 InvocationID b 관련 d c 1에서 모든 요청 결과적으로, 스냅숏 적용 된 이후 d c 1에 수행 된 업데이트 수렴 안전 하 게 됩니다. 또한 자녀가 되었던 복제 d c 2 (표시 됨 d c 1 돌아가기 간접 줄 별로) 때문에 다음 예약 된 복제에 d c 1로 다시 (있음 d c 1에서 스냅샷 복원 한 후 손실 된) d c t 2에 1에 수행 된 업데이트 설정 복제 것 합니다.  
  
후 게스트에서 virtualization 세이프 가드를 NTDS 복제 Active Directory 개체 차이점 돌아오는 비 정식으로 파트너 도메인 컨트롤러에서 됩니다. 디렉터리 서비스 대상의 최신 vector 적절 하 게 업데이트 됩니다. 그런 다음 게스트 SYSVOL 동기화 됩니다.  
  
-   FRS을 사용 하는 경우 게스트 NTFRS 서비스 멈추고 d 2 BURFLAGS 레지스트리 값으로 설정 됩니다. 그런 다음 비 정식으로 인바인드를 다시 사용 하 여 기존 바뀌지 SYSVOL 데이터 복제 가능한 경우 NTFRS 서비스를 시작 합니다.  
  
-   게스트 DFSR 서비스를 중지 하 고 DFSR 데이터베이스 파일을 삭제 DFSR를 사용 하는 경우 (기본 위치: %systemroot%\system 볼륨 information\dfsr\\*<database GUID>*). 그런 다음 비 정식으로 인바인드를 다시 사용 하 여 기존 바뀌지 SYSVOL 데이터 복제 가능한 경우 DFSR 서비스를 시작 합니다.  
  
> [!NOTE]  
> -   하이퍼바이저 비교 VM 세대 ID를 제공 하지 않으면, 하이퍼바이저 virtualization 보호 기능을 지원 하지 않습니다 및 Windows Server 2008 R2 실행 하는 가상화 도메인 컨트롤러 등 게스트 운영는 이전 버전입니다. DC 파트너가 보지 마지막 최고 USN 지난 하지 발전 Usn 복제 시작를 시도 하는 경우 게스트 USN 롤백 격리 보호를 구현 합니다. USN 롤백 격리 보호에 대 한 자세한 내용은 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx)  
  


