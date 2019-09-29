---
title: Server Core 2008 이란?
description: Windows Server 2008의 Server Core 설치 옵션에 대 한 자세한 정보
ms.prod: windows-server
ms.author: helohr
ms.date: 11/01/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 0a109d0bfc4fc09b5e8097059d68b728d17752a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383378"
---
# <a name="what-is-server-core-2008"></a>Server Core 2008 이란?
>적용 대상: Windows Server 2008

>[!NOTE]
>이 정보는 Windows Server 2008에 적용 됩니다. Windows server의 Server Core에 대 한 자세한 내용은 [Windows server의 Server Core 설치](https://docs.microsoft.com/windows-server/administration/server-core/what-is-server-core)를 참조 하세요. 

Server Core 옵션은 Windows Server 2008 Standard, Enterprise 또는 Datacenter edition을 배포할 때 사용할 수 있는 새로운 최소 설치 옵션입니다. Server Core는이 챕터의 뒷부분에 설명 된 대로 특정 서버 역할만 설치 하도록 지 원하는 최소 Windows Server 2008 설치를 제공 합니다. 이는 사용 가능한 모든 서버 역할 및 기타 Microsoft 또는 타사 서버 응용 프로그램 (예: Microsoft Exchange Server 또는 SAP)의 설치를 지 원하는 Windows Server 2008에 대 한 전체 설치 옵션과 대조 됩니다. 

더 진행 하기 전에 "설치 옵션" 이라는 문구를 설명 해야 합니다. 일반적으로 Windows Server 2008의 복사본을 구입할 때 특정 버전 또는 Sku (재고 유지 단위)를 사용할 수 있는 라이선스를 구매 합니다. 표 1-1에는 사용 가능한 다양 한 Windows Server 2008 버전이 나와 있습니다. 이 표에는 각 버전에 대해 사용할 수 있는 설치 옵션 (Full, Server Core 또는 둘 다)도 표시 됩니다.

**표 1-1** Windows Server 2008 버전 및 설치 옵션에 대 한 지원

| 버전       | 전체          | Server Core  |
| ------------- | :-------------: | :------------: |
| Windows Server 2008 Standard (x86 및 x64)       | X | X        |
| Windows Server 2008 Enterprise (x86 및 x64)       | X | X        |
| Windows Server 2008 Datacenter (x86 및 x64)        | X | X       |
| Windows 웹 서버 2008 (x86 및 x64)       | X | X  |
| Itanium 기반 시스템용 Windows Server 2008       | X |     |
| Windows HPC Server 2008 (x 64에만 해당)       | X |   |
| Windows Server 2008 Standard (Hyper-v 불포함) (x86 및 x64) | X | X |
| Windows Server 2008 Enterprise (Hyper-v 불포함) (x86 및 x64)  | X | X |
| Windows Server 2008 Standard (Hyper-v 불포함) (x86 및 x64) | X | X |

"설치 옵션"이 무엇 인지 이해 하려면 Windows Server 2008 Enterprise Edition의 복사본을 설치 하는 데 사용할 수 있는 볼륨 라이선스를 구매 했다고 가정해 보겠습니다. 볼륨 라이선스 미디어를 시스템에 삽입 하 고 설치 프로세스를 시작할 때 그림 1-1에 표시 된 것 처럼 화면에 표시 되는 화면 중 하나가 표시 되는 버전 및 설치 옵션을 제공 합니다.

![설치할 Server Core 설치 옵션 선택](../media/what-is-server-core-2008/FIg1-1.png)

**그림 1-1** 설치할 Server Core 설치 옵션 선택

그림 1-1에서 볼륨 라이선스 (또는 정품 미디어에 대 한 제품 키)는 두 번째 옵션 (Windows Server 2008 Enterprise의 전체 설치)과 다섯 번째 옵션 (Windows의 Server Core 설치) 중에서 선택할 수 있는 두 가지 설치 옵션을 제공 합니다. Server 2008 Enterprise)를 선택 합니다. 

