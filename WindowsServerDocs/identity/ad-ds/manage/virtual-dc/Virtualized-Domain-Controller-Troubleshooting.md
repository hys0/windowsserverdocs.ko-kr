---
ms.assetid: 249ba1be-b0d3-4a77-99af-3699074a2b6e
title: "가상화 도메인 컨트롤러 문제 해결"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 63f96e7a3035bc25f7a7a349acb6bf26f62a2a3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-troubleshooting"></a>가상화 도메인 컨트롤러 문제 해결

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 가상화 도메인 컨트롤러 기능 문제 해결 대 방법을 자세히 설명 합니다.  
  
-   [도메인 컨트롤러 복제 가상화 문제 해결](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootVDCCloning)  
  
-   [가상화 도메인 컨트롤러 안전 복원이 문제 해결](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootVDCSafeRestore)  
  
## <a name="BKMK_Intro"></a>소개  
문제 해결는 기술을 향상 하는 가장 중요 한 방법은 빌드를 테스트 랩 이며 엄격한 일반 작동 시나리오를 검사 합니다. 오류가 발생 하면 더 명확 하 고 다음 도메인 컨트롤러 프로 모션의 작동 방식을 배웁니다 있는 이후 이해 하기 쉽게 됩니다. 또한 빌드 분석 및 네트워크 분석 기술을 수도 있습니다. 이렇게만 가상화 된 도메인 컨트롤러 배포 모든 분산된 시스템 기술에 대 한 이동합니다.  
  
도메인 컨트롤러 구성 고급 문제 해결에 중요 한 요소는 다음과 같습니다.  
  
1.  포커스가 및 세부 사항에 주의 선형 분석 결합 합니다.  
  
2.  네트워크 캡처 분석을 이해합니다.  
  
3.  기본 제공 로그 이해  
  
이 항목의 세 번째 범위를 벗어나는 1과 2은 몇 가지 자세히 설명 될 수 있습니다. 가상화 도메인 컨트롤러 문제 해결을 논리 선형 방법은 필요합니다. 제공 되는 데이터를 사용 하 여 문제에 접근 하만 방식을 복잡 한 도구 및 분석 제공 된 출력 및 로깅 모든 때 키가입니다.  
  
## <a name="BKMK_TshootVDCCloning"></a>도메인 컨트롤러 복제 가상화 문제 해결  
이 섹션 커버:  
  
-   [문제 해결 도구](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_Tools)  
  
-   [로그인 옵션](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_LoggingOptions)  
  
-   [도메인 문제 해결에 대 한 일반 방법론 컨트롤러 복제](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_GeneralMethodology)  
  
-   [서버 Core 및 이벤트 로그](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_ServerCoreEvents)  
  
-   [특정 문제 해결](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_SpecificProblems)  
  
문제 해결 전략 가상화 도메인 컨트롤러 복제할이 일반 포맷 다음과 같습니다.  
  
![가상 dc 문제 해결](media/Virtualized-Domain-Controller-Troubleshooting/ADDS_VDC_TroublehsootingFlowchart.png)  
  
### <a name="BKMK_Tools"></a>문제 해결 도구  
  
#### <a name="BKMK_LoggingOptions"></a>로그인 옵션  
로그 기본 제공 되는 도메인 컨트롤러 복제 문제 해결에 대 한 가장 중요 한 도구입니다. 모든 이러한 로그 활성화 되어 최대 세부 정보 표시 기본적으로 구성 됩니다.  
  
|||  
|-|-|  
|**작업**|**로그**|  
|**복제**|이벤트 viewer\Windows logs\System<br />이벤트 viewer\Applications 및 서비스 logs\Directory 서비스<br />-%systemroot%\debug\dcpromo.log|  
|**프로 모션**|-%systemroot%\debug\dcpromo.log<br />이벤트 viewer\Applications 및 서비스 logs\Directory 서비스<br />이벤트 viewer\Windows logs\System<br />이벤트 viewer\Applications 및 서비스 logs\File 복제 서비스<br />이벤트 viewer\Applications 및 서비스 logs\DFS 복제|  
  
#### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>도구 및 도메인 컨트롤러 구성 문제 해결에 대 한 명령  
로그에 설명 되어 있지 문제를 해결 하려면 다음 도구를 사용 하 여 시작 지점으로 다음과 같습니다.  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   네트워크 3.4 모니터  
  
### <a name="BKMK_GeneralMethodology"></a>도메인 문제 해결에 대 한 일반 방법론 컨트롤러 복제  
  
1.  VM DS 수리 모드 (DSRM)에 부팅? 이 문제 해결이 필요한 나타냅니다. 사용 하 여 DSRM에 로그온 할 **. \Administrator** 계정 및 DSRM 암호를 지정 합니다.  
  
    1.  검사는 나타나면 Dcpromo.log 합니다.  
  
        1.  특정 위치 복제 초기 단계 성공 하지만 도메인 컨트롤러 프로 모션 실패?  
  
        2.  PDC 에뮬레이터에서 돌아왔습니다 오류와 같은 오류 로컬 도메인 컨트롤러 또는 광고 DS 환경을 사용 하 여 문제를 나타냅니다 수행?  
  
    2.  시스템 및 디렉터리 서비스 이벤트 로그 dccloneconfig.xml와 CustomDCCloneAllowList.xml 검사  
  
        1.  호환 되지 않는 응용 프로그램은 CustomDCCloneAllowList.xml에 필요한 허용 목록?  
  
        2.  IP 주소 또는 컴퓨터 이름을 중복 또는 dccloneconfig.xml에서 잘못 된 인가요?  
  
        3.  유효 하지 Active Directory 사이트는 dccloneconfig.xml에 있나요?  
  
        4.  IP 주소에서에서 설정 되지 않은 dccloningconfig.xml 및 DHCP 서버가 없는?  
  
        5.  온라인과 RPC 프로토콜을 통해 사용 가능한 PDC 에뮬레이터 인가요?  
  
        6.  도메인 컨트롤러 복제할 수 도메인 컨트롤러 그룹의 회원 인지 확인 합니다. 사용 권한은입니다 **DC 자체 복제를 만들 수 있도록** 도메인 루트 해당 그룹에 대 한 설정 하나요?  
  
        7.  Dccloneconfig.xml 파일 올바른 구문 분석 함으로써 구문을 오류의 포함 되어 있습니까?  
  
        8.  하이퍼바이저 지원  
  
        9. 복제 성공적으로 시작 된 후 도메인 컨트롤러 프로 모션 실패 했나요?  
  
        10. 최대 수를 초과 자동으로 생성 도메인 컨트롤러 이름 (9999) 웠 나요?  
  
        11. MAC 주소 중복  
  
2.  DC 소스와 동일 복제 호스트 이름을 인가요?  
  
    1.  허용 되는 위치 중 하나에 Dccloneconfig.xml 파일은?  
  
3.  표준 모드로 부팅 VM 및 완료 되 면 복제 이지만 도메인 컨트롤러 제대로 작동 하지 않는?  
  
    1.  호스트 이름이 복제에 변경 되는 경우 먼저 확인 합니다. 호스트 이름이 다른 경우 복제 완료 최소한 일부 라도 했습니다.  
  
    2.  도메인 컨트롤러에서 dccloneconfig.xml, 소스 도메인 컨트롤러의 중복 IP 주소를 있는 했지만 원본 도메인 컨트롤러 오프 라인 복제 하는 동안?  
  
    3.  도메인 컨트롤러를 광고 하면 문제를 복제 없이 열어야 일반 이후 프로 모션 문제가 있는지으로 처리 합니다.  
  
    4.  도메인 컨트롤러 알리지 않습니다 이후 프로 모션 오류에 대 한 디렉터리 서비스, 시스템, 응용 프로그램, 파일 복제 및 Dfs 이벤트 로그를 검사 합니다.  
  
#### <a name="disabling-dsrm-boot"></a>DSRM 부팅을 해제  
에 부팅 DSRM 모든 오류로 인해 원인을 오류를 진단 하 고는 나타나면 dcpromo.log는 복제 다시 시도할 수 없는, 나타내지는지 않습니다 경우 오류 원인을 해결 DSRM 플래그 초기화 합니다. 다시 부팅 하면; 자체적으로 실패 복제 표준 모드를 반환 하지 않는 다시 복제 시도 하기 위해 DS 복원 모드 부팅 플래그를 제거 해야 합니다. 이러한 단계를 모두 권한 관리자 권한으로 실행을 해야합니다.  
  
##### <a name="removing-dsrm-with-msconfigexe"></a>Msconfig.exe와 DSRM 제거  
시스템 구성 도구를 사용 하 GUI 부팅 DSRM를 설정 하려면:  
  
1.  Msconfig.exe 실행  
  
2.  에 **부팅** 탭의 **부팅 옵션**을 선택 취소 **안전 부팅** (이미 옵션을 선택 되어 **Active Directory 복구** 사용 하도록 설정)  
  
3.  확인을 클릭 하 고 메시지가 표시 되 면를 다시 시작  
  
##### <a name="removing-dsrm-with-bcdeditexe"></a>Bcdedit.exe와 DSRM 제거  
을 해제 하려면 DSRM 부팅 명령줄에서 부팅 구성 데이터 저장소 편집기를 사용 하 여 다음과 같습니다.  
  
1.  확인 하 고 실행 CMD를 엽니다.  
  
    ```  
    Bcdedit.exe /deletevalue safeboot  
    ```  
  
2.  사용 하 여 컴퓨터를 다시 시작 합니다.  
  
    ```  
    Shutdown.exe /t /0 /r  
    ```  
  
> [!NOTE]  
> Windows PowerShell 콘솔 Bcdedit.exe 에서도 작동합니다. 여기 명령은 다음과 같습니다.  
>   
> Bcdedit.exe /deletevalue safeboot  
>   
> 컴퓨터를 다시 시작  
  
### <a name="BKMK_ServerCoreEvents"></a>서버 Core 및 이벤트 로그  
이벤트 로그 가상화 도메인 컨트롤러 복제 작업에 대 한 유용한 정보 많이 포함 되어 있습니다. 기본적으로 Windows Server 2012 컴퓨터 설치 없는 그래픽 인터페이스 및 따라서 로컬 이벤트 뷰어 스냅인 실행할 수 있는 방법이 없습니다입니다 서버 Core 설치를는 합니다.  
  
이벤트 로그 서버 Core 설치를 실행 하는 서버를 검토 합니다.  
  
-   로컬에서 Wevtutil.exe 도구를 실행  
  
-   PowerShell cmdlet Get WinEvent 로컬로 실행  
  
-   Windows 방화벽 고급 규칙 인바인드 통신할 수 있도록 "원격 이벤트 로그 관리" 그룹 (또는 해당 포트)을 사용 하는 경우 원격으로 Eventvwr.exe, wevtutil.exe, 또는 Winevent 다운로드를 사용 하 여 이벤트 로그 관리할 수 있습니다. 이 Windows PowerShell 3.0에서 NETSH.exe, 그룹 정책 또는 새 설정 NetFirewallRule cmdlet 사용 하 여 서버 Core 설치에서 수행할 수 있습니다.  
  
> [!WARNING]  
> DSRM에 있는 동안 그래픽 셸 컴퓨터를 다시 추가 하지 마십시오. Windows 서비스 (CBS) 스택 DSRM 또는 안전 모드에서 올바르게 작동할 수 없습니다. 추가 기능 또는 DSRM에 있는 동안 역할을 시도 하지 완료 되 고 일반적으로 부팅 될 때까지 불안정에서 컴퓨터를 종료 합니다. 가상화 도메인 컨트롤러 복제본 DSRM에서 일반적으로 부팅할 수 없거나 대부분의 경우 일반적으로 부팅 되지 해야 할 때문에 안전 하 게 그래픽 셸을 추가할 수지 않습니다. 그렇게 지원 되지 않으며 사용할 수 없는 서버를 남길 수 있습니다.  
  
### <a name="BKMK_SpecificProblems"></a>특정 문제 해결  
  
#### <a name="events"></a>이벤트  
모든 가상화 도메인 컨트롤러 복제 이벤트 VM 복제본 도메인 컨트롤러의 디렉터리 서비스 이벤트 로그에 기록 됩니다. 응용 프로그램, 파일 복제 서비스 및 Dfs 이벤트 로그 실패 복제 하는 데 유용한 문제 해결 정보를 포함할 수도 있습니다. PDC로 RPC 호출 하는 동안 오류 PDC 에뮬레이터 이벤트 로그에서 찾아보실 수 있습니다.  
  
디렉터리 서비스 이벤트 로그 노트 및 오류에 대 한 제안 된 해상도에서 Windows Server 2012 복제 특정 이벤트 다음과 같습니다.  
  
##### <a name="directory-services-event-log"></a>디렉터리 서비스 이벤트 로그  
  
|||  
|-|-|  
|**이벤트 ID**|**2160**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|로컬 * <COMPUTERNAME> * 구성 파일 복제 가상 도메인 컨트롤러를 발견 했습니다.<br /><br />구성 파일 복제 가상 도메인 컨트롤러에서 찾아보실은: %1<br /><br />가상 도메인 컨트롤러 복제 구성 파일이 있는지 로컬 가상 도메인 컨트롤러 다른 가상 도메인 컨트롤러의 복제본 나타냅니다. * <COMPUTERNAME> * 복제 자체에 시작 됩니다.|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다. 작업 디렉터리 DSA, %systemroot%\ntds 및 루트 dcclconeconfig.xml 파일에 대 한 모든 로컬 또는 이동식 디스크를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2161**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|로컬 * <COMPUTERNAME> * 구성 파일 복제 가상 도메인 컨트롤러 찾을 수 없습니다. 로컬 컴퓨터 복제 DC 아닙니다.|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다. 작업 디렉터리 DSA, %systemroot%\ntds 및 루트 dcclconeconfig.xml 파일에 대 한 모든 로컬 또는 이동식 디스크를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2162**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|가상 도메인 컨트롤러 복제 실패 했습니다.<br /><br />시스템 이벤트 로그와 시도 복제 가상 도메인 컨트롤러에 해당 하는 오류에 대 한 자세한 내용은 %systemroot%\debug\dcpromo.log 로그인 이벤트를 확인 하세요.<br /><br />오류 코드: %1|  
|**노트 및 해결 방법**|이 오류 메시지 지침 따르고는을 해결 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2163**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|DsRoleSvc 서비스 복제 로컬 가상 도메인 컨트롤러를 시작 했습니다.|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다. 작업 디렉터리 DSA, %systemroot%\ntds 및 루트 dcclconeconfig.xml 파일에 대 한 모든 로컬 또는 이동식 디스크를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2164**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*로컬 가상 도메인 컨트롤러 복제할 DsRoleSvc 서비스를 시작 하지 못했습니다.|  
|**노트 및 해결 방법**|(DsRoleSvc) DS 역할 서버 서비스에 대 한 서비스 설정을 검사 하 고 해당 시작 유형 수동으로 설정 되어 있는지 확인 합니다. 제 3 자 프로그램이이 서비스를 시작 하지 못하는을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2165**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*로컬 가상 도메인 컨트롤러의 복제 하는 동안 스레드를 시작할 수 없습니다.<br /><br />오류 코드: 1%<br /><br />오류 메시지: %2<br /><br />스레드에서 이름: 3%|  
|**노트 및 해결 방법**|Microsoft 고객 지원에 문의|  
  
|||  
|-|-|  
|**이벤트 ID**|**2166**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*RPCSS 서비스를 DSRM로 다시 부팅 해야 합니다. 실패 실행 상태로 초기화 하는 RPCSS 기다리고 있습니다.<br /><br />오류 코드: 1%|  
|**노트 및 해결 방법**|시스템 이벤트 로그 및 서비스 설정을 RPC 서버 서비스 (Rpcss)에 대 한 확인|  
  
|||  
|-|-|  
|**이벤트 ID**|**2167**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*가상 도메인 컨트롤러 지식을 초기화할 수 없습니다. 자세한 내용은 이전 로그 항목을 참조 하십시오.<br /><br />추가 데이터<br /><br />오류 코드: 1%|  
|**노트 및 해결 방법**|이 오류 메시지 지침 따르고는을 해결 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2168**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|Microsoft에서 Windows-ActiveDirectory_DomainService<br /><br />DC 지원된 하이퍼바이저에서 실행 되 고 있습니다. VM 세대 ID는 검색 합니다.<br /><br />현재 값 VM 세대 id: %1|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2169**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|ID가 없습니다 VM 세대 감지 합니다. DC 실제 컴퓨터, Hyper-v의 하위 수준 버전 또는 id. VM 세대를 지원 하지 않는 하이퍼바이저 호스트<br /><br />추가 데이터<br /><br />오류 코드를 생성 VM id: 1% 검사할 때는 반환|  
|**노트 및 해결 방법**|성공 이벤트 복제 하는 경우입니다. 그렇지 않은 경우, 시스템 이벤트 로그를 검사 하 고 하이퍼바이저 제품 지원 문서 검토 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2170**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|경고|  
|**메시지**|ID를 생성 변경 발견 되었습니다.<br /><br />DS (이전 값)에 캐시 세대 ID: 1%<br /><br />현재 VM (새 값)에서 생성 ID: %2<br /><br />ID를 생성 변경 가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다. *<COMPUTERNAME>*도메인 컨트롤러 복구 새 호출 ID를 만듭니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 지원 되는 방법을 복원 하려면 또는 롤백 Active Directory 도메인 서비스 데이터베이스의 콘텐츠 백업을 복원 하는 시스템 상태 된 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여입니다.|  
|**노트 및 해결 방법**|성공 이벤트를 복제 경우입니다. 그렇지 않은 경우, 시스템 이벤트 로그를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2171**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|ID를 생성 변경 되지 발견 되었습니다.<br /><br />DS (이전 값)에 캐시 세대 ID: 1%<br /><br />현재 VM (새 값)에서 생성 ID: %2|  
|**노트 및 해결 방법**|성공 이벤트를 복제 하는 경우이 가상화 DC 재부팅할에서 표시 해야 합니다. 그렇지 않은 경우, 시스템 이벤트 로그를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2172**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성을 읽어보세요.<br /><br />GenerationId 특성 값: %1|  
|**노트 및 해결 방법**|성공 이벤트를 복제 경우입니다. 그렇지 않은 경우, 시스템 이벤트 로그를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2173**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성 읽기 하지 못했습니다. 데이터베이스 트랜잭션이 실패 하 여 발생할 수 있습니다 또는 생성 id 로컬 데이터베이스에 존재 하지 않습니다. GenerationId dcpromo 또는 DC 가상 도메인 컨트롤러 않습니다 후 처음으로 다시 부팅 하는 동안 존재 하지 않습니다.<br /><br />추가 데이터<br /><br />오류 코드: 1%|  
|**노트 및 해결 방법**|성공 이벤트를 복제 경우 이며 복제 완료 된 후 처음으로 VM 다시 부팅 되기 합니다. 또한 가상 도메인 컨트롤러에서 무시할 수 있습니다. 그렇지 않은 경우, 시스템 이벤트 로그를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2174**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|DC 가상 도메인 컨트롤러 복제본 아니고 복원된 가상 도메인 컨트롤러 스냅숏을 아닙니다.|  
|**노트 및 해결 방법**|성공 이벤트 복제 하는 경우입니다. 그렇지 않은 경우, 시스템 이벤트 로그를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2175**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|지원 되지 않는 플랫폼에서 가상 도메인 컨트롤러 복제 구성 파일이 있습니다.|  
|**노트 및 해결 방법**|이 dccloneconfig.xml 찾았지만 VM 세대 ID를 찾을 수, 실제 컴퓨터 또는 VM 세대 ID를 지원 하지 않는 하이퍼바이저 dccloneconfig.xml 파일이 있으면 때와 같은 때 발생|  
  
