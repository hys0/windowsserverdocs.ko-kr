---
title: 네트워크 파일 시스템 개요
description: 네트워크 파일 시스템은 무엇을 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: fb31cff44cac6bd66f9aa5b7234ff3fd3b215ccf
ms.sourcegitcommit: bad0692ffd0773f61ac62bd140a421cb02c68acf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/22/2019
ms.locfileid: "9099142"
---
# 네트워크 파일 시스템 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 네트워크 파일 시스템 역할 서비스 및 Windows Server의 파일 및 저장소 서비스 서버 역할에 포함 된 기능을 설명 합니다. 시스템 NFS (네트워크 파일) 파일 공유 위한 Windows 및 비 Windows 컴퓨터로 모두 포함 된 솔루션을 제공 합니다.

## 기능 설명

NFS 프로토콜을 사용 하 여 Windows 및 Linux 등 UNIX 다른 비 Windows 운영 체제를 실행 하는 컴퓨터 간에 파일을 전송할 수 있습니다.

Windows Server의 NFS NFS 및 NFS 용 클라이언트에 대 한 서버를 포함합니다. Windows Server를 실행 하는 컴퓨터는 다른 비 Windows 클라이언트 컴퓨터에 대 한 NFS 파일 서버 역할을 하도록 NFS 용 서버를 사용할 수 있습니다. NFS 용 클라이언트 비 Windows NFS 서버에 저장 된 파일에 액세스 하려면 Windows Server를 실행 하는 Windows 기반 컴퓨터 수 있습니다.

## Windows 및 Windows Server 버전

Windows는 NFS 클라이언트 및 서버 운영 체제 버전 및 패밀리에 따라 여러 버전을 지원합니다. 

| 운영 체제 | NFS 서버 버전 |NFS 클라이언트 버전|
| ----------------- | ------------------- | ----------------- |
| Windows 7, Windows 8.1, Windows 10 | 해당 없음 | NFSv2, NFSv3 |
| Windows Server 2008, Windows Server 2008 R2 | NFSv2, NFSv3 | NFSv2, NFSv3 |
| Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019 | NFSv2, NFSv3, NFSv4.1  | NFSv2, NFSv3 |

## 유용한 팁

NFS를 사용 하 여 몇 가지 방법은 다음과 같습니다.

- 다양 한 플랫폼 클라이언트에서 동일한 파일 공유에 SMB와 NFS 프로토콜을 통해 다중 프로토콜 액세스를 제공 하기 위해 Windows NFS 파일 서버를 사용 합니다.
- 비 Windows 클라이언트 컴퓨터 NFS 파일 공유에 대 한 액세스를 제공 하기 위해 주로 비 Windows 운영 체제 환경에서 Windows NFS 파일 서버를 배포 합니다.
- SMB와 NFS 프로토콜을 통해 액세스할 수 있는 파일 공유에 데이터를 저장 하 여 다른 운영 체제에서 응용 프로그램을 마이그레이션하십시오.

## 새로운 기능 및 변경된 기능

네트워크 파일 시스템의 새로운 기능과 변경 된 NFS 4.1 버전에 대 한 지원 및 향상 된 배포 및 관리 효율성에 포함 됩니다. 내용 또는 Windows Server 2012에서 변경 된 기능에 대 한 내용은 다음 표를 검토.