## <a name="full-vs-server-core"></a>완전 트랜잭션 내구성과 Server Core 
Microsoft Windows 플랫폼의 초반부터 Windows server는 기본적으로 모든 종류의 기능을 포함 하는 "모든" 서버 였습니다. 이러한 서버 중 일부는 실제로 네트워킹 환경에서 사용 하지 못할 수 있습니다. 예를 들어, 시스템에 Windows Server 2003를 설치한 경우에는이 서비스가 필요 하지 않더라도 RRAS (라우팅 및 원격 액세스 서비스)에 대 한 이진 파일이 서버에 설치 됩니다 (여전히 RRAS를 구성 하 고 사용할 수 있도록 설정 해야 함). Windows Server 2008에서는 서버에 특정 역할을 설치 하도록 선택한 경우에만 서버 역할에 필요한 이진 파일을 설치 하 여 이전 버전을 개선 합니다. 그러나 Windows Server 2008의 전체 설치 옵션은 종종 특정 사용 시나리오에 필요 하지 않은 많은 서비스 및 기타 구성 요소를 설치 합니다. 

Microsoft에서 Windows Server 2008에 대 한 두 번째 설치 옵션인 Server Core를 만든 이유 때문에 일반적으로 사용 되는 특정 서버 역할의 지원에 필수적인 서비스 및 기타 기능을 제거 해야 합니다. 예를 들어 dns (Domain Name System) 서버에는 보안상의 이유로 DNS 서버에서 웹을 검색 하지 않으려는 경우 Windows Internet Explorer가 설치 되어 있지 않아도 됩니다. 및 dns 서버는 강력한 Dnscmd 명령을 사용 하 여 명령줄에서 또는 DNS MMC (Microsoft Management Console) 스냅인을 사용 하 여 원격으로 DNS의 거의 모든 측면을 관리할 수 있으므로 GUI (그래픽 사용자 인터페이스)가 필요 하지 않습니다.

이러한 문제를 방지 하기 위해 Microsoft는 Active Directory Domain Services (AD DS), DNS, DHCP (Dynamic Host Configuration Protocol), 파일 및 인쇄 등의 핵심 네트워크 서비스를 실행 하는 데 반드시 필요한 것은 아니지만 Windows Server 2008에서 모든 항목을 제거 하기로 결정 했습니다. 다른 서버 역할은 거의 없습니다. 결과는 제한 된 수의 역할 및 기능만 지 원하는 서버를 만드는 데 사용할 수 있는 새 Server Core 설치 옵션입니다. 

## <a name="the-server-core-gui"></a>Server Core GUI
시스템에 Server Core를 설치 하 고 처음으로 로그온 하는 경우에는 약간의 문제가 있습니다. 그림 1-2에서는 처음 로그온 한 후의 Server Core 사용자 인터페이스를 보여 줍니다.

![Server Core 사용자 인터페이스](../media/what-is-server-core-2008/Fig1-2.png)

**그림 1-2** Server Core 사용자 인터페이스

데스크톱이 없습니다. 즉, 시작 메뉴, 작업 표시줄 및 표시 하는 데 사용할 수 있는 다른 기능을 포함 하는 Windows 탐색기 셸이 없습니다. 명령 프롬프트만 있습니다. 즉, 명령을 한 번에 하나씩 입력 하거나, 느리거나 스크립트 및 배치 파일을 사용 하 여 Server Core 설치를 구성 하는 대부분의 작업을 수행 해야 합니다 .이를 통해 구성의 속도를 높이고 간소화 하는 데 도움이 될 수 있습니다. 작업을 자동화 하는 작업 Server Core의 무인 설치를 수행 하는 경우 응답 파일을 사용 하 여 일부 초기 구성 작업을 수행할 수도 있습니다. 

Netsh.exe, sqlservr.exe 및 Dnscmd와 같은 명령줄 도구를 사용 하는 전문가를 대상으로 하는 관리자의 경우, Server Core 설치를 구성 및 관리 하는 것이 편리 하 고 재미 있습니다. 그러나 전문가가 아닌 사용자의 경우에는 모두 손실 되지 않습니다. 여전히 표준 Windows Server 2008 MMC 도구를 사용 하 여 Server Core 설치를 관리할 수 있습니다. Windows Server 2008 또는 Windows Vista 서비스 팩 1의 전체 설치를 실행 하는 다른 시스템에만 사용 해야 합니다. 

