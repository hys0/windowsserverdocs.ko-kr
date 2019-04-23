---
title: Windows Admin Center 사용 하 여 서버 관리
description: Windows Admin Center (프로젝트 브라 티)를 사용 하 여 서버 관리
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 04ade4a14272c7840b5036ca6ad5a3bf3d09bcf9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891154"
---
# <a name="manage-servers-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 서버 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="managing-windows-server-machines"></a>Windows Server 컴퓨터를 관리합니다.

Windows Server 2012를 실행 하거나 나중에 다양 한 도구를 사용 하 여 서버를 관리 하려면 Windows Admin Center 인증서, 장치, 이벤트, 프로세스, 역할 및 기능, 업데이트, Virtual Machines 및 더를 포함 하는 개별 서버를 추가할 수 있습니다.

![서버 연결 개요 화면](../media/manage-servers/server-overview.png)

## <a name="adding-a-server-to-windows-admin-center"></a>Windows Admin Center 서버 추가

에 추가 하려면 서버를 Windows Admin Center:

1. 클릭 **+ 추가** 모든 연결 합니다.
2. 추가 하도록 선택 된 **서버 연결**합니다.
3. 서버의 이름을 입력 하 고, 메시지가 표시 되 면 사용할 자격 증명입니다.
4. 클릭 **제출** 완료 합니다.

서버 개요 페이지에서 연결 목록에 추가 됩니다. 서버에 연결 하려면 클릭 합니다.

> [!NOTE]
> 추가할 수도 있습니다 [장애 조치 클러스터](manage-failover-clusters.md) 하거나 [하이퍼 수렴 형 클러스터](manage-hyper-converged.md) Windows Admin Center 별도 연결으로 합니다.

## <a name="tools"></a>Tools

다음 도구를 서버 연결에 사용할 수 있습니다.

