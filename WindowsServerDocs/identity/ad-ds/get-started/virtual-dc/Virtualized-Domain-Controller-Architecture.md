---
ms.assetid: 341614c6-72c2-444f-8b92-d2663aab7070
title: 가상화된 도메인 컨트롤러 아키텍처
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e8673b9e66a0aa3b6bea89b91ae5022efb26c65c
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323155"
---
# <a name="virtualized-domain-controller-architecture"></a>가상화된 도메인 컨트롤러 아키텍처

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 가상화된 도메인 컨트롤러 복제 및 안전 복원 아키텍처에 대해 알아봅니다. 복제 및 안전 복원 프로세스를 순서도와 함께 표시한 다음 프로세스의 각 단계에 대해 자세히 설명합니다.  
  
-   [가상화 된 도메인 컨트롤러 복제 아키텍처](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)  
  
-   [가상화 된 도메인 컨트롤러 안전 복원 아키텍처](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)  
  
## <a name="BKMK_CloneArch"></a>가상화 된 도메인 컨트롤러 복제 아키텍처  
  
### <a name="overview"></a>개요  
가상화된 도메인 컨트롤러 복제에서는 하이퍼바이저 플랫폼을 기반으로 **VM-Generation ID**라는 식별자를 노출하여 가상 머신 생성을 검색합니다. AD DS는 도메인 컨트롤러의 수준을 올리는 동안 초기에 이 식별자 값을 해당 데이터베이스(NTDS.DIT)에 저장합니다. 가상 컴퓨터를 부팅하면 가상 컴퓨터의 현재 VM-Generation ID 값이 데이터베이스에 있는 값과 비교됩니다. 두 값이 서로 다르면 도메인 컨트롤러에서 호출 ID를 다시 설정하고 RID 풀을 삭제하여 USN이 다시 사용되거나 잠재적으로 중복된 보안 주체가 생성되는 것을 방지합니다. 그런 다음 도메인 컨트롤러는 [복제 세부 처리](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneProcessDetails)의 3단계에 설명된 위치에서 DCCloneConfig.xml 파일을 찾습니다. DCCloneConfig.xml 파일을 찾으면 해당 파일이 복제본으로 배포 중인 것으로 결론을 내리므로 원본 미디어에서 복사한 기존 NTDS.DIT 및 SYSVOL 콘텐츠로 다시 수준을 올려 자체를 추가 도메인 컨트롤러로 프로비전하기 위해 복제를 시작합니다.  
  
VM-GenerationID를 지원하는 하이퍼바이저와 지원하지 않는 하이퍼바이저가 혼합된 환경에서는 VM-GenerationID를 지원하지 않는 하이퍼바이저에 복제 미디어가 실수로 배포될 수 있습니다. DCCloneConfig.xml 파일의 존재는 DC를 복제하기 위한 관리 의도를 나타냅니다. 따라서 부팅 중 DCCloneConfig.xml 파일을 찾았지만 호스트에서 VM-GenerationID가 제공되지 않은 경우 나머지 환경에 미치는 영향을 방지하기 위해 복제 DC가 DSRM(디렉터리 서비스 복원 모드)으로 부팅됩니다. 이후에 복제 미디어를 VM-GenerationID를 지원하는 하이퍼바이저로 이동한 다음 복제를 다시 시도할 수 있습니다.  
  