이 책의 3 ~ 6 장에서 Server Core 설치를 구성 및 관리 하는 방법에 대해 자세히 알아보고, 이후 장에서는 특정 서버 역할 및 기타 구성 요소를 관리 하는 방법을 다룹니다. 다양 한 Windows 명령줄 도구 및 사용 방법에 대 한 자세한 내용은 다음 두 가지 좋은 리소스를 참조 하세요.
* Windows Server 2008 기술 라이브러리의 명령 참조 섹션 () 
* William R. Stanek *의 Windows 명령줄 관리자의 포켓 컨설턴트* (Microsoft Press, 2008) 

표 1-2에는 Server Core 설치에서 사용할 수 있는 주 GUI 응용 프로그램 및 해당 실행 파일이 나열 되어 있습니다.

**표 1-2** Server Core 설치에서 사용할 수 있는 GUI 응용 프로그램

| GUI 응용 프로그램 | 경로를 포함 하는 실행 파일 |
| -------------   | -------------       | 
| 명령 프롬프트 | %WINDIR%\System32\Cmd.exe |
| Microsoft 지원 진단 도구 | %WINDIR%\System32\MSdt.exe |
| Windows 메모장 | %WINDIR%\System32\Notepad.exe |
| 레지스트리 편집기 | %WINDIR%\System32\Regedt32.exe |
| 시스템 정보 | %WINDIR%\System32\MSinfo32.exe |
| 작업 관리자 | %WINDIR%\System32\Taskmgr.exe |
| Windows Installer | %WINDIR%\System32\MSiexec.exe |

매우 간단한 목록입니다. 이제 Server Core에 포함 되지 않은 사용자 인터페이스 요소 목록이 있습니다.
* Windows 탐색기 desktop shell (explorer.exe) 및 지원 기능 (예: 테마) 
* 모든 MMC 콘솔 
* 국가 및 언어 옵션 (국제 .cpl) 및 날짜 및 시간 (Timedate .cpl)을 제외한 모든 제어판 유틸리티 
* Internet Explorer 및 HTML 도움말을 비롯 한 모든 HTML(Hypertext Markup Language) (HTML) 렌더링 엔진 
* Windows 메일 
* Windows Media Player 
* 그림판, 계산기 및 워드 패드와 같은 대부분의 액세서리

Server core에도 .NET Framework 없습니다. 즉, Server Core 설치에서 관리 코드를 실행 하는 것이 지원 되지 않습니다. 네이티브 코드만-Windows Api (응용 프로그래밍 인터페이스)를 사용 하 여 작성 된 코드는 Server Core에서 실행할 수 있습니다. 요약 하자면, .NET Framework 또는 Explorer.exe 셸에서 종속 된 모든 GUI 응용 프로그램은 Server Core에서 실행 되지 않습니다. 

>[!NOTE]
>Windows PowerShell에는 .NET Framework 필요 하므로 Server Core에 Windows PowerShell을 설치할 수 없습니다. 그러나 PowerShell WMI 명령만 사용 하는 경우 Windows PowerShell을 사용 하 여 Server Core 설치를 원격으로 관리할 수 있습니다.

## <a name="supported-server-roles"></a>지원 되는 서버 역할 
Server Core 설치에는 Windows Server 2008 전체 설치와 비교 하 여 제한 된 수의 서버 역할만 포함 됩니다. 표 1-3에서는 Windows Server 2008 Enterprise Edition의 전체 설치 및 Server Core 설치에 사용할 수 있는 역할을 비교 합니다. 

**표 1-3** Windows Server 2008 Enterprise Edition의 전체 및 Server Core 설치에 대 한 서버 역할 비교

| 서버 역할  | 전체 설치에서 사용 가능  | Server Core에서 사용 가능  |
| ------------- | :-------------: | :------------: |
| AD CS(Active Directory 인증서 서비스)  | X |  |
| AD DS(Active Directory 도메인 서비스)  | X  | X |
| AD FS(Active Directory Federation Services)  | X  |  |
| AD LDS(Active Directory Lightweight Directory Services)  | X  | X |
| AD RMS(Active Directory Rights Management Services)  | X  |  |
| 응용 프로그램 서버  | X  |  |
| DHCP 서버  | X  | X |
| DNS 서버  | X  | X |
| 팩스 서버  | X  |  |
| 파일 서비스  | X  | X |
| Hyper-V  | X | X |
| 네트워크 정책 및 액세스 서비스  | X  |  |
| 인쇄 서비스  | X  | X |
| 스트리밍 미디어 서비스  | X  | X |
| 터미널 서비스  | X  |  |
| UDDI 서비스  | X  |  |
| 웹 서버(IIS) | X | X |
| Windows 배포 서비스  | X |  |