|||  
|-|-|  
|**이벤트 ID**|**2176**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|가상 도메인 컨트롤러 복제 구성 파일의 이름을 변경 합니다.<br /><br />추가 데이터<br /><br />오래 된 파일 이름을: %1<br /><br />새 파일 이름: %2|  
|**노트 및 해결 방법**|이름 바꾸기 VM 생성 ID 변경 되지 않은 때문에, 백업 소스 VM 부팅할 때 예상 합니다. 원본 도메인 컨트롤러를에서 복제 하려고 수 없습니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2177**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|가상 도메인 컨트롤러 복제 구성 파일의 이름을 변경 하지 못했습니다.<br /><br />추가 데이터<br /><br />파일 이름: 1%<br /><br />오류 코드: %%32|  
|**노트 및 해결 방법**|VM 세대 ID 변경 되지 않은 때문에, 백업 소스 VM 부팅할 때 예상 시도를 이름을 바꿉니다. 원본 도메인 컨트롤러를에서 복제 하려고 수 없습니다. 파일 이름을 바꾸고 설치 된 제 3 자 제품에 파일 이름 바꾸기 하지 못하게 조사 수동으로 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2178**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|가상 도메인 컨트롤러 복제 구성 파일을 감지 있지만 VM 세대 ID 변경 되지 않았습니다. 로컬 DC 복제 원본 DC입니다. 복제 구성 파일을 이름을 바꿉니다.|  
|**노트 및 해결 방법**|VM 세대 ID 변경 되지 않은 때문에 VM 소스를 다시 부팅 하는 경우 필요 합니다. 원본 도메인 컨트롤러를에서 복제 하려고 수 없습니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2179**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성 다음 매개 변수를 설정 했습니다.<br /><br />GenerationID 특성: 1%|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2180**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|경고|  
|**메시지**|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성을 설정 하지 못했습니다.<br /><br />추가 데이터<br /><br />오류 코드: 1%|  
|**노트 및 해결 방법**|시스템 이벤트 로그 및 나타나면 Dcpromo.log 검사 합니다. 특정 오류 MS TechNet, MS 기술 및 MS 블로그 각 평소 상태를 확인 하 고 다음 문제 해결을 조회 이러한 결과에 따라 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2182**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|내부 이벤트: 디렉터리 서비스 원격 DSA 복제 하 라는 메시지가 표시 되었습니다.|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2183**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|내부 이벤트: * <COMPUTERNAME> * 원격 디렉터리 시스템 에이전트 복제할 요청을 완료 합니다.<br /><br />원래 DC 이름: %3<br /><br />DC 이름: %4 복제 요청<br /><br />DC 사이트: %5 복제 요청<br /><br />추가 데이터<br /><br />오류: % 값 1 %2|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2184**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*복제 DC에 대 한 도메인 컨트롤러 계정을 만들 수 없습니다.<br /><br />원래 DC 이름: %1<br /><br />2 복제 % 수가 허용된<br /><br />복제 하 여 생성할 수 있는 도메인 컨트롤러 계정 수를 제한 * <COMPUTERNAME> *초과 되었습니다.|  
|**노트 및 해결 방법**|자동으로 원천 도메인 컨트롤러 이름을 이름이 규칙에 따라 도메인 컨트롤러는 내리는 하지 않을 경우 9999 시간을 생성할 수 있습니다. 사용 하 여는 <computername> 요소 xml 다른 이름의 DC에서 새 고유한 이름을 또는 복제 생성할 수 있습니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2191**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*DNS 업데이트를 사용 하지 않도록 설정 하려면 다음 레지스트리 값을 설정 합니다.<br /><br />레지스트리 키: 1%<br /><br />레지스트리 가치: %2<br /><br />레지스트리 가치 데이터: %3<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다. 복제 완료 된 후 복제 프로세스 DNS 업데이트를 다시 사용 됩니다.|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2192**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*DNS 업데이트를 사용 하지 않도록 설정 하려면 다음 레지스트리 값 설정 하지 못했습니다.<br /><br />레지스트리 키: 1%<br /><br />레지스트리 가치: %2<br /><br />레지스트리 가치 데이터: %3<br /><br />오류 코드: %4<br /><br />오류 메시지: %5<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다.|  
|**노트 및 해결 방법**|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 레지스트리 업데이트를 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2193**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*다음 레지스트리 값 DNS 업데이트를 사용 하도록 설정 합니다.<br /><br />레지스트리 키: 1%<br /><br />레지스트리 가치: %2<br /><br />레지스트리 가치 데이터: %3<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다.|  
|**노트 및 해결 방법**|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2194**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*다음 레지스트리 값 DNS 업데이트를 사용 하도록 설정 하지 못했습니다.<br /><br />레지스트리 키: 1%<br /><br />레지스트리 가치: %2<br /><br />레지스트리 가치 데이터: %3<br /><br />오류 코드: %4<br /><br />오류 메시지: %5<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다.|  
|**노트 및 해결 방법**|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 레지스트리 업데이트를 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2195**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|DSRM 부팅 설정 하지 못했습니다.<br /><br />오류 코드: 1%<br /><br />오류 메시지: %2<br /><br />실패 가상 도메인 컨트롤러 복제 하지 않거나 경우 가상 도메인 컨트롤러 복제 구성 파일에서 지원 되지 않는 하이퍼바이저 문제 해결을 위해 로컬 컴퓨터 DSRM로 다시 부팅 됩니다. 설정 DSRM 부팅 실패 했습니다.|  
|**노트 및 해결 방법**|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 레지스트리 업데이트를 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2196**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|종료 권한을 사용할 수 없습니다.<br /><br />오류 코드: 1%<br /><br />오류 메시지: %2<br /><br />실패 가상 도메인 컨트롤러 복제 하지 않거나 경우 가상 도메인 컨트롤러 복제 구성 파일에서 지원 되지 않는 하이퍼바이저 문제 해결을 위해 로컬 컴퓨터 DSRM로 다시 부팅 됩니다. 종료 권한을 사용 하지 못했습니다.|  
|**노트 및 해결 방법**|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 사용 권한을 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2197**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|시스템 종료 시작 하지 못했습니다.<br /><br />오류 코드: 1%<br /><br />오류 메시지: %2<br /><br />실패 가상 도메인 컨트롤러 복제 하지 않거나 경우 가상 도메인 컨트롤러 복제 구성 파일에서 지원 되지 않는 하이퍼바이저 문제 해결을 위해 로컬 컴퓨터 DSRM로 다시 부팅 됩니다. 시작 시스템을 종료 하지 못했습니다.|  
|**노트 및 해결 방법**|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 사용 권한을 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2198**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*만들거나 다음 복제 DC 개체 수정 하지 못했습니다.<br /><br />추가 데이터.<br /><br />개체:<br /><br />%1<br /><br />오류 값: %2<br /><br />%3|  
|**노트 및 해결 방법**|특정 오류 MS TechNet, MS 기술 및 MS 블로그 각 평소 상태를 확인 하 고 다음 문제 해결을 조회 이러한 결과에 따라 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2199**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*개체 이미 있기 때문에 다음과 같은 복제 DC 개체를 만들 수 없습니다.<br /><br />추가 데이터.<br /><br />소스 DC 다음과 같습니다.<br /><br />%1<br /><br />개체:<br /><br />%2|  
|**노트 및 해결 방법**|유효성 검사는 dccloneconfig.xml 기존 도메인 컨트롤러를 지정 하지 않은 또는 이름 편집 하지 않고는 dccloneconfig.xml 복사본 복제본 여러 개에서 사용 되지 했습니다. 관리자는 수준을. 올린 결정 충돌 예상 아직 없는 경우 기존 도메인 컨트롤러를 내릴 수 해야 하는 경우에 대해 토론 연락할 기존 도메인 컨트롤러 메타 데이터 청소 복제 다른 이름을 사용 해야 하는 경우 또는 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2203**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|마지막 가상 도메인 컨트롤러 복제 실패 했습니다. 이것은 처음으로 다시 부팅 후 다음 이므로이 해야 하는 복제 다시 시도 합니다. 그러나 두 가상 도메인 컨트롤러 복제 구성 파일이 없으면 되거나 세대 ID 변경 가상 컴퓨터에서 감지 되 합니다. 부팅 DSRM에 있습니다.<br /><br />마지막 가상 도메인 컨트롤러 복제 실패: 1%<br /><br />가상 도메인 컨트롤러 복제 구성 파일이 있는지 다음과 %2<br /><br />가상 컴퓨터 생성 ID 변경 검색: %3|  
|**노트 및 해결 방법**|하는 경우 손실 되거나 잘못 된 dccloneconfig.xml으로 인해 이전에 실패 복제 필요 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|2210|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|<COMPUTERNAME> 복제본 도메인 컨트롤러에 대 한 개체 만들 수 없습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %6<br /><br />복제본 도메인 컨트롤러 이름: %1<br /><br />다시 시도 루프: %2<br /><br />예외 값: %3<br /><br />오류 값: %4<br /><br />DSID: %5|  
|노트 및 해결 방법|시스템 및 디렉터리 서비스 이벤트 로그 및에 대 한 자세한 내용은 복제 실패 한 이유 나타나면 dcpromo.log 검토 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|2211|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제본 도메인 컨트롤러에 대 한 개체 만들었습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %3<br /><br />복제본 도메인 컨트롤러 이름: %1<br /><br />다시 시도 루프: %2|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2212|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 시작 복제 도메인 컨트롤러에 대 한 개체를 만들 수 있습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />복제 이름: %2<br /><br />복제 사이트: %3<br /><br />RODC 복제: %4|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2213|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 읽기 전용 도메인 컨트롤러 복제에 대 한 새로운 KrbTgt 개체를 만들었습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />새 KrbTgt 개체 Guid: %2|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2214|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 컴퓨터 개체를 복제 도메인 컨트롤러를 만듭니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />원래 도메인 컨트롤러: %2<br /><br />복제본 도메인 컨트롤러: %3|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2215|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 여기에서 복제 도메인 컨트롤러를 추가 합니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />사이트: %2|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2216|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제본 도메인 컨트롤러 서버 컨테이너를 만듭니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />서버 컨테이너: %2|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2217|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제본 도메인 컨트롤러 서버 개체를 만듭니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />서버 개체: %2|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2218|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제본 도메인 컨트롤러에 대 한 NTDS 설정을 개체를 만듭니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />개체: %2|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2219|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제 읽기 전용 도메인 컨트롤러에 대 한 연결 개체 만듭니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2220|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제 읽기 전용 도메인 컨트롤러에 대 한 SYSVOL 개체 만듭니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2221|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|<COMPUTERNAME> 복제 도메인 컨트롤러에 대해 임의의 암호를 생성 하지 않습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />복제본 도메인 컨트롤러 이름: %2<br /><br />오류: %3%4|  
|노트 및 해결 방법|검사 시스템 이벤트에 대 한 자세한 내용은 이유 컴퓨터 계정 암호를 만들 수 없습니다.|  
  
|||  
|-|-|  
|이벤트 ID|2222|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|<COMPUTERNAME> 복제 도메인 컨트롤러에 대 한 암호를 설정 하지 못했습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />복제본 도메인 컨트롤러 이름: %2<br /><br />오류: %3%4|  
|노트 및 해결 방법|검사 시스템 이벤트에 대 한 자세한 내용은 이유 컴퓨터 계정 암호 설정할 수 없습니다.|  
  