| 도구 | 설명 |
| ---- | ----------- |
| [개요](#overview) | 서버 세부 정보 보기 및 서버 상태를 제어 합니다. |
| [Backup](#backup) | 보기 및 Azure Backup 구성 |  
| [인증서](#certificates) | 보기 및 인증서를 수정 합니다. |
| [컨테이너](#containers) | 컨테이너 보기 |
| [디바이스](#devices) | 보기 및 장치를 수정 합니다. |
| [이벤트](#events) | 이벤트 보기 |
| [파일](#files) | 파일 및 폴더 찾아보기 |
| [방화벽](#firewall) | 보기 및 방화벽 규칙 수정 |
| [설치 된 앱](#installed-apps) | 보기 및 설치 된 앱 제거 |
| [로컬 사용자 및 그룹](#local-users-and-groups) | 로컬 사용자 및 그룹 보기 및 수정 |
| [Network](#network) | 보기 및 네트워크 장치를 수정 합니다. |
| [PowerShell](#powershell) | PowerShell 통해 서버와 상호 작용 |
| [프로세스](#processes) | 보기 및 수정 프로세스를 실행 합니다. |
| [Registry](#registry) | 보기 및 레지스트리 항목 수정 |
| [원격 데스크톱](#remote-desktop) | 원격 데스크톱을 통해 서버와 상호 작용 |
| [역할 및 기능](#roles-and-features) | 역할 및 기능 보기 및 수정 |
| [예약 된 작업](#scheduled-tasks) | 보기 및 예약 된 작업 수정 |
| [Services](#services) | 보기 및 서비스를 수정 합니다. |
| [저장소](#storage) | 보기 및 저장 장치를 수정 합니다. |
| [저장소 마이그레이션 서비스](#storage-migration-service) | 서버 및 파일 공유를 Azure 또는 Windows Server 2019 마이그레이션 |
| [저장소 복제본](#storage-replica) | 저장소 복제본을 사용 하 여 서버 간 저장소 복제 관리 |
| [시스템 정보](#system-insights) | 시스템 Insights 사용 하면 서버의 기능에 대 한 정보를 증가 합니다. |
| [업데이트](#updates) | 설치 하는 보기와 새 업데이트 확인 |
| [Virtual Machines](manage-virtual-machines.md) | 가상 컴퓨터 보기 및 관리 |
| [가상 스위치](#virtual-switches) | 보기 및 가상 스위치 관리 |

## <a name="overview"></a>개요

**개요** 도로 작업을 수행 하 고 대상 컴퓨터 또는 서버에서 설정을 수정 CPU, 메모리 및 네트워크 성능을의 현재 상태를 확인할 수 있습니다.

### <a name="features"></a>기능

서버 관리자 개요에서 다음과 같은 기능이 지원 됩니다.

- 서버 세부 정보 보기
- 활동 보기 CPU
- 메모리 활동 보기
- 네트워크 활동 보기
- 서버를 다시 시작
- 서버 종료
- 서버에서 디스크 메트릭을 사용 하도록 설정
- 서버에서 컴퓨터 ID 편집

[**서버 개요에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D)합니다.

## <a name="backup"></a>백업

**백업** 손상, 공격 또는 재해 로부터 Microsoft Azure에 직접 서버를 백업 하 여 Windows 서버를 보호할 수 있습니다.
[Azure Backup에 대해 알아봅니다.](https://aka.ms/windows-admin-center-backup)

[백업 Windows Admin Center 대 한 피드백 제공](https://aka.ms/backup-wac-feedback)

### <a name="features"></a>기능

다음 기능은 백업에서 지원 됩니다.

- Azure에 백업 상태의 개요를 보려면
- 백업 항목 및 일정 구성
- 시작 하거나 백업 작업을 중지 합니다.
- 백업 작업 기록 보기 및 상태
- 복구 지점을 보려면 및 데이터 복구
- 백업 데이터 삭제

## <a name="certificates"></a>인증서

**인증서** 컴퓨터 또는 서버의 인증서 저장소를 관리할 수 있습니다.

### <a name="features"></a>기능

인증서에서 다음과 같은 기능이 지원 됩니다.

- 탐색 하 고 기존 인증서를 검색 합니다.
- 인증서 세부 정보 보기
- 인증서 내보내기
- 인증서 갱신
- 새 인증서를 요청 합니다.
- 인증서 삭제

[**인증서에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D)합니다.

## <a name="containers"></a>컨테이너

**컨테이너** Windows Server 컨테이너 호스트에서 컨테이너를 볼 수 있습니다. Windows Server Core 컨테이너를 실행 중인 경우 이벤트 로그를 볼 수 있으며 컨테이너의 CLI에 액세스할 수 있습니다.

[**컨테이너에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D)합니다.

## <a name="devices"></a>장치

**장치** 컴퓨터 또는 서버에 연결 된 장치를 관리할 수 있습니다.

### <a name="features"></a>기능

장치에서 다음과 같은 기능이 지원 됩니다.

- 찾아보기 및 검색 하는 장치
- 장치 세부 정보 보기
- 장치를 사용 하지 않도록 설정
- 장치 드라이버 업데이트

[**장치에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)합니다.

## <a name="events"></a>이벤트

**이벤트** 컴퓨터 또는 서버에서 이벤트 로그를 관리할 수 있습니다.

### <a name="features"></a>기능

이벤트에서 다음과 같은 기능이 지원 됩니다.

- 찾아보기 및 검색 이벤트
- 이벤트 세부 정보 보기
- 로그에서 이벤트 지우기
- 이벤트 로그에서 내보내기

[**이벤트에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D)합니다.

## <a name="files"></a>파일

**파일** 컴퓨터 또는 서버에서 파일 및 폴더를 관리할 수 있습니다.

### <a name="features"></a>기능

파일에서 다음과 같은 기능이 지원 됩니다.

- 파일 및 폴더 찾아보기
- 파일 또는 폴더 검색
- 새 폴더 만들기
- 파일 또는 폴더를 삭제 합니다.
- 파일 또는 폴더를 다운로드 합니다.
- 파일 또는 폴더 업로드
- 파일 또는 폴더 이름 바꾸기
- Zip 파일 추출
- 파일 또는 폴더 속성 보기
- 파일 서버 리소스 관리자 관리 [할당량](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management)
- 추가, 편집 또는 파일 공유를 제거 합니다.
- 사용자 및 그룹 권한 파일 공유를 수정 합니다.

[**파일에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D)합니다.

## <a name="firewall"></a>방화벽

**방화벽** 방화벽 설정 및 컴퓨터 또는 서버에 대 한 규칙을 관리할 수 있습니다.

### <a name="features"></a>기능

방화벽에서 다음과 같은 기능이 지원 됩니다.

- 방화벽 설정의 개요를 보려면
- 들어오는 방화벽 규칙 보기
- 나가는 방화벽 규칙 보기
- 방화벽 규칙 검색
- 방화벽 규칙 세부 정보 보기
- 새 방화벽 규칙 만들기
- 방화벽 규칙을 사용할지 설정 합니다.
- 방화벽 규칙 삭제
- 방화벽 규칙의 속성 편집

[**방화벽에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D)합니다.

## <a name="installed-apps"></a>설치 된 앱

**설치 된 앱** 나열 하 고 설치 된 응용 프로그램을 제거할 수 있습니다.

[**설치 된 앱에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D)합니다.

## <a name="local-users-and-groups"></a>로컬 사용자 및 그룹

**로컬 사용자 및 그룹** 보안 그룹 및 컴퓨터 또는 서버에서 로컬로 존재 하는 사용자를 관리할 수 있습니다.

### <a name="features"></a>기능

로컬 사용자 및 그룹에서 다음과 같은 기능이 지원 됩니다.

- 보기 및 검색 사용자 및 그룹
- 새 사용자 또는 그룹 만들기
- 사용자의 그룹 멤버 자격 관리
- 사용자 또는 그룹 삭제
- 사용자의 암호를 변경 합니다.
- 사용자 또는 그룹의 속성을 편집

[**로컬 사용자 및 그룹에 대 한 피드백 및 제안된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## <a name="network"></a>네트워크

**네트워크** 네트워크 장치 및 컴퓨터 또는 서버에서 설정을 관리할 수 있습니다.

### <a name="features"></a>기능

다음 기능은 네트워크에서 지원 됩니다.

- 탐색 하 고 기존 네트워크 어댑터를 검색 합니다.
- 네트워크 어댑터의 세부 정보 보기
- 네트워크 어댑터의 속성 편집
- 만들기는 [Azure 네트워크 어댑터 (미리 보기 기능)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/)

[**네트워크에 대 한 피드백 및 제안된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## <a name="powershell"></a>PowerShell

**PowerShell** PowerShell 세션을 통해 서버나 컴퓨터를 사용 하 여 상호 작용할 수 있습니다.

### <a name="features"></a>기능

PowerShell에서 다음과 같은 기능이 지원 됩니다.

- 서버에서 대화형 PowerShell 세션 만들기
- 서버에서 PowerShell 세션에서 연결 끊기

[**PowerShell에 대 한 피드백 및 제안된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## <a name="processes"></a>프로세스

**프로세스** 컴퓨터 또는 서버에서 실행 중인 프로세스를 관리할 수 있습니다.

### <a name="features"></a>기능

프로세스에서 다음과 같은 기능이 지원 됩니다.

- 탐색 하 고 실행 중인 프로세스에 대 한 검색
- 프로세스 세부 정보 보기
- 프로세스 시작
- 프로세스 종료
- 프로세스 덤프 만들기
- 프로세스 핸들 찾기

[**프로세스에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D)합니다.

## <a name="registry"></a>레지스트리

**레지스트리** 레지스트리 키와 값을 컴퓨터 또는 서버에서 관리할 수 있습니다.

### <a name="features"></a>기능

레지스트리에서 다음 기능이 지원 됩니다.

- 레지스트리 키 및 값 검색
- 추가 또는 레지스트리 값 수정
- 레지스트리 값 삭제

[**레지스트리에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D)합니다.

## <a name="remote-desktop"></a>원격 데스크톱

**원격 데스크톱** 대화형 데스크톱 세션을 통해 서버나 컴퓨터를 사용 하 여 상호 작용할 수 있습니다.

### <a name="features"></a>기능

원격 데스크톱의 다음과 같은 기능이 지원 됩니다.

- 대화형 원격 데스크톱 세션을 시작 합니다.
- 원격 데스크톱 세션에서 연결 끊기
- 원격 데스크톱 세션을 Ctrl + Alt + Del 보내기

[**원격 데스크톱에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D)합니다.

## <a name="roles-and-features"></a>역할 및 기능

**역할 및 기능** 역할 및 기능을 서버를 관리할 수 있습니다.

### <a name="features"></a>기능

다음 기능은 역할 및 기능에서 지원 됩니다.

- 서버에 역할 및 기능 목록을 검색합니다
- 역할이 나 기능 세부 정보 보기
- 역할 또는 기능 설치
- 역할이 나 기능 제거

[**역할 및 기능에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D)합니다.

## <a name="scheduled-tasks"></a>예약된 작업

**예약 된 작업** 컴퓨터 또는 서버에서 예약 된 작업을 관리할 수 있습니다.

### <a name="features"></a>기능

예약 된 작업에 다음과 같은 기능이 지원 됩니다.

- 작업 scheduler 라이브러리 찾아보기
- 예약 된 작업 편집
- 사용 및 예약 된 작업을 사용 하지 않도록 설정
- 예약 된 작업의 시작 및 중지
- 예약 된 작업 만들기

[**예약 된 작업에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D)합니다.

## <a name="services"></a>서비스

**서비스** 컴퓨터 또는 서버에서 서비스를 관리할 수 있습니다.

### <a name="features"></a>기능

서비스에서 다음과 같은 기능이 지원 됩니다.

- 서버에서 찾아보기 및 검색 서비스
- 서비스의 세부 정보 보기
- 서비스 시작
- 서비스 일시 중지
- 서비스 속성 편집

[**서비스에 대 한 피드백 및 제안된 기능을 보려면**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D)합니다.

## <a name="storage"></a>스토리지

**저장소** 컴퓨터 또는 서버에서 저장소 장치를 관리할 수 있습니다.

### <a name="features"></a>기능

저장소에 다음과 같은 기능이 지원 됩니다.

- 탐색 하 고 서버에서 기존 디스크를 검색 합니다.
- 디스크 세부 정보 보기
- 볼륨 만들기
- 디스크 초기화
- 만들기, 연결 및 분리할 가상 하드 디스크 (VHD)
- 디스크를 오프 라인으로 전환
- 볼륨 포맷
- 볼륨 크기를 조정합니다
- 볼륨 속성 편집
- 볼륨 삭제
- 할당량 관리 설치

[**저장소에 대 한 피드백 및 제안된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## <a name="storage-migration-service"></a>저장소 마이그레이션 서비스

**저장소 마이그레이션 서비스** 서버 마이그레이션 및 파일 공유를 Azure 또는 Windows Server 2019 수 있습니다-앱 또는 사용자가 아무 것도 변경 하지 않고도 합니다.
[저장소 마이그레이션 서비스의 개요 가져오기](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>저장소 마이그레이션 서비스에는 Windows Server 2019에 필요합니다.

## <a name="storage-replica"></a>저장소 복제본

사용 하 여 **저장소 복제본** 서버 간 저장소 복제를 관리 합니다.
[저장소 복제본에 자세히 알아보기](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## <a name="system-insights"></a>시스템 인사이트

**시스템 Insights** 에서는 예측 분석에 고유 하 게 제공 하는 데 Windows Server 서버 기능에 대 한 정보를 증가 합니다.
[시스템 Insights 개요](http://aka.ms/systeminsights)

>[!NOTE]
>시스템 정보에는 Windows Server 2019에 필요 합니다.

## <a name="updates"></a>업데이트

**업데이트** 컴퓨터 또는 서버에서 Microsoft 및/또는 Windows 업데이트를 관리할 수 있습니다.

### <a name="features"></a>기능

다음과 같은 기능이 업데이트에서 지원 됩니다.

- 사용 가능한 Windows 또는 Microsoft 업데이트를 확인 합니다.
- 업데이트 기록의 목록을 보려면
- 업데이트 설치
- Microsoft Update에서 업데이트에 대 한 온라인 확인
- 관리할 [Azure 업데이트 관리](https://docs.microsoft.com/azure/automation/automation-update-management) 통합

[**업데이트에 대 한 피드백 및 제안된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## <a name="virtual-machines"></a>가상 머신

참조 [Windows Admin Center 사용 하 여 Virtual Machines 관리](manage-virtual-machines.md)

## <a name="virtual-switches"></a>가상 스위치

**가상 스위치** 컴퓨터 또는 서버에서 Hyper-v 가상 스위치를 관리할 수 있습니다.

### <a name="features"></a>기능

가상 스위치에는 다음과 같은 기능이 지원 됩니다.

- 서버에서 가상 스위치를 찾아 찾아보기
- 새 가상 스위치 만들기
- 가상 스위치 이름 바꾸기
- 기존 가상 스위치를 삭제 합니다.
- 가상 스위치의 속성을 편집

[**가상 스위치에 대 한 피드백 및 제안된 기능 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