복제 미디어가 VM-GenerationID를 지원하는 하이퍼바이저에 배포되었지만 DCCloneConfig.xml 파일이 제공되지 않은 경우에는 DC에서 해당 DIT와 새 VM DIT 간의 VM-GenerationID 변경 내용을 검색하여 USN 재사용 및 SID 중복을 방지하기 위한 보호 기능을 트리거합니다. 그러나 복제가 시작되지 않으므로 보조 DC가 원본 DC와 동일한 ID로 계속 실행됩니다. 환경 내 비일관성을 방지하려면 이 보조 DC를 최대한 빨리 네트워크에서 제거해야 합니다. 업데이트가 아웃바운드 복제되는 것을 확인하는 동안 이 두 번째 DC를 회수하는 방법에 대한 자세한 내용은 Microsoft 기술 자료 문서 [2742970](https://support.microsoft.com/kb/2742970)을 참조하세요.  
  
### <a name="BKMK_CloneProcessDetails"></a>복제 세부 처리  
다음 다이어그램에서는 초기 복제 작업 및 복제 다시 시도 작업의 아키텍처를 보여 줍니다. 이러한 프로세스에 대해서는 이 항목의 뒷부분에서 자세히 설명합니다.  
  
**초기 복제 작업**  
  
![가상화 된 DC 아키텍처](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_InitialCloningProcess.png)  
  
**복제 다시 시도 작업**  
  
![가상화 된 DC 아키텍처](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_CloningRetryProcess.png)  
  
이 프로세스의 자세한 단계는 다음과 같습니다.  
  
1.  기존 가상 컴퓨터 도메인 컨트롤러가 VM-Generation ID를 지원하는 하이퍼바이저에서 부팅됩니다.  
  
    1.  이 VM에는 수준 올리기 후 해당 AD DS 컴퓨터 개체에 설정된 기존 VM Generation-ID 값이 없습니다.  
  
    2.  Null인 경우에도 다음 컴퓨터 만들기는 새 VM Generation-ID가 일치하지 않으므로 여전히 복제를 의미합니다.  
  
    3.  VM Generation-ID는 다음에 DC를 다시 부팅한 후 설정되며 복제되지 않습니다.  
  
2.  그런 다음 가상 컴퓨터는 VMGenerationCounter 드라이버에서 제공된 VM-Generation ID를 읽어 VM-Generation ID 두 개를 비교합니다.  
  
    1.  ID가 일치하면 새 가상 컴퓨터가 아니므로 복제가 진행되지 않습니다. DCCloneConfig.xml 파일이 있는 경우 도메인 컨트롤러에서 복제를 방지하기 위해 시간 날짜 스탬프를 사용하여 파일 이름을 바꿉니다. 서버는 계속 정상적으로 부팅됩니다. 가상 도메인 컨트롤러의 모든 다시 부팅은 Windows Server 2012에서 이 방식으로 작동합니다.  
  
    2.  두 ID가 일치하지 않으면 이전 도메인 컨트롤러의 NTDS.DIT가 포함된 새 가상 컴퓨터(또는 복원된 스냅샷)입니다. DCCloneConfig.xml 파일이 있는 경우 도메인 컨트롤러에서 복제 작업을 계속 진행합니다. 파일이 없으면 스냅샷 복원 작업을 계속합니다. [가상화된 도메인 컨트롤러 안전 복원 아키텍처](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)를 참조하세요.  
  
    3.  하이퍼바이저에서 비교를 위한 VM-Generation ID를 제공하지 않지만 DCCloneConfig.xml 파일이 있는 경우, 게스트는 파일 이름을 바꾼 다음 중복 도메인 컨트롤러로부터 네트워크를 보호하기 위해 DSRM로 부팅됩니다. dccloneconfig.xml 파일이 없으면 게스트가 정상적으로 부팅됩니다(이 경우 네트워크에 중복 도메인 컨트롤러가 있을 수 있음). 이 중복 도메인 컨트롤러를 회수하는 방법에 대한 자세한 내용은 Microsoft 기술 자료 문서 [2742970](https://support.microsoft.com/kb/2742970)을 참조하세요.  
  
3.  NTDS 서비스에서 VDCisCloning DWORD 레지스트리 값 이름의 값을 확인합니다(HKEY_Local_Machine\System\CurrentControlSet\Services\Ntds\Parameters).  
  
    1.  값이 없으면 이번이 이 가상 컴퓨터에 대한 첫 번째 복제 시도입니다. 게스트가 로컬 RID 풀을 무효화하고 도메인 컨트롤러의 새 복제 호출 ID를 설정하는 VDC 개체 중복 보호 기능을 구현합니다.  
  
    2.  이미 0x1로 설정되어 있으면 이번이 이전 복제 작업에 실패하여 "다시 시도"하는 복제 시도입니다. VDC 개체 중복 안전 조치는 수행되지 않습니다. 이전에 이미 한 번 실행되었고 게스트를 불필요하게 여러 번 변경하기 때문입니다.  
  
4.  IsClone DWORD 레지스트리 값 이름이 기록됩니다(Hkey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters).  
  
5.  이후 재부팅 시 DS 복구 모드로 시작하도록 NTDS 서비스가 게스트 부팅 플래그를 변경합니다.  
  
6.  NTDS 서비스가 허용된 세 위치(DSA 작업 디렉터리, %windir%\NTDS 또는 드라이브 루트(드라이브 문자 순)의 이동식 읽기/쓰기 미디어) 중 하나에서 DcCloneConfig.xml 파일을 읽으려고 시도합니다.  
  
    1.  올바른 위치에 파일이 없으면 게스트가 IP 주소 중복을 확인합니다. IP 주소가 중복되지 않은 경우 서버가 정상적으로 부팅됩니다. 중복된 IP 주소가 있으면 중복 도메인 컨트롤러로부터 네트워크를 보호하기 위해 컴퓨터가 DSRM으로 부팅됩니다.  
  
    2.  올바른 위치에 파일이 있으면 NTDS 서비스가 해당 설정의 유효성을 검사합니다. 파일 또는 특정 설정이 비어 있으면 NTDS에서 이러한 설정에 대해 자동 값을 구성합니다.  
  
    3.  DcCloneConfig.xml이 있지만 잘못된 항목을 포함하거나 읽을 수 없으면 복제에 실패하고 게스트가 DSRM(디렉터리 서비스 복원 모드)으로 부팅됩니다.  
  
7.  게스트가 실수로 인한 원본 컴퓨터 이름 및 IP 주소의 하이재킹을 방지하기 위해 모든 DNS 자동 등록을 해제합니다.  
  
8.  게스트가 클라이언트의 네트워크 AD DS 요청에 대한 보급 또는 응답을 방지하기 위해 Netlogon 서비스를 중지합니다.  
  
9. NTDS에서 DefaultDCCloneAllowList.xml 또는 CustomDCCloneAllowList.xml의 일부가 아닌 서비스 또는 프로그램이 설치되어 있지 않은지 확인합니다.  
  
    1.  기본 예외 허용 목록 또는 사용자 지정 예외 허용 목록에 없는 서비스 또는 프로그램이 설치되어 있으면 복제에 실패하고 중복 도메인 컨트롤러로부터 네트워크를 보호하기 위해 게스트가 DSRM으로 부팅됩니다.  
  
    2.  비호환성 문제가 없으면 복제가 계속됩니다.  
  
10. DCCloneConfig.xml 네트워크 설정이 비어 있어 자동 IP 주소 지정이 사용되는 경우 게스트는 네트워크 어댑터에서 DHCP를 사용하여 IP 주소 임대, 네트워크 라우팅 및 이름 확인 정보를 가져옵니다.  
  
11. 게스트가 PDC 에뮬레이터 FSMO 역할을 실행하는 도메인 컨트롤러를 찾아 연결합니다. 이때 DNS 및 DCLocator 프로토콜을 사용합니다. RPC 연결을 설정하고 IDL_DRSAddCloneDC 메서드를 호출하여 도메인 컨트롤러 컴퓨터 개체를 복제합니다.  
  
    1.  게스트의 원본 컴퓨터 개체에 "DC가 자신의 복제를 만들도록 허용" 도메인 헤드 확장 권한이 있으면 복제가 계속 진행됩니다.  
  
    2.  게스트의 원본 컴퓨터 개체에 이 확장 권한이 없으면 복제에 실패하고 중복 도메인 컨트롤러로부터 네트워크를 보호하기 위해 게스트가 DSRM으로 부팅됩니다.  
  
12. AD DS 컴퓨터 개체 이름이 DCCloneConfig.xml에 지정되거나 PDCE에 자동으로 생성된 이름과 일치하도록 설정됩니다. NTDS에서는 해당 Active Directory 논리 사이트에 대한 올바른 NTDS 설정 개체를 만듭니다.  
  
    1.  이것이 PDC 복제이면 게스트가 로컬 컴퓨터의 이름을 바꾼 후 다시 부팅됩니다. 다시 부팅 한 후 다시 1-10 단계를 거칩니다 그런 다음 13 단계로 이동 합니다.  
  
    2.  이것이 복제본 DC 복제이면 이 단계에서 다시 부팅되지 않습니다.  
  
13. 게스트가 DS 역할 서버 서비스에 수준 올리기 설정을 제공합니다. 그러면 수준 올리기가 시작됩니다.  
  
14. DS 역할 서버 서비스가 모든 AD DS 관련 서비스(NTDS, NTFRS/DFSR, KDC, DNS)를 중지합니다.  
  
15. 게스트가 다른 도메인 컨트롤러(기본 Windows 시간 서비스 계층에 있는 도메인 컨트롤러이므로 PDCE를 사용함)와의 NT5DS(Windows NTP) 시간 동기화를 강제로 실행합니다. 게스트가 PDCE에 연결하며, 모든 기존 Kerberos 티켓이 플러시됩니다.  
  
16. 게스트가 DFSR 또는 NTFRS 서비스를 자동으로 실행되도록 구성합니다. 모든 기존 DFSR 및 NTFRS 데이터베이스 파일을 삭제 하는 게스트 (기본값: c:\windows\ntfrs and c:\system volume information\dfsr\\ *< database_GUID >* ), 다음 서비스를 시작할 때 SYSVOL의 신뢰할 수 없는 동기화를 강제 합니다. 나중에 동기화가 시작될 때 SYSVOL을 미리 시드하기 위해 게스트는 SYSVOL의 파일 내용은 삭제하지 않습니다.  
  
17. 게스트의 이름이 바뀝니다. 일반적인 수준 올리기에서처럼 c:\windows\system32에 포함된 템플릿 데이터베이스를 사용하는 대신 기존 NTDS.DIT 데이터베이스 파일을 원본으로 사용하여 게스트의 DS 역할 서버 서비스가 AD DS 구성(수준 올리기)을 시작합니다.  
  
18. 게스트가 RID 마스터 FSMO 역할 소유자에 연결하여 새 RID 풀 할당을 가져옵니다.  
  
19. 수준 올리기 프로세스에서 새 호출 ID를 만들고 복제된 도메인 컨트롤러에 대한 NTDS 설정 개체를 다시 만듭니다(이는 복제에 상관없이 기존 NTDS.DIT 데이터베이스를 사용할 때 도메인 수준 올리기의 일부임).  
  
20. NTDS가 파트너 도메인 컨트롤러에서 누락되거나 더 새롭거나 더 상위 버전인 개체에 복제됩니다. 원본 도메인 컨트롤러가 오프라인으로 전환되었을 때부터 NTDS.DIT에 개체가 이미 포함되어 있으므로 인바운드 복제 트래픽을 최소화하기 위해 가능한 한 이러한 개체가 사용됩니다. 글로벌 카탈로그 파티션이 채워집니다.  
  
21. DFSR 또는 FRS 서비스가 시작되며, 데이터베이스가 없기 때문에 복제 파트너에서 SYSVOL이 신뢰할 수 없는 방식으로 인바운드 동기화됩니다. 이 프로세스에서는 네트워크 복제 트래픽을 최소화하기 위해 SYSVOL 폴더의 기존 데이터를 다시 사용합니다.  
  
22. 컴퓨터가 고유하게 이름이 지정되고 네트워크에 연결되어 있으므로 게스트가 DNS 클라이언트 등록을 다시 활성화합니다.  
  
23. 게스트가 이전 컴퓨터 이름 및 SID에 대한 참조를 제거하기 위해 DefaultDCCloneAllowList.xml <SysprepInformation> 요소에 지정된 SYSPREP 모듈을 실행합니다.  
  
24. 복제 수준 올리기가 완료됩니다.  
  
    1.  다음에 정상적으로 다시 부팅되도록 게스트가 DSRM 부팅 플래그를 제거합니다.  
  
    2.  다음 부팅 시 다시 읽지 않도록 게스트가 날짜 시간 스탬프를 추가하여 DCCloneConfig.xml의 이름을 바꿉니다.  
  
    3.  게스트가 HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters 아래에서 VdcIsCloning DWORD 레지스트리 값 이름을 제거합니다.  
  
    4.  게스트가 HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters 아래의 "VdcCloningDone" DWORD 레지스트리 값 이름을 0x1로 설정합니다. Windows에서는 이 값을 사용하지 않고 대신 타사에 대한 마커로 제공합니다.  
  
25. 게스트가 자체 복제된 도메인 컨트롤러 개체의 msDS-GenerationID 특성을 현재 게스트 VM-Generation ID와 일치하도록 업데이트합니다.  
  
26. 게스트가 다시 시작됩니다. 이제 정상적인 보급 도메인 컨트롤러가 되었습니다.  
  
## <a name="BKMK_SafeRestoreArch"></a>가상화 된 도메인 컨트롤러 안전 복원 아키텍처  
  
### <a name="overview"></a>개요  
AD DS에서는 하이퍼바이저 플랫폼을 기반으로 **VM-Generation ID**라는 식별자를 노출하여 가상 머신의 스냅샷 복원을 검색합니다. AD DS는 도메인 컨트롤러의 수준을 올리는 동안 초기에 이 식별자 값을 해당 데이터베이스(NTDS.DIT)에 저장합니다. 관리자가 이전 스냅샷에서 가상 컴퓨터를 복원하면 가상 컴퓨터의 현재 VM-Generation ID 값이 데이터베이스에 있는 값과 비교됩니다. 두 값이 서로 다르면 도메인 컨트롤러에서 호출 ID를 다시 설정하고 RID 풀을 삭제하여 USN이 다시 사용되거나 잠재적으로 중복된 보안 주체가 생성되는 것을 방지합니다. 안전 복원이 발생할 수 있는 다음 두 가지 시나리오가 있습니다.  
  
-   종료되어 있는 동안 스냅샷이 복원된 후 가상 도메인 컨트롤러가 시작된 경우  
  
-   실행 중인 가상 도메인 컨트롤러에서 스냅샷이 복원된 경우  
  
    스냅샷의 가상화된 도메인 컨트롤러가 종료되지 않고 일시 중단된 상태에 있는 경우 새 RID 풀 요청을 트리거하려면 AD DS 서비스를 다시 시작해야 합니다. 서비스 스냅인을 사용하거나 Windows PowerShell(Restart-service NTDS-force)을 사용하여 AD DS 서비스를 다시 시작할 수 있습니다.  
  
다음 섹션에는 각 시나리오의 안전 복원에 대해 자세히 설명합니다.  
  
### <a name="safe-restore-detailed-processing"></a>안전 복원 세부 처리  
다음 순서도에서는 종료되어 있는 동안 스냅샷이 복원된 후 가상 도메인 컨트롤러가 시작된 경우에 안전 복원이 발생하는 방식을 보여 줍니다.  
  
![가상화 된 DC 아키텍처](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringNormalBoot.png)  
  
1.  스냅샷이 복원된 후 가상 컴퓨터가 부팅된 경우 스냅샷 복원으로 인해 하이퍼바이저 호스트에서 새 VM-Generation ID를 제공합니다.  
  
2.  가상 컴퓨터의 새 VM-Generation ID는 데이터베이스에 있는 VM-Generation ID와 비교됩니다. 두 ID는 일치하지 않으므로 가상화 세이프가드(이전 섹션의 3단계 참조)가 사용됩니다. 복원에서 적용이 완료되면 해당 AD DS 컴퓨터 개체에 설정된 VM-GenerationID가 하이퍼바이저 호스트에서 제공한 새 ID와 일치하도록 업데이트됩니다.  
  
3.  게스트에서 다음을 통해 가상화 안전 조치를 적용합니다.  
  
    1.  로컬 RID 풀 무효화  
  
    2.  도메인 컨트롤러 데이터베이스에 대한 새 호출 ID 설정  
  
> [!NOTE]  
> 안전 복원의 이 부분은 복제 프로세스와 겹칩니다. 이 프로세스는 가상 도메인 컨트롤러의 안전 복원에 대한 프로세스이지만 스냅샷이 복원된 다음 부팅된 후에는 복제 프로세스 중에 동일한 단계가 발생합니다.  
  
다음 다이어그램에서는 실행 중인 가상 도메인 컨트롤러에서 스냅샷이 복원된 경우 가상화 안전 조치가 USN 롤백으로 인한 확산을 방지하는 방법을 보여 줍니다.  
  
![가상화 된 DC 아키텍처](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringSnapShotRestore.png)  
  
> [!NOTE]  
> 위 그림은 개념을 설명하기 위해 간소화된 것입니다.  
  
1.  T1 시점에 하이퍼바이저 관리자는 가상 DC1의 스냅샷을 만듭니다. 이 시점에 DC1의 USN 값(실제로는**highestCommittedUsn** )은 100이고, InvocationId(위 다이어그램에 ID로 표시) 값은 A(실제로는 GUID일 수 있음)입니다. savedVMGID 값은 DC의 DIT 파일에 있는 VM-GenerationID입니다(DC 컴퓨터 개체에 대해 **msDS-GenerationId**특성에 저장됨). VMGID는 가상 컴퓨터 드라이버에서 사용할 수 있는 VM-GenerationId의 현재 값입니다. 이 값은 하이퍼바이저에서 제공됩니다.  
  
2.  나중에 T2 시점에 100명의 사용자가 이 DC에 추가됩니다. 사용자를 T1과 T2 사이에 이 DC에서 수행되었을 수 있는 업데이트의 예로 간주하면 됩니다. 이러한 업데이트에는 실제로 사용자 만들기, 그룹 만들기, 암호 업데이트, 특성 업데이트 등이 혼합될 수 있습니다. 이 예에서는 각 업데이트에서 하나의 고유한 USN(실제로는 사용자 만들기에 둘 이상의 USN이 사용될 수 있음)을 사용합니다. 이러한 업데이트를 커밋하기 전에 DC1에서 해당 데이터베이스에 있는 VM-GenerationID 값(savedVMGID)이 드라이버에서 사용할 수 있는 현재 값(VMGID)과 일치하는지 확인합니다. 아직 롤백이 발생하지 않아 두 값이 동일하므로 업데이트가 커밋되고 USN이 200까지 이동합니다. 이는 다음 업데이트에서 USN 201을 사용할 수 있음을 나타냅니다. InvocationId, savedVMGID 또는 VMGID는 변경되지 않습니다. 이러한 업데이트는 다음 복제 주기에서 DC2에 복제됩니다. D c 1은 단순히 DC1 (A) @USN = 200으로 표시 된 상위 워터 마크 (및 **UptoDatenessVector**)를 업데이트 합니다. 즉, DC2는 InvocationId A 컨텍스트에서 USN 200까지 DC1의 모든 업데이트를 인식합니다.  
  
3.  T3 시점에는 T1 시점에 생성된 스냅샷이 DC1에 적용됩니다. DC1이 롤백되었으므로 해당 USN이 100으로 롤백됩니다. 이는 101부터 USN을 사용하여 후속 업데이트와 연결할 수 있음을 나타냅니다. 그러나 이 시점에서는 VMGID 값이 VM-GenerationID를 지원하는 하이퍼바이저의 값과 다를 수 있습니다.  
  
4.  이후에 DC1은 업데이트를 수행할 때 해당 데이터베이스에 있는 VM-GenerationId 값(savedVMGID)이 가상 컴퓨터 드라이버의 값(VMGID)과 동일한지 확인합니다. 이 예에서는 같지 않으므로 DC1은 이를 롤백을 암시하는 것으로 추론하여 가상화 안전 조치를 트리거합니다. 즉, 해당 InvocationId(ID = B)를 다시 설정하고 RID 풀(위 다이어그램에는 표시되지 않음)을 삭제합니다. 그런 다음, 해당 데이터베이스에 새 VMGID 값을 저장 하 고 새 InvocationId B.의 컨텍스트에서 이러한 업데이트 (USN 101-250) 커밋 다음 복제 주기에 DC2를 인식 하지 못하므로 DC1에서 InvocationId B의 컨텍스트에서 없으므로 모든 InvocationID B에 연결 하는 DC1에서 요청 따라서 스냅샷 적용 후 DC1에서 수행된 업데이트가 안전하게 수렴합니다. 또한 T2에 DC1에서 수행된 업데이트 집합(스냅샷 복원 후 DC1에서 손실된)은 DC2에 복제되었으므로 예정된 다음 복제 시 DC1에 다시 복제됩니다(DC1에 다시 연결된 점선으로 표시).  
  
게스트에서 가상화 안전 조치를 적용한 후 NTDS는 파트너 도메인 컨트롤러에서 신뢰할 수 없는 방식으로 Active Directory 개체 차이점을 인바운드로 복제합니다. 대상 디렉터리 서비스의 최신 벡터가 이에 따라 업데이트된 다음 게스트에서 SYSVOL을 동기화합니다.  
  
-   FRS를 사용하는 경우 게스트는 NTFRS 서비스를 중지하고 D2 BURFLAGS 레지스트리 값을 설정합니다. 그런 다음 가능한 경우 변경되지 않은 기존 SYSVOL 데이터를 다시 사용하여 신뢰할 수 없는 방식으로 인바운드 복제를 수행하는 NTFRS 서비스를 시작합니다.  
  
-   DFSR를 사용 하는 게스트 DFSR 서비스를 중지 하 고 DFSR 데이터베이스 파일 삭제 (기본 위치: %systemroot%\system volume information\dfsr\\ *<database GUID>* ). 그런 다음 가능한 경우 변경되지 않은 기존 SYSVOL 데이터를 다시 사용하여 신뢰할 수 없는 방식으로 인바운드 복제를 수행하는 DFSR 서비스를 시작합니다.  
  
> [!NOTE]  
> -   하이퍼바이저에서 비교할 수 있는 VM-Generation ID를 제공하지 않는 경우에는 하이퍼바이저에서 가상화 안전 조치를 지원하지 않으므로 게스트가 Windows Server 2008 R2 이하를 실행하는 가상화된 도메인 컨트롤러처럼 작동합니다. 게스트는 파트너 DC에서 마지막으로 확인한 가장 높은 USN을 초과하지 않은 USN으로 복제를 시작하려는 시도가 있는 경우 USN 롤백 격리 보호를 구현합니다. USN 롤백 격리 보호에 대 한 자세한 내용은 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx)  
  