Server Core에 사용할 수 있는 역할은 일반적으로 아키텍처 (x86 또는 x64)와 제품 버전에 관계 없이 동일 하지만 다음과 같은 몇 가지 예외가 있습니다.
* Hyper-v (가상화) 역할은 hyper-v 제품 미디어를 사용 하 여 Windows Server 2008를 구매한 경우에만 사용할 수 있습니다 (Hyper-v는 x64 버전 에서만 사용할 수 있음). 이 역할이 필요 하지 않은 경우 대신 Hyper-v 제품 미디어 없이 Windows Server 2008를 구매할 수 있습니다. 
* Standard Edition의 파일 서비스 역할은 하나의 독립 실행형 분산 파일 시스템 (DFS) 루트로 제한 되며, DFS (파일 간 복제)를 지원 하지 않습니다. 
* Server Core에 스트리밍 Media Services 역할을 설치 하려면 Microsoft 다운로드 센터에서 서버 아키텍처 (x86 또는 x64)에 대 한 적절 한 Microsoft 업데이트 독립 실행형 패키지 (.msu 파일)를 다운로드 하 여 설치 해야 합니다.
* 웹 서버 (IIS) 역할은 ASP.NET를 지원 하지 않습니다. 이는 server core 웹 서버에서 수행할 수 있는 작업을 제한 하는 Server Core에서 .NET Framework 지원 되지 않기 때문입니다. 

## <a name="supported-optional-features"></a>지원 되는 선택적 기능
Server Core 설치에는 Windows Server 2008 전체 설치에서 사용할 수 있는 기능의 제한 된 하위 집합만 지원 됩니다. 표 1-4에서는 Windows Server 2008 Enterprise Edition의 전체 설치 및 Server Core 설치에 사용할 수 있는 기능을 비교 합니다.

**표 1-4** Windows Server 2008 Enterprise Edition의 전체 및 Server Core 설치 기능 비교

| 기능  | 전체 설치에서 사용 가능  | Server Core에서 사용 가능  |
| ------------- | :-------------: | :------------: |
| .NET Framework 3.0 기능  | X  |  |
| BitLocker 드라이브 암호화  | X  | X |
| BITS 서버 확장  | X  |  |
| 연결 관리자 관리 키트  | X |  |
| 데스크톱 환경  | X |  |
| 장애 조치(failover) 클러스터링  | X  | X |
| 그룹 정책 관리  | X  |  |
| 인터넷 인쇄 클라이언트  | X  |  |
| 인터넷 저장소 이름 서버  | X  |  |
| LPR 포트 모니터  | X  |  |
| 메시지 큐  | X  |  |
| 다중 경로 IO  | X  | X |
| 네트워크 부하 분산  | X  | X |
| 피어 이름 확인 프로토콜  | X  |  |
| qWave(Quality Windows Audio Video Experience)  | X |  |
| 원격 지원  | X  |  |
| 원격 차등 압축 | X  |  |
| 원격 서버 관리 도구  | X  |  |
| 이동식 저장소 관리자 | X  | X |
| RPC Over HTTP 프록시 | X  |  |
| 단순 TCP/IP 서비스  | X  |  |
| SMTP 서버  | X  |  |
| SMNP 서비스  | X  | X  |
| San 저장소 관리자  | X  |  |
| UNIX 기반 응용 프로그램용 하위 시스템 | X | X  |
| 텔넷 클라이언트  | X | X  |
| 텔넷 서버  | X   |  |
| TFTP 클라이언트  | X   |  |
| Windows 내부 데이터베이스  | X  |  |
| Windows PowerShell  | X  |  |
| Windows 제품 정품 인증 서비스  | X   |  |
| Windows Server 백업 기능  | X  | X  |
| Windows 시스템 리소스 관리자  | X  |  |
| WINS 서버  | X | X |
| 무선 LAN 서비스 | X  |  |