|기능|새로운 기능 또는 업데이트된 기능|설명|
|---|---|---|
|[NFS 4.1 버전](#nfs-version-4.1)|신규|향상 된 보안, 성능 및 상호 운용성 NFS 버전 3에 비해 합니다.|
|[NFS 인프라](#nfs-infrastructure)|업데이트됨|배포 및 관리 효율성을 개선 하 고 보안을 향상 시킵니다.|
|[NFS 버전 3 지속적인 가용성](#nfs-version-3-continuous-availability)|업데이트됨|NFS 버전 3 클라이언트에서 지속적인 가용성을 향상 시킵니다.|
|[배포 및 관리 효율성 향상](#deployment-and-manageability-improvements)|업데이트됨|쉽게 배포 하 고 NFS 새로운 Windows PowerShell cmdlet 및 새 WMI 공급자를 사용 하 여 관리할 수 있습니다.|

## NFS 4.1 버전

NFS 버전 4.1 모든 필수 측면의 일부는 선택 사항 측면, [RFC 5661](https://tools.ietf.org/html/rfc5661)외에도 구현합니다.

- **의사 파일 시스템**을 물리적 및 논리적 네임 스페이스를 구분 하 고 버전 3 NFS 및 NFS 버전 2와 호환 되는 파일 시스템입니다. 별칭 의사 파일 시스템의 일부인 내보낸된 파일 시스템에 제공 됩니다.
- **복합 Rpc** 관련 작업을 결합 시키고 활성도 줄어듭니다.
- **세션** 및 세션 트렁킹 하나만 의미 체계를 통해 지속적인 가용성과 NFS 4.1 클라이언트와 NFS 서버 간에 여러 네트워크를 활용 하는 동안 성능을 개선할 수 있습니다.

## NFS 인프라

Windows Server 2012에서 전체 NFS 인프라에 대 한 개선은 다음과 같습니다.

- **원격 프로시저 호출 (RPC) / 외부 데이터 표현 (XDR)** 전송 인프라를 기반으로 WinSock 네트워크 프로토콜은 모두 NFS 용 서버 및 NFS 용 클라이언트에 사용할 수 있습니다. 이 전송 장치 인터페이스 (TDI), 더 나은 지원을 제공 하 고 향상 된 확장성 및 수신 측 크기 조정 (RSS)을 제공.
- **RPC 포트 멀티플렉서** 기능은 방화벽 친화적인 (관리를 더 적은 포트) 및 NFS의 배포를 간소화 합니다.
- **자동 조정 캐시 및 스레드 풀은** 동적 이며 캐시를 자동으로 조정 되 고 워크 로드에 따라 풀 스레드는 새로운 RPC/x d R 인프라의 리소스 관리 기능. NFS 배포 되는 즉시 최적의 성능을 제공 하는 매개 변수를 조정할 때 관련 된 추측 작업 완전히 제거 됩니다.
- 기존 krb5 및 krb5i 인증 옵션 Kerberos 개인 정보 (Krb5p) 지원 추가 하 여 **새 Kerberos 개인 정보 보호 구현 및 인증 옵션** 을 선택 합니다.
- **Identity 매핑 Windows PowerShell 모듈** cmdlet 하기 쉽도록 id 매핑을 관리, Active Directory Lightweight Directory Services (AD LDS), 구성 및 UNIX 및 Linux 암호 및 플랫 파일을 설정 합니다.
- Nfs 버전 4.1 NFS 공유 아래에 탑재 된 볼륨에 액세스할 수 **볼륨 탑재 지점을** 있습니다.
- **포트 멀티플렉싱** 기능은 RPC 포트 멀티플렉서 (포트 2049), 방화벽 이며 NFS 배포를 간소화를 지원 합니다.

## NFS 버전 3 지속적인 가용성

NFS 버전 3 클라이언트는 더 많은 가용성과 가동 중지 빠르고 투명 계획 된 장애 조치를 가질 수 있습니다. 장애 조치 프로세스는 때문에 NFS 버전 3 클라이언트에 대 한 더 빠릅니다.

- 이제 클러스터링 인프라 리소스의 장애 조치 시간을 크게 향상 하는 공유 당 하나의 리소스 대신 네트워크 이름 당 하나의 리소스를 허용 합니다.
- NFS 서버에서 장애 조치 경로 성능 향상을 위해 조정 됩니다.
- NFS 서버에 등록 하는 와일드 카드는 더 이상 필요, 되며 장애 조치를 더 세부적.
- 장애 조치 프로세스는 네트워크 상태 모니터 (NSM) 알림 보내집니다 및 클라이언트는 더 이상 TCP 시간 제한에 실패 한 다시 연결할 때까지 기다릴 필요가 서버를 통해 합니다.

NFS 용 서버 지원 투명 한 장애 조치는 참고 수동으로 시작한 경우에 일반적으로 하는 동안 계획 된 유지 관리 합니다. 예기치 않은 장애 발생 하는 경우 NFS 클라이언트 연결 손실 됩니다. NFS 용 서버 다시 시작 키 필터를 사용 하 여 모든 통합을 수도 없습니다. 이 로컬 앱 또는 SMB 세션 NFS 클라이언트는 계획 된 장애 조치 바로 뒤에 액세스 하는 동일한 파일에 액세스 하려고 시도 하면 NFS 클라이언트 손실 될 수 있습니다 (투명 한 장애 조치 성공 하지 않습니다.) 연결을 의미 합니다.

## 배포 및 관리 효율성 향상

배포 및 관리 NFS이 같은 방법으로 개선 됩니다.

- 새로운 40 명의 Windows PowerShell cmdlet 하기 쉽도록 구성 하 고 NFS 파일 공유를 관리 합니다. 자세한 내용은 [Windows PowerShell의 NFS Cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)을 참조 하세요.
- 로컬 플랫 파일 매핑 저장소 및 id 매핑을 구성 하기 위한 새로운 Windows PowerShell cmdlet을 사용 하 여 id 매핑을 향상 됩니다.
- 서버 관리자 그래픽 사용자 인터페이스는 사용 하기 쉽습니다.
- 새 WMI 버전 2 공급자가 더 쉽게 관리에 사용할 수 있습니다.
- RPC 포트 멀티플렉서 (포트 2049) 방화벽 이며 NFS의 배포를 간소화 합니다.

## 서버 관리자 정보

서버 관리자-또는 최신 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) -에서 사용 하 여 추가 역할 및 기능 마법사를 추가할 역할 서비스 NFS 용 서버 (파일 및 iSCSI 서비스 역할). 기능을 설치 하는 방법에 대 한 일반적인 정보, [설치 또는 제거 역할, 역할 서비스 또는 기능을](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>)참조 하세요. NFS 도구에 대 한 서버 NFS 용 서버를 관리 하는 네트워크 파일 시스템 MMC 스냅인에 대 한 서비스 및 NFS 구성 요소에 대 한 클라이언트를 포함 합니다. 스냅인를 사용 하는 컴퓨터에 설치 된 NFS 구성 요소에 대 한 서버를 관리할 수 있습니다. NFS 용 서버에는 여러 Windows 명령줄 관리 도구가 포함 되어 있습니다.

- **탑재** 원격 NFS 공유 (라고도 내보내기)를 로컬에서 탑재 하 고 Windows 클라이언트 컴퓨터에서 로컬 드라이브 문자에 매핑합니다.
- **Nfsadmin** 구성 설정을 서버의 NFS 및 클라이언트에 대 한 NFS 구성 요소를 관리합니다.
- **Nfsshare** NFS 용 서버를 사용 하 여 공유 되는 폴더에 대 한 NFS 공유 설정을 구성 합니다.
- **Nfsstat** 표시 하거나 NFS 용 서버에서 받은 호출에 대 한 통계를 다시 설정 합니다.
- **Showmount** NFS 용 서버에서 내보낸 탑재 된 파일 시스템을 표시 합니다.
- **Umount** NFS 탑재 된 드라이브를 제거합니다.

NFS 용으로 특별히 몇 가지 새로운 cmdlet을 사용 하 여 Windows PowerShell 용 NFS 모듈을 소개 하는 Windows Server 2012에서 NFS는 합니다. 이러한 cmdlet NFS 관리 작업을 자동화 하는 간편한 방법을 제공 합니다. 자세한 내용은 [Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)을 참조 하세요.

## 추가 정보

다음 표에서 NFS 평가 대 한 추가 리소스를 제공 합니다.

|콘텐츠 유형|참조|
|---|---|
|배포|[네트워크 파일 시스템 배포](deploy-nfs.md)|
|작업|[Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|관련 기술|[WindowsServer의 저장소](../storage.md)|