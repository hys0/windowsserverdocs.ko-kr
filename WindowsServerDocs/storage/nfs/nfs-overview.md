---
title: 네트워크 파일 시스템 개요
description: 네트워크 파일 시스템에 대해 설명 합니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2589e21c54fa864629f81b5889d0442c6f0de254
ms.sourcegitcommit: 568b924d32421256f64abfee171304f1daf320d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85070556"
---
# <a name="network-file-system-overview"></a>네트워크 파일 시스템 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server의 파일 및 저장소 서비스 서버 역할에 포함 된 네트워크 파일 시스템 역할 서비스 및 기능에 대해 설명 합니다. NFS (네트워크 파일 시스템)는 Windows 및 비 Windows 컴퓨터를 포함 하는 유형이 다른 환경을 제공 하는 기업에 대 한 파일 공유 솔루션을 제공 합니다.

## <a name="feature-description"></a>기능 설명

NFS 프로토콜을 사용 하 여 Windows 및 기타 Windows 이외의 운영 체제 (예: Linux 또는 UNIX) 간에 파일을 전송할 수 있습니다.

Windows Server의 NFS에는 nfs 용 서버와 NFS 용 클라이언트가 포함 되어 있습니다. Windows Server를 실행 하는 컴퓨터는 NFS 용 서버를 사용 하 여 다른 비 Windows 클라이언트 컴퓨터에 대 한 NFS 파일 서버 역할을 할 수 있습니다. NFS 용 클라이언트를 사용 하면 windows Server를 실행 하는 Windows 기반 컴퓨터에서 비 Windows NFS 서버에 저장 된 파일에 액세스할 수 있습니다.

## <a name="windows-and-windows-server-versions"></a>Windows 및 Windows Server 버전

Windows는 운영 체제 버전 및 제품군에 따라 여러 버전의 NFS 클라이언트 및 서버를 지원 합니다. 

| 운영 체제 | NFS 서버 버전 |NFS 클라이언트 버전|
| ----------------- | ------------------- | ----------------- |
| Windows 7, Windows 8.1, Windows 10 | 해당 없음 | NFSv2, NFSv3 |
| Windows Server 2008, Windows Server 2008 R2 | NFSv2, NFSv3 | NFSv2, NFSv3 |
| Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019 | NFSv2, NFSv3, NFSv 4.1  | NFSv2, NFSv3 |

## <a name="practical-applications"></a>유용한 팁

NFS를 사용할 수 있는 몇 가지 방법은 다음과 같습니다.

- Windows NFS 파일 서버를 사용 하 여 다중 플랫폼 클라이언트에서 SMB 및 NFS 프로토콜을 통해 동일한 파일 공유에 대 한 다중 프로토콜 액세스를 제공 합니다.
- Windows NFS 파일 서버를 주로 사용 하지 않는 windows 운영 체제 환경에 배포 하 여 비 Windows 클라이언트 컴퓨터에 NFS 파일 공유에 대 한 액세스를 제공 합니다.
- SMB 및 NFS 프로토콜을 통해 액세스할 수 있는 파일 공유에 데이터를 저장 하 여 한 운영 체제에서 다른 운영 체제로 응용 프로그램을 마이그레이션합니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

네트워크 파일 시스템의 새롭고 변경 된 기능에는 NFS 버전 4.1 및 향상 된 배포 및 관리 효율성에 대 한 지원이 포함 됩니다. Windows Server 2012에서 새로 또는 변경 된 기능에 대 한 자세한 내용은 다음 표를 참조 하십시오.