또한 Server Core에서 사용할 수 있는 기능과 관련 하 여 알아야 할 몇 가지 사항이 있습니다.
* 일부 기능에는 Server Core에서 제대로 작동 하는 특수 하드웨어가 필요할 수 있습니다. 이러한 기능에는 BitLocker 드라이브 암호화, 장애 조치 (Failover) 클러스터링, 다중 경로 IO, 네트워크 부하 분산 및 이동식 저장소가 포함 됩니다. 
* Standard Edition에서는 장애 조치 (Failover) 클러스터링을 사용할 수 없습니다.

## <a name="server-core-architecture"></a>Server Core 아키텍처
Server Core에 대해 자세히 살펴보기, 전체 설치와 비교 하 여 Windows Server 2008의 Server Core 설치 아키텍처를 간략하게 살펴보겠습니다. 첫째, Server Core는 Windows Server 2008의 다른 버전이 아니라 시스템에 Windows Server 2008을 설치할 때 선택할 수 있는 설치 옵션 일 뿐입니다. 이것은 다음을 의미합니다.
* Server Core 설치에 대 한 커널은 동일한 하드웨어 아키텍처 (x86 또는 x64) 및 edition의 전체 설치에 있는 것과 동일 합니다. 
* Server Core 설치에 이진 파일이 있는 경우 동일한 하드웨어 아키텍처 (x86 또는 x64) 및 edition의 전체 설치에는 해당 특정 이진 파일의 동일한 버전이 있습니다 (뒷부분에서 설명 하는 두 가지 예외). 
* 특정 설정 (예: 특정 서비스의 특정 방화벽 예외 또는 시작 유형)에 특정 기본 구성이 Server Core 설치에 있는 경우이 설정은 동일 하 게 전체 설치에 대해 동일한 방식으로 구성 됩니다. 하드웨어 아키텍처 (x86 또는 x64) 및 edition.

그림 1-3에서는 Windows Server 2008의 전체 설치 및 Server Core 설치의 아키텍처에 대 한 간단한 보기를 보여 줍니다. 점선은 Server Core의 아키텍처를 나타내고 전체 다이어그램은 전체 설치의 아키텍처를 나타냅니다. 

이 다이어그램에서는 핵심 운영 체제 기능의 하위 집합에 서버 코어가 생성 되는 Windows Server 2008의 모듈식 아키텍처를 보여 줍니다. 동일한 하드웨어 아키텍처 및 버전의 경우 server core를 새로 설치 하는 경우에도 전체 설치에 제공 되는 모든 파일은 Server Core에만 있는 특수 파일 두 개 (Scregedit.exe. .wsf 및 Oclist .exe)를 제외 하 고 전체 설치에도 제공 됩니다. 이러한 특수 파일은 Server Core 설치의 초기 구성과 역할 및 선택적 구성 요소의 추가 또는 제거를 간소화 하기 위해 Server Core에 포함 되었습니다. 

![Server Core 및 전체 설치의 아키텍처](../media/what-is-server-core-2008/Fig1-3.png)

**그림 1-3** Server Core 및 전체 설치의 아키텍처

## <a name="driver-support"></a>드라이버 지원
그림 1-3에 표시 된 Server Core의 아키텍처 다이어그램은 분명 하 게 간소화 되었습니다. 표시 되지 않는 한 가지 사항은 Server Core와 전체 설치 간의 장치 드라이버 지원의 차이점입니다. Windows Server 2008 전체 설치에는 다양 한 하드웨어 구성에 제품을 설치할 수 있는 다양 한 유형의 장치에 대 한 다양 한 기본 드라이버가 포함 되어 있습니다. Windows Vista와 같은 클라이언트 운영 체제에는 일반적으로 서버에서 사용 되지 않는 디지털 카메라 및 스캐너와 같은 장치를 지원 하기 위한 더 많은 드라이버가 포함 되어 있습니다. 

새 장치가 Windows Server 2008 전체 설치에 연결 되어 있거나 설치 되어 있는 경우 PnP (플러그 앤 플레이) 하위 시스템은 먼저 장치에 대 한 기본 제공 드라이버가 있는지 여부를 확인 합니다. 호환 되는 기본 제공 드라이버가 있는 경우 PnP 하위 시스템에서 자동으로 드라이버를 설치 하 고 장치가 작동 합니다. Windows Server 2008 전체 설치에서는 드라이버가 설치 되어 있고 장치를 사용할 준비가 되었음을 나타내는 풍선 팝업 알림이 표시 될 수 있습니다. 