|||  
|-|-|  
|이벤트 ID|2223|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|<COMPUTERNAME> 복제 도메인 컨트롤러에 대 한 컴퓨터 계정 암호를 설정 했습니다.<br /><br />추가 데이터.<br /><br />Id 복제: %1<br /><br />복제본 도메인 컨트롤러 이름: %2<br /><br />다시 시도 번 총: %3|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2224|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 실패 했습니다. 관리 서비스 계정 복제 컴퓨터에 있는 다음 %1 다음과 같습니다.<br /><br />%2<br /><br />성공 하려면 복제 모든 관리 서비스 계정 제거 해야 합니다. 이 작업은 제거 ADComputerServiceAccount PowerShell cmdlet 사용 합니다.|  
|노트 및 해결 방법|독립 실행형 Msa를 사용 하는 경우 필요 합니다 (MSA 그룹화 할). 수행 *하지* 제대로 작성 되지-계정을 제거 하려면 이벤트 조언을 따릅니다. Use Uninstall-AdServiceAccount - [https://technet.microsoft.com/library/hh852310](https://technet.microsoft.com/library/hh852310).<br /><br />-Windows Server 2008 R2에 처음 릴리스-독립 실행형 Msa 그룹 Msa (gMSA)와 Windows Server 2012에서 바뀌었습니다. GMSAs 복제를 지원 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|2225|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|알림|  
|메시지|캐시 된 비밀 다음 보안 사용자의 로컬 도메인 컨트롤러에서 제거 되었습니다.<br /><br />%1<br /><br />읽기 전용 도메인 컨트롤러 복제, 후 비밀 복제 소스 읽기 전용 도메인 컨트롤러에서 이전에 캐시 된는 복제 도메인 컨트롤러에서 제거 됩니다.|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|2226|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|캐시 된 비밀 다음 보안 사용자의 로컬 도메인 컨트롤러에서 제거할 수 없습니다.<br /><br />%1<br /><br />오류: %2 (3%)<br /><br />읽기 전용 도메인 컨트롤러의 경우 암호는 이전에 공격자 도난 되거나 손상 복제에서 해당 자격 증명을 가져올 수 있도록 위험 감소를 위해 복제에 제거할 복제 소스 읽기 전용 도메인 컨트롤러 필요에 캐시 된 복제 한 후. 보안 사용자 매우 권한이 있는 계정이 고 공격 으로부터 보호 해야 rootDSE 작업 rODCPurgeAccount 수동으로 로컬 도메인 컨트롤러에는 암호를 지우려면 사용 하십시오.|  
|노트 및 해결 방법|시스템 및 디렉터리 서비스 이벤트 로그 대 한 자세한 내용은 검사 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|2227|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|예외는 로컬 도메인 컨트롤러에서 캐시 비밀 정보를 제거 하는 동안 발생 합니다.<br /><br />추가 데이터.<br /><br />예외 값: %1<br /><br />오류 값: %2<br /><br />DSID: %3<br /><br />읽기 전용 도메인 컨트롤러의 경우 암호는 이전에 공격자 도난 되거나 손상 복제에서 해당 자격 증명을 가져올 수 있도록 위험 감소를 위해 복제에 제거할 복제 소스 읽기 전용 도메인 컨트롤러 필요에 캐시 된 복제 한 후. 매우 권한이 있는 계정 보안 사용자 다음 중 하나 공격 으로부터 보호 해야 하는 경우 수동으로 로컬 도메인 컨트롤러에는 암호를 지우려면 rootDSE 작업 rODCPurgeAccount 사용 하십시오.|  
|노트 및 해결 방법|시스템 및 디렉터리 서비스 이벤트 로그 대 한 자세한 내용은 검사 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|2228|  
|원본|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|심각도|오류|  
|메시지|가상 컴퓨터 생성 ID이 도메인 컨트롤러의 Active Directory 데이터베이스에는이 가상 컴퓨터의 현재 값 다릅니다. 그러나 가상 도메인 컨트롤러 복제 구성 파일 (DCCloneConfig.xml) 찾을 수 없습니다 하므로 도메인 컨트롤러 복제을 시도 하지 않았습니다. 작업 복제 하는 도메인 컨트롤러를 사용 하는 경우에 DCCloneConfig.xml 지원 되는 위치 중 하나에 제공 되 확인 하십시오. 또한,이 도메인 컨트롤러의 IP 주소 다른 도메인 컨트롤러의 IP 주소 충돌합니다. 서비스 중단 없이 발생 되도록 도메인 컨트롤러 구성 된 DSRM에 부팅을 합니다.<br /><br />추가 데이터.<br /><br />중복 IP 주소: %1|  
|노트 및 해결 방법|이 보호 장치 (예를 들어 DHCP를 사용 하 여 때가 아니라는) 가능한 경우 중복 도메인 컨트롤러를 중지 합니다. 유효한 DcCloneConfig.xml 파일을 추가, DSRM 플래그 제거 및 복제을 다시 시도|  
  
|||  
|-|-|  
|이벤트 ID|29218|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 실패 했습니다. 복제 도메인 컨트롤러에 DSRM 디렉터리 서비스 복원 모드 ()을 다시 부팅 된 및 복제 작업을 완료할 수 없습니다.<br /><br />하세요 확인 이전에 기록 이벤트와 일치 하는 오류에 대 한 자세한 내용은 %systemroot%\debug\dcpromo.log 가상 도메인 컨트롤러 복제 시도 하 고 여부이 복제 이미지를 다시 사용할 수 있습니다.<br /><br />하나 또는 여러 개의 로그 항목 복제 프로세스 다시 시도할 수 없는 경우, 이미지 안전 하 게 삭제 해야 합니다. 그렇지 않으면 수 오류를 수정, DSRM 부팅 지우기 있으며; 정상적으로 다시 부팅 재부팅 복제 작업을 다시 시도 합니다.|  
|노트 및 해결 방법|시스템 및 디렉터리 서비스 이벤트 로그 및에 대 한 자세한 내용은 복제 실패 한 이유 나타나면 dcpromo.log 검토 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29219|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|알림|  
|메시지|가상 도메인 컨트롤러 복제 했습니다.|  
|노트 및 해결 방법|예기치 않은 경우 성공 이벤트 및 있는 문제입니다.|  
  
|||  
|-|-|  
|이벤트 ID|29248|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 Winlogon 알림 얻는 하지 못했습니다. 반환된 오류 코드는 %1 (%2) 1입니다.<br /><br />이 오류에 대 한 자세한 내용은 시도 복제 가상 도메인 컨트롤러에 해당 하는 오류에 대 한 %systemroot%\debug\dcpromo.log을 검토 하십시오.|  
|노트 및 해결 방법|Microsoft 고객 지원에 문의|  
  
|||  
|-|-|  
|이벤트 ID|29249|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 가상 도메인 컨트롤러 구성 파일을 구문 하지 못했습니다.<br /><br />반환된 HRESULT 코드 %1입니다.<br /><br />구성 파일이: %2<br /><br />구성 파일에서 오류를 수정 하 고 복제 다시 시도 하세요.<br /><br />이 오류에 대 한 자세한 내용은 %systemroot%\debug\dcpromo.log 참조 하세요.|  
|노트 및 해결 방법|XML 편집기를 사용 하 여 구문 오류에 대 한 dclconeconfig.xml 파일 및 DCCloneConfigSchema.xsd 스키마 파일을 검사 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29250|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 실패 했습니다. 소프트웨어는 또는 가상 도메인 컨트롤러 복제 허용된 응용 프로그램 목록에서 복제 가상 도메인 컨트롤러에서 현재 사용 되는 서비스를 제공 하지 합니다.<br /><br />다음 누락 된 항목은 다음과 같습니다.<br /><br />%2<br /><br />(있는 경우) %1 정의 포함 목록 사용 했습니다.<br /><br />비 복제 가능한 응용 프로그램이 설치 되어 있는 경우 복제 작업을 완료할 수 없습니다.<br /><br />Active Directory PowerShell Cmdlet 다운로드-ADDCCloningExcludedApplicationList 응용 프로그램은 복제 컴퓨터에 설치 되어 있지만 허용 목록에 포함 되지 않은 확인을 실행 하 고 가상 도메인 컨트롤러 복제와 호환 되는 경우 허용 목록에 추가 합니다. 가상 도메인 컨트롤러 복제와 호환 되지 않는 응용 프로그램이 있는 경우 다시 복제 작업 시도 하기 전에 제거 하세요.<br /><br />복제 프로세스 가상 도메인 컨트롤러 파일을 검색 허용된 응용 프로그램 목록, CustomDCCloneAllowList.xml, 다음 검색 순서;에 따라 첫 번째 파일을 찾을 수 사용 되 고 다른 모든 무시 됩니다.<br /><br />1. 레지스트리 값 이름: HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters\AllowListFolder<br /><br />2 DSA 작업 디렉터리 폴더가 있는 같은 디렉터리.<br /><br />3입니다. %windir%\NTDS<br /><br />4. 순 루트 드라이브의 드라이브 문자가의 읽기/쓰기 이동식 미디어|  
|노트 및 해결 방법|메시지 지침을 따릅니다.|  
  
|||  
|-|-|  
|이벤트 ID|29251|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 복제 컴퓨터의 IP 주소를 다시 설정 하지 못했습니다.<br /><br />반환된 오류 코드는 %1 (%2) 1입니다.<br /><br />이 오류가 발생 하 여 잘못 가상 도메인 컨트롤러 구성 파일의 네트워크 구성 섹션에서 발생할 수 있습니다.<br /><br />%Systemroot%\debug\dcpromo.log IP 주소 가상 도메인 컨트롤러 시도 복제 하는 동안 초기화에 해당 하는 오류에 대 한 자세한 내용은 참조 하세요.<br /><br />Details on resetting machine IP addresses on the cloned machine can be found at https://go.microsoft.com/fwlink/?LinkId=208030|  
|노트 및 해결 방법|IP 정보는 dccloneconfig.xml에 명시 된 유효 하며, 원래 소스 컴퓨터 중복 되지 확인 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29253|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 실패 했습니다. 복제본 도메인 컨트롤러 주 도메인 컨트롤러 (PDC) 작업 마스터 복제 컴퓨터의 홈 도메인 복제 된 컴퓨터에서 찾을 수 없습니다.<br /><br />반환된 오류 코드는 %1 (%2) 1입니다.<br /><br />하세요 복제 컴퓨터의 홈 도메인 주 도메인 컨트롤러 라이브 도메인 컨트롤러에 할당, 온라인 상태를 확인 작동 합니다. 필요한 포트 및 프로토콜 복제 기계 주 도메인 컨트롤러에 LDAP/RPC 연결 되어 있는지 확인 합니다.|  
|노트 및 해결 방법|복제 도메인 컨트롤러 IP의 유효성을 검사 하 고 DNS 정보 설정 됩니다. Dcdiag.exe /test:locatorcheck PDCE 온라인 상태 이면의 유효성을 검사를 사용 하 여, Nltest.exe 누르고를 사용 하 여:* <PDCE> * /dclist:* <domain> * 유효한 RPC에 실패 복제 하는 동안 PDCE에서 네트워크 캡처를 가져와 하 고 교통량 분석 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29254|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 %1 주 도메인 컨트롤러에 연결 하지 않습니다.<br /><br />반환된 오류 코드는 %2 (%3) 2입니다.<br /><br />주 도메인 컨트롤러 %1 온라인 작동를 확인 하세요. 필요한 포트 및 프로토콜 복제 기계 주 도메인 컨트롤러에 LDAP/RPC 연결 되어 있는지 확인 합니다.|  
|노트 및 해결 방법|복제 도메인 컨트롤러 IP의 유효성을 검사 하 고 DNS 정보 설정 됩니다. Dcdiag.exe /test:locatorcheck PDCE 온라인 상태 이면의 유효성을 검사를 사용 하 여, Nltest.exe 누르고를 사용 하 여:* <PDCE> * /dclist:* <domain> * 유효한 RPC에 실패 복제 하는 동안 PDCE에서 네트워크 캡처를 가져와 하 고 교통량 분석 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29255|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 실패 했습니다.<br /><br />개체를 만드는 복제 이미지에 필요한 %1 주 도메인 컨트롤러에서 오류를 반환 %2 (3%).<br /><br />복제 도메인 컨트롤러 복제 자체 권한이 있는지 확인 하세요. 디렉터리 서비스 이벤트 로그 %1 주 도메인 컨트롤러에 관련된 이벤트를 확인 합니다.|  
|노트 및 해결 방법|특정 오류 MS TechNet, MS 기술 및 MS 블로그 각 일반적인 상태를 확인 하 고 다음 문제 해결을 조회 이러한 결과에 따라 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29256|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|%1 오류 코드 디렉터리 서비스 복원 모드 플래그에 부팅을 설정할 수 없습니다.<br /><br />%Systemroot%\debug\dcpromo.log 오류에 대 한 자세한 내용은 참조 하세요.|  
|노트 및 해결 방법|디렉터리 서비스 로그 및 대 한 자세한 내용은 나타나면 dcpromo.log 검사 합니다. 이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 사용 권한을 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29257|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 종료 했습니다. %1 오류 코드 컴퓨터를 다시 부팅 하지 못했습니다.<br /><br />복제 작업을 완료 하려면 컴퓨터를 다시 부팅 하세요.|  
|노트 및 해결 방법|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 사용 권한을 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29264|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|디렉터리 서비스 복원 모드 플래그에 부팅을 지우려면 %1 오류 코드 없습니다.<br /><br />%Systemroot%\debug\dcpromo.log 오류에 대 한 자세한 내용은 참조 하세요.|  
|노트 및 해결 방법|디렉터리 서비스 로그 및 대 한 자세한 내용은 나타나면 dcpromo.log 검사 합니다. 이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 사용 권한을 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|이벤트 ID|29265|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|알림|  
|메시지|가상 도메인 컨트롤러 복제 했습니다. 가상 도메인 컨트롤러 복제 구성 파일 %1%2 이름이 변경 되었습니다.|  
|노트 및 해결 방법|해당 없음, 성공 이벤트입니다.|  
  
|||  
|-|-|  
|이벤트 ID|29266|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 했습니다. 오류 코드 (3%) %2 가상 도메인 컨트롤러 복제 구성 파일의 이름을 바꾸려면 %1 시도가 실패 했습니다.|  
|노트 및 해결 방법|수동으로 dccloneconfig.xml 파일을 이름을 바꿉니다.|  
  
|||  
|-|-|  
|이벤트 ID|29267|  
|원본|Microsoft Windows-위해-DSROLE-서버|  
|심각도|오류|  
|메시지|가상 도메인 컨트롤러 복제 가상 도메인 컨트롤러 복제 허용 응용 프로그램 목록을 확인 하려면 하지 못했습니다.<br /><br />반환된 오류 코드는 %1 (%2) 1입니다.<br /><br />이 오류가 발생할 수 있습니다 구문을 사용 하 여 복제에 오류가 허용 목록 파일 (현재 체크 파일은: 3%). 이 오류에 대 한 자세한 내용은 %systemroot%\debug\dcpromo.log 참조 하세요.|  
|노트 및 해결 방법|이벤트 지침을 따릅니다.|  
  
##### <a name="error-messages"></a>오류 메시지  
실패 한 가상화 도메인 컨트롤러 복제;에 대 한 직접 대화형 오류가 시스템에서 기록 모든 복제 정보 및 디렉터리 서비스를 기록 하 고 도메인 컨트롤러 프로 모션 나타나면 dcpromo.log에서 기록 합니다. 그러나 서버가 DS 복원 모드로 부팅 하는 경우 조사 즉시 프로 모션 또는 복제 실패 했습니다.  
  
나타나면 dcpromo.log 오류 복제 확인 하는 첫 번째 곳입니다. 나열 된 오류를 따라 디렉터리 서비스 및 진단 추가 대 한 시스템 로그 이후에 검토 해야 할 수도 있습니다.  
  
#### <a name="known-issues-and-support-scenarios"></a>알려진된 문제 및 지원 시나리오  
Windows Server 2012 개발 과정에서 나타납니다 일반적인 문제는 다음과 같습니다. 이러한 문제의 모든 "으로 설계" 되 고 유효한 해결 또는 더 적합 한 기술 처음부터 되지 않도록 합니다. 일부 최신 버전의 Windows Server 2012에서 확인할 수 있습니다.  
  
|||  
|-|-|  
|**문제**|**복제 DSRM 실패**|  
|**증상이**|디렉터리 서비스 복원 모드 복제 부팅|  
|**해상도 및 노트**|섹션 가상화 도메인 컨트롤러 배포 섹션의 다음 단계를 모두 확인 하 고 [도메인 컨트롤러 복제 문제 해결에 대 한 일반 방법](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_GeneralMethodology)<br /><br />KB 2742844 설명합니다.|  
  
|||  
|-|-|  
|**문제**|**DHCP를 사용 하 여을 복제할 때 추가 IP 임대**|  
|**증상이**|DHCP를 사용 하 여 성공적으로 DC 복제을 후 복사본의 첫 번째 부팅 DHCP 임대를 걸립니다. 그런 다음 서버는 이름이 변경 하 고 DC로 다시 시작을 두 번째 DHCP 임대가 됩니다. 첫 번째 IP 주소 해제 되지 않는다 하 고 "알 수 없는" 임대와 결국|  
|**해상도 및 노트**|직접 dhcp에서 사용 되지 않은 주소 임대 삭제 하거나 정상적으로 만료 될 수 있도록 합니다. KB 2742836 설명합니다.|  
  
|||  
|-|-|  
|**문제**|**오랜 시간이 지난 후에 DSRM 복제 실패**|  
|**증상이**|일시 중지 것 이므로 복제 "은 도메인 컨트롤러 복제 X에 % 완료"에 대 한 8과 15 분 합니다. 이 후 복제 실패 하 고 DSRM 부팅 합니다.|  
|**해상도 및 노트**|복제 컴퓨터 중복 IP 주소를 사용 하는 또는 PDC 찾을 수 없는 DHCP 또는 SLAAC, 동적 IP 주소를 받을 수 없습니다. 여러 재시도 복제 수행한 지연 시킬 수 있습니다. 복제 수 있도록 네트워킹 문제를 해결 합니다.<br /><br />KB 2742844 설명합니다.|  
  
|||  
|-|-|  
|**문제**|**복제 서비스의 모든 사용자 이름 다시 하지 않는**|  
|**증상이**|*3 부* 서비스 사용자 이름 SPN ()는 모두 포트 NetBIOS 이름 및 포트를 않고도 그렇지 않은 경우 동일한 NetBIOS 이름, 비 포트 항목 새 컴퓨터 이름으로 다시 않습니다. 예를 들어:<br /><br />customspn / DC1:200 app1 잘못 기호를 사용 하는 / *새 컴퓨터 이름을 다시이*<br /><br />customspn/d c 1/app1 잘못 기호 사용 *새 컴퓨터 이름으로 다시 않습니다이*<br /><br />포트에 관계 없이 세 부분 Spn, 다시 및 정식된 이름 만들어집니다. 예를 들어, 이러한 만들어집니다 성공적으로 복제에 다음과 같습니다.<br /><br />customspn DC1:202 잘못 기호를 사용 하는 / *다시이*<br /><br />customspn/d c 1 잘못 사용 OF 기호 *다시이*<br /><br />잘못 된 기호 사용 customspn/DC1.corp.contoso.com:202 *이 다시 이름*<br /><br />잘못 된 기호 사용 customspn/DC1.corp.contoso.com *다시이*|  
|**해상도 및 노트**|이 복제 뿐만 아니라, Windows에서 도메인 컨트롤러 이름 바꾸기 프로세스에 대 한 제한 됩니다. 모든 시나리오의 이름 바꾸기 논리가에서 3 부 SPN 처리 하지 않습니다. 가장 포함 된 Windows 서비스 필요에 따라 누락 된 Spn 다시 것 처럼, 영향을 받지 않습니다. 다른 응용 프로그램이 문제를 해결 하려면 SPN를 수동으로 입력 해야 합니다.<br /><br />KB 2742874 설명합니다.|  
  
|||  
|-|-|  
|**문제**|**일반 네트워킹 오류 DSRM으로 부팅 실패를 복제**|  
|**증상이**|디렉터리 서비스 복구 모드로 복제 부팅 됩니다. 오류 네트워킹 일반 가지가 있습니다.|  
|해상도 및 노트|새 복제 중복 고정 MAC 주소를; 원본 도메인 컨트롤러에서 할당 받은 하지 않았는지 확인 VM 원본과 복제 가상 컴퓨터에 대 한 하이퍼바이저 호스트에서이 명령을 실행 하 여 고정 MAC 주소를 사용 하는 경우 확인할 수 있습니다.<br /><br />Get VM VMName *테스트 vm* & #124; Get VMNetworkAdapter & #124; fl *<br /><br />MAC 주소 고정 고유한 주소를 변경 하거나 동적 MAC 주소를 사용 하 여으로 전환 합니다.<br /><br />Kb 2742844 설명|  
  
|||  
|-|-|  
|**문제**|**원본 DC 중복 DSRM으로 부팅 실패를 복제**|  
|**증상이**|새로운 복제 복제 없이 부팅 합니다. dccloneconfig.xml 바뀌지 하 고 서버 DS 복원 모드로 시작 합니다. 디렉터리 서비스 이벤트 로그 오류 2164 표시<br /><br />*<COMPUTERNAME>*로컬 가상 도메인 컨트롤러 복제할 DsRoleSvc 서비스를 시작 하지 못했습니다.|  
|**해상도 및 노트**|(DsRoleSvc) DS 역할 서버 서비스에 대 한 서비스 설정을 검사 하 고 해당 시작 유형 수동으로 설정 되어 있는지 확인 합니다. 제 3 자 프로그램이이 서비스를 시작 하지 못하는을 확인 합니다.<br /><br />이 보조 DC 업데이트 아웃 바운드 복제는 하면서 확보 하는 방법에 대 한 자세한 내용은 Microsoft 기술 자료 2742970 참조 합니다.|  
  
|||  
|-|-|  
|**문제**|**오류 8610 DSRM, 부팅 실패 복제,**|  
|**증상이**|디렉터리 서비스 복원 모드 복제 부팅 됩니다. Dcpromo.log (있는 ERROR_DS_ROLE_NOT_VERIFIED 8610 나 0x21A2) 8610 오류가 표시|  
|**해상도 및 노트**|PDC 검색할 수 있도록 하지만 계정 차단은 자체 역할의 하 수 있도록 복제 충분 하지 수행한 경우 부과 됩니다. 예를 들어 복제 시작 되 고 다른 관리자가 PDCE FSMO 역할 새 DC로 이동 합니다.<br /><br />KB 2742916 설명합니다.|  
  
|||  
|-|-|  
|**문제**|**일반 네트워킹 오류 DSRM으로 부팅 실패를 복제**|  
|**증상이**|디렉터리 서비스 복원 모드 복제 부팅 됩니다. 오류 네트워킹 일반 가지가 있습니다.|  
|**해상도 및 노트**|새 복제 중복 고정 MAC 주소를; 원본 도메인 컨트롤러에서 할당 받은 하지 않았는지 확인 VM 원본과 복제 가상 컴퓨터에 대 한 Hyper-v 호스트에서이 명령을 실행 하 여 고정 MAC 주소를 사용 하는 경우 확인할 수 있습니다.<br /><br />Get VM VMName *테스트 vm* & #124; Get VMNetworkAdapter & #124; fl *<br /><br />MAC 주소 고정 고유한 주소를 변경 하거나 동적 MAC 주소를 사용 하 여으로 전환 합니다.<br /><br />KB 2742844 설명합니다.|  
  
|||  
|-|-|  
|**문제**|**DSRM로 부팅 실패를 복제**|  
|**증상이**|디렉터리 서비스 수리 모드로 부팅 복제|  
|**해상도 및 노트**|dccloneconfig.xml 스키마 정의가 포함 되어 있는지 확인 (선 2 sampledccloneconfig.xml 참조).<br /><br />**< d3c:DCCloneConfig xmlns:d3c="uri:microsoft.com:schemas:DCCloneConfig" >**<br /><br />Kb 2742844 설명|  
  
|||  
|-|-|  
|문제|**로그온 서버가 DSRM에 로그인 하는 사용할 수 있는 오류**|  
|**증상이**|디렉터리 서비스 복구 모드로 복제 부팅 됩니다. 로그온 하 고 오류가 하려고 합니다.<br /><br />**현재는 로그온 서버가 로그인 요청을 처리 하는 데 사용할 수 있는**|  
|**해상도 및 노트**|DSRM 관리자 계정과 도메인 계정을 사용 하 여 로그온 있는지 확인 합니다. 왼쪽된 화살표를 사용 하 여 및 사용자 이름을 입력 합니다.<br /><br />**. \administrator**<br /><br />Kb 2742908 설명|  
  
|||  
|-|-|  
|**문제**|**오류 DSRM에 복제 원본 실패**|  
|**증상이**|복제 하는 동안 오류가 발생 하면 8437 "복제 DC 개체 만들기 PDC 실패 에서" (0x20f5)|  
|**해상도 및 노트**|중복 컴퓨터 이름은 DC 또는 기존 DC 원본으로 DCCloneConfig.xml에서 설정 했습니다. 컴퓨터 이름 NetBIOS 컴퓨터 이름 형식 (15 자, FQDN 하지)에 필요 합니다.<br /><br />유효한 고유한 이름을 설정 하 여 dccloneconfig.xml 파일을 해결 합니다.<br /><br />Kb 2742959 설명|  
  
|||  
|-|-|  
|**문제**|**새 addccloneconfigfile 오류 "범위 아웃 된"**|  
|**증상이**|새 addccloneconfigfile cmdlet을 실행 하는 오류를 메시지가 나타납니다.<br /><br />인덱스 범위 아웃 했습니다. 또는 양의 컬렉션의 크기 보다 해야 합니다.|  
|**해상도 및 노트**|관리자 권한이 Windows PowerShell 콘솔에서 cmdlet을 실행 해야 합니다. 이 오류는 컴퓨터에서 로컬 관리자가 그룹 구성원 부족 인해 발생 합니다.<br /><br />Kb 2742927 설명|  
  
|||  
|-|-|  
|**문제**|**복제 중복 DC 실패**|  
|**증상이**|원본 DC 기존 중복 복제 없이 복제 부팅|  
|**해상도 및 노트**|컴퓨터 복사 된 및 시작 있지만 DcCloneConfig.xml 파일 지원 되는 위치에 포함 되어 있지 않습니다 하 고 원본 도메인 컨트롤러와 중복 IP 주소를 없었습니다. DC는 데이터 손실을 방지 하려면 올바르게 제거 해야 합니다.<br /><br />Kb 2742970 설명|  
  
|||  
|-|-|  
|**문제**|**새 ADDCCloneConfigFile 실패 GC 사용할 수 없는 경우 원본 도메인 컨트롤러 복제할 수 도메인 컨트롤러 그룹의 회원은 경우 검사 서버를 없는 작동 오류가 발생 합니다.**|  
|**증상이**|새로 만들기 ADDCCloneConfigFile dccloneconfig.xml 파일을 만들을 실행 하는 오류를 메시지가 나타납니다.<br /><br />코드-서버 작동 하지 않습니다.|  
|**해상도 및 노트**|새로 만들기 ADDCCloneConfigFile를 실행 하 고 해당 gc 복제할 수 도메인 컨트롤러 그룹에 소스 도메인 컨트롤러의 회원 복제 되었는지 확인 서버에서는 gc 연결을 확인 합니다.<br /><br />경우에 위치 GC 또는 DC 수 있는 되었습니다 오프 라인 최근에 대 한 DC locator 캐시 플러시 하는 수단으로 다음 명령을 실행 합니다.<br /><br />코드-nltest /dsgetdc: /GC /FORCE|  
  
### <a name="advanced-troubleshooting"></a>고급 문제 해결  
이 모듈을 사용 하 여 고급 문제 해결을 학습 하는 방법을 찾습니다 *작동* 로그 샘플 발생 한 문제 중 몇 가지 설명 합니다. 성공 가상화 도메인 컨트롤러 작업을 같이 이해 하는 경우 오류 귀하의 환경에 확실 한 됩니다. 이러한 로그의 오름차순와 해당 소스 하 여 표시 되 *예상* 각 로그 내 복제 도메인 컨트롤러 관련 된 이벤트 (된 경우 경고 하 고 오류).  
  
#### <a name="cloning-a-domain-controller"></a>도메인 컨트롤러 복제  
여기에서 복제본 도메인 컨트롤러 DHCP를 사용 하 여 IP 주소, SYSVOL 복제 FRS 또는 DFSR 사용 하 여 (참조 적절 한 로그 필요에 따라), 글로벌 카탈로그 이며 빈 dccloneconfig.xml 파일을 사용 합니다.  
  
##### <a name="directory-services-event-log"></a>디렉터리 서비스 이벤트 로그  
디렉터리 서비스 로그 대부분의 이벤트 기반 복제 운영 정보가 포함 되어 있습니다. 하이퍼바이저 VM 세대 ID를 변경 하 고 NTDS 서비스 것 메모, 다음 RID 풀 무효화 호출 ID 변경 새로운 세대 VM ID가 설정 하 고 서버 복제 데이터 돌아오는 Active Directory. DFSR 서비스가 중단 되 고 신뢰할 수 없는 동기화 강제로 SYSVOL 호스트 하는 데이터베이스 삭제 됩니다 인바인드 합니다. USN 높은 워터 조정 됩니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**2160**|ActiveDirectory_DomainService|로컬 Active Directory 도메인 서비스 가상 도메인 컨트롤러 복제 구성 파일을 발견 했습니다.<br /><br />가상 도메인 컨트롤러 복제 구성 파일을 찾을 다음과 같습니다.<br /><br />*<path>*\DCCloneConfig.xml<br /><br />가상 도메인 컨트롤러 복제 구성 파일이 있는지 로컬 가상 도메인 컨트롤러 다른 가상 도메인 컨트롤러의 복제본 나타냅니다. Active Directory 도메인 서비스 복제 자체에 시작 됩니다.|  
|**2191**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 DNS 업데이트를 사용 하지 않도록 설정 하려면 다음 레지스트리 값을 설정 합니다.<br /><br />레지스트리 키:<br /><br />SYSTEM\CurrentControlSet\Services\Netlogon\Parameters<br /><br />레지스트리 값:<br /><br />UseDynamicDns<br /><br />레지스트리 값 데이터.<br /><br />0<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다. 복제 완료 된 후 복제 프로세스 DNS 업데이트를 다시 사용 됩니다.|  
|**2191**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 DNS 업데이트를 사용 하지 않도록 설정 하려면 다음 레지스트리 값을 설정 합니다.<br /><br />레지스트리 키:<br /><br />SYSTEM\CurrentControlSet\Services\Dnscache\Parameters<br /><br />레지스트리 값:<br /><br />RegistrationEnabled<br /><br />레지스트리 값 데이터.<br /><br />0<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다. 복제 완료 된 후 복제 프로세스 DNS 업데이트를 다시 사용 됩니다.<br /><br />"정보 2 월 7 일 2012 3:12:49 오후 Microsoft-Windows-ActiveDirectory_DomainService 2191 내부 구성" Active Directory 도메인 서비스 DNS 업데이트를 사용 하지 않도록 설정 하려면 다음 레지스트리 값으로 설정 합니다.<br /><br />레지스트리 키:<br /><br />SYSTEM\CurrentControlSet\Services\Tcpip\Parameters<br /><br />레지스트리 값:<br /><br />DisableDynamicUpdate<br /><br />레지스트리 값 데이터.<br /><br />1<br /><br />복제 과정 로컬 컴퓨터 짧은 시간 동안는 복제 소스 컴퓨터와 동일한 컴퓨터 이름이 있을 수 있습니다. DNS A 및 AAAA 기록 등록 하는 클라이언트 복제 진행 로컬 컴퓨터에 요청을 보낼 수 있도록이 기간 동안 비활성화 됩니다. 복제 완료 된 후 복제 프로세스 DNS 업데이트를 다시 사용 됩니다.|  
|**2172**|ActiveDirectory_DomainService|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성을 읽어보세요.<br /><br />GenerationId 특성 값 다음과 같습니다.<br /><br />*<Number>*|  
|**2170**|ActiveDirectory_DomainService|ID를 생성 변경 발견 되었습니다.<br /><br />DS (이전 값)에 캐시 세대 ID:<br /><br />*<Number>*<br /><br />현재 VM (새 값)에서 생성 ID:<br /><br />*<Number>*<br /><br />ID를 생성 변경 가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다. Active Directory 도메인 서비스는 도메인 컨트롤러 복구 새 호출 ID를 만듭니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 지원 되는 방법을 복원 하려면 또는 롤백 Active Directory 도메인 서비스 데이터베이스의 콘텐츠 백업을 복원 하는 시스템 상태 된 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여입니다.|  
|**1109**|ActiveDirectory_DomainService|이 디렉터리 서버에 대 한 invocationID 특성 변경 되었습니다. 백업을 만들 때 최고 업데이트 일련 번호는 다음과 같습니다.<br /><br />InvocationID 특성 (이전 값):<br /><br />*<GUID>*<br /><br />InvocationID 특성 (새 값):<br /><br />*<GUID>*<br /><br />일련 번호 업데이트:<br /><br />*<Number>*<br /><br />디렉터리 서버에서 미디어 백업에서 복원 될 때의 invocationID 변경 되는 쓰기 응용 디렉터리 파티션을 호스트 하도록 구성, 가상 컴퓨터 스냅숏은 적용 된 후, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업 후 다시 시작 되었습니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 복원 하거나 롤백 지원 되는 방법을 Active Directory 도메인 서비스 데이터베이스의 콘텐츠 백업을 복원 하는 시스템 상태 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여입니다.|  
|**1000**|ActiveDirectory_DomainService|Microsoft Active Directory 도메인 서비스 시작 완료 합니다.|  
|**1394**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 데이터베이스를 업데이트 하지 못하는 문제가 해결 됩니다. Active Directory 도메인 서비스 데이터베이스에 새 업데이트가 성공 됩니다. 네트워크 로그온 서비스가 다시 시작|  
|**2163**|ActiveDirectory_DomainService|DsRoleSvc 서비스 복제 로컬 가상 도메인 컨트롤러를 시작 했습니다.|  
|**326**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 데이터베이스 (월 1 일 C:\Windows\NTDS\ntds.dit)를 연결합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.016, [7] 0.000, [8] 0.000, [9] 0.000, 10 [] 0.000, [11] 0.000, [12] 0.000 합니다.<br /><br />캐시 저장: 1|  
|**103**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 중지 인스턴스 (0).<br /><br />종료 변경: 0<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.032, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, 10 [] 0.000, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000 합니다.|  
|**102**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 (6.02.8225.0000) 새로운 인스턴스 (0)를 시작 합니다.|  
|**105**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 새로운 인스턴스 (0)를 시작 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.016, [2] 0.000, [3] 0.015, [4] 0.078, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.046, 10 [] 0.000, [11] 0.000 합니다.|  
|**1004**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 성공적으로 종료 되었습니다.|  
|**102**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 (6.02.8225.0000) 새로운 인스턴스 (0)를 시작 합니다.|  
|**326**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 데이터베이스 (월 1 일 C:\Windows\NTDS\ntds.dit)를 연결합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.015, [3] 0.016, [4] 0.000, [5] 0.031, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, 10 [] 0.000, [11] 0.000, [12] 0.000 합니다.<br /><br />캐시 저장: 1|  
|**105**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 새로운 인스턴스 (0)를 시작 합니다. (시간 1 초 =)<br /><br />내부 타이밍 순서: [1] 0.031, [2] 0.000, [3] 0.000, [4] 0.391, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, 10 [] 0.000, [11] 0.000 합니다.|  
|**1109**|ActiveDirectory_DomainService|이 디렉터리 서버에 대 한 invocationID 특성 변경 되었습니다. 백업을 만들 때 최고 업데이트 일련 번호는 다음과 같습니다.<br /><br />InvocationID 특성 (이전 값):<br /><br />*<GUID>*<br /><br />InvocationID 특성 (새 값):<br /><br />*<GUID>*<br /><br />일련 번호 업데이트:<br /><br />*<Number>*<br /><br />디렉터리 서버에서 미디어 백업에서 복원 될 때의 invocationID 변경 되는 쓰기 응용 디렉터리 파티션을 호스트 하도록 구성, 가상 컴퓨터 스냅숏은 적용 된 후, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업 후 다시 시작 되었습니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 복원 하거나 롤백 지원 되는 방법을 Active Directory 도메인 서비스 데이터베이스의 콘텐츠 백업을 복원 하는 시스템 상태 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여입니다.|  
|**1168**|ActiveDirectory_DomainService|내부 오류: 된 Active Directory 도메인 서비스 오류가 발생 했습니다.<br /><br />추가 데이터<br /><br />오류 값 (소수점):<br /><br />2<br /><br />오류 값 (16 진):<br /><br />2<br /><br />내부 ID:<br /><br />7011658|  
|**1110**|ActiveDirectory_DomainService|프로 모션 글로벌 카탈로그이 도메인 컨트롤러의 다음 기간에 대 한 지연 됩니다.<br /><br />기간 (분):<br /><br />5<br /><br />이 필요한 것 필요한 파티션 드 알리는 먼저 준비할 수 있도록 합니다. 레지스트리를 디렉터리 시스템 에이전트 글로벌 카탈로그 로컬 도메인 컨트롤러 홍보 하기 전에 대기 초를 지정할 수 있습니다. 글로벌 카탈로그 지연 광고 레지스트리 가치에 대 한 자세한 내용은 참조 리소스 Kit 분산 시스템 가이드|  
|**103**|NTDS ISAM|(536) NTDS NTDSA: 데이터베이스 엔진 중지 인스턴스 (0).<br /><br />종료 변경: 0<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.047, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.016, 10 [] 0.000, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000 합니다.|  
|**1004**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 성공적으로 종료 되었습니다.|  
|**1539**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 다음 하드 디스크의 디스크 소프트웨어 기반 쓰기 캐시를 해제할 수 없습니다.<br /><br />하드 디스크:<br /><br />c:<br /><br />시스템의 작동이 중단 데이터가 손실 될 수 있습니다.|  
|**2179**|ActiveDirectory_DomainService|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성 다음 매개 변수를 설정 했습니다.<br /><br />GenerationID 특성:<br /><br />*<Number>*|  
|**2173**|ActiveDirectory_DomainService|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성 읽기 하지 못했습니다. 데이터베이스 트랜잭션이 실패 하 여 발생할 수 있습니다 또는 생성 id 로컬 데이터베이스에 존재 하지 않습니다. GenerationId dcpromo 또는 DC 가상 도메인 컨트롤러 않습니다 후 처음으로 다시 부팅 하는 동안 존재 하지 않습니다.<br /><br />추가 데이터<br /><br />오류 코드:<br /><br />6|  
|**1000**|ActiveDirectory_DomainService|Microsoft Active Directory 도메인 서비스 시작 완료 6.2.8225.0 버전|  
|**1394**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 데이터베이스를 업데이트 하지 못하는 문제가 해결 됩니다. Active Directory 도메인 서비스 데이터베이스에 새 업데이트가 성공 됩니다. 네트워크 로그온 서비스가 다시 시작 합니다.|  
|**1128**|ActiveDirectory_DomainService|1128 정보 일관성 검사 "복제 연결 만든 다음 소스 디렉터리 서비스에서 로컬 디렉터리 서비스를 합니다.<br /><br />디렉터리 서비스 소스:<br /><br />CN NTDS 설정을 =*<Domain Controller DN>*<br /><br />로컬 디렉터리 서비스 다음과 같습니다.<br /><br />CN NTDS 설정을 =*<Domain Controller DN>*<br /><br />추가 데이터<br /><br />코드 이유:<br /><br />0 x 2<br /><br />내부 ID 지점 만들기.<br /><br />f0a025d|  
|**1999**|ActiveDirectory_DomainService|원본 디렉터리 서비스에 제공 대상 디렉터리 서비스 업데이트 일련 번호를 최적화 합니다. 원본 및 대상 디렉터리 서비스는 일반적인 복제 파트너 합니다. 대상 디렉터리 서비스 일반적인 복제 파트너와 최신 상태 이며 소스 디렉터리 서비스는이 파트너의 백업을 사용 하 여 설치 된 합니다.<br /><br />디렉터리 서비스 ID 대상:<br /><br />*<GUID> (<FQDN>)*<br /><br />디렉터리 서비스 ID 일반적인:<br /><br />*<GUID>*<br /><br />일반적인 속성 USN:<br /><br />*<Number>*<br /><br />따라서 최신 vector 대상 디렉터리 서비스의 다음 설정으로 구성 되어 있습니다.<br /><br />이전 개체 USN:<br /><br />0<br /><br />이전 속성 USN:<br /><br />0<br /><br />데이터베이스 GUID.<br /><br />*<GUID>*<br /><br />개체 USN:<br /><br />*<Number>*<br /><br />속성 USN:<br /><br />*<Number>*|  
  
##### <a name="system-event-log"></a>시스템 이벤트 로그  
다음 표시가 복제 작업의 시스템 이벤트 로그에 있습니다. 으로 하이퍼바이저 게스트 컴퓨터 복제 또는 스냅숏을에서 복원 된는 도메인 컨트롤러 나중 보안 사용자 중복 되지 않도록 하려면 해당 RID 풀 즉시 무효화 됩니다. 진행 복제, 다양 한 예상 되는 작업 및 메시지 표시, 서비스의 시작 및 중지 주로 주위 되 고 일부이 발생 하는 오류 예상 합니다. 성공 복제 전반적인 시스템 이벤트 로그 노트를 완료 합니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**16654**|삼-디렉터리-서비스|계정-Rid (식별자)의 풀 무효화 되었습니다. 예상 되는 다음과 같은 경우에 발생할 수 있습니다.<br /><br />1. 도메인 컨트롤러 백업에서 복원 됩니다.<br /><br />2. 실행 가상 컴퓨터에서 도메인 컨트롤러 스냅숏을에서 복원 됩니다.<br /><br />3. 관리자가 풀 무효화 수동으로|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 Active Directory 도메인 Services 서비스입니다.|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 Kerberos 키 메일 센터 서비스입니다.|  
|**3096**|Netlogon|이 도메인 주 도메인 컨트롤러를 찾을 수 없습니다.|  
|**7036**|서비스를 제어 관리자|보안 계정 관리자 서비스 실행 중인 상태가 됩니다.|  
|**7036**|서비스를 제어 관리자|서버 서비스 실행 중인 상태가 됩니다.|  
|**7036**|서비스를 제어 관리자|Netlogon 서비스가 실행 중인 상태가 됩니다.|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 Active Directory 웹 서비스 서비스입니다.|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 DFS 복제 서비스입니다.|  
|**7036**|서비스를 제어 관리자|파일 복제 서비스 서비스 실행 중인 상태가 됩니다.|  
|**14533**|Microsoft에서 Windows-DfsSvc|DFS 네임 스페이스 모든 빌드 마쳤습니다.|  
|**14531**|Microsoft에서 Windows-DfsSvc|초기화 중 DFS 서버의 마쳤습니다.|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 DFS Namespace 서비스입니다.|  
|**7023**|서비스를 제어 관리자|다음과 같은 오류가 발생 하 여 사이트 간 어디서 나 메시지 서비스가 중단 되었습니다.<br /><br />지정된 된 서버 요청한 작업을 수행할 수 없습니다.|  
|**7036**|서비스를 제어 관리자|어디서 나 메시지 사이트 간 서비스 중지 상태로 입력합니다.|  
|**5806**|Netlogon|이 도메인 컨트롤러의 동적 업데이트 수동으로 비활성화 되었습니다.<br /><br />사용자 작업<br /><br />이 도메인 컨트롤러 동적 업데이트를 사용 하거나 파일 '%SystemRoot%\System32\Config\Netlogon.dns'에서 DNS 데이터베이스에 DNS 레코드를 수동으로 추가를 다시 구성. "|  
|**16651**|삼-디렉터리-서비스|새 계정을 식별자 풀에 대 한 요청이 실패 했습니다. 요청에 성공 하면 될 때까지 작업을 다시 시도 합니다. 이 오류는<br /><br />요청한 FSMO 작업이 실패 했습니다. 현재 FSMO 소유자에 연결할 수 없습니다.|  
|**7036**|서비스를 제어 관리자|DNS 서버 서비스 실행 중인 상태가 됩니다.|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 DS 역할 서버 서비스.|  
|**7036**|서비스를 제어 관리자|Netlogon 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|파일 복제 서비스 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|Kerberos 키 메일 센터 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|DNS 서버 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|Active Directory 도메인 서비스 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|Netlogon 서비스가 실행 중인 상태가 됩니다.|  
|**7040**|서비스를 제어 관리자|시작 종류 Active Directory 도메인 서비스 서비스를 사용 하지 않으면 자동 시작 화면에서 변경 되었습니다.|  
|**7036**|서비스를 제어 관리자|Netlogon 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|파일 복제 서비스 서비스 실행 중인 상태가 됩니다.|  
|**29219**|위해 DSROLE 서버|가상 도메인 컨트롤러 복제 했습니다.|  
|**29223**|위해 DSROLE 서버|이 서버 도메인 컨트롤러 됩니다.|  
|**29265**|위해 DSROLE 서버|가상 도메인 컨트롤러 복제 했습니다. 구성 파일 C:\Windows\NTDS\DCCloneConfig.xml 복제 가상 도메인 컨트롤러에 C:\Windows\NTDS\DCCloneConfig.20120207-151533.xml 이름이 변경 되었습니다.|  
|**1074**|User32|프로세스가 C:\Windows\system32\lsass.exe (d c 2) 다음과 같은 이유 때문에 대 한 권한 NT \ 시스템 사용자를 대신 하 여 d c 2 컴퓨터를 다시 시작 시작: 운영 체제: 재구성 (계획 됨)<br /><br />코드 이유가: 0x80020004<br /><br />종료 유형: 다시 시작<br /><br />설명: "|  
  
##### <a name="dcpromolog"></a>DCPROMO 합니다. 로그  
나타나면 Dcpromo.log 디렉터리 서비스 이벤트 로그에 대 한 설명이 복제의 실제 프로 모션 부분을 포함 합니다. 로그 수준의 이벤트 로그 항목 전달 수 있다는 설명 제공 하지 않는, 추가 주석이 모듈의이 섹션에 포함 되어 있습니다.  
  
프로 모션 프로세스 의미 시작 복제 DC는 현재 구성의 스크러빙할 (훨씬는 IFM 판촉)와 같은 기존 광고 데이터베이스를 사용 하 여 다시 수준을 눌렀다가 DC 광고의 인바인드 변경 델타 복제 SYSVOL 및 복제 완료 되 고 있습니다.  
  
> [!NOTE]  
> 날짜 열을 제거 하 여이 모듈 쉽도록,에서 로그 수정 되었습니다.  
  
> [!NOTE]  
> 추가 대 한 내용은 나타나면 dcpromo.log 이해 및 Windows Server 2012에서 문제 해결 광고 DS 간체 관리를 참조 합니다.  
>   
> [https://go.microsoft.com/fwlink/p/?LinkId=237244](https://go.microsoft.com/fwlink/p/?LinkId=237244)  
  
-   프로 모션 복제 기반 시작  
  
-   디렉터리 서비스 복원 모드 플래그 서버 부팅 되지 않는 다시 정상적으로 원래 복제와 원인 이름 또는 디렉터리 서비스 충돌으로 되도록 설정  
  
-   디렉터리 서비스 이벤트 로그 업데이트  
  
```  
15:14:01 [INFO] vDC Cloneing: Setting Boot into DSRM flag succeeded.  
15:14:01 [WARNING] Cannot get user Token for Format Message: 1725l  
15:14:01 [INFO] vDC Cloning: Created vDCCloningUpdate event.  
15:14:01 [INFO] vDC Cloning: Created vDCCloningComplete event.  
```  
  
-   도메인 컨트롤러 알리지 않는 되도록 NetLogon 서비스 중지  
  
```  
15:14:01 [INFO] Stopping service NETLOGON  
15:14:01 [INFO] ControlService(STOP) on NETLOGON returned 1(gle=0)  
15:14:01 [INFO] DsRolepWaitForService: waiting for NETLOGON to enter one of 7 states  
15:14:01 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:02 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=1  
15:14:02 [INFO] DsRolepWaitForService: exiting because NETLOGON entered STOPPED state  
15:14:02 [INFO] DsRolepWaitForService(for any end state) on NETLOGON service returned 0  
15:14:02 [INFO] ControlService(STOP) on NETLOGON returned 0(gle=1062)  
15:14:02 [INFO] Exiting service-stop loop after service NETLOGON entered STOPPED state  
15:14:02 [INFO] StopService on NETLOGON returned 0  
15:14:02 [INFO] Configuring service NETLOGON to 1 returned 0  
15:14:02 [INFO] Updating service status to 4  
15:14:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   사용자 지정 관리자 지정한 dccloneconfig.xml 파일을 검사 합니다.  
  
-   여기서 샘플 파일인 빈, 설정이 모두를 자동으로 생성 하 고 필요한 네트워크에서는 자동 IP 주소  
  
```  
15:14:02 [INFO] vDC Cloning: Clone config file C:\Windows\NTDS\DCCloneConfig.xml is considered to be a blank file (containing 0 bytes)  
15:14:02 [INFO] vDC Cloning: Parsing clone config file C:\Windows\NTDS\DCCloneConfig.xml returned HRESULT 0x0  
```  
  
-   프로그램이 모두 설치 DefaultDCCloneAllowList.xml 또는 CustomDCCloneAllowList.xml 포함 되지 않은 없거나 서비스는 유효성 검사  
  
```  
15:14:02 [INFO] vDC Cloning: Checking allowed list:  
15:14:03 [INFO] vDC Cloning: Completed checking allowed list:  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   관리자가 IP 정보가 지정 되지 않았습니다 이후 네트워크 어댑터에 DHCP를 사용 하도록 설정  
  
```  
15:14:03 [INFO] vDC Cloning: Enable DHCP:  
15:14:03 [INFO] WMI Instance: Win32_NetworkAdapterConfiguration.Index=12  
15:14:03 [INFO] Method: EnableDHCP  
15:14:03 [INFO] HRESULT code: 0x0 (0)  
15:14:03 [INFO] Return Value: 0x0 (0)  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   PDC 에뮬레이터를 찾습니다.  
  
-   (이 경우 생성 자동으로)는 복제 사이트 설정  
  
-   (이 경우 생성 자동으로)는 복제 이름을 설정합니다  
  
```  
15:14:03 [INFO] vDC Cloning: Found PDC. Name: DC1.root.fabrikam.com  
15:14:04 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:04 [INFO] vDC Cloning: Winlogon UI Notification #1: Domain Controller cloning is at 5% completion...  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #2: Domain Controller cloning is at 10% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Site of the cloned DC: Default-First-Site-Name  
```  
  
-   새 복제 컴퓨터 개체 만들기  
  
-   일치 하는 새 이름을 복제 이름 바꾸기  
  
```  
15:14:05 [INFO] vDC Cloning: Clone DC objects are created on PDC.  
15:14:05 [INFO] Name of the cloned DC: DC2-CL0001  
15:14:05 [INFO] DsRolepSetRegStringValue on System\CurrentControlSet\Services\NTDS\Parameters\CloneMachineName to DC2-CL0001 returned 0  
15:14:05 [INFO] vDC Cloning: Save CloneMachineName in registry: 0x0 (0)  
```  
  
-   이전 dccloneconfig.xml 또는 자동으로 생성 규칙에 따라 판촉 설정이 제공  
  
```  
15:14:05 [INFO] vDC Cloning: Promotion parameters setting:  
15:14:05 [INFO] DNS Domain Name: root.fabrikam.com  
15:14:05 [INFO] Replica Partner: \\DC1.root.fabrikam.com  
15:14:05 [INFO] Site Name: Default-First-Site-Name  
15:14:05 [INFO] DS Database Path: C:\Windows\NTDS  
15:14:05 [INFO] DS Log Path: C:\Windows\NTDS  
15:14:05 [INFO] SysVol Root Path: C:\Windows\SYSVOL  
15:14:05 [INFO] Account: root.fabrikam.com\DC2-CL0001$  
15:14:05 [INFO] Options: DSROLE_DC_CLONING (0x800400)  
```  
  
-   프로 모션 시작  
  
```  
15:14:05 [INFO] Promote DC as a clone  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #3: Domain Controller cloning is at 15% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #4: Domain Controller cloning is at 16% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Validate supplied paths  
15:14:05 [INFO] Validating path C:\Windows\NTDS.  
15:14:05 [INFO] Path is a directory  
15:14:05 [INFO] Path is on a fixed disk drive.  
15:14:05 [INFO] Validating path C:\Windows\NTDS.  
15:14:05 [INFO] Path is a directory  
15:14:05 [INFO] Path is on a fixed disk drive.  
15:14:05 [INFO] Validating path C:\Windows\SYSVOL.  
15:14:05 [INFO] Path is on a fixed disk drive.  
15:14:05 [INFO] Path is on an NTFS volume  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #5: Domain Controller cloning is at 17% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] Start the worker task  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #6: Domain Controller cloning is at 20% completion...  
15:14:05 [INFO] Request for promotion returning 0  
15:14:05 [INFO] vDC Cloning: Winlogon UI Notification #7: Domain Controller cloning is at 21% completion...  
15:14:05 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   중지 하 고 구성 모든 광고 DS 관련 서비스 (NTDS, NTFRS/DFSR, KDC, DNS)  
  
> [!NOTE]  
> 이 시나리오에서을 종료할 시간이 오래 DNS 서비스 필요 합니다. 광고 통합이 더 이상-중지 NTDS 서비스 전에 사용할 수 있는 영역을 사용 하는 것 처럼 뒷부분 모듈의이 섹션에서 설명 DNS 이벤트를 참조 하세요.  
  
```  
15:14:15 [INFO] Stopping service NTDS  
15:14:15 [INFO] Stopping service NtFrs  
15:14:15 [INFO] ControlService(STOP) on NtFrs returned 1(gle=0)  
15:14:15 [INFO] DsRolepWaitForService: waiting for NtFrs to enter one of 7 states  
15:14:15 [INFO] DsRolepWaitForService: QueryServiceStatus on NtFrs returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:16 [INFO] DsRolepWaitForService: QueryServiceStatus on NtFrs returned 1 (gle=0), SvcStatus.dwCS=1  
15:14:16 [INFO] DsRolepWaitForService: exiting because NtFrs entered STOPPED state  
15:14:16 [INFO] DsRolepWaitForService(for any end state) on NtFrs service returned 0  
15:14:16 [INFO] ControlService(STOP) on NtFrs returned 0(gle=1062)  
15:14:16 [INFO] Exiting service-stop loop after service NtFrs entered STOPPED state  
15:14:16 [INFO] StopService on NtFrs returned 0  
15:14:16 [INFO] Configuring service NtFrs to 1 returned 0  
15:14:16 [INFO] Stopping service Kdc  
15:14:16 [INFO] ControlService(STOP) on Kdc returned 1(gle=0)  
15:14:16 [INFO] DsRolepWaitForService: waiting for Kdc to enter one of 7 states  
15:14:16 [INFO] DsRolepWaitForService: QueryServiceStatus on Kdc returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:17 [INFO] DsRolepWaitForService: QueryServiceStatus on Kdc returned 1 (gle=0), SvcStatus.dwCS=1  
15:14:17 [INFO] DsRolepWaitForService: exiting because Kdc entered STOPPED state  
15:14:17 [INFO] DsRolepWaitForService(for any end state) on Kdc service returned 0  
15:14:17 [INFO] ControlService(STOP) on Kdc returned 0(gle=1062)  
15:14:17 [INFO] Exiting service-stop loop after service Kdc entered STOPPED state  
15:14:17 [INFO] StopService on Kdc returned 0  
15:14:17 [INFO] Configuring service Kdc to 1 returned 0  
15:14:17 [INFO] Stopping service DNS  
15:14:17 [INFO] ControlService(STOP) on DNS returned 1(gle=0)  
15:14:17 [INFO] DsRolepWaitForService: waiting for DNS to enter one of 7 states  
15:14:17 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:18 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:19 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:20 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:21 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:22 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:23 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:24 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:25 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:26 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:27 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:28 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:29 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:30 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:31 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:32 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:33 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:34 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:35 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:36 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:37 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:38 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:39 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:40 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:41 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:42 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:43 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:44 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:45 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:46 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:47 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:48 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:49 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:50 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:51 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:52 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:53 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:54 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:55 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:56 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:57 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:58 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:14:59 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=3  
15:15:00 [INFO] DsRolepWaitForService: QueryServiceStatus on DNS returned 1 (gle=0), SvcStatus.dwCS=1  
15:15:00 [INFO] DsRolepWaitForService: exiting because DNS entered STOPPED state  
15:15:00 [INFO] DsRolepWaitForService(for any end state) on DNS service returned 0  
15:15:00 [INFO] ControlService(STOP) on DNS returned 0(gle=1062)  
15:15:00 [INFO] Exiting service-stop loop after service DNS entered STOPPED state  
15:15:00 [INFO] StopService on DNS returned 0  
15:15:00 [INFO] Configuring service DNS to 1 returned 0  
15:15:00 [INFO] ControlService(STOP) on NTDS returned 1(gle=1062)  
15:15:00 [INFO] DsRolepWaitForService: waiting for NTDS to enter one of 7 states  
15:15:00 [INFO] DsRolepWaitForService: QueryServiceStatus on NTDS returned 1 (gle=0), SvcStatus.dwCS=3  
15:15:01 [INFO] DsRolepWaitForService: QueryServiceStatus on NTDS returned 1 (gle=0), SvcStatus.dwCS=1  
15:15:01 [INFO] DsRolepWaitForService: exiting because NTDS entered STOPPED state  
15:15:01 [INFO] DsRolepWaitForService(for any end state) on NTDS service returned 0  
15:15:01 [INFO] ControlService(STOP) on NTDS returned 0(gle=1062)  
15:15:01 [INFO] Exiting service-stop loop after service NTDS entered STOPPED state  
15:15:01 [INFO] StopService on NTDS returned 0  
15:15:01 [INFO] Configuring service NTDS to 1 returned 0  
15:15:01 [INFO] Configuring service NTDS  
15:15:01 [INFO] Configuring service NTDS to 64 returned 0  
15:15:01 [INFO] vDC Cloning: Winlogon UI Notification #8: Domain Controller cloning is at 22% completion...  
15:15:01 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:01 [INFO] vDC Cloning: Winlogon UI Notification #9: Domain Controller cloning is at 25% completion...  
15:15:01 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   강제로 다른 도메인 컨트롤러 (일반적으로 PDCE) NT5DS (NTP) 시간 동기화  
  
```  
15:15:02 [INFO] Forcing time sync  
```  
  
-   복사본의 소스 도메인 컨트롤러 계정을 보유 하는 도메인 컨트롤러에 문의  
  
-   모든 기존 Kerberos 티켓 플러시  
  
```  
15:15:02 [INFO] Searching for a domain controller for the domain root.fabrikam.com that contains the account DC2$  
15:15:02 [INFO] Located domain controller DC1.root.fabrikam.com for domain root.fabrikam.com  
15:15:02 [INFO] vDC Cloning: Winlogon UI Notification #10: Domain Controller cloning is at 26% completion...  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:02 [INFO] Directing kerberos authentication to DC1.root.fabrikam.com returns 0  
15:15:02 [INFO] DsRolepFlushKerberosTicketCache() successfully flushed the Kerberos ticket cache  
15:15:02 [INFO] vDC Cloning: Winlogon UI Notification #11: Domain Controller cloning is at 27% completion...  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:02 [INFO] Using site Default-First-Site-Name for server \\DC1.root.fabrikam.com  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:02 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   NetLogon 서비스를 중지 하 고 해당 시작 유형 설정  
  
```  
15:15:02 [INFO] Stopping service NETLOGON  
15:15:02 [INFO] Stopping service NETLOGON  
15:15:02 [INFO] vDC Cloning: Winlogon UI Notification #12: Domain Controller cloning is at 29% completion...  
15:15:02 [INFO] ControlService(STOP) on NETLOGON returned 1(gle=0)  
15:15:02 [INFO] DsRolepWaitForService: waiting for NETLOGON to enter one of 7 states  
15:15:02 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=3  
15:15:03 [INFO] DsRolepWaitForService: QueryServiceStatus on NETLOGON returned 1 (gle=0), SvcStatus.dwCS=1  
15:15:03 [INFO] DsRolepWaitForService: exiting because NETLOGON entered STOPPED state  
15:15:03 [INFO] DsRolepWaitForService(for any end state) on NETLOGON service returned 0  
15:15:03 [INFO] ControlService(STOP) on NETLOGON returned 0(gle=1062)  
15:15:03 [INFO] Exiting service-stop loop after service NETLOGON entered STOPPED state  
15:15:03 [INFO] StopService on NETLOGON returned 0  
15:15:03 [INFO] Configuring service NETLOGON to 1 returned 0  
15:15:03 [INFO] Stopped NETLOGON  
15:15:03 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:03 [INFO] vDC Cloning: Winlogon UI Notification #13: Domain Controller cloning is at 30% completion...  
```  
  
-   자동으로 실행 NTFRS/DFSR 서비스를 구성  
  
-   다음 서비스를 시작할 때 sysvol 신뢰할 수 없는 동기화 하려면 자녀의 기존 데이터베이스 파일 삭제  
  
```  
15:15:03 [INFO] Configuring service DFSR  
15:15:03 [INFO] Configuring service DFSR to 256 returned 0  
15:15:03 [INFO] Configuring service NTFRS  
15:15:03 [INFO] Configuring service NTFRS to 256 returned 0  
15:15:03 [INFO] Removing DFSR Database files for SysVol  
15:15:03 [INFO] Removing FRS Database files in C:\Windows\ntfrs\jet  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edb.log  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edbres00001.jrs  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edbres00002.jrs  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\log\edbtmp.log  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\ntfrs.jdb  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\sys\edb.chk  
15:15:03 [INFO] Removed C:\Windows\ntfrs\jet\temp\tmp.edb  
15:15:04 [INFO] Created system volume path  
15:15:04 [INFO] Configuring service DFSR  
15:15:04 [INFO] Configuring service DFSR to 128 returned 0  
15:15:04 [INFO] Configuring service NTFRS  
15:15:04 [INFO] Configuring service NTFRS to 128 returned 0  
15:15:04 [INFO] vDC Cloning: Winlogon UI Notification #14: Domain Controller cloning is at 40% completion...  
15:15:04 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
```  
  
-   기존 NTDS 데이터베이스 파일을 사용 하 여 프로 모션 프로세스 시작  
  
-   RID 마스터에 문의  
  
> [!NOTE]  
> AD DS 서비스 설치 되어 있지 않으면 실제로 여기, 이것은 레거시 instrumentation 로그에서  
  
```  
15:15:04 [INFO] Installing the Directory Service  
15:15:04 [INFO] Calling NtdsInstall for root.fabrikam.com  
15:15:04 [INFO] Starting Active Directory Domain Services installation  
15:15:04 [INFO] Validating user supplied options  
15:15:04 [INFO] Determining a site in which to install  
15:15:04 [INFO] Examining an existing forest...  
15:15:04 [INFO] Starting a replication cycle between DC1.root.fabrikam.com and the RID operations master (2008r2-01.root.fabrikam.com), so that the new replica will be able to create users, groups, and computer objects...  
15:15:04 [INFO] Configuring the local computer to host Active Directory Domain Services  
15:15:04 [INFO] EVENTLOG (Warning): NTDS General / Service Control : 1539  
Active Directory Domain Services could not disable the software-based disk write cache on the following hard disk.  
Hard disk:  
c:  
Data might be lost during system failures.  
15:15:10 [INFO] EVENTLOG (Informational): NTDS General / Internal Processing : 2041  
Duplicate event log entries were suppressed.  
See the previous event log entry for details. An entry is considered a duplicate if  
the event code and all of its insertion parameters are identical. The time period for  
this run of duplicates is from the time of the previous event to the time of this event.  
Event Code:  
80000603  
Number of duplicate entries:   
2  
15:15:10 [INFO] EVENTLOG (Informational): NTDS General / Internal Configuration : 2121  
This Active Directory Domain Services server is disabling the Recycle Bin. Deleted objects may not be undeleted at this time.  
```  
  
-   원본 컴퓨터 데이터베이스에 있었던 기존 호출 ID 변경  
  
-   이 복제에 대 한 새로운 NTDS 설정을 개체 만들기  
  
-   광고 파트너 도메인 컨트롤러에서 개체 델타 복제  
  
> [!NOTE]  
> 모든 개체 복제 나열 되는 경우에 업데이트를 포함할 하는 데 필요한 메타 데이터 뿐입니다. 모든 변경된 개체 복제 NTDS 데이터베이스에 이미 있고 복제 다시 IFM 기반 프로 모션을 사용 하 여 처럼 필요 하지 않습니다.  
  
```  
15:15:10 [INFO] EVENTLOG (Informational): NTDS Replication / Replication : 1109  
The invocationID attribute for this directory server has been changed. The highest update sequence number at the time the backup was created is as follows:  
InvocationID attribute (old value):  
24e7b22f-4706-402d-9b4f-f2690f730b40  
InvocationID attribute (new value):  
f74cefb2-89c2-442c-b1ba-3234b0ed62f8  
Update sequence number:  
20520  
The invocationID is changed when a directory server is restored from backup media, is configured to host a writeable application directory partition, has been resumed after a virtual machine snapshot has been applied, after a virtual machine import operation, or after a live migration operation. Virtualized domain controllers should not be restored using virtual machine snapshots. The supported method to restore or rollback the content of an Active Directory Domain Services database is to restore a system state backup made with an Active Directory Domain Services-aware backup application.  
15:15:10 [INFO] EVENTLOG (Error): NTDS General / Internal Processing : 1168  
Internal error: An Active Directory Domain Services error has occurred.  
Additional Data  
Error value (decimal):  
2  
Error value (hexadecimal):  
2  
Internal ID:  
7011658  
15:15:11 [INFO] Creating the NTDS Settings object for this Active Directory Domain Controller on the remote AD DC DC1.root.fabrikam.com...  
15:15:11 [INFO] Replicating the schema directory partition  
15:15:11 [INFO] Replicated the schema container.  
15:15:12 [INFO] Active Directory Domain Services updated the schema cache.  
15:15:12 [INFO] Replicating the configuration directory partition  
15:15:12 [INFO] Replicating data CN=Configuration,DC=root,DC=fabrikam,DC=com: Received 2612 out of approximately 2612 objects and 94 out of approximately 94 distinguished name (DN) values...  
15:15:12 [INFO] Replicated the configuration container.  
15:15:13 [INFO] Replicating critical domain information...  
15:15:13 [INFO] Replicating data DC=root,DC=fabrikam,DC=com: Received 109 out of approximately 109 objects and 35 out of approximately 35 distinguished name (DN) values...  
15:15:13 [INFO] Replicated the critical objects in the domain container.  
```  
  
-   누락 된 업데이트도 필요에 따라 GC 파티션을 채우려면  
  
-   프로 모션 AD DS 중요 한 부분을 수행  
  
```  
15:15:13 [INFO] EVENTLOG (Informational): NTDS General / Global Catalog : 1110  
Promotion of this domain controller to a global catalog will be delayed for the following interval.  
Interval (minutes):  
5  
This delay is necessary so that the required directory partitions can be prepared before the global catalog is advertised. In the registry, you can specify the number of seconds that the directory system agent will wait before promoting the local domain controller to a global catalog. For more information about the Global Catalog Delay Advertisement registry value, see the Resource Kit Distributed Systems Guide.  
15:15:14 [INFO] EVENTLOG (Informational): NTDS General / Service Control : 1000  
Microsoft Active Directory Domain Services startup complete, version 6.2.8225.0   
15:15:15 [INFO] Creating new domain users, groups, and computer objects  
15:15:16 [INFO] Completing Active Directory Domain Services installation  
15:15:16 [INFO] NtdsInstall for root.fabrikam.com returned 0  
15:15:16 [INFO] DsRolepInstallDs returned 0  
15:15:16 [INFO] Installed Directory Service  
```  
  
-   SYSVOL의 인바인드 복제가 완료  
  
```  
15:15:16 [INFO] vDC Cloning: Winlogon UI Notification #15: Domain Controller cloning is at 60% completion...  
15:15:16 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] Completed system volume replication  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #16: Domain Controller cloning is at 70% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] SetProductType to 2 [LanmanNT] returned 0  
15:15:18 [INFO] Set the product type  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #17: Domain Controller cloning is at 71% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #18: Domain Controller cloning is at 72% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] Set the system volume path for NETLOGON  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #19: Domain Controller cloning is at 73% completion...  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] Replicating non critical information  
15:15:18 [INFO] User specified to not replicate non-critical data  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #20: Domain Controller cloning is at 80% completion...  
15:15:18 [INFO] Stopped the DS  
15:15:18 [INFO] vDC Cloning: Set vDCCloningUpdate event.  
15:15:18 [INFO] vDC Cloning: Winlogon UI Notification #21: Domain Controller cloning is at 90% completion...  
15:15:18 [INFO] Configuring service NTDS  
15:15:18 [INFO] Configuring service NTDS to 16 returned 0  
```  
  
-   DNS 등록 클라이언트를 사용 하도록 설정  
  
```  
15:15:18 [INFO] vDC Cloning: Set DisableDynamicUpdate reg value to 0 to enable dynamic update records registration.  
15:15:18 [INFO] vDC Cloning: Set UseDynamicDns reg value to 1 to enable dynamic update records registration.  
15:15:18 [INFO] vDC Cloning: Set RegistrationEnabled reg value to 1 to enable dynamic update records registration.  
```  
  
-   SYSPREP 모듈은 DefaultDCCloneAllowList.xml에 지정 된 실행 <SysprepInformation> 요소입니다.  
  
```  
15:15:18 [INFO] vDC Cloning: Running sysprep providers.  
15:15:32 [INFO] vDC Cloning: Completed running sysprep providers.  
```  
  
-   완료 되 복제 프로 모션  
  
-   서버 정상적으로 다음에 부팅 DSRM 부팅 플래그 제거  
  
-   읽지 다시 다음 번에 하 고 dccloneconfig.xml 이름 바꾸기  
  
-   컴퓨터를 다시 시작  
  
```  
15:15:32 [INFO] The attempted domain controller operation has completed  
15:15:32 [INFO] Updating service status to 4  
15:15:32 [INFO] DsRolepSetOperationDone returned 0  
15:15:32 [INFO] vDC Cloning: Set vDCCloningComplete event.  
15:15:32 [INFO] vDC Cloneing: Clearing Boot into DSRM flag succeeded.  
15:15:32 [INFO] vDC Cloning: Winlogon UI Notification #22: Cloning Domain Controller succeeded. Now rebooting...  
15:15:33 [INFO] vDC Cloning: Renamed vDC clone configuration file.  
15:15:33 [INFO] vDC Cloning: The old name is: C:\Windows\NTDS\DCCloneConfig.xml  
15:15:33 [INFO] vDC Cloning: The new name is: C:\Windows\NTDS\DCCloneConfig.20120207-151533.xml  
15:15:34 [INFO] vDC Cloning: Release Ipv4 on interface 'Wired Ethernet Connection 2', result=0.  
15:15:34 [INFO] vDC Cloning: Release Ipv6 on interface 'Wired Ethernet Connection 2', result=0.  
15:15:34 [INFO] Rebooting machine  
```  
  
##### <a name="active-directory-web-services-event-log"></a>Active Directory 웹 서비스 이벤트 로그  
복제 진행 중일 때 확보십시오 합니다. 오랜 시간 동안 DIT 데이터베이스 오프 라인 자주입니다. ADWS 서비스가 하나 이상의 이벤트를 기록합니다. 복제 완료 되 면 ADWS 서비스 시작 되 면 있는 유효한 컴퓨터 인증서가 아직 아직 (있을 수도 있는 자동 등록 된 Microsoft PKI 배포 귀하의 환경에 따라 되지 않을 수 있습니다) 메모 하 고 다음 인스턴스 새 도메인 컨트롤러를 시작 합니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**1202**|ADWS 인스턴스 이벤트|이 컴퓨터 지정된 디렉터리 인스턴스 호스팅하고 이제 하지만 Active Directory 웹 서비스 수리 하지 못했습니다. Active Directory 웹 서비스 정기적으로이 작업을 다시 됩니다.<br /><br />디렉터리 인스턴스: NTDS<br /><br />디렉터리 인스턴스 LDAP 포트: 389<br /><br />디렉터리 인스턴스 SSL 포트: 636|  
|**1000**|ADWS 인스턴스 이벤트|Active Directory 웹 서비스를 시작 하 고|  
|**1008**|ADWS 인스턴스 이벤트|축소 된 성공적으로 active Directory 웹 서비스의 보안 권한만|  
|**1100**|ADWS 인스턴스 이벤트|에 지정 된 값은 <appsettings> 오류 없이 로드 된 Active Directory 웹 서비스에 대 한 구성 파일의 합니다.|  
|**1400**|ADWS 인스턴스 이벤트|ADWS 인증서 이벤트 "Active Directory 웹 서비스 찾지 못했습니다 지정된 인증서 이름의 서버 인증서 합니다. 인증서가 SSL/TLS 연결을 사용 하 여 필요 합니다. TLS SSL/연결을 사용 하려면 신뢰할 수 있는 인증 기관 (캐나다)에서 유효한 서버 인증 인증서가 컴퓨터에 설치 되어 있는지 확인 합니다.<br /><br />인증서 이름:*<Server FQDN>*|  
|**1100**|ADWS 인스턴스 이벤트|에 지정 된 값은 <appsettings> 오류 없이 로드 된 Active Directory 웹 서비스에 대 한 구성 파일의 합니다.|  
|**1200**|ADWS 인스턴스 이벤트|Active Directory 웹 서비스 지정된 디렉터리 인스턴스를 서비스 이제 않습니다.<br /><br />디렉터리 인스턴스: NTDS<br /><br />디렉터리 인스턴스 LDAP 포트: 389<br /><br />디렉터리 인스턴스 SSL 포트: 636|  
  
##### <a name="dns-server-event-log"></a>DNS 서버 이벤트 로그  
DNS 서비스 DNS 서비스는 광고 DS 데이터베이스 오프 라인일 때 계속 실행 되는 발생 복제 하는 동안 간단한 예상된 작동 중단을 발생 합니다. 통합 Active Directory DNS을 사용 하 여 하지만 표준 주 또는 보조 DNS 사용 하는 경우에 하지 발생 합니다. 이러한 오류 여러 번 로그인 합니다. 복제 완료 된 후 DNS 정상적으로 다시 온라인 상태가 됩니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**4013**|DNS 서버-서비스|DNS 서버를 서비스에 대 한 Active Directory 도메인 AD DS 디렉터리의 초기 동기화가 완료 되 신호를 기다리고 있습니다. 중요 한 DNS 데이터가 도메인 컨트롤러에 아직 복제 되지 수 있으므로 초기 동기화 완료 될 때까지 DNS 서버 서비스 시작할 수 없습니다. AD DS 이벤트 로그 이벤트에 문제가 DNS 이름 확인 표시를이 도메인에 대 한 또 다른 DNS 서버의 IP 주소가이 컴퓨터의 인터넷 프로토콜 속성에서 DNS 서버 목록에 추가 하는 것이 좋습니다. 이 이벤트 AD DS 초기 동기화가 성공적으로 완료 신호가 될 때까지 2 분 마다 기록 됩니다.|  
|**4015**|DNS 서버-서비스|DNS 서버 Active Directory에서 오류가 발생 했습니다. Active Directory 제대로 작동 하는지 확인 합니다. (있음 비어 있을 수도 있음) 확장된 오류 디버그 정보는 "" "합니다. 이벤트 오류 포함 되어 있습니다.|  
|**4000**|DNS 서버-서비스|DNS 서버 Active Directory를 열 수 없습니다.  이 DNS 서버 얻고이 영역에 대 한 디렉터리의 정보를 사용 하도록 구성 된 및는 없이 영역을 로드할 수 없습니다.  Active Directory 제대로 작동 하는지 확인 하 고 영역 다시 로드 됩니다. 이벤트에 오류 코드입니다.|  
|**4013**|DNS 서버-서비스|DNS 서버를 서비스에 대 한 Active Directory 도메인 AD DS 디렉터리의 초기 동기화가 완료 되 신호를 기다리고 있습니다. 중요 한 DNS 데이터가 도메인 컨트롤러에 아직 복제 되지 수 있으므로 초기 동기화 완료 될 때까지 DNS 서버 서비스 시작할 수 없습니다. AD DS 이벤트 로그 이벤트에 문제가 DNS 이름 확인 표시를이 도메인에 대 한 또 다른 DNS 서버의 IP 주소가이 컴퓨터의 인터넷 프로토콜 속성에서 DNS 서버 목록에 추가 하는 것이 좋습니다. 이 이벤트 AD DS 초기 동기화가 성공적으로 완료 신호가 될 때까지 2 분 마다 기록 됩니다.|  
|**2**|DNS 서버-서비스|DNS 서버가 시작 했습니다.|  
|**4**|DNS 서버-서비스|DNS 서버를 백그라운드 영역에 로드를 마쳤습니다. 자녀가 각 영역 구성에서 허용 모든 영역 DNS 업데이트와 영역 전송을 사용할 수 있습니다.|  
  
##### <a name="file-replication-service-event-log"></a>파일 복제 서비스 이벤트 로그  
파일 복제 서비스 복제 하는 동안 파트너 로부터 비 정식으로 동기화 됩니다. 복제이 NTFRS 데이터베이스 파일을 삭제 하 고 그대로 SYSVOL의 내용을, 예약 된 데이터를 사용 하 여 수행 합니다. 동기화 하는 두 가지 시도 예상 됩니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**13562**|NtFrs|다음은 도메인 컨트롤러 DC2.root.fabrikam.com FRS 복제에 대 한 투표 구성 정보를 설정 하는 동안 파일 복제 서비스에서 발생 한 오류 및 경고의 요약입니다.<br /><br />도메인 컨트롤러 연결할 수 없습니다. 다음 폴링 주기에 다시 시도|  
|**13502**|NtFrs|파일 복제 서비스를 중지 합니다.|  
|**13565**|NtFrs|파일 복제 서비스 다른 도메인 컨트롤러의 데이터를 사용 하 여 시스템 볼륨을 초기화 하 고 있습니다. 이 프로세스를 완료 될 때까지 컴퓨터 d c 2 도메인 컨트롤러 될 수 있습니다. 그런 다음 시스템 볼륨 SYSVOL으로 공유 됩니다.<br /><br />SYSVOL 공유 명령 프롬프트를 확인 하려면 다음을 입력 합니다.<br /><br />네트워크 공유<br /><br />파일 복제 서비스 초기화 프로세스가 완료 되 면 SYSVOL 공유 표시 됩니다.<br /><br />시스템 볼륨 초기화 시간이 걸릴 수 있습니다. 시간은 시스템 볼륨 데이터의 양, 다른 도메인 컨트롤러 및 복제 간격 도메인 컨트롤러의 사용 가능 여부에 따라 달라 집니다.|  
|**13501**|NtFrs|파일 복제 서비스를 시작 하 고|  
|**13502**|NtFrs|파일 복제 서비스를 중지 합니다.|  
|**13503**|NtFrs|파일 복제 서비스 중지 했습니다.|  
|**13565**|NtFrs|파일 복제 서비스 다른 도메인 컨트롤러의 데이터를 사용 하 여 시스템 볼륨을 초기화 하 고 있습니다. 이 프로세스를 완료 될 때까지 컴퓨터 d c 2 도메인 컨트롤러 될 수 있습니다. 그런 다음 시스템 볼륨 SYSVOL으로 공유 됩니다.<br /><br />SYSVOL 공유 명령 프롬프트를 확인 하려면 다음을 입력 합니다.<br /><br />네트워크 공유<br /><br />파일 복제 서비스 초기화 프로세스가 완료 되 면 SYSVOL 공유 표시 됩니다.<br /><br />시스템 볼륨 초기화 시간이 걸릴 수 있습니다. 시간은 시스템 볼륨 데이터의 양, 다른 도메인 컨트롤러 및 복제 간격 도메인 컨트롤러의 사용 가능 여부에 따라 달라 집니다.|  
|**13501**|NtFrs|파일 복제 서비스를 시작 합니다.|  
|**13553**|NtFrs|파일 복제 서비스가이 컴퓨터 다음 복제 집합에 성공적으로 추가:<br /><br />"도메인 시스템 볼륨 (SYSVOL 공유)"<br /><br />이 이벤트와 관련 된 정보는 다음과 같습니다.<br /><br />컴퓨터 DNS 이름은*<Domain Controller FQDN>*<br /><br />복제본 세트 회원 이름*<Domain Controller>*<br /><br />복제본 설정 루트 경로가*<path>*<br /><br />디렉터리 경로 준비 복제본은*<path>*<br /><br />복제본 작업 디렉터리 경로*<path>*|  
|**13520**|NtFrs|파일 복제 서비스 기존 파일 이동 <path>에 * <path> *\NtFrs_PreExisting___See_EventLog 합니다.<br /><br />파일 복제 서비스에 파일을 삭제 수 * <path> *언제 든 지 \NtFrs_PreExisting___See_EventLog 합니다. 부재 중에 복사 하 여 파일 삭제 되지 않도록에서 저장할 수 있습니다 * <path> *\NtFrs_PreExisting___See_EventLog 합니다. 파일 기타 복제 파트너에 이미 있는 경우 c:\windows\sysvol\domain에 파일을 복사 이름 충돌이 발생할 수 있습니다.<br /><br />경우에 따라 파일 복제 서비스에서 파일을 복사할 수 * <path> *에 \NtFrs_PreExisting___See_EventLog * <path> * 복제 몇 가지 다른 파트너 로부터 파일 복제 하는 대신 합니다.<br /><br />영역에 있는 파일을 삭제 하 여 언제 든 지 복구할 수 * <path> *\NtFrs_PreExisting___See_EventLog. "|  
|**13508**|NtFrs|그 파일 복제 서비스는 데 문제가 있는 * \\\\ <Domain Controller FQDN> * 에 * <Domain Controller> * 에 대 한 * <path> * 사용 하 고<br /><br />DNS name *\\\\<Domain Controller FQDN>*. FRS가 계속 다시 시도 합니다.<br /><br />이 경고가 표시 되는 이유는 다음과가 같습니다.<br /><br />[1] FRS DNS 이름을 확인 올바르게 수 없는 * \\\\ <Domain Controller FQDN> * 이 컴퓨터에서 합니다.<br /><br />[2] FRS 실행 되 고 있지 * \\\\ <Domain Controller FQDN> *합니다.<br /><br />[3]이 복제본이에 대 한 Active Directory 도메인 서비스의 토폴로지 정보 모든 도메인 컨트롤러에 아직 복제 하지 않았습니다.<br /><br />연결을 문제가 해결 될 후 메시지가 표시 됩니다 다른 이벤트 로그 나타내는 연결 되었습니다 되 면이 이벤트 로그 메시지가 표시 됩니다.|  
|**13509**|NtFrs|파일 복제 서비스에서 복제 활성화 * \\\\ <Domain Controller FQDN> * 에 * <Domain Controller> * 에 대 한 * <Path> * 후 반복 해 서 다시 시도 합니다.|  
|**13516**|NtFrs|파일 복제 서비스 컴퓨터 때문에 더 이상 * <Domain Controller> * 최대화 도메인 컨트롤러에서 합니다. 시스템 볼륨이 초기화 되 고 Netlogon 서비스 시스템 볼륨은 이제 SYSVOL으로 공유할 준비가 통보 했습니다.<br /><br />타이핑 "net 공유" SYSVOL 공유를 확인 하려면. "|  
  
##### <a name="dfs-replication-event-log"></a>DFS 복제 이벤트 로그  
DFSR 서비스를 복제 하는 동안 파트너 로부터 비 정식으로 동기화 됩니다. 복제이 DFSR 데이터베이스 파일을 삭제 하 고 그대로 SYSVOL의 내용을, 예약 된 데이터를 사용 하 여 수행 합니다. 동기화 하는 두 가지 시도 예상 됩니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**1004**|DFSR|DFS 복제 서비스 시작 했습니다.|  
|**1314**|DFSR|Dfs 서비스 로그 파일 디버그 구성 했습니다.<br /><br />자세한 내용은 다음과 같습니다.<br /><br />로그 경로 파일 디버그: C:\Windows\debug|  
|**6102**|DFSR|DFS 복제 서비스 WMI 공급자를 성공적으로 등록|  
|**1206**|DFSR|도메인 컨트롤러 DC2.corp.contoso.com 구성 정보에 액세스 DFS 복제 서비스에 연결 했습니다.|  
|**1210**|DFSR|DFS 복제 서비스를 받는 복제 요청에 대 한 RPC 수신기를 설정 했습니다.<br /><br />자세한 내용은 다음과 같습니다.<br /><br />포트: 0 "|  
|**4614**|DFSR|DFS 복제 서비스 SYSVOL 로컬 경로 C:\Windows\SYSVOL\domain에 초기화 하 고 초기 복제 하는 데 기다리는 것이 있습니다. 복제 된 폴더를 해당 파트너와 복제가 될 때까지 초기 동기화 상태 유지 됩니다. 서버 도메인 컨트롤러에 올렸습니다 과정을 진행 경우, 도메인 컨트롤러 광고 한이 문제가 해결 될 때까지 도메인 컨트롤러 역할 하지 않습니다. 지정 된 파트너 초기 동기화 상태 이기도 또는 공유 위반이이 서버에 동기화 파트너 발생 하는 경우 발생할 수 있습니다. 이 동안 이벤트가 발생 SYSVOL 마이그레이션에서 파일 FRS (복제 서비스) DFS 복제,이 문제를 해결 될 때까지 변경 아웃 복제 하지 않습니다. 이 서버를 다른 도메인 컨트롤러 관련 동기화에 SYSVOL 폴더를 발생할 수 있습니다.<br /><br />자세한 내용은 다음과 같습니다.<br /><br />복제 폴더 이름: SYSVOL 공유<br /><br />복제 폴더 ID:*<GUID>*<br /><br />도메인 시스템 볼륨 복제 그룹 이름:<br /><br />복제 그룹 ID:*<GUID>*<br /><br />회원 번호:*<GUID>*<br /><br />읽기 전용: 0|  
|**4604**|DFSR|DFS 복제 서비스 로컬 경로 C:\Windows\SYSVOL\domain에 복제 SYSVOL 폴더를 초기화 했습니다. This member has completed initial synchronization of SYSVOL with partner dc1.corp.contoso.com.  To check for the presence of the SYSVOL share, open a command prompt window and then type ""net share"".<br /><br />자세한 내용은 다음과 같습니다.<br /><br />복제 폴더 이름: SYSVOL 공유<br /><br />복제 폴더 ID:*<GUID>*<br /><br />도메인 시스템 볼륨 복제 그룹 이름:<br /><br />복제 그룹 ID:*<GUID>*<br /><br />회원 번호:*<GUID>*<br /><br />Sync 파트너 다음과 같습니다.*<domain controller FQDN>*|  
  
## <a name="BKMK_TshootVDCSafeRestore"></a>가상화 도메인 컨트롤러 안전 복원이 문제 해결  
  
### <a name="tools-for-troubleshooting"></a>문제 해결 도구  
  
#### <a name="logging-options"></a>로그인 옵션  
로그 기본 제공 되는 도메인 컨트롤러 스냅숏 안전 복원이 문제 해결에 대 한 가장 중요 한 도구입니다. 모든 이러한 로그 활성화 되어 최대 세부 정보 표시 기본적으로 구성 됩니다.  
  
|||  
|-|-|  
|**작업**|**로그**|  
|**스냅숏 만들기**|이벤트 viewer\Applications 및 서비스 logs\Microsoft\Windows\Hyper V-동료|  
|**스냅샷 복원**|이벤트 viewer\Applications 및 서비스 logs\Directory 서비스<br />이벤트 viewer\Windows logs\System<br />이벤트 viewer\Windows logs\Application<br />이벤트 viewer\Applications 및 서비스 logs\File 복제 서비스<br />이벤트 viewer\Applications 및 서비스 logs\DFS 복제<br />이벤트 viewer\Applications 및 서비스 logs\DNS<br />이벤트 viewer\Applications 및 서비스 logs\Microsoft\Windows\Hyper V-동료|  
  
#### <a name="tools-and-commands-for-troubleshooting-domain-controller-configuration"></a>도구 및 도메인 컨트롤러 구성 문제 해결에 대 한 명령  
로그에 설명 되어 있지 문제를 해결 하려면 다음 도구를 사용 하 여 시작 지점으로 다음과 같습니다.  
  
-   Dcdiag.exe  
  
-   Repadmin.exe  
  
-   네트워크 3.4 모니터  
  
#### <a name="BKMK_TshhotSafeRestore"></a>일반 방법론 도메인 컨트롤러 안전 복원이 문제 해결  
  
1.  이 스냅숏을 안전 복원이 예상 했지만 문제가 있나요?  
  
    1.  디렉터리 서비스 이벤트 로그 검사  
  
        1.  스냅샷을 복원 오류 있습니까?  
  
        2.  광고 복제 오류 있습니까?  
  
    2.  시스템 이벤트 로그 검사  
  
        1.  통신 오류 있습니까?  
  
        2.  광고 오류 있습니까?  
  
2.  스냅숏을 안전 복원이 예기치 않은?  
  
    1.  사용자 또는 롤백 원인을 확인할 수 하이퍼바이저 감사 로그 검사  
  
    2.  모든 하이퍼바이저 관리자에 게 문의 하 고 누가 알리지 않고는 VM 롤백 계정으로 검색  
  
3.  서버 구현 USN 롤백 보호 이며 복원 하지 안전 하 게?  
  
    1.  디렉터리 서비스 이벤트 지원 되지 않는 하이퍼바이저 또는 통합 서비스에 대 한 로그를 검토  
  
    2.  운영 체제를 검사 하 고 Windows Server 2012를 실행 중인의 유효성을 검사?  
  
### <a name="BKMK_TshootSpecificSafeRestore"></a>특정 문제 해결  
  
#### <a name="events"></a>이벤트  
모든 가상화 도메인 컨트롤러 안전 스냅숏을 복원 이벤트 VM 복원된 도메인 컨트롤러의 디렉터리 서비스 이벤트 로그에 기록 됩니다. 응용 프로그램, 시스템, 파일이 복제 서비스 Dfs 이벤트 로그 실패 복원 유용한 문제 해결 정보를 포함할 수도 있습니다.  
  
디렉터리 서비스 이벤트 로그에서 Windows Server 2012 안전 복원이 관련 이벤트 아래에 있습니다.  
  
|||  
|-|-|  
|**이벤트 ID**|**2170**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|경고|  
|**메시지**|ID를 생성 변경 발견 되었습니다.<br /><br />DS (이전 값)에 캐시 세대 ID: 1%<br /><br />현재 VM (새 값)에서 생성 ID: %2<br /><br />ID를 생성 변경 가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다. *<COMPUTERNAME>*도메인 컨트롤러 복구 새 호출 ID를 만듭니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 지원 되는 방법을 복원 하려면 또는 롤백 Active Directory 도메인 서비스 데이터베이스의 콘텐츠 백업을 복원 하는 시스템 상태 된 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여입니다.|  
|**노트 및 해결 방법**|스냅숏이 필요한 경우에 성공 이벤트입니다. 그렇지 않으면 하이퍼 V 동료 이벤트 로그를 검토 하거나 하이퍼바이저 관리자에 게 문의 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2174**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|DC 가상 도메인 컨트롤러 복제본 아니고 복원된 가상 도메인 컨트롤러 스냅숏을 아닙니다.|  
|**노트 및 해결 방법**|실제 도메인 컨트롤러 또는 스냅숏을에서 복원 되지 가상화 도메인 컨트롤러를 시작 하면 예상된 이벤트|  
  
|||  
|-|-|  
|**이벤트 ID**|**2181**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|가상 컴퓨터 되돌리고 이전 상태로 인해 거래 중단 되었습니다.  가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 거래 추적 VM 생성 ID 변경|  
  
|||  
|-|-|  
|**이벤트 ID**|**2185**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*SYSVOL 폴더를 복제 하는 데 사용 FRS 또는 DFSR 서비스를 중지 합니다.<br /><br />서비스 이름: 1%<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원을 초기화 해야 합니다. 이 FRS 또는 DFSR 서비스 SYSVOL 폴더를 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 하 여 수행 됩니다. 이벤트 2187 FRS 또는 DFSR 서비스를 다시 시작할 때 기록 됩니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 이 도메인 컨트롤러의 모든 SYSVOL 데이터를 파트너 DC의 복사본과 대체 됩니다.|  
|**이벤트 ID**|2186|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*SYSVOL 폴더를 복제 하는 데 사용 하 여 FRS 또는 DFSR 서비스를 중지 하지 못했습니다.<br /><br />서비스 이름: 1%<br /><br />오류 코드: %2<br /><br />오류 메시지: 3%<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원을 초기화 해야 합니다. 이렇게 SYSVOL 폴더를 복제 하는 데 사용 하 고 다음을 복원 트리거하 값 해당 레지스트리 키와 시작 FRS 또는 DFSR 복제 서비스를 중지 합니다. *<COMPUTERNAME>*현재 실행 중인 서비스를 중지 하려면 실패 하 고 신뢰할 수 없는 복원을 완료할 수 없습니다. 신뢰할 수 없는 복원의 수동으로 수행 하세요.|  
|**노트 및 해결 방법**|자세한 내용은 FRS 시스템과 DFSR 이벤트 로그를 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2187**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*SYSVOL 폴더를 복제 하는 데 사용 FRS 또는 DFSR 서비스를 시작 합니다.<br /><br />서비스 이름: 1%<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원 초기화 해야 합니다. 이 작업을 수행 FRS 또는 DFSR 서비스 SYSVOL 폴더를 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 합니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 이 도메인 컨트롤러의 모든 SYSVOL 데이터를 파트너 DC의 복사본과 대체 됩니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2188**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*SYSVOL 폴더를 복제 하는 데 사용 하 여 FRS 또는 DFSR 서비스를 시작 하지 못했습니다.<br /><br />서비스 이름: 1%<br /><br />오류 코드: %2<br /><br />오류 메시지: 3%<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원 초기화 해야 합니다. FRS 또는 DFSR 서비스 SYSVOL 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 하면 됩니다. *<COMPUTERNAME>*실패 SYSVOL 폴더를 복제 하는 데 사용 하 여 FRS 또는 DFSR 서비스를 시작 하 고 신뢰할 수 없는 복원을 완료할 수 없습니다. 신뢰할 수 없는 복원을 수동으로 수행 하 고 서비스를 다시 시작 합니다.|  
|**노트 및 해결 방법**|자세한 내용은 FRS 시스템과 DFSR 이벤트 로그를 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2189**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*신뢰할 수 없는 복원 하는 동안 SYSVOL 복제 초기화 하려면 다음 레지스트리 값을 설정 합니다.<br /><br />레지스트리 키: 1%<br /><br />레지스트리 가치: %2<br /><br />레지스트리 가치 데이터: %3<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원 초기화 해야 합니다. FRS 또는 DFSR 서비스 SYSVOL 폴더를 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 하면 됩니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 이 도메인 컨트롤러의 모든 SYSVOL 데이터를 파트너 DC의 복사본과 대체 됩니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2190**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*신뢰할 수 없는 복원 하는 동안 SYSVOL 복제 초기화 하려면 다음 레지스트리 값을 설정 하지 못했습니다.<br /><br />레지스트리 키: 1%<br /><br />레지스트리 가치: %2<br /><br />레지스트리 가치 데이터: %3<br /><br />오류 코드: %4<br /><br />오류 메시지: %5<br /><br />Active Directory 섬에는 도메인 컨트롤러 역할 가상 컴퓨터를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원 초기화 해야 합니다. FRS 또는 DFSR 서비스 SYSVOL 폴더를 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 하면 됩니다. *<COMPUTERNAME>*위의 레지스트리 값으로 설정 되지 않았으며 신뢰할 수 없는 복원을 완료할 수 없습니다. 신뢰할 수 없는 복원의 수동으로 수행 하세요.|  
|**노트 및 해결 방법**|이벤트 로그 응용 프로그램 및 시스템 검사 합니다. 레지스트리 업데이트를 차단 하는 제 3 자 응용 프로그램을 확인 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2200**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*도메인 컨트롤러를 최신 상태로 복제가 초기화 합니다. 이벤트 2201 복제 완료 되 면 기록 됩니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 광고 인바인드 복제가의 시작 부분에 표시 됩니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2201**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*도메인 컨트롤러를 최신 상태로 복제가 마쳤습니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 광고 인바인드 복제가의 끝을 표시 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2202**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*도메인 컨트롤러를 최신 상태로 복제가 실패 합니다. 다음 주기적인 복제 후 도메인 컨트롤러 업데이트 됩니다.|  
|**노트 및 해결 방법**|디렉터리 서비스 및 시스템 이벤트 로그를 검사 합니다. 복제 강제로 시도 하 고 오류가 있는지 확인 하려면 repadmin.exe를 사용 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2204**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*가상 컴퓨터 생성 id 변경을 발견 했습니다. 변경 가상 도메인 컨트롤러를 이전 상태로 되돌릴 되는 것을 의미 합니다. *<COMPUTERNAME>*되돌린된 도메인 컨트롤러 확산 수 있는 데이터를 보호 하 고 생성 중복 Sid로 보안 사용자를 보호 하기 위해 다음과 같은 작업을 수행 합니다.<br /><br />새 호출 ID 만들기<br /><br />현재 RID 풀 무효화<br /><br />다음 인바인드 복제가에 FSMO 역할의 소유권을 검사할 합니다. 이 기간 동안 도메인 컨트롤러 FSMO 역할 유지 하는 경우 해당 역할 사용할 수 없게 됩니다.<br /><br />SYSVOL 복제 서비스 복원 작업을 시작 합니다.<br /><br />복제 기능을 최신 상태로 되돌린된 도메인 컨트롤러를 시작 합니다.<br /><br />새로운 RID 풀을 요청 합니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 이 모든 다양 한 재설정 안전 복원이 과정의 일환으로 발생 하는 작업에 설명 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2205**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*현재 RID 풀 가상 도메인 컨트롤러 이전 상태로 돌아갑니다 된 후 무효화 됩니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 도메인 컨트롤러에 여행 하 게 됨 시간 및은 이미 발급 한 것으로 로컬 RID 풀을 삭제 해야 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2206**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*현재 RID 풀 가상 도메인 컨트롤러 이전 상태로 돌아갑니다 된 후에 실패 했습니다.<br /><br />추가 데이터.<br /><br />오류 코드: %1<br /><br />오류 값: %2|  
|**노트 및 해결 방법**|디렉터리 서비스 및 시스템 이벤트 로그를 검사 합니다. 유효성을 검사 Dcdiag.exe /test:ridmanager를 사용 하 여이 서버에서 제거 마스터 온라인 상태 인지 연락할 수 있습니다|  
  
|||  
|-|-|  
|**이벤트 ID**|**2207**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*가상 도메인 컨트롤러 이전 상태로 돌아갑니다 된 후 복원 하지 못했습니다. 다시 부팅 DSRM에 요청 했습니다. 이전 이벤트에 대 한 자세한 내용 확인 하세요.|  
|**노트 및 해결 방법**|디렉터리 서비스 및 시스템 이벤트 로그를 검사 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2208**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|알림|  
|**메시지**|*<COMPUTERNAME>*신뢰할 수 없는 복원 하는 동안 SYSVOL 복제 초기화 DFSR 데이터베이스를 삭제 합니다.|  
|**노트 및 해결 방법**|스냅샷을 복원 하는 경우 필요 합니다. 이렇게 하면 DFSR SYSVOL DC 파트너 로부터 비 정식으로 동기화 됩니다. 다른 DFSR 복제 폴더에서 동일한 SYSVOL 볼륨 (도메인 컨트롤러 권장 되지 않습니다 호스트 사용자 지정 하려면 DFSR SYSVOL 같은 볼륨 설정)을 동기화 됩니다도 비 정식으로 note 합니다.|  
  
|||  
|-|-|  
|**이벤트 ID**|**2209**|  
|**원본**|Microsoft에서 Windows-ActiveDirectory_DomainService|  
|**심각도**|오류|  
|**메시지**|*<COMPUTERNAME>*DFSR 데이터베이스를 삭제 하지 못했습니다.<br /><br />추가 데이터.<br /><br />오류 코드: %1<br /><br />오류 값: %2<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. *<COMPUTERNAME>*로컬 SYSVOL 복제에서 신뢰할 수 없는 복원 초기화 해야 합니다. DFSR에 대 한 DFSR 서비스를 중지 DFSR 데이터베이스를 삭제 하 고 서비스를 다시 시작 하면 됩니다. DFSR 다시 시작 되는 데이터베이스 다시 및 초기 동기화 시작 합니다.|  
|**노트 및 해결 방법**|DFSR 이벤트 로그 살펴봅니다.|  
  
#### <a name="error-messages"></a>오류 메시지  
실패 가상화 도메인 컨트롤러 안전 스냅숏을 복원;에 대 한 직접 대화형 오류가 없는 모든 복제 정보 디렉터리 서비스 이벤트 로그에 기록합니다. 물론 모든 중요 한 서버 또는 복제 광고 오류 되는지에 증상이 다른 곳으로 합니다.  
  
#### <a name="known-issues-and-support-scenarios"></a>알려진된 문제 및 지원 시나리오  
[문제 해결 도메인 컨트롤러 안전 복원 하는 것에 대 한 일반 방법론](../../../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md#BKMK_TshootSpecificSafeRestore) 일반적으로 적절 하 게 대부분의 문제를 해결 합니다.  
  
|||  
|-|-|  
|**문제**|**새로운 보안 사용자 최근에 안전 복원된 도메인 컨트롤러에 만들 수는 없습니다.**|  
|**증상이**|스냅숏을 복원한 후 된 도메인 컨트롤러 실패의 새 보안 사용자 (사용자, 컴퓨터, 그룹)을 시도 합니다.<br /><br />0x2010 오류<br /><br />디렉터리 서비스 관련 식별자 할당할 수 없습니다.|  
|**해상도 및 노트**|이 문제는 마스터 FSMO 제거 역할의 오래 된 기술 복원된 된 컴퓨터에 발생 합니다. 스냅숏을 촬영 하 고 나중에 복원 된 후이 또는 다른 도메인 컨트롤러 역할 이동, 복원된 도메인 컨트롤러 하지는 기술 RID 마스터의 초기 복제가 완료 될 때까지 않을 수 있습니다.<br /><br />이 문제를 해결 하려면 광고 복제가 완료 허용 복원된 도메인 컨트롤러의 인바인드 합니다. 여전히 작동 하지 않으면 모든 도메인 컨트롤러 DC 호스트 제거 마스터는 동일한 올바른 기술 있는지 확인 합니다.|  
  
|||  
|-|-|  
|**문제**|**복원 된 도메인 컨트롤러 수행 하지 SYSVOL 공유, 광고**|  
|**증상이**|스냅숏을 복원한 후 하나 이상의 Dc 알리지 않는, sysvol를 공유 하지 및 최신 SYSVOL 내용을 하지 않은|  
|**해상도 및 노트**|DC 업스트림 파트너 DFSR 또는 FRS. 올바르게 복제 하는 작업 SYSVOL 복제 없는 이 문제 안전 복원이 관련 이지만 고객 복원된 되지 않은 Dc에 영향을 주지 다른 복제 문제를 알고 되지 않았기 때문에, 안전 복원이 문제도 나타날 수는|  
  
### <a name="advanced-troubleshooting"></a>고급 문제 해결  
이 모듈을 사용 하 여 고급 문제 해결을 학습 하는 방법을 찾습니다 *작동* 로그 샘플 발생 한 문제 중 몇 가지 설명 합니다. 성공 가상화 도메인 컨트롤러 작업을 같이 이해 하는 경우 오류 귀하의 환경에 확실 한 됩니다. 이러한 로그의 오름차순와 해당 소스 하 여 표시 되 *예상* 각 로그 내 복제 도메인 컨트롤러 관련 된 이벤트 합니다.  
  
#### <a name="restoring-a-domain-controller-that-replicates-sysvol-using-dfsr"></a>복원 SYSVOL DFSR를 사용 하 여 복제 하는 도메인 컨트롤러  
  
##### <a name="directory-services-event-log"></a>디렉터리 서비스 이벤트 로그  
디렉터리 서비스 로그 대부분의 안전 복원이 작동 정보가 포함 되어 있습니다. 하이퍼바이저 VM 세대 ID를 변경 하 고 NTDS 서비스 것 메모, 다음 RID 풀 무효화 호출 ID 변경 새로운 세대 VM ID가 설정 광고 데이터 돌아오는 서버 복제 되어 있습니다. DFSR 서비스가 중단 되 고 신뢰할 수 없는 동기화 강제로 SYSVOL 호스트 하는 데이터베이스 삭제 됩니다 인바인드 합니다. USN 높은 워터 조정 됩니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**2170**|ActiveDirectory_DomainService|ID를 생성 변경 발견 되었습니다.<br /><br />DS (이전 값)에 캐시 세대 ID:<br /><br />*<number>*<br /><br />현재 VM (새 값)에서 생성 ID:<br /><br />*<number>*<br /><br />ID를 생성 변경 가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다. Active Directory 도메인 서비스는 도메인 컨트롤러 복구 새 호출 ID를 만듭니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 지원 되는 방법을 복원 하려면 또는 롤백 Active Directory 도메인 서비스 데이터베이스의 콘텐츠는 백업을 복원 하는 시스템 상태 된 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여. "|  
|**2181**|ActiveDirectory_DomainService|가상 컴퓨터 되돌리고 이전 상태로 인해 거래 중단 되었습니다.  가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다.|  
|**2204**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 가상 컴퓨터 생성 id 변경을 검색에 변경 가상 도메인 컨트롤러를 이전 상태로 되돌릴 되는 것을 의미 합니다. Active Directory 도메인 서비스 되돌린된 도메인 컨트롤러 확산 수 있는 데이터를 보호 하 고 생성 중복 Sid로 보안 사용자를 보호 하기 위해 다음과 같은 작업을 수행 합니다.<br /><br />새 호출 ID 만들기<br /><br />현재 RID 풀 무효화<br /><br />다음 인바인드 복제가에 FSMO 역할의 소유권을 검사할 합니다. 이 기간 동안 도메인 컨트롤러 FSMO 역할 유지 하는 경우 해당 역할 사용할 수 없게 됩니다.<br /><br />SYSVOL 복제 서비스 복원 작업을 시작 합니다.<br /><br />복제 기능을 최신 상태로 되돌린된 도메인 컨트롤러를 시작 합니다.<br /><br />새로운 RID 풀을 요청 합니다. "|  
|**2181**|ActiveDirectory_DomainService|가상 컴퓨터 되돌리고 이전 상태로 인해 거래 중단 되었습니다.  가상 컴퓨터 스냅숏은의 응용 프로그램, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업이 완료 된 후 발생합니다.|  
|**1109**|ActiveDirectory_DomainService|이 디렉터리 서버에 대 한 invocationID 특성 변경 되었습니다. 백업을 만들 때 최고 업데이트 일련 번호는 다음과 같습니다.<br /><br />InvocationID 특성 (이전 값):<br /><br />*<GUID>*<br /><br />InvocationID 특성 (새 값):<br /><br />*<GUID>*<br /><br />일련 번호 업데이트:<br /><br />*<number>*<br /><br />디렉터리 서버에서 미디어 백업에서 복원 될 때의 invocationID 변경 되는 쓰기 응용 디렉터리 파티션을 호스트 하도록 구성, 가상 컴퓨터 스냅숏은 적용 된 후, 가상 컴퓨터 가져오기가 또는 실시간 마이그레이션 작업 후 다시 시작 되었습니다. 가상 컴퓨터 스냅숏을 사용 하 여 가상화 도메인 컨트롤러를 복원할 수 해야 합니다. 지원 되는 방법을 복원 하거나 롤백 Active Directory 도메인 서비스 데이터베이스의 콘텐츠는 백업을 복원 하는 시스템 상태 Active Directory 도메인 서비스 인식 백업 응용 프로그램을 사용 하 여 합니다. "|  
|**2179**|ActiveDirectory_DomainService|컴퓨터에서 도메인 컨트롤러의 개체를 GenerationId 특성 다음 매개 변수를 설정 했습니다.<br /><br />GenerationID 특성:<br /><br />*<number>*|  
|**2200**|ActiveDirectory_DomainService|Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. Active Directory 도메인 서비스 복제가 도메인 컨트롤러를 최신 상태로 초기화 합니다. 이벤트 2201 복제 완료 되 면 기록 됩니다.|  
|**2201**|ActiveDirectory_DomainService|Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. Active Directory 도메인 서비스 복제 도메인 컨트롤러를 최신 상태로를 완료 했습니다.|  
|**2185**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 SYSVOL 폴더를 복제 하는 데 사용 FRS 또는 DFSR 서비스를 중지 합니다.<br /><br />서비스 이름:<br /><br />DFSR<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. Active Directory 도메인 서비스에서 로컬 SYSVOL 복제 신뢰할 수 없는 복원을 초기화 해야 합니다. 이 FRS 또는 DFSR 서비스 SYSVOL 폴더를 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 하 여 수행 됩니다. 이벤트 2187 기록 됩니다 FRS 또는 DFSR 서비스를 다시 시작 합니다. "|  
|**2208**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 DFSR 데이터베이스 신뢰할 수 없는 복원 하는 동안 SYSVOL 복제 초기화를 삭제 합니다.<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. Active Directory 도메인 서비스에서 로컬 SYSVOL 복제 신뢰할 수 없는 복원을 초기화 해야 합니다. DFSR에 대 한 DFSR 서비스를 중지 DFSR 데이터베이스를 삭제 하 고 서비스를 다시 시작 하면 됩니다. Upon restarting DFSR will rebuild the databases and start the initial sync. "|  
|**2187**|ActiveDirectory_DomainService|Active Directory 도메인 서비스 SYSVOL 폴더를 복제 하는 데 사용 FRS 또는 DFSR 서비스를 시작 합니다.<br /><br />서비스 이름:<br /><br />DFSR<br /><br />Active Directory 가상 컴퓨터 섬에는 도메인 컨트롤러를 이전 상태로 되돌릴가 발견 했습니다. 로컬 SYSVOL 복제에서 신뢰할 수 없는 복원 초기화 하는 데 필요한 active Directory 도메인 서비스입니다. 이 작업을 수행 FRS 또는 DFSR 서비스 SYSVOL 폴더를 복제 하는 데 사용 중지 하 고 해당 레지스트리 키와 값 복원을 트리거하을 시작 합니다. "|  
|**1587**|ActiveDirectory_DomainService|디렉터리 서비스 복원 되었습니다 또는 응용 프로그램 파티션을 개최 된 하도록 구성 된 합니다. 결과적으로, 해당 복제 id 변경 되었습니다. 파트너는 이전 id를 사용 하 복제 변경 요청 했습니다. 시작 일련 번호를 수정 했습니다.<br /><br />디렉터리 서비스 대상에 해당 하는 다음과 같은 개체 GUID 백업 미디어에서 로컬 디렉터리 서비스 복원 된는 USN 앞에 있는 USN에서 시작 변경 요청 했습니다.<br /><br />개체 GUID.<br /><br />*<GUID> (<FQDN of partner domain controller>)*<br /><br />복원 당시 USN:<br /><br />*<number>*<br /><br />따라서 최신 vector 대상 디렉터리 서비스의 다음 설정으로 구성 되어 있습니다.<br /><br />이전 데이터베이스 GUID.<br /><br />*<GUID>*<br /><br />이전 개체 USN:<br /><br />*<number>*<br /><br />이전 속성 USN:<br /><br />*<number>*<br /><br />새 데이터베이스 GUID.<br /><br />*<GUID>*<br /><br />새 개체 USN:<br /><br />*<number>*<br /><br />새 속성 USN:<br /><br />*<number>*|  
  
##### <a name="system-event-log"></a>시스템 이벤트 로그  
시스템 이벤트 로그 정보는 호스트 시간이와 동기화 하 고 오프 라인 가상 컴퓨터 온라인 상태로 전환 될 때 발생 하는 컴퓨터 시간에 있습니다. RID 풀 무효화 고 FRS 또는 DFSR 서비스가 다시 시작 됩니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**1**|커널 일반|시스템 시간으로 변경 *있나요?<now>* *< 날짜/시간 스냅샷을 >*합니다.<br /><br />변경 이유: 응용 프로그램 또는 시스템 구성 요소는 시간을 변경 합니다.|  
|**16654**|삼-디렉터리-서비스|계정-Rid (식별자)의 풀 무효화 되었습니다. 예상 되는 다음과 같은 경우에 발생할 수 있습니다.<br /><br />1. 도메인 컨트롤러 백업에서 복원 됩니다.<br /><br />2. 실행 가상 컴퓨터에서 도메인 컨트롤러 스냅숏을에서 복원 됩니다.<br /><br />3. 관리자 풀을 무효화 수동으로 했습니다.<br /><br />See https://go.microsoft.com/fwlink/?LinkId=226247 for more information.|  
|**7036**|서비스를 제어 관리자|DFS 복제 서비스 중지 상태로 입력 합니다.|  
|**7036**|서비스를 제어 관리자|실행 중인 상태가 DFS 복제 서비스입니다.|  
  
##### <a name="application-event-log"></a>이벤트 로그 응용 프로그램  
로그 메모 DFSR 데이터베이스 중지 하 고 시작 합니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**103**|ESENT|(1360) DFSRs \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: 데이터베이스 엔진이 인스턴스 (0) 중지 합니다.<br /><br />종료 변경: 0<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.141, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, 10 [] 0.000, [11] 0.016, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000 합니다.|  
|**102**|ESENT|(532) DFSRs \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: 데이터베이스 엔진이 (6.02.8189.0000) 새로운 인스턴스 (0)을 시작 합니다.|  
|**105**|ESENT|(532) DFSRs \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: 데이터베이스 엔진 새로운 인스턴스 (0)를 시작 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, 10 [] 0.000, [11] 0.000 합니다.|  
|||(532) DFSRs \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db: 데이터베이스 엔진은 만든 새 데이터베이스 (월 1 일 \\\.\C:\System Volume Information\DFSR\database*_<GUID>*\dfsr.db). (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.016, [4] 0.062, [5] 0.000, [6] 0.016, [7] 0.000, [8] 0.000, [9] 0.015, 10 [] 0.000, [11] 0.000 합니다.|  
  
##### <a name="dfs-replication-event-log"></a>DFS 복제 이벤트 로그  
DFSR 서비스를 중지 하 고 SYSVOL 포함 하는 데이터베이스를 신뢰할 수 없는 동기화 삭제 되 인바인드 합니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**1006**|DFSR|DFS 복제 서비스를 중지 합니다.|  
|**1008**|DFSR|Dfs 서비스가 중지 했습니다.|  
|**1002**|DFSR|DFS 복제 서비스를 시작 합니다.|  
|**1004**|DFSR|DFS 복제 서비스 시작 했습니다.|  
|**1314**|DFSR|Dfs 서비스 로그 파일 디버그 구성 했습니다.<br /><br />자세한 내용은 다음과 같습니다.<br /><br />로그 경로 파일 디버그: C:\Windows\debug|  
|**6102**|DFSR|성공적으로 DFS 복제 서비스 WMI 공급자를 등록 합니다.|  
|**1206**|DFSR|Dfs 서비스 성공적으로 연결한 도메인 컨트롤러 * <domain controller FQDN> * 구성 정보에 액세스할 수 있습니다.|  
|**1210**|DFSR|DFS 복제 서비스를 받는 복제 요청에 대 한 RPC 수신기를 설정 했습니다.<br /><br />자세한 내용은 다음과 같습니다.<br /><br />포트: 0|  
|**4614**|DFSR|DFS 복제 서비스 SYSVOL 로컬 경로 C:\Windows\SYSVOL\domain에 초기화 하 고 초기 복제 하는 데 기다리는 것이 있습니다. 복제 된 폴더를 해당 파트너와 복제가 될 때까지 초기 동기화 상태 유지 됩니다. 서버 도메인 컨트롤러에 올렸습니다 과정을 진행 경우, 도메인 컨트롤러 광고 한이 문제가 해결 될 때까지 도메인 컨트롤러 역할 하지 않습니다. 지정 된 파트너 초기 동기화 상태 이기도 또는 공유 위반이이 서버에 동기화 파트너 발생 하는 경우 발생할 수 있습니다. 이 동안 이벤트가 발생 SYSVOL 마이그레이션에서 파일 FRS (복제 서비스) DFS 복제,이 문제를 해결 될 때까지 변경 아웃 복제 하지 않습니다. 이 서버를 다른 도메인 컨트롤러 관련 동기화에 SYSVOL 폴더를 발생할 수 있습니다.<br /><br />자세한 내용은 다음과 같습니다.<br /><br />복제 폴더 이름: SYSVOL 공유<br /><br />복제 폴더 ID:*<GUID>*<br /><br />도메인 시스템 볼륨 복제 그룹 이름:<br /><br />복제 그룹 ID:*<GUID>*<br /><br />회원 번호:*<GUID>*<br /><br />읽기 전용: 0|  
|**4604**|DFSR|DFS 복제 서비스 로컬 경로 C:\Windows\SYSVOL\domain에 복제 SYSVOL 폴더를 초기화 했습니다. This member has completed initial synchronization of SYSVOL with partner dc1.corp.contoso.com.  To check for the presence of the SYSVOL share, open a command prompt window and then type "net share".<br /><br />자세한 내용은 다음과 같습니다.<br /><br />복제 폴더 이름: SYSVOL 공유<br /><br />복제 폴더 ID:*<GUID>*<br /><br />도메인 시스템 볼륨 복제 그룹 이름:<br /><br />복제 그룹 ID:*<GUID>*<br /><br />회원 번호:*<GUID>*<br /><br />Sync 파트너 다음과 같습니다.*<partner domain controller FQDN>*|  
  
#### <a name="restoring-a-domain-controller-that-replicates-sysvol-using-frs"></a>복원 SYSVOL FRS 사용 하 여 복제 하는 도메인 컨트롤러  
이 경우 DFSR 이벤트 로그 대신 파일 복제 이벤트 로그 사용 됩니다. 또한 로그 FRS 관련 다양 한 이벤트를 기록합니다. 그렇지 않으면 디렉터리 서비스 및 시스템 이벤트 로그 메시지는 일반적으로 동일한와 동일한 주문 이전에 설명 합니다.  
  
##### <a name="file-replication-service-event-log"></a>파일 복제 서비스 이벤트 로그  
FRS 서비스를 멈추고 SYSVOL 비 정식으로 동기화 하도록 d 2 BURFLAGS 값으로 다시 시작 합니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**13502**|NTFRS|파일 복제 서비스를 중지 합니다.|  
|**13503**|NTFRS|파일 복제 서비스 중지 했습니다.|  
|**13501**|NTFRS|파일 복제 서비스를 시작 하 고|  
|**13512**|NTFRS|파일 복제 서비스가 디렉터리 c:\windows\ntfrs\jet DC4 컴퓨터에 포함 된 드라이브에 디스크 쓰기 캐시 검색. 전원이 드라이브를 중단 하 고 중요 업데이트는 손실 파일 복제 서비스를 복구할 수 있습니다.|  
|**13565**|NTFRS|파일 복제 서비스 다른 도메인 컨트롤러의 데이터를 사용 하 여 시스템 볼륨을 초기화 하 고 있습니다. 이 프로세스를 완료 될 때까지 컴퓨터 DC4 도메인 컨트롤러 될 수 있습니다. 그런 다음 시스템 볼륨 SYSVOL으로 공유 됩니다.<br /><br />SYSVOL 공유 명령 프롬프트를 확인 하려면 다음을 입력 합니다.<br /><br />네트워크 공유<br /><br />파일 복제 서비스 초기화 프로세스가 완료 되 면 SYSVOL 공유 표시 됩니다.<br /><br />시스템 볼륨 초기화 시간이 걸릴 수 있습니다. 시간은에서 시스템 볼륨을 다른 도메인 컨트롤러 및 복제 간격 도메인 컨트롤러의 사용 가능성 데이터의 양에 따라. "|  
|**13520**|NTFRS|파일 복제 서비스 기존 파일 이동 * <path> * 에 * <path> *\NtFrs_PreExisting___See_EventLog 합니다.<br /><br />파일 복제 서비스에 파일을 삭제 수 * <path> *언제 든 지 \NtFrs_PreExisting___See_EventLog 합니다. 부재 중에 복사 하 여 파일 삭제 되지 않도록에서 저장할 수 있습니다 * <path> *\NtFrs_PreExisting___See_EventLog 합니다. 에 파일을 복사 * <path> * 파일 다른 복제 파트너에 이미 있는 경우 이름 충돌이 발생할 수 있습니다.<br /><br />경우에 따라 파일 복제 서비스에서 파일을 복사할 수 * <path> *에 \NtFrs_PreExisting___See_EventLog * <path> * 복제 몇 가지 다른 파트너 로부터 파일 복제 하는 대신 합니다.<br /><br />영역에 있는 파일을 삭제 하 여 언제 든 지 복구할 수 * <path> *\NtFrs_PreExisting___See_EventLog 합니다.|  
|**13553**|NTFRS|파일 복제 서비스가이 컴퓨터 다음 복제 집합에 성공적으로 추가:<br /><br />"도메인 시스템 볼륨 (SYSVOL 공유)"<br /><br />이 이벤트와 관련 된 정보는 다음과 같습니다.<br /><br />컴퓨터 DNS 이름은 "*<domain controller FQDN>*"<br /><br />복제본 설정 회원 이름은 "*<domain controller name>*"<br /><br />복제본 설정 루트 경로가 "*<path>*"<br /><br />디렉터리 경로 준비 복제본이 "* <path> * "<br /><br />복제본 작업 디렉터리 경로가 "*<path>*"|  
|**13554**|NTFRS|파일 복제 서비스가 복제 세트 아래에 표시 된 연결을 추가 했습니다.<br /><br />"도메인 시스템 볼륨 (SYSVOL 공유)"<br /><br />인바인드 "*<partner domain controller FQDN>*"<br /><br />에 "*<partner domain controller FQDN>*"<br /><br />자세한 내용은 후속 이벤트 로그 메시지가 나타날 수 있습니다.|  
|**13516**|NTFRS|더 이상 파일 복제 서비스 최대화 도메인 컨트롤러에서 컴퓨터 DC4 때문입니다. 시스템 볼륨이 초기화 되 고 Netlogon 서비스 시스템 볼륨은 이제 SYSVOL으로 공유할 준비가 통보 했습니다.<br /><br />타이핑 "net 공유" SYSVOL 공유에 대 한 확인 합니다.|  
  
##### <a name="application-event-log"></a>이벤트 로그 응용 프로그램  
FRS 데이터베이스를 중지 하 고 시작 되 고은 d 2 BURFLAGS 작업으로 인해 제거 합니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**원본**|**메시지**|  
|**327**|ESENT|(1424) ntfrs 데이터베이스 엔진 (c:\windows\ntfrs\jet\ntfrs.jdb 월 1 일) 데이터베이스를 분리 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.015, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.516, [7] 0.000, [8] 0.000, [9] 0.000, 10 [] 0.000, [11] 0.063, [12] 0.000 합니다.<br /><br />캐시 다시: 0|  
|**103**|ESENT|(1424) ntfrs 데이터베이스 엔진이 인스턴스 (0) 중지 합니다.<br /><br />종료 변경: 0<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.031, 10 [] 0.000, [11] 0.016, [12] 0.000, [13] 0.000, [14] 0.047, [15] 0.000 합니다.|  
|**102**|ESENT|(3000) ntfrs 데이터베이스 엔진이 (6.02.8189.0000) 새로운 인스턴스 (0)을 시작 합니다.|  
|**105**|ESENT|(3000) ntfrs 데이터베이스 엔진 새로운 인스턴스 (0)를 시작 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.062, 10 [] 0.000, [11] 0.141 합니다.|  
|**103**|ESENT|(3000) ntfrs 데이터베이스 엔진이 인스턴스 (0) 중지 합니다.<br /><br />종료 변경: 0<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.000, 10 [] 0.000, [11] 0.000, [12] 0.000, [13] 0.015, [14] 0.000, [15] 0.000 합니다.|  
|**102**|ESENT|(3000) ntfrs 데이터베이스 엔진이 (6.02.8189.0000) 새로운 인스턴스 (0)을 시작 합니다.|  
|**105**|ESENT|(3000) ntfrs 데이터베이스 엔진 새로운 인스턴스 (0)를 시작 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.078, 10 [] 0.000, [11] 0.109 합니다.|  
|**325**|ESENT|(3000) ntfrs 데이터베이스 엔진 새 (c:\windows\ntfrs\jet\ntfrs.jdb 월 1 일) 데이터베이스를 만들었습니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.016, [4] 0.016, [5] 0.000, [6] 0.015, [7] 0.000, [8] 0.000, [9] 0.078, 10 [] 0.016, [11] 0.000 합니다.|  
|**103**|ESENT|(3000) ntfrs 데이터베이스 엔진이 인스턴스 (0) 중지 합니다.<br /><br />종료 변경: 0<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.000, [3] 0.000, [4] 0.000, [5] 0.078, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.125, 10 [] 0.016, [11] 0.000, [12] 0.000, [13] 0.000, [14] 0.000, [15] 0.000 합니다.|  
|**102**|ESENT|(3000) ntfrs 데이터베이스 엔진이 (6.02.8189.0000) 새로운 인스턴스 (0)을 시작 합니다.|  
|**105**|ESENT|(3000) ntfrs 데이터베이스 엔진 새로운 인스턴스 (0)를 시작 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.016, [2] 0.000, [3] 0.000, [4] 0.094, [5] 0.000, [6] 0.000, [7] 0.000, [8] 0.000, [9] 0.032, 10 [] 0.000, [11] 0.000 합니다.|  
|**326**|ESENT|(3000) ntfrs 데이터베이스 엔진 데이터베이스 (월 1 일 c:\windows\ntfrs\jet\ntfrs.jdb)를 연결 합니다. (시간 0 초 =)<br /><br />내부 타이밍 순서: [1] 0.000, [2] 0.015, [3] 0.000, [4] 0.000, [5] 0.016, [6] 0.015, [7] 0.000, [8] 0.000, [9] 0.000, 10 [] 0.000, [11] 0.000, [12] 0.000 합니다.<br /><br />캐시 저장: 1|  
  


