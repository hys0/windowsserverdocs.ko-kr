---
title: 네트워크 파일 시스템 개요
description: 네트워크 파일 시스템에 새로운 기능에 대해 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b0d339df588c784f8fe46f7dd0e6ce2975d0c48
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034656"
---
# <a name="network-file-system-overview"></a>네트워크 파일 시스템 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 네트워크 파일 시스템 역할 서비스 및 Windows Server의 File and Storage Services 서버 역할에 포함 된 기능을 설명 합니다. 네트워크 파일 시스템 (NFS) 파일 공유 Windows 및 비 Windows 컴퓨터를 모두 포함 된 이기종 환경의 기업 위한 솔루션을 제공 합니다.

## <a name="feature-description"></a>기능 설명

NFS 프로토콜을 사용 하 여 Windows 및 Linux 또는 UNIX와 같은 기타 비 Windows 운영 체제를 실행 하는 컴퓨터 간에 파일을 전송할 수 있습니다.

Windows Server에서 NFS는 NFS와 NFS 용 클라이언트에 대 한 서버를 포함합니다. Windows Server를 실행 하는 컴퓨터를 다른 비 Windows 클라이언트 컴퓨터에 대 한 NFS 파일 서버를 프록시로 NFS 용 서버를 사용할 수 있습니다. NFS 용 클라이언트는 비-Windows NFS 서버에 저장 된 파일에 액세스 하려면 Windows Server를 실행 하는 Windows 기반 컴퓨터를 허용 합니다.

## <a name="windows-and-windows-server-versions"></a>Windows 및 Windows Server 버전

Windows 운영 체제 버전 및 제품군에 따라 서버를 확인 하 고 NFS 클라이언트의 여러 버전을 지원합니다. 

| 운영 체제 | NFS 서버 버전 |NFS 클라이언트 버전|
| ----------------- | ------------------- | ----------------- |
| Windows 7, Windows 8.1, Windows 10 | 해당 사항 없음 | NFSv2, NFSv3 |
| Windows Server 2008, Windows Server 2008 R2 | NFSv2, NFSv3 | NFSv2, NFSv3 |
| Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019 | NFSv2, NFSv3, NFSv4.1  | NFSv2, NFSv3 |

## <a name="practical-applications"></a>유용한 팁

여기 일부의 NFS를 사용할 수 있습니다.

- Windows NFS 파일 서버를 사용 하 여 다중 플랫폼 클라이언트에서 동일한 파일 공유에 SMB 및 NFS 프로토콜을 통해 다중 프로토콜 액세스를 제공 합니다.
- 비 Windows 클라이언트 컴퓨터 액세스 NFS 파일 공유를 제공 하는 주로 비 Windows 운영 체제 환경에서 Windows NFS 파일 서버를 배포 합니다.
- SMB 및 NFS 프로토콜을 통해 액세스할 수 있는 파일 공유에 데이터를 저장 하 여 다른 한 운영 체제에서 응용 프로그램을 마이그레이션하십시오.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

네트워크 파일 시스템에서 새로운 기능과 변경 된 기능에는 NFS 버전 4.1에 대 한 지원 및 향상 된 배포 및 관리 효율성 포함 됩니다. Windows Server 2012에서 도입 되거나 변경 된 기능에 대 한 내용은 다음 표를 검토 합니다.

