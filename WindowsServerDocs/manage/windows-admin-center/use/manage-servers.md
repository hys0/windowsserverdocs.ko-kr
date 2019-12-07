---
title: Windows 관리 센터를 사용 하 여 서버 관리
description: Windows 관리 센터 (Project Honolulu)를 사용 하 여 서버 관리
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 11/21/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 9a116cc9d86dfe0bb4450efa0f18580a062af722
ms.sourcegitcommit: 7c7fc443ecd0a81bff6ed6dbeeaf4f24582ba339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2019
ms.locfileid: "74903722"
---
# <a name="manage-servers-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 서버 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="managing-windows-server-machines"></a>Windows Server 컴퓨터 관리

Windows Server 2012 이상을 실행 하는 개별 서버를 Windows 관리 센터에 추가 하 여 인증서, 장치, 이벤트, 프로세스, 역할 및 기능, 업데이트, Virtual Machines 등의 포괄적인 도구 집합으로 서버를 관리할 수 있습니다.

![서버 연결 개요 화면](../media/manage-servers/server-overview.png)

## <a name="adding-a-server-to-windows-admin-center"></a>Windows 관리 센터에 서버 추가

Windows 관리 센터에 서버를 추가 하려면 다음을 수행 합니다.

1. 모든 연결에서 **+ 추가** 를 클릭 합니다.
2. **서버 연결**을 추가 하도록 선택 합니다.
3. 서버 이름을 입력 하 고, 메시지가 표시 되 면 사용할 자격 증명을 입력 합니다.
4. **제출을** 클릭 하 여 완료 합니다.

이 서버는 개요 페이지의 연결 목록에 추가 됩니다. 클릭 하 여 서버에 연결 합니다.

> [!NOTE]
> Windows 관리 센터에서 [장애 조치 (failover) 클러스터](manage-failover-clusters.md) 또는 [하이퍼 수렴 형 클러스터](manage-hyper-converged.md) 를 별도의 연결로 추가할 수도 있습니다.

## <a name="tools"></a>도구

서버 연결에 사용할 수 있는 도구는 다음과 같습니다.