Server Core 설치에서 드라이버 설치 프로세스는 두 가지 자격을 사용 하는 것과 동일 합니다 (PnP 하위 시스템은 Server Core에 있음). 첫째, Server Core는 최소 수의 기본 제공 드라이버만 포함 하 고 다음 유형의 장치만 포함 합니다.
* 표준 비디오 그래픽 배열 (VGA) 비디오 드라이버 
* 저장 장치용 드라이버 
* 네트워크 어댑터용 드라이버

여기에 표시 된 세 가지 장치 범주 각각에 대해 Server Core는 동일한 하드웨어 아키텍처에 대해 해당 하는 전체 설치에 있는 동일한 기본 제공 드라이버를 포함 합니다. 

또한 PnP 하위 시스템이 새 장치용 드라이버를 자동으로 설치 하는 경우 자동으로 수행 되므로 풍선 팝업 알림이 표시 되지 않습니다. 왜 안 돼요? Server Core에는 GUI 없으므로 작업 표시줄은 없으므로 작업 표시줄에 알림 영역이 없습니다. 

따라서 Server Core 설치에 인쇄 서비스 역할을 추가할 때 프린터를 설치 하려면 어떻게 해야 하나요? 서버에 프린터 드라이버를 수동으로 추가 하는 경우-Server Core에는 기본 인쇄 드라이버가 없습니다.

## <a name="service-footprint"></a>서비스 공간
Server Core는 최소 설치 이므로 동일한 하드웨어 아키텍처 및 버전의 해당 전체 설치 보다 더 작은 시스템 서비스 공간을 사용 합니다. 예를 들어 약 75 시스템 서비스는 Windows Server 2008 전체 설치 시 기본적으로 설치 되며,이 중 약 50는 자동으로 시작 되도록 구성 됩니다. 이와 대조적으로 Server Core에는 기본적으로 설치 되는 70 대의 서비스만 있고 이러한 시작의 경우 40 개 미만으로 자동으로 설치 됩니다. 

표 1-5에는 Server Core 설치 시 기본적으로 설치 되는 서비스와 각 서비스에서 사용 하는 계정에 대 한 시작 모드가 나열 되어 있습니다.

**표 1-5** 기본적으로 Server Core에 설치 된 시스템 서비스