|기능|새로운 기능 또는 업데이트된 기능|설명|
|---|---|---|
|[NFS 버전 4.1](#nfs-version-41)|단추를 사용하여 새|향상 된 보안, 성능 및 상호 운용성 NFS 버전 3 비교 합니다.|
|[NFS 인프라](#nfs-infrastructure)|업데이트됨|배포 및 관리 효율성을 개선 하 고 보안을 강화 합니다.|
|[NFS 버전 3에 대 한 지속적인 가용성](#nfs-version-3-continuous-availability)|업데이트됨|NFS 버전 3 클라이언트에서 지속적인 가용성을 향상 시킵니다.|
|[배포 및 관리 효율성 향상](#deployment-and-manageability-improvements)|업데이트됨|쉽게 배포 하 고 새 Windows PowerShell cmdlet 및 새로운 WMI 공급자를 사용 하 여 NFS를 관리할 수 있습니다.|

## <a name="nfs-version-41"></a>NFS 버전 4.1

NFS 버전 4.1의 몇 가지 선택적 측면 외에도 필요한 측면은 모든 구현 [RFC 5661](https://tools.ietf.org/html/rfc5661):

- **파일 시스템 의사**, 물리적 및 논리적 네임 스페이스를 구분 하며 NFS 버전 3 및 NFS 버전 2와 호환 되는 파일 시스템입니다. 별칭 의사 파일 시스템에 참가 하는 내보낸된 파일 시스템에 제공 됩니다.
- **Rpc 복합** 관련 작업을 결합 하 고 데이터 전송량을 줄입니다.
- **세션 및 세션 트렁킹** 하나만 의미 체계를 사용 하도록 설정 하 고 지속적인 가용성 및 성능을 NFS 서버 NFS 4.1 클라이언트와 여러 네트워크를 활용 하는 동안 허용 합니다.

## <a name="nfs-infrastructure"></a>NFS 인프라

Windows Server 2012의 NFS 인프라 전체에 향상 된 기능 아래에서 자세히 설명 합니다.

- 합니다 **원격 프로시저 호출 (RPC) / XDR External Data Representation ()** 전송 WinSock 네트워크 프로토콜에서 제공 되는 NFS 용 서버 모두에서 NFS 용 클라이언트에 사용할 수 있습니다. 이 전송 장치 인터페이스 TDI ()를 대체, 더 나은 지원을 제공 및 향상 된 확장성 및 수신 RSS (수신측 배율)를 제공 합니다.
- 합니다 **멀티플렉서 RPC 포트** 기능은 방화벽 친화적 (관리할 적은 포트) 및 NFS의 배포를 간소화 합니다.
- **자동 조정 된 캐시 및 스레드 풀** 는 리소스는 동적 캐시를 자동으로 튜닝 스레드 풀 작업을 기준으로 하는 새 RPC/XDR 인프라의 관리 기능입니다. 이 NFS 배포 되는 즉시 최적의 성능을 제공 하는 매개 변수를 튜닝 하는 경우 관련 된 추측 완전히 제거 합니다.
- **새 Kerberos 개인 정보 구현 및 인증 옵션** 기존 강화 하려면 krb5 및 krb5i 인증 옵션과 함께 Kerberos 개인 정보 보호 (Krb5p) 지원 추가 합니다.
- **Id 매핑 Windows PowerShell 모듈** cmdlet 쉽게 id 매핑 관리, Active Directory Lightweight Directory Services (AD LDS)를 구성 하 고, UNIX 및 Linux 암호 및 플랫 파일을 설정 합니다.
- **볼륨 탑재 지점을** NFS 버전 4.1 사용 하 여 NFS 공유에서 탑재 된 볼륨에 액세스할 수 있습니다.
- 합니다 **포트에 멀티플렉싱** 기능은 RPC 포트 멀티플렉서 (포트 2049) 방화벽 친화적 이며 NFS 배포를 간소화 하는 지원 합니다.

## <a name="nfs-version-3-continuous-availability"></a>NFS 버전 3에 대 한 지속적인 가용성

NFS 버전 3 클라이언트 자세한 가용성과 가동 중지 시간 감소를 사용 하 여 신속 하 고 투명 하 게 계획 된 장애 조치를 가질 수 있습니다. 장애 조치 프로세스가 하므로 더 빠릅니다 NFS 버전 3 클라이언트용:

- 이제 클러스터링 인프라에는 네트워크 이름 리소스의 장애 조치 시간을 크게 향상 되는 공유 당 하나의 리소스 대신 당 하나의 리소스 수 있습니다.
- NFS 서버 내에서 장애 조치 경로 더 나은 성능을 위해 조정 됩니다.
- NFS 서버에서 와일드 카드 등록 더 이상 필요 하 고 장애 조치는 더 풍부 합니다.
- 장애 조치 프로세스를 네트워크 상태 모니터 (NSM) 알림을 보내고, 클라이언트가 더 이상 기다려야 TCP 시간 제한에 대 한 장애에 다시 연결 하려면 서버를 통해.

NFS용 서버는 일반적으로 계획된 유지 관리 기간 동안 수동으로 시작된 경우에만 투명 장애 조치(failover)를 지원합니다. 계획되지 않은 장애 조치(failover)가 발생하는 경우 NFS 클라이언트의 연결이 끊깁니다. 또한 NFS 용 서버 다시 시작 키를 사용 하 여 모든 통합이 없습니다. 따라서 계획된 장애 조치(failover) 직후 NFS 클라이언트가 액세스하고 있는 동일한 파일에 로컬 앱이나 SMB 세션에서 액세스하려고 하면 NFS 클라이언트의 연결이 끊길 수 있습니다(투명 장애 조치(failover)가 성공하지 않음).

## <a name="deployment-and-manageability-improvements"></a>배포 및 관리 효율성 향상

배포 및 관리 NFS 다음과 같이 향상 되었습니다.

- 40 명의 새로운 Windows PowerShell cmdlet 쉽게 구성 하 고 NFS 파일 공유를 관리 합니다. 자세한 내용은 [Windows PowerShell의 NFS Cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)합니다.
- Id 매핑 id 매핑을 구성 하기 위한 새로운 Windows PowerShell cmdlet을 로컬 플랫 파일 매핑 저장소를 사용 하 여 향상 되었습니다.
- 서버 관리자 그래픽 사용자 인터페이스를 사용 하 여 쉽습니다.
- 새 WMI 버전 2 공급자가 관리 간소화 하기 위해 사용할 수 있습니다.
- RPC 포트 멀티플렉서 (포트 2049) 방화벽 친화적 이며 NFS의 배포를 간소화 합니다.

## <a name="server-manager-information"></a>서버 관리자 정보

서버 관리자-또는 최신 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) -추가 역할 및 기능 마법사를 사용 하 여는 NFS 용 서버 역할 서비스를 추가할 (파일 및 iSCSI 서비스 역할). 기능 설치에 대한 일반 정보는 [역할, 역할 서비스 또는 기능 설치/제거](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>)를 참조하세요. NFS 도구에 대 한 서버 네트워크 파일 시스템 MMC 스냅인에 대 한 NFS 용 서버를 관리 하는 서비스 및 NFS 구성 요소에 대 한 클라이언트에 포함 됩니다. 스냅인을 사용 하 여, 컴퓨터에 설치 하는 NFS 구성 요소에 대 한 서버를 관리할 수 있습니다. NFS 용 서버는 몇 가지 Windows 명령줄 관리 도구를도 포함 되어 있습니다.

- **탑재** 원격 NFS 공유 (라고도: 내보내기)를 로컬로 탑재 하 고 Windows 클라이언트 컴퓨터의 로컬 드라이브 문자에 매핑합니다.
- **Nfsadmin** 구성 서버의 NFS 및 클라이언트에 대 한 NFS 구성 요소의 설정을 관리 합니다.
- **Nfsshare** NFS 용 서버를 사용 하 여 공유 되는 폴더에 대 한 NFS 공유 설정을 구성 합니다.
- **Nfsstat** 표시 하거나 NFS 용 서버에서 받은 호출에 대 한 통계를 다시 설정 합니다.
- **Showmount** NFS 용 서버에서 내보낸 마운트된 파일 시스템을 표시 합니다.
- **Umount** NFS 탑재 된 드라이브를 제거 합니다.

Windows Server 2012의 NFS 모듈이 도입 되었으며 NFS Windows PowerShell에 대 한 몇 가지 새 cmdlet을 사용 하 여 NFS에 맞게 합니다. 이러한 cmdlet에는 NFS 관리 작업을 자동화 하는 쉬운 방법을 제공 합니다. 자세한 내용은 [Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)합니다.

## <a name="additional-information"></a>추가 정보

다음 표에서 NFS를 평가 하기 위한 추가 리소스를 제공 합니다.

|콘텐츠 형식|참조|
|---|---|
|배포|[네트워크 파일 시스템 배포](deploy-nfs.md)|
|작업|[Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|관련 기술|[Windows Server에서 저장소](../storage.md)|