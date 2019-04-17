---
title: Windows Admin Center를 사용 하 여 서버를 관리 합니다.
description: Windows Admin Center (Project Honolulu)를 사용 하 여 서버를 관리 합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93a40345d05a6230596832b2d455d36eee2401b5
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296685"
---
# Windows Admin Center를 사용 하 여 서버를 관리 합니다.

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md) [지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## Windows Server 컴퓨터 관리

Windows Server 2012를 실행 하거나 나중에 다양 한 도구를 사용 하 여 서버를 관리 하려면 Windows Admin Center를 포함 하 여 인증서, 장치, 이벤트, 프로세스, 역할 및 기능, 업데이트, 가상 컴퓨터 및 더 개별 서버를 추가할 수 있습니다.

![서버 연결 개요 화면](../media/manage-servers/server-overview.png)

## Windows Admin Center에는 서버 추가

Windows Admin Center를 서버를 추가 합니다.

1. 모든 연결에서 **+ 추가** 클릭 합니다.
2. **서버 연결**을 추가 하려면 선택 합니다.
3. 서버의 이름을 입력 하 고 메시지가 표시 되 면 자격 증명을 사용 합니다.
4. **제출** 을 완료를 클릭 합니다.

서버 개요 페이지에서 연결 목록에 추가 됩니다. 서버에 연결을 클릭 합니다.

> [!NOTE]
> Windows Admin Center에서 별도 연결으로 [장애 조치 클러스터](manage-failover-clusters.md) 또는 [하이퍼 수렴 형 클러스터](manage-hyper-converged.md) 를 추가할 수도 있습니다.

## 도구

다음 도구 서버 연결에 사용할 수 있습니다.

| 도구 | 설명 |
| ---- | ----------- |
| [개요](#overview) | 서버 세부 정보 보기 및 컨트롤 서버 상태 |
| [Active Directory](#active-directory-preview) | Active Directory 관리 |
| [백업](#backup) | 보기 및 Azure 백업 구성 |  
| [인증서](#certificates) | 보기 및 인증서를 수정 합니다. |
| [컨테이너](#containers) | 컨테이너 보기 |
| [장치](#devices) | 보기 및 장치를 수정 합니다. |
| [DHCP](#dhcp) | 보기 및 DHCP 서버 구성 관리 |
| [DNS](#dns) | 보기 및 DNS 서버 구성 관리 |
| [이벤트](#events) | 이벤트 보기 |
| [파일](#files) | 파일 및 폴더를 검색 합니다. |
| [방화벽](#firewall) | 보기 및 방화벽 규칙을 수정 |
| [설치 된 앱](#installed-apps) | 보기 및 설치 된 앱을 제거 |
| [로컬 사용자 및 그룹](#local-users-and-groups) | 보기 및 로컬 사용자 및 그룹 수정 |
| [네트워크](#network) | 보기 및 네트워크 장치 수정 |
| [PowerShell](#powershell) | PowerShell 통해 서버와 상호 작용 |
| [프로세스](#processes) | 보기 및 실행 중인 프로세스 수정 |
| [레지스트리](#registry) | 보기 및 레지스트리 항목을 수정 |
| [원격 데스크톱](#remote-desktop) | 원격 데스크톱을 통해 서버와 상호 작용 |
| [역할 및 기능](#roles-and-features) | 보기 및 역할 및 기능을 수정 |
| [예약된 작업](#scheduled-tasks) | 보기 및 예약 된 작업을 수정 |
| [서비스](#services) | 보고 서비스 수정 |
| [설정](#settings) | 보고 서비스 수정 |
| [저장소](#storage) | 보기 및 저장 장치를 수정 합니다. |
| [저장소 마이그레이션 서비스](#storage-migration-service) | 서버 및 파일 공유 Azure 또는 Windows Server 2019로 마이그레이션 |
| [저장소 복제본](#storage-replica) | 저장소 복제본을 사용 하 여 서버 간 저장소 복제 관리 |
| [시스템 인사이트](#system-insights) | 시스템 인 사이트에서는 서버 기능에 대 한 정보를 증가 합니다. |
| [업데이트](#updates) | 보기를 설치 하 고 새 업데이트를 확인 |
| [가상 컴퓨터](manage-virtual-machines.md) | 보기 및 가상 컴퓨터 관리 |
| [가상 스위치](#virtual-switches) | 보기 및 가상 스위치 관리 |

## 개요

**개요** CPU, 메모리 및 네트워크 성능, 현재 상태를 확인 뿐 아니라 작업을 수행 하 고 대상 컴퓨터 또는 서버에서 설정을 수정할 수 있습니다.

### 기능

다음과 같은 기능 개요 서버 관리자에서에서 지원 됩니다.

- 서버 세부 정보 보기
- 활동 CPU 보기
- 메모리 활동 보기
- 네트워크 활동 보기
- 서버를 다시 시작
- 서버 종료
- 서버에서 디스크 메트릭을 사용 하도록 설정
- 서버에 컴퓨터 ID를 편집 합니다.
- 하이퍼링크 (IPMI 호환 BMC 필요)를 사용 하 여 BMC IP 주소를 확인 합니다.

[**보기 피드백 및 서버 개요에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BOverview%5D).

## Active Directory (미리 보기)

**Active Directory** 는 [확장 피드](../configure/using-extensions.md)제공 되는 초기 미리 보기입니다.

### 기능

다음과 같은 Active Directory 관리 사용할 수 있습니다.

- 사용자 계정 만들기
- 그룹 만들기
- 사용자, 컴퓨터 및 그룹에 대 한 검색
- 사용자, 컴퓨터 및 그리드에서 선택한 그룹에 대 한 세부 정보 창
- 글로벌 그리드 작업 사용자, 컴퓨터 및 그룹 (사용/사용 안 함, 제거)
- 사용자 암호 다시 설정
- 사용자 개체: 기본 속성 & 그룹 구성원 구성
- 컴퓨터 개체: 단일 컴퓨터에 대 한 위임을 구성
- 그룹 개체: (한 번에 1 추가/제거 사용자) 구성원을 관리  

[**보기 피드백 및 Active Directory에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BActive%20Directory%5D)입니다.

## 백업

**Microsoft Azure에 직접 서버를 백업 하 여 Windows server 손상을, 공격 또는 재해 로부터 보호할 수 있습니다.**
[Azure 백업에 대해 알아봅니다.](https://aka.ms/windows-admin-center-backup)

[Windows Admin Center에서 백업에 대 한 피드백 제공](https://aka.ms/backup-wac-feedback)

### 기능

다음과 같은 기능 백업에서 지원 됩니다.

- Azure 백업 상태에 대 한 개요를 보려면
- 백업 항목 및 일정 구성
- 시작 또는 백업 작업을 중지 합니다.
- 백업 작업 기록 보기 및 상태
- 복구 지점 보고 데이터를 복구
- 백업 데이터 삭제

## 인증서

**인증서** 를 사용 하는 컴퓨터 또는 서버에 인증서 저장소를 관리할 수 있습니다.

### 기능

인증서에는 다음과 같은 기능이 지원 됩니다.

- 탐색 및 기존 인증서를 검색 합니다.
- 인증서의 세부 정보 보기
- 인증서 내보내기
- 인증서 갱신
- 새 인증서 요청
- 인증서를 삭제 합니다.

[**보기 피드백 및 인증서에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BCertificates%5D)입니다.

## 컨테이너

**컨테이너** 를 사용 하면 Windows Server 컨테이너 호스트에서 컨테이너를 볼 수 있습니다. 실행 중인 Windows Server Core 컨테이너의 경우 이벤트 로그를 볼 수 있으며 컨테이너의 CLI에 액세스할 수 있습니다.

[**보기 피드백 및 컨테이너에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BContainers%5D)입니다.

## 장치

**장치** 를 사용 하는 컴퓨터 또는 서버에 연결 된 장치를 관리할 수 있습니다.

### 기능

다음과 같은 기능이 장치에서 지원 됩니다.

- 디바이스 검색 및 검색
- 장치 세부 정보 보기
- 장치를 사용 하지 않도록 설정
- 장치에서 드라이버 업데이트

[**보기 피드백 및 장치에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDevices%5D)입니다.

## DHCP

**DHCP** 를 사용 하는 컴퓨터 또는 서버에 연결 된 장치를 관리할 수 있습니다.

### 기능

- 만들기/구성/보기 IPV4 및 IPV6 범위
- 주소 제외를 만들고 시작 및 종료 IP 주소를 구성 합니다.
- 주소 예약을 만들고 구성 클라이언트 MAC 주소 (IPV4) DUID 및 IAID (IPV6)

[**보기 피드백 및 DHCP에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDHCP%5D)입니다.

## DNS

**DNS** 를 사용 하는 컴퓨터 또는 서버에 연결 된 장치를 관리할 수 있습니다.

### 기능

- DNS 정방향 조회 영역, 역방향 조회 영역 및 DNS 레코드의 세부 정보 보기
- 정방향 조회 영역 만들기 (주, 보조 또는 스텁), 정방향 조회 영역 속성 구성
- 호스트를 만들고 DNS 레코드의 CNAME 또는 MX 유형 (A 또는 AAAA)
- DNS 레코드 속성 구성
- IPV4 및 IPV6 역방향 조회 영역 만들기 (주, 보조 및 스텁), 역방향 조회 영역 속성 구성
- PTR 만들기 CNAME 유형의 DNS 역방향 조회 영역에서 기록 합니다.

[**보기 피드백 및 DHCP에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BDNS%5D)입니다.

## 이벤트

**이벤트** 를 사용 하는 컴퓨터 또는 서버에서 이벤트 로그를 관리할 수 있습니다.

### 기능

다음과 같은 기능 이벤트에서 지원 됩니다.

- 탐색 및 검색 이벤트
- 이벤트 세부 정보 보기
- 이벤트 로그에서 지우기
- 이벤트 로그에서 내보내기

[**보기 피드백 및 이벤트에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BEvents%5D)입니다.

## 파일

**파일** 을 사용 하는 컴퓨터 또는 서버에서 파일 및 폴더를 관리할 수 있습니다.

### 기능

파일에는 다음과 같은 기능이 지원 됩니다.

- 파일 및 폴더를 검색 합니다.
- 파일 또는 폴더에 대 한 검색
- 새 폴더를 만듭니다
- 파일 또는 폴더를 삭제 합니다.
- 파일 또는 폴더를 다운로드 합니다.
- 파일 또는 폴더 업로드
- 파일 또는 폴더 이름 바꾸기
- Zip 파일 추출
- 파일 또는 폴더 속성 보기
- 파일 서버 리소스 관리자 [할당량](https://docs.microsoft.com/windows-server/storage/fsrm/quota-management) 관리
- 추가, 편집 또는 파일 공유를 제거 합니다.
- 사용자 및 그룹 파일 공유 사용 권한을 수정합니다

[**보기 피드백 및 파일에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFiles%5D)입니다.

## 방화벽

**방화벽** 을 사용 하면 방화벽 설정 및 컴퓨터 또는 서버에서 규칙을 관리할 수 있습니다.

### 기능

다음과 같은 기능 방화벽에서 지원 됩니다.

- 방화벽 설정의 개요를 보려면
- 들어오는 방화벽 규칙 보기
- 방화벽 규칙을 보내는 보기
- 검색 방화벽 규칙
- 방화벽 규칙 세부 정보 보기
- 새 방화벽 규칙 만들기
- 활성화 또는 비활성화 방화벽 규칙
- 방화벽 규칙 삭제
- 방화벽 규칙의 속성을 편집

[**보기 피드백 및 방화벽에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BFirewall%5D)입니다.

## 설치 된 앱

**설치 된 앱** 목록 및 설치 된 응용 프로그램을 제거할 수 있습니다.

[**보기 피드백 및 설치 된 앱에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BInstalled%20Apps%5D)입니다.

## 로컬 사용자 및 그룹

**로컬 사용자 및 그룹** 보안 그룹 및 컴퓨터 또는 서버에 로컬로 저장 된 사용자를 관리할 수 있습니다.

### 기능

다음과 같은 기능은 로컬 사용자 및 그룹에서 지원 됩니다.

- 보기 및 검색 사용자 및 그룹
- 새 사용자 또는 그룹 만들기
- 사용자의 그룹 구성원을 관리
- 사용자 또는 그룹을 삭제 합니다.
- 사용자의 암호를 변경 합니다.
- 사용자 또는 그룹의 속성을 편집

[**보기 피드백 및 로컬 사용자 및 그룹에 대 한 제안 된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BLocal%20users%20and%20Groups%5D)

## 네트워크

**네트워크** 를 사용 하면 네트워크 장치 및 컴퓨터 또는 서버에서 설정을 관리할 수 있습니다.

### 기능

다음과 같은 기능은 네트워크에서 지원 됩니다.

- 탐색 및 기존 네트워크 어댑터를 검색 합니다.
- 네트워크 어댑터의 세부 정보 보기
- 네트워크 어댑터의 속성 편집
- [Azure 네트워크 어댑터 (미리 보기 기능)](https://blogs.technet.microsoft.com/networking/2018/09/05/azurenetworkadapter/) 만들기

[**보기 피드백 및 네트워크에 대 한 제안 된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BNetwork%5D)

## PowerShell

**PowerShell** 을 사용 하는 컴퓨터 또는 PowerShell 세션을 통해 서버와 상호 작용할 수 있습니다.

### 기능

PowerShell에서 다음과 같은 기능이 지원 됩니다.

- 서버에서 대화형 PowerShell 세션 만들기
- 서버에서 PowerShell 세션에서 분리

[**보기 피드백 및 PowerShell에 대 한 제안 된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BPowerShell%5D)

## 프로세스

**프로세스** 를 사용 하는 컴퓨터 또는 서버에서 실행 중인 프로세스를 관리할 수 있습니다.

### 기능

다음과 같은 기능 프로세스에서 지원 됩니다.

- 탐색 및 실행 중인 프로세스에 대 한 검색
- 프로세스 세부 정보 보기
- 프로세스를 시작
- 프로세스 종료
- 프로세스 덤프 만들기
- 프로세스 핸들 찾기

[**보기 피드백 및 프로세스에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BProcesses%5D)입니다.

## 레지스트리

**레지스트리** 를 사용 하면 레지스트리 키와 값의 컴퓨터나 서버를 관리할 수 있습니다.

### 기능

다음과 같은 기능 레지스트리에서 지원 됩니다.

- 레지스트리 키와 값 찾아보기
- 레지스트리 값을 수정 하거나 추가
- 레지스트리 값을 삭제

[**보기 피드백 및 레지스트리에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRegistry%5D)입니다.

## 원격 데스크톱

**원격 데스크톱** 을 사용 하는 컴퓨터 또는 데스크톱 대화형 세션을 통해 서버와 상호 작용할 수 있습니다.

### 기능

원격 데스크톱에서 다음과 같은 기능이 지원 됩니다.

- 대화형 원격 데스크톱 세션 시작
- 원격 데스크톱 세션에서 분리
- 원격 데스크톱 세션에 Ctrl + Alt + Del 보내기

[**보기 피드백과 원격 데스크톱에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRemote%20Desktop%5D)입니다.

## 역할 및 기능

**역할 및 기능** 역할 및 기능에는 서버를 관리할 수 있습니다.

### 기능

다음과 같은 기능 역할 및 기능에서 지원 됩니다.

- 역할 및 기능 서버에서 목록을 검색합니다
- 역할 또는 기능 세부 정보 보기
- 역할 또는 기능 설치
- 역할 또는 기능을 제거

[**보기 피드백 및 역할 및 기능에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BRoles%20and%20Features%5D)입니다.

## 예약된 작업

**예약 된 작업** 을 사용 하면 컴퓨터 또는 서버에서 예약 된 작업을 관리할 수 있습니다.

### 기능

예약 된 작업에는 다음과 같은 기능이 지원 됩니다.

- 작업 스케줄러 라이브러리를 검색 합니다.
- 예약 된 작업을 편집
- _AMP_ 사용 안 함 예약 된 작업을 사용 하도록 설정
- _AMP_ 중지 예약 된 작업을 시작
- 예약 된 작업 만들기

[**보기 피드백 및 예약 된 작업에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BScheduled%20Tasks%5D)입니다.

## 서비스

**서비스** 를 사용 하는 컴퓨터 또는 서버에서 서비스를 관리할 수 있습니다.

### 기능

다음과 같은 기능 서비스에서 지원 됩니다.

- 탐색 및 서버에는 서비스 검색
- 서비스의 세부 정보 보기
- 서비스 시작
- 서비스를 일시 중지
- 서비스 속성 편집

[**보기 피드백 및 서비스에 대 한 제안된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BServices%5D)입니다.

## 설정

**설정** 컴퓨터 또는 서버에서 설정을 관리 하도록 중앙 위치입니다.

### 기능

- 보기 및 사용자 및 시스템 환경 변수를 수정 합니다.
- [Azure 모니터](azure-monitor.md) 에서 경고를 모니터링을 위한 구성 보기
- 보기 및 전원 구성을 수정합니다
- 보기 및 원격 데스크톱 설정 수정
- 보기 및 역할 기반 액세스 제어 설정 수정
- 보기 및 해당 하는 경우 Hyper-v 호스트 설정 수정

## 저장소

**저장소** 를 사용 하는 컴퓨터 또는 서버에 저장 장치를 관리할 수 있습니다.

### 기능

다음과 같은 기능 저장소에서 지원 됩니다.

- 탐색 및 서버에 기존 디스크 검색
- 디스크 세부 정보 보기
- 볼륨 만들기
- 디스크 초기화
- 만들기, 연결 하 고, 가상 하드 디스크 (VHD)를 분리 합니다.
- 오프 라인으로 디스크
- 볼륨을 포맷합니다
- 볼륨의 크기를 조정합니다
- 볼륨 속성 편집
- 볼륨을 삭제
- 할당량 관리 설치

[**보기 피드백 및 저장소에 대 한 제안 된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BStorage%5D)

## 저장소 마이그레이션 서비스

**저장소 마이그레이션 서비스** 를 사용 하면 서버 마이그레이션 파일 공유 Azure 또는 Windows Server 2019를-앱 또는 사용자가 아무 것도 변경할 필요 없이 합니다.
[저장소 마이그레이션 서비스에 대 한 개요](https://go.microsoft.com/fwlink/?linkid=2016155)

>[!NOTE]
>저장소 마이그레이션 서비스는 Windows Server 2019에 필요합니다.

## 저장소 복제본

**저장소 복제본** 을 사용 하 여 서버 간 저장소 복제 관리.
[저장소 복제본에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui)

## 시스템 인사이트

**시스템 인 사이트** 에서 기본적으로 예측 분석을 도입을 제공 하는 데 Windows Server 서버 기능에 대 한 정보를 증가 합니다.
[시스템 인 사이트에 대 한 개요](http://aka.ms/systeminsights)

>[!NOTE]
>시스템 인 사이트는 Windows Server 2019에 필요 합니다.

## 업데이트

**업데이트** 를 사용 하는 컴퓨터 또는 서버에서 Microsoft 및/또는 Windows 업데이트를 관리할 수 있습니다.

### 기능

다음과 같은 기능 업데이트에서 지원 됩니다.

- 사용 가능한 Windows 또는 Microsoft 업데이트 보기
- 업데이트 기록의 목록을 보려면
- 업데이트 설치
- Microsoft 업데이트에서 업데이트에 대 한 온라인 확인
- [Azure 업데이트 관리](https://docs.microsoft.com/azure/automation/automation-update-management) 통합 관리

[**피드백 및 제안된 기능 업데이트에 대 한 보기**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BUpdates%5D)

## 가상 컴퓨터

[Windows Admin Center를 사용 하 여 가상 컴퓨터 관리](manage-virtual-machines.md) 를 참조 하세요.

## 가상 스위치

**가상 스위치** 를 사용 하는 컴퓨터 또는 서버에서 Hyper-v 가상 스위치를 관리할 수 있습니다.

### 기능

다음과 같은 기능은 가상 스위치에서 지원 됩니다.

- 탐색 및 가상 스위치는 서버에서 검색
- 새 가상 스위치 만들기
- 가상 스위치 이름 바꾸기
- 기존 가상 스위치가 삭제
- 가상 스위치의 속성을 편집

[**보기 피드백 및 가상 스위치에 대 한 제안 된 기능**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5BVirtual%20Switch%5D)