| 서비스 이름  | Display name  | 시작 모드  | 계정  |
| ------------- | ------------- | ------------ | ------------ |
| AeLookupSvc  | 응용 프로그램 환경  | 자동 | LocalSystem |
| AppMgmt  | 응용 프로그램 관리  | 수동 | LocalSystem |
| BFE | 기본 필터링 엔진  | 자동 | LocalService |
| BITS | BITS(Background Intelligent Transfer Service)  | 자동 | LocalSystem |
| 브라우저 | 컴퓨터 브라우저  | 수동 | LocalSystem |
| CertPropSvc | 인증서 전파  | 수동 | LocalSystem |
| COMSysApp  | COM+ 시스템 응용 프로그램  | 수동 | LocalSystem |
| CryptSvc  | 암호화 서비스  | 자동 | 네트워크 서비스 |
| DcomLaunch  | DCOM Server Process Launcher  | 자동 | LocalSystem |
| Dhcp  | DHCP 클라이언트  | 자동 | LocalService |
| Dnscache | DNS 클라이언트  | 자동 | 네트워크 서비스 |
| DPS  | 진단 정책 서비스  | 자동 | LocalService |
| Eventlog | Windows 이벤트 로그  | 자동 | LocalService |
| EventSystem  | COM + 이벤트 시스템  | 자동 | LocalService |
| FCRegSvc  | Microsoft 파이버 채널 Platform 등록 서비스  | 수동 | LocalService |
| gpsvc  | 그룹 정책 클라이언트  | 자동 | LocalSystem |
| hidserv | 휴먼 인터페이스 장치 액세스  | 수동 | LocalSystem |
| hkmsvc  | 상태 키 및 인증서 관리  | 수동 | LocalSystem |
| IKEEXT  | IKE 및 AuthIP IPsec 키 지정 모듈  | 자동 | LocalSystem |
| iphlpsvc  | IP 도우미  | 자동 | LocalSystem |
| KeyIso | CNG 키 격리  | 수동 | LocalSystem |
| KtmRm  | DTC(Distributed Transaction Coordinator)용 KtmRm  | 자동 | 네트워크 서비스 |
| LanmanServer  | 서버  | 자동 | LocalSystem |
| LanmanWorkstation  | Workstatione  | 자동 | LocalService |
| lltdsvc  | Link-Layer Topology Discovery Mapper  | 수동 | LocalService |
| lmhosts  | TCP/IP NetBIOS 도우미  | 자동 | LocalService |
| MpsSvc  | Windows 방화벽  | 자동 | LocalService |
| MSDTC  | DTC(Microsoft Distributed Transaction Coordinator)  | 자동 | 네트워크 서비스 |
| MSiSCSI  | Microsoft iSCSI 초기자 서비스  | 수동 | LocalSystem |
| msiserver  | Windows Installer  | 수동 | LocalSystem |
| napagent  | 네트워크 액세스 보호 에이전트  | 수동 | 네트워크 서비스 |
| Netlogon  | Netlogon  | 수동 | LocalSystem |
| netprofm  | 네트워크 목록 서비스  | 자동 | LocalService |
| NlaSvc  | 네트워크 위치 인식  | 자동 | 네트워크 서비스 |
| nsi  | 네트워크 저장소 인터페이스 서비스  | 자동 | LocalService |
| pla  | 성능 로그 및 경고  | 수동 | LocalService |
| PlugPlay  | 플러그 앤 플레이  | 자동 | LocalSystem |
| PolicyAgent  | IPSec 정책 에이전트  | 자동 | 네트워크 서비스 |
| ProfSvc  | 사용자 프로필 서비스  | 자동 | LocalSystem |
| ProtectedStorage  | 보호 된 저장소  | 수동 | LocalSystem |
| RemoteRegistry  | 원격 레지스트리  | 자동 | LocalService |
| RpcSs  | RPC(원격 프로시저 호출)  | 자동 | 네트워크 서비스 |
| RSoPProv | 공급자 정책 결과 집합  | 수동 | LocalSystem |
| sacsvr  | 특수 관리 콘솔 도우미  | 수동 | LocalSystem |
| SamSs  | 보안 계정 관리자  | 자동 | LocalSystem |
| SCardSvr | 스마트 카드  | 수동 | LocalService |
| 일정 | 작업 스케줄러  | 자동 | LocalSystem |
| SCPolicySvc | 스마트 카드 제거 정책  | 수동 | LocalSystem |
| seclogon | 보조 타일  | 자동 | LocalSystem |
| SENS | 시스템 이벤트 알림 서비스  | 자동 | LocalSystem |
| SessionEnv | 터미널 서비스 구성  | 수동 | LocalSystem |
| slsvc  | 소프트웨어 라이선스 | 자동 | 네트워크 서비스 |
| SNMPTRAP  | SNMP 트랩  | 수동 | LocalService |
| swprv  | Microsoft 소프트웨어 섀도 복사본 공급자 | 수동 | LocalSystem |
| TBS | TPM 기본 서비스  | 수동 | LocalService |
| TermService  | 터미널 서비스 | 자동 | 네트워크 서비스 |
| TrustedInstaller | Windows 모듈 설치 관리자  | 자동 | LocalSystem |
| UmRdpService | 터미널 서비스 UserMode 포트 리디렉터  | 수동 | LocalSystem |
| vds | 가상 디스크  | 수동 | LocalSystem |
| VSS | 볼륨 섀도 복사본  | 수동 | LocalSystem |
| W32Time | Windows 시간  | 자동 | LocalService |
| WcsPlugInService  | Windows 색 시스템  | 수동 | LocalService |
| WdiServiceHost  | 진단 서비스 호스트  | 수동 | LocalService |
| WdiSystemHost  | 진단 시스템 호스트  | 수동 | LocalSystem |
| Wecsvc | Windows 이벤트 수집기  | 수동 | 네트워크 서비스 |
| WinHttpAuto-ProxySvc  | WinHTTP 웹 프록시 자동 검색 서비스  | 자동 | LocalService |
| Winmgmt | Windows Management Instrumentation | 자동 | LocalSystem |
| WinRM  | Windows 원격 관리(WS-Management) | 자동 | 네트워크 서비스 |
| wmiApSrv  | WMI Performance Adapter  | 수동 | LocalSystem |
| wuauserv | Windows 업데이트 | 자동 | LocalSystem |