| 도구 | 설명 |
| ---- | ----------- |
| [개요](#overview) | 서버 세부 정보 및 컨트롤 서버 상태 보기 |
| [Active Directory](#active-directory-preview) | Active Directory 관리 |
| [Backup](#backup) | Azure Backup 보기 및 구성 |  
| [인증서](#certificates) | 인증서 보기 및 수정 |
| [SSIS 로그 구성](#containers) | 컨테이너 보기 |
| [디바이스](#devices) | 장치 보기 및 수정 |
| [DHCP](#dhcp) | DHCP 서버 구성 보기 및 관리 |
| [DNS](#dns) | DNS 서버 구성 보기 및 관리 |
| [이벤트](#events) | 이벤트 보기 |
| [파일](#files) | 파일 및 폴더 찾아보기 |
| [Firewall](#firewall) | 방화벽 규칙 보기 및 수정 |
| [설치 된 앱](#installed-apps) | 설치 된 앱 보기 및 제거 |
| [로컬 사용자 및 그룹](#local-users-and-groups) | 로컬 사용자 및 그룹 보기 및 수정 |
| [Network](#network) | 네트워크 장치 보기 및 수정 |
| [패킷 모니터링](https://aka.ms/wac1908) | 네트워크 패킷 모니터링 |
| [성능 모니터](https://aka.ms/perfmon-blog) | 성능 카운터 및 보고서 보기 |
| [PowerShell](#powershell) | PowerShell을 통해 서버와 상호 작용 |
| [프로세스](#processes) | 실행 중인 프로세스 보기 및 수정 |
| [Registry](#registry) | 레지스트리 항목 보기 및 수정 |
| [원격 데스크톱](#remote-desktop) | 원격 데스크톱을 통해 서버와 상호 작용 |
| [역할 및 기능](#roles-and-features) | 역할 및 기능 보기 및 수정 |
| [예약 된 작업](#scheduled-tasks) | 예약 된 작업 보기 및 수정 |
| [서비스](#services) | 서비스 보기 및 수정 |
| [설정](#settings) | 서비스 보기 및 수정 |
| [저장소](#storage) | 저장 장치 보기 및 수정 |
| [저장소 마이그레이션 서비스](#storage-migration-service) | Azure 또는 Windows Server 2019로 서버 및 파일 공유 마이그레이션 |
| [스토리지 복제본](#storage-replica) | 저장소 복제본을 사용 하 여 서버 간 저장소 복제 관리 |
| [시스템 인사이트](#system-insights) | 시스템 정보를 통해 서버 작동에 대 한 통찰력을 높일 수 있습니다. |
| [Updates](#updates) | 설치 된 보기 및 새 업데이트 확인 |
| [Virtual Machines](manage-virtual-machines.md) | 가상 컴퓨터 보기 및 관리 |
| [가상 스위치](#virtual-switches) | 가상 스위치 보기 및 관리 |

## <a name="overview"></a>개요

**개요** 를 사용 하면 CPU, 메모리 및 네트워크 성능의 현재 상태를 볼 수 있을 뿐만 아니라 대상 컴퓨터 또는 서버에서 작업을 수행 하 고 설정을 수정할 수 있습니다.

### <a name="features"></a>기능

서버 관리자 개요에서 지원 되는 기능은 다음과 같습니다.

- 서버 세부 정보 보기
- CPU 작업 보기
- 메모리 작업 보기
- 네트워크 활동 보기
- 서버 다시 시작
- 서버 종료
- 서버에서 디스크 메트릭 사용
- 서버에서 컴퓨터 ID 편집
- 하이퍼링크가 있는 BMC IP 주소 보기 (IPMI 호환 BMC 필요).

[**서버 개요에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D).

## <a name="active-directory-preview"></a>Active Directory (미리 보기)

**Active Directory** 는 [확장 피드에서](../configure/using-extensions.md)사용할 수 있는 초기 미리 보기입니다.

### <a name="features"></a>기능

사용할 수 있는 Active Directory 관리는 다음과 같습니다.

- 사용자 만들기
- 그룹 만들기
- 사용자, 컴퓨터 및 그룹 검색
- 표에서 선택 하는 경우 사용자, 컴퓨터 및 그룹에 대 한 세부 정보 창
- 전역 그리드 작업 사용자, 컴퓨터 및 그룹 (사용 안 함/사용, 제거)
- 사용자 암호 다시 설정
- 사용자 개체: 그룹 멤버 자격 & 기본 속성 구성
- 컴퓨터 개체: 단일 컴퓨터에 대 한 위임 구성
- 그룹 개체: 멤버 자격 관리 (한 번에 1 개의 사용자 추가/제거)  

[**Active Directory에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BActive%20Directory%5D).

## <a name="backup"></a>백업

**백업을** 사용 하면 서버를 Microsoft Azure에 직접 백업 하 여 손상, 공격 또는 재해 로부터 Windows 서버를 보호할 수 있습니다.
[Azure Backup에 대해 자세히 알아보세요.](https://aka.ms/windows-admin-center-backup)

[Windows 관리 센터에서 백업에 대 한 피드백 제공](https://aka.ms/backup-wac-feedback)

### <a name="features"></a>기능

백업에서 지원 되는 기능은 다음과 같습니다.

- Azure 백업 상태 개요 보기
- 백업 항목 및 일정 구성
- 백업 작업 시작 또는 중지
- 백업 작업 기록 및 상태 보기
- 복구 지점의 보기 및 데이터 복구
- 백업 데이터 삭제

## <a name="certificates"></a>인증서

**인증서** 를 사용 하 여 컴퓨터 또는 서버의 인증서 저장소를 관리할 수 있습니다.

### <a name="features"></a>기능

인증서에서 지원 되는 기능은 다음과 같습니다.

- 기존 인증서 찾아보기 및 검색
- 인증서 세부 정보 보기
- 인증서 내보내기
- 인증서 갱신
- 새 인증서 요청
- 인증서 삭제

[**인증서에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D).

## <a name="containers"></a>컨테이너

**컨테이너** 를 사용 하면 Windows Server 컨테이너 호스트에서 컨테이너를 볼 수 있습니다. Windows Server Core 컨테이너를 실행 하는 경우에는 이벤트 로그를 확인 하 고 컨테이너의 CLI에 액세스할 수 있습니다.

[**컨테이너에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D)

## <a name="devices"></a>장치

**장치** 를 사용 하면 컴퓨터 또는 서버에서 연결 된 장치를 관리할 수 있습니다.

### <a name="features"></a>기능

장치에서 지원 되는 기능은 다음과 같습니다.

- 장치 찾아보기 및 검색
- 디바이스 세부 정보 보기
- 디바이스 사용 안 함
- 장치에서 드라이버 업데이트

[**장치에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)

## <a name="dhcp"></a>DHCP

**DHCP** 를 사용 하면 컴퓨터 또는 서버에서 연결 된 장치를 관리할 수 있습니다.

### <a name="features"></a>기능

- IPV4 및 IPV6 범위 만들기/구성/보기
- 주소 제외 만들기 및 시작 및 끝 IP 주소 구성
- 주소 예약 만들기 및 클라이언트 MAC 주소 (IPV4), DUID 및 IAID (IPV6) 구성

[**DHCP에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDHCP%5D).

## <a name="dns"></a>DNS

**DNS** 를 사용 하면 컴퓨터 또는 서버에서 연결 된 장치를 관리할 수 있습니다.

### <a name="features"></a>기능

- DNS 전방 조회 영역, 역방향 조회 영역 및 DNS 레코드의 세부 정보 보기
- 전방 조회 영역 (기본, 보조 또는 스텁) 만들기 및 전방 조회 영역 속성 구성
- 호스트 (A 또는 AAAA), CNAME 또는 MX 유형의 DNS 레코드를 만듭니다.
- DNS 레코드 속성 구성
- IPV4 및 IPV6 역방향 조회 영역 (기본, 보조 및 스텁) 만들기, 역방향 조회 영역 속성 구성
- 역방향 조회 영역 아래에서 PTR, CNAME 유형의 DNS 레코드를 만듭니다.

[**DHCP에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDNS%5D).

## <a name="events"></a>이벤트

**이벤트** 를 사용 하 여 컴퓨터 또는 서버에서 이벤트 로그를 관리할 수 있습니다.

### <a name="features"></a>기능

이벤트에서 지원 되는 기능은 다음과 같습니다.

- 찾아보기 및 검색 이벤트
- 이벤트 세부 정보 보기
- 로그에서 이벤트 지우기
- 로그에서 이벤트 내보내기

[**이벤트에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D).

## <a name="files"></a>파일

**파일** 을 사용 하 여 컴퓨터 또는 서버에서 파일 및 폴더를 관리할 수 있습니다.

### <a name="features"></a>기능

파일에서 지원 되는 기능은 다음과 같습니다.

- 파일 및 폴더 찾아보기
- 파일이 나 폴더를 검색 합니다.
- 새 폴더 만들기
- 파일 또는 폴더 삭제
- 파일 또는 폴더 다운로드
- 파일 또는 폴더 업로드
- 파일 또는 폴더 이름 바꾸기
- Zip 파일 추출
- 파일 또는 폴더 속성 보기
- 파일 공유 추가, 편집 또는 제거
- 파일 공유에 대 한 사용자 및 그룹 권한 수정

[**파일에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D)

## <a name="firewall"></a>방화벽

**방화벽** 을 통해 컴퓨터 또는 서버에서 방화벽 설정 및 규칙을 관리할 수 있습니다.

### <a name="features"></a>기능

방화벽에서 지원 되는 기능은 다음과 같습니다.

- 방화벽 설정 개요 보기
- 들어오는 방화벽 규칙 보기
- 나가는 방화벽 규칙 보기
- 방화벽 규칙 검색
- 방화벽 규칙 세부 정보 보기
- 새 방화벽 규칙을 만듭니다.
- 방화벽 규칙 사용 또는 사용 안 함
- 방화벽 규칙 삭제
- 방화벽 규칙의 속성 편집

[**방화벽에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D).

## <a name="installed-apps"></a>설치 된 앱

**설치 된 앱** 을 사용 하면 설치 된 응용 프로그램을 나열 하 고 제거할 수 있습니다.

[**설치 된 앱에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D).

## <a name="local-users-and-groups"></a>로컬 사용자 및 그룹

**로컬 사용자 및 그룹** 을 사용 하면 컴퓨터 또는 서버에서 로컬로 존재 하는 보안 그룹 및 사용자를 관리할 수 있습니다.

### <a name="features"></a>기능

로컬 사용자 및 그룹에서 지원 되는 기능은 다음과 같습니다.

- 사용자 및 그룹 보기 및 검색
- 새 사용자 또는 그룹 만들기
- 사용자의 그룹 구성원 자격 관리
- 사용자 또는 그룹 삭제
- 사용자 암호를 변경합니다.
- 사용자 또는 그룹의 속성 편집

[**로컬 사용자 및 그룹에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## <a name="network"></a>네트워크

**네트워크** 를 사용 하면 컴퓨터 또는 서버에서 네트워크 장치 및 설정을 관리할 수 있습니다.

### <a name="features"></a>기능

네트워크에서 지원 되는 기능은 다음과 같습니다.

- 기존 네트워크 어댑터 찾아보기 및 검색
- 네트워크 어댑터의 세부 정보 보기
- 네트워크 어댑터의 속성 편집
- [Azure 네트워크 어댑터 만들기 (미리 보기 기능)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**네트워크에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## <a name="powershell"></a>PowerShell

**Powershell** 을 사용 하면 powershell 세션을 통해 컴퓨터 또는 서버와 상호 작용할 수 있습니다.

### <a name="features"></a>기능

PowerShell에서 지원 되는 기능은 다음과 같습니다.

- 서버에서 대화형 PowerShell 세션 만들기
- 서버의 PowerShell 세션에서 연결 끊기

[**PowerShell에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## <a name="processes"></a>Processes

**프로세스** 를 사용 하 여 컴퓨터 또는 서버에서 실행 중인 프로세스를 관리할 수 있습니다.

### <a name="features"></a>기능

프로세스에서 지원 되는 기능은 다음과 같습니다.

- 실행 중인 프로세스 찾아보기 및 검색
- 프로세스 정보 보기
- 프로세스 시작
- 프로세스 종료
- 프로세스 덤프 만들기
- 프로세스 핸들 찾기

[**프로세스에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D).

## <a name="registry"></a>레지스트리

**레지스트리** 를 사용 하면 컴퓨터 또는 서버에서 레지스트리 키와 값을 관리할 수 있습니다.

### <a name="features"></a>기능

레지스트리에서 지원 되는 기능은 다음과 같습니다.

- 레지스트리 키 및 값 찾아보기
- 레지스트리 값 추가 또는 수정
- 레지스트리 값 삭제

[**레지스트리의 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D)

## <a name="remote-desktop"></a>원격 데스크톱

**원격 데스크톱** 을 사용 하면 대화형 데스크톱 세션을 통해 컴퓨터 또는 서버와 상호 작용할 수 있습니다.

### <a name="features"></a>기능

원격 데스크톱에서 지원 되는 기능은 다음과 같습니다.

- 대화형 원격 데스크톱 세션 시작
- 원격 데스크톱 세션에서 연결 끊기
- 원격 데스크톱 세션에 Ctrl + Alt + Del 보내기

[**원격 데스크톱에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D).

## <a name="roles-and-features"></a>역할 및 기능

**역할 및 기능** 을 사용 하면 서버에서 역할 및 기능을 관리할 수 있습니다.

### <a name="features"></a>기능

역할 및 기능에서 지원 되는 기능은 다음과 같습니다.

- 서버에서 역할 및 기능 목록 찾아보기
- 역할 또는 기능 세부 정보 보기
- 역할 또는 기능 설치
- 역할 또는 기능 제거

[**역할 및 기능에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D).

## <a name="scheduled-tasks"></a>예약된 작업

**예약 된 작업** 을 통해 컴퓨터 또는 서버에서 예약 된 작업을 관리할 수 있습니다.

### <a name="features"></a>기능

예약 된 작업에서 지원 되는 기능은 다음과 같습니다.

- 작업 scheduler 라이브러리 찾아보기
- 예약 된 작업 편집
- 예약 된 작업 사용 & 사용 안 함
- 예약 된 작업을 시작 & 중지
- 예약 된 작업 만들기

[**예약 된 작업에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D).

## <a name="services"></a>서비스

**서비스** 를 사용 하면 컴퓨터 또는 서버에서 서비스를 관리할 수 있습니다.

### <a name="features"></a>기능

서비스에서 지원 되는 기능은 다음과 같습니다.

- 서버에서 서비스 찾아보기 및 검색
- 서비스의 세부 정보 보기
- 서비스 시작
- 서비스 일시 중지
- 서비스 속성 편집

[**서비스에 대 한 사용자 의견 및 제안 된 기능을 봅니다**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D).

## <a name="settings"></a>설정

**설정은** 컴퓨터 또는 서버에서 설정을 관리할 수 있는 중앙 위치입니다.

### <a name="features"></a>기능

- 사용자 및 시스템 환경 변수 보기 및 수정
- [Azure Monitor](azure-monitor.md) 에서 경고 모니터링에 대 한 구성을 확인 합니다.
- 전원 구성 보기 및 수정
- 원격 데스크톱 설정 보기 및 수정
- 역할 기반 액세스 제어 설정 보기 및 수정
- Hyper-v 호스트 설정 보기 및 수정 (해당 하는 경우)

## <a name="storage"></a>저장소

**저장소** 를 사용 하면 컴퓨터 또는 서버에서 저장 장치를 관리할 수 있습니다.

### <a name="features"></a>기능

저장소에서 지원 되는 기능은 다음과 같습니다.

- 서버에서 기존 디스크 찾아보기 및 검색
- 디스크 세부 정보 보기
- 볼륨 만들기
- 디스크 초기화
- VHD (가상 하드 디스크) 만들기, 연결 및 분리
- 디스크를 오프 라인 상태로 만들기
- 볼륨 포맷
- 볼륨 크기 조정
- 볼륨 속성 편집
- 볼륨 삭제
- 할당량 관리 설치
- 파일 서버 리소스 관리자 할당량 [저장소 관리-할당량 만들기/업데이트 >](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management)

[**저장소에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## <a name="storage-migration-service"></a>스토리지 마이그레이션 서비스

**Storage Migration Service** 를 사용 하면 앱 또는 사용자가 아무것도 변경 하지 않고도 서버 및 파일 공유를 Azure 또는 Windows Server 2019로 마이그레이션할 수 있습니다.
[Storage Migration Service 개요 보기](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>Storage Migration Service에는 Windows Server 2019이 필요 합니다.

## <a name="storage-replica"></a>저장소 복제본

**저장소 복제본** 을 사용 하 여 서버 간 저장소 복제를 관리할 수 있습니다.
[저장소 복제본에 대 한 자세한 정보](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## <a name="system-insights"></a>시스템 인사이트

**System Insights** 는 서버 작동에 대 한 통찰력을 향상 시킬 수 있도록 Windows server에 기본적으로 제공 되는 예측 분석을 도입 합니다.
[시스템 정보에 대 한 개요 보기](https://aka.ms/systeminsights)

>[!NOTE]
>시스템 정보를 사용 하려면 Windows Server 2019이 필요 합니다.

## <a name="updates"></a>업데이트

**업데이트** 를 사용 하면 컴퓨터 또는 서버에서 Microsoft 및/또는 Windows 업데이트를 관리할 수 있습니다.

### <a name="features"></a>기능

업데이트에서 지원 되는 기능은 다음과 같습니다.

- 사용 가능한 Windows 또는 Microsoft 업데이트 보기
- 업데이트 기록 목록 보기
- 업데이트 설치
- 온라인에서 업데이트 확인 Microsoft 업데이트
- [Azure 업데이트 관리](https://docs.microsoft.com/azure/automation/automation-update-management) 통합 관리

[**업데이트에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## <a name="virtual-machines"></a>가상 머신

[Windows 관리 센터를 사용 하 여 Virtual Machines 관리를](manage-virtual-machines.md) 참조 하세요.

## <a name="virtual-switches"></a>가상 스위치

**가상 스위치** 를 사용 하면 컴퓨터 또는 서버에서 hyper-v 가상 스위치를 관리할 수 있습니다.

### <a name="features"></a>기능

가상 스위치에서 지원 되는 기능은 다음과 같습니다.

- 서버에서 가상 스위치 찾아보기 및 검색
- 새 가상 스위치 만들기
- 가상 스위치 이름 바꾸기
- 기존 가상 스위치를 삭제 합니다.
- 가상 스위치의 속성 편집

[**가상 스위치에 대 한 사용자 의견 및 제안 된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