|기능|새로운 기능 또는 업데이트된 기능|Description|
|---|---|---|
|[NFS 버전 4.1](#nfs-version-41)|단추를 사용하여 새|NFS 버전 3과 비교 하 여 보안, 성능 및 상호 운용성이 향상 되었습니다.|
|[NFS 인프라](#nfs-infrastructure)|업데이트됨|배포 및 관리 효율성을 향상 하 고 보안을 강화 합니다.|
|[NFS 버전 3 지속적인 가용성](#nfs-version-3-continuous-availability)|업데이트됨|NFS 버전 3 클라이언트의 지속적인 가용성을 향상 시킵니다.|
|[배포 및 관리 효율성 향상](#deployment-and-manageability-improvements)|업데이트됨|새 Windows PowerShell cmdlet 및 새로운 WMI 공급자를 사용 하 여 NFS를 쉽게 배포 하 고 관리할 수 있습니다.|

## <a name="nfs-version-41"></a>NFS 버전 4.1

NFS 버전 4.1는 [RFC 5661](https://tools.ietf.org/html/rfc5661)의 일부 선택적 측면 외에도 필요한 모든 측면을 구현 합니다.

- 물리적 및 논리적 네임 스페이스를 구분 하 고 NFS 버전 3 및 NFS 버전 2와 호환 되는 파일 시스템의 **의사 파일 시스템**입니다. 의사 파일 시스템의 일부인 내보낸 파일 시스템에 대 한 별칭이 제공 됩니다.
- **복합 rpc** 는 관련 작업을 결합 하 고 데이터 전송량을 줄입니다.
- **세션 및 세션 트렁킹** 는 하나의 의미 체계를 사용 하며 nfs 4.1 클라이언트와 nfs 서버 간에 여러 네트워크를 활용 하는 동시에 지속적인 가용성과 성능을 향상 시킬 수 있습니다.

## <a name="nfs-infrastructure"></a>NFS 인프라

Windows Server 2012에서 전체 NFS 인프라의 향상 된 기능은 아래에 자세히 설명 되어 있습니다.

- WinSock 네트워크 프로토콜에서 제공 하는 **RPC (원격 프로시저 호출** ) 전송 인프라는 Nfs 용 서버와 Nfs 용 클라이언트 모두에서 사용할 수 있습니다. 이는 TDI (전송 장치 인터페이스)를 대체 하며, 더 나은 지원을 제공 하 고, 더 나은 확장성 및 RSS (수신측 배율)를 제공 합니다.
- **RPC 포트 멀티플렉서** 기능은 방화벽에 친숙 하 고 (관리할 포트가 적고) NFS 배포를 간소화 합니다.
- **자동 조정 된 캐시 및 스레드 풀** 은 워크 로드에 따라 자동으로 캐시 및 스레드 풀을 튜닝 하는 새 RPC/XDR 인프라의 리소스 관리 기능입니다. 이렇게 하면 매개 변수를 튜닝 하는 데 필요한 추측을 완전히 제거 하 여 NFS가 배포 되는 즉시 최적의 성능을 제공 합니다.
- 기존 krb5.conf 및 krb5i 인증 옵션과 함께 Kerberos 개인 정보 (Krb5p) 지원이 추가 된 **새로운 kerberos 개인 정보 구현 및 인증 옵션** 입니다.
- **Id 매핑 Windows PowerShell 모듈** cmdlet을 사용 하면 보다 쉽게 id 매핑을 관리 하 고, Active Directory LDS(Lightweight Directory Services) (AD LDS)를 구성 하 고, UNIX 및 Linux passwd와 플랫 파일을 설정할 수 있습니다.
- **볼륨 탑재 지점을** 사용 하면 nfs 버전 4.1을 사용 하 여 nfs 공유에 탑재 된 볼륨에 액세스할 수 있습니다.
- **포트 멀티플렉싱** 기능은 방화벽에 친숙 하 고 NFS 배포를 간소화 하는 RPC 포트 멀티플렉서 (포트 2049)를 지원 합니다.

## <a name="nfs-version-3-continuous-availability"></a>NFS 버전 3 지속적인 가용성

NFS 버전 3 클라이언트는 더 높은 가용성을 제공 하 고 가동 중지 시간을 줄여 빠르고 투명 한 장애 조치를 수행할 수 있습니다. NFS 버전 3 클라이언트의 경우 다음과 같은 이유로 장애 조치 (failover) 프로세스가 더 빠릅니다.

- 이제 클러스터링 인프라에서 공유 당 하나의 리소스 대신 네트워크 이름 당 하나의 리소스를 허용 하므로 리소스의 장애 조치 (failover) 시간이 크게 향상 됩니다.
- NFS 서버 내의 장애 조치 (Failover) 경로는 성능 향상을 위해 조정 됩니다.
- NFS 서버에서 와일드 카드 등록은 더 이상 필요 하지 않으며 장애 조치 (failover)는 보다 세밀 하 게 조정 됩니다.
- NSM (네트워크 상태 모니터) 알림은 장애 조치 (failover) 프로세스 후에 전송 되며, 클라이언트는 더 이상 TCP 시간 제한을 장애 조치 (failover) 된 서버에 다시 연결할 때까지 기다릴 필요가 없습니다.

NFS용 서버는 일반적으로 계획된 유지 관리 기간 동안 수동으로 시작된 경우에만 투명 장애 조치(failover)를 지원합니다. 계획되지 않은 장애 조치(failover)가 발생하는 경우 NFS 클라이언트의 연결이 끊깁니다. NFS 용 서버에는 다시 시작 키 필터와의 통합도 없습니다. 따라서 계획된 장애 조치(failover) 직후 NFS 클라이언트가 액세스하고 있는 동일한 파일에 로컬 앱이나 SMB 세션에서 액세스하려고 하면 NFS 클라이언트의 연결이 끊길 수 있습니다(투명 장애 조치(failover)가 성공하지 않음).

## <a name="deployment-and-manageability-improvements"></a>배포 및 관리 효율성 향상

NFS 배포 및 관리는 다음과 같은 방식으로 개선 되었습니다.

- 40를 초과 하는 새 Windows PowerShell cmdlet을 사용 하면 NFS 파일 공유를 쉽게 구성 하 고 관리할 수 있습니다. 자세한 내용은 [Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)을 참조 하세요.
- Id 매핑은 로컬 플랫 파일 매핑 저장소 및 id 매핑을 구성 하기 위한 새로운 Windows PowerShell cmdlet으로 향상 됩니다.
- 서버 관리자 그래픽 사용자 인터페이스를 사용 하는 것이 더 쉽습니다.
- 새 WMI 버전 2 공급자는 더 쉽게 관리할 수 있습니다.
- RPC 포트 멀티플렉서 (포트 2049)는 방화벽에 친숙 하며 NFS 배포를 간소화 합니다.

## <a name="server-manager-information"></a>서버 관리자 정보

서버 관리자 또는 최신 [Windows 관리 센터](../../manage/windows-admin-center/understand/windows-admin-center.md) -역할 및 기능 추가 마법사를 사용 하 여 NFS 용 서버 역할 서비스 (파일 및 iSCSI 서비스 역할)를 추가 합니다. 기능 설치에 대한 일반 정보는 [역할, 역할 서비스 또는 기능 설치/제거](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>)를 참조하세요. Nfs 용 서버 도구에는 nfs 용 서버와 NFS 용 클라이언트 구성 요소를 관리 하는 네트워크 파일 시스템용 서비스 MMC 스냅인이 포함 되어 있습니다. 스냅인을 사용 하 여 컴퓨터에 설치 된 NFS 용 서버 구성 요소를 관리할 수 있습니다. NFS 용 서버에는 다음과 같은 몇 가지 Windows 명령줄 관리 도구도 포함 되어 있습니다.

- **탑재** 는 원격 NFS 공유 (내보내기 라고도 함)를 로컬로 탑재 하 고 Windows 클라이언트 컴퓨터의 로컬 드라이브 문자에 매핑합니다.
- **Nfsadmin** 은 Nfs 용 서버와 Nfs 용 클라이언트 구성 요소에 대 한 구성 설정을 관리 합니다.
- **NFSSHARE** Nfs 용 서버를 사용 하 여 공유 되는 폴더에 대 한 nfs 공유 설정을 구성 합니다.
- **NFSSTAT** NFS 용 서버에서 받은 호출의 통계를 표시 하거나 다시 설정 합니다.
- **SHOWMOUNT** NFS 용 서버에서 내보낸 탑재 된 파일 시스템을 표시 합니다.
- **분리할** NFS 탑재 드라이브를 제거 합니다.

Windows Server 2012의 NFS에는 nfs 용으로 제공 되는 몇 가지 새로운 cmdlet이 포함 된 Windows PowerShell 용 NFS 모듈이 도입 되었습니다. 이러한 cmdlet은 NFS 관리 작업을 자동화 하는 쉬운 방법을 제공 합니다. 자세한 내용은 [Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)을 참조 하세요.

## <a name="additional-information"></a>추가 정보

다음 표에서는 NFS를 평가 하기 위한 추가 리소스를 제공 합니다.

|콘텐츠 유형|참조|
|---|---|
|배포|[네트워크 파일 시스템 배포](deploy-nfs.md)|
|작업|[Windows PowerShell의 NFS cmdlet](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|관련 기술|[Windows Server의 스토리지](../storage.yml)|