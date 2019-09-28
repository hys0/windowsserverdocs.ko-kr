---
title: 네트워크 파일 시스템 배포
description: 네트워크 파일 시스템을 배포 하는 방법을 설명 합니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22c8725c227719ee143baa8f4abd3a5cc5dcf883
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393971"
---
# <a name="deploy-network-file-system"></a>네트워크 파일 시스템 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nfs (네트워크 파일 시스템)는 NFS 프로토콜을 사용 하 여 Windows Server 및 UNIX 운영 체제를 실행 하는 컴퓨터 간에 파일을 전송할 수 있도록 하는 파일 공유 솔루션을 제공 합니다. 이 항목에서는 NFS를 배포 하기 위해 수행 해야 하는 단계에 대해 설명 합니다.

## <a name="whats-new-in-network-file-system"></a>네트워크 파일 시스템의 새로운 기능

Windows Server 2012에서 NFS에 대 한 다음 같습니다 변경 되었습니다.

- **NFS 버전 4.1에 대 한 지원**. 이 프로토콜 버전에는 다음과 같은 향상 된 기능이 포함 되어 있습니다.
  - 방화벽을 탐색 하는 것이 더 쉽고 접근성이 향상 됩니다.
  - 는 rpcsec\_GSS 프로토콜을 지원 하 여 더 강력한 보안을 제공 하 고 클라이언트와 서버가 보안을 협상할 수 있도록 합니다.
  - UNIX 및 Windows 파일 의미 체계를 지원 합니다.
  - 는 클러스터 된 파일 서버 배포를 활용 합니다.
  - WAN 친화적인 복합 프로시저를 지원 합니다.

- **Windows PowerShell 용 NFS 모듈** 기본 제공 NFS cmdlet을 사용 하면 다양 한 작업을 보다 쉽게 자동화할 수 있습니다. Cmdlet 이름은 다른 Windows PowerShell cmdlet ("Get" 및 "Set"와 같은 동사 사용)과 일치 하므로 Windows PowerShell을 사용 하는 사용자가 새 cmdlet을 사용 하는 방법을 보다 쉽게 알 수 있습니다.
- **NFS 관리 기능이 향상**되었습니다. 새 중앙 집중식 UI 기반 관리 콘솔은 클러스터 된 파일 서버를 관리 하는 것 외에도 SMB 및 NFS 공유, 할당량, 파일 화면 및 분류의 구성 및 관리를 간소화 합니다.
- **Id 매핑 향상**. Id 매핑을 구성 하는 새로운 UI 지원 및 작업 기반 Windows PowerShell cmdlet을 사용 하 여 관리자가 id 매핑 원본을 빠르게 구성한 다음 사용자에 대 한 개별 매핑된 id를 만들 수 있습니다. 향상 된 기능을 통해 관리자는 NFS 및 SMB를 통해 다중 프로토콜 액세스를 위한 공유를 쉽게 설정할 수 있습니다.
- **클러스터 리소스 모델 재구성**. 이러한 향상 된 기능은 Windows NFS 및 SMB 프로토콜 서버에 대 한 클러스터 리소스 모델 간에 일관성을 유지 하 고 관리를 간소화 합니다. 공유 수가 많은 NFS 서버의 경우 리소스 네트워크 및 많은 수의 NFS 공유를 포함 하는 볼륨에 대 한 장애 조치 (failover)를 수행 하는 데 필요한 WMI 호출 수가 줄어듭니다.
- **Resume Key Manager와 통합**합니다. Resume 키 관리자는 파일 서버 및 파일 시스템 상태를 추적 하 고 Windows SMB 및 NFS 프로토콜 서버가 파일 서버에 데이터를 저장 하는 클라이언트 또는 서버 응용 프로그램을 중단시 키 지 않고 장애 조치 (failover) 할 수 있도록 하는 구성 요소입니다. 이러한 향상 된 기능은 Windows Server 2012를 실행 하는 파일 서버의 지속적인 가용성 기능에 대 한 핵심 구성 요소입니다.

## <a name="scenarios-for-using-network-file-system"></a>네트워크 파일 시스템 사용에 대 한 시나리오

NFS는 Windows 기반 및 UNIX 기반 운영 체제의 혼합 환경을 지원 합니다. 다음 배포 시나리오는 NFS를 사용 하 여 지속적으로 사용 가능한 Windows Server 2012 파일 서버를 배포 하는 방법의 예입니다.

### <a name="provision-file-shares-in-heterogeneous-environments"></a>다른 유형의 환경에서 파일 공유 프로 비전

이 시나리오는 Windows 및 기타 운영 체제 (예: UNIX 또는 Linux 기반 클라이언트 컴퓨터)로 구성 된 이기종 환경의 조직에 적용 됩니다. 이 시나리오에서는 SMB 및 NFS 프로토콜을 통해 동일한 파일 공유에 대 한 다중 프로토콜 액세스를 제공할 수 있습니다. 일반적으로이 시나리오에서는 Windows 파일 서버를 배포할 때 Windows 및 UNIX 기반 컴퓨터의 사용자 간에 작업을 쉽게 수행할 수 있습니다. 파일 공유를 구성 하는 경우 smb 프로토콜을 통해 Windows 사용자가 파일에 액세스 하 고, UNIX 기반 컴퓨터의 사용자는 일반적으로 NFS 프로토콜을 통해 파일에 액세스 합니다.

이 시나리오의 경우 유효한 id 매핑 소스 구성이 있어야 합니다. Windows Server 2012에서는 다음과 같은 id 매핑 저장소를 지원 합니다.

- 매핑 파일
- AD DS(Active Directory 도메인 서비스)
- Active Directory LDS(Lightweight Directory Services) (AD LDS)와 같은 RFC 2307 호환 LDAP 저장소
- 사용자 이름 매핑 (UNM) 서버

### <a name="provision-file-shares-in-unix-based-environments"></a>UNIX 기반 환경에서 파일 공유 프로 비전

이 시나리오에서 Windows 파일 서버는 UNIX 기반 클라이언트 컴퓨터용 NFS 파일 공유에 대 한 액세스를 제공 하기 위해 주로 UNIX 기반 환경에 배포 됩니다. 매핑되지 않은 UNIX 사용자 액세스 (UUUA) 옵션은 Windows Server 2008 r 2에서 NFS 공유에 대해 처음 구현 되었으므로 UNIX에서 Windows 계정 매핑을 만들지 않고 NFS 데이터를 저장 하는 데 Windows Server를 사용할 수 있습니다. UUUA를 사용 하면 관리자가 계정 매핑을 구성 하지 않고도 NFS를 신속 하 게 프로 비전 하 고 배포할 수 있습니다. NFS에 대해 사용 하도록 설정 된 경우 UUUA는 매핑되지 않은 사용자를 나타내는 사용자 지정 Sid (보안 식별자)를 만듭니다. 매핑된 사용자 계정은 표준 Windows Sid (보안 식별자)를 사용 하 고 매핑되지 않은 사용자는 사용자 지정 NFS Sid를 사용 합니다.

## <a name="system-requirements"></a>시스템 요구 사항

NFS 용 서버는 모든 버전의 Windows Server 2012에 설치할 수 있습니다. Nfs 서버 또는 NFS 클라이언트를 실행 하는 UNIX 기반 컴퓨터에서 nfs 서버 및 클라이언트 구현이 다음 프로토콜 사양 중 하나를 준수 하는 경우 NFS를 사용할 수 있습니다.

1. NFS 버전 4.1 프로토콜 사양 (RFC [5661](https://tools.ietf.org/html/rfc5661)에 정의 됨)
2. NFS 버전 3 프로토콜 사양 (RFC [1813](https://tools.ietf.org/html/rfc1813)에 정의 됨)
3. NFS 버전 2 프로토콜 사양 (RFC [1094](https://tools.ietf.org/html/rfc1094)에 정의 됨)

## <a name="deploy-nfs-infrastructure"></a>NFS 인프라 배포

다음 컴퓨터를 배포 하 고 LAN (local area network)에 연결 해야 합니다.

- 두 가지 NFS 용 서비스 구성 요소를 설치 하는 Windows Server 2012를 실행 하는 하나 이상의 컴퓨터: Nfs 용 서버와 NFS 용 클라이언트 이러한 구성 요소는 동일한 컴퓨터나 다른 컴퓨터에 설치할 수 있습니다.
- NFS 서버와 NFS 클라이언트 소프트웨어를 실행 하는 하나 이상의 UNIX 기반 컴퓨터입니다. Nfs 서버를 실행 하는 UNIX 기반 컴퓨터는 nfs 파일 공유 또는 내보내기를 호스팅합니다 .이 파일은 Windows Server 2012를 실행 하는 컴퓨터에서 NFS 용 클라이언트를 사용 하는 클라이언트로 액세스 합니다. 원하는 대로 동일한 UNIX 기반 컴퓨터 또는 다른 UNIX 기반 컴퓨터에 NFS 서버 및 클라이언트 소프트웨어를 설치할 수 있습니다.
- Windows Server 2008 R2 기능 수준에서 실행 되는 도메인 컨트롤러입니다. 도메인 컨트롤러는 Windows 환경에 대 한 사용자 인증 정보 및 매핑을 제공 합니다.
- 도메인 컨트롤러를 배포 하지 않은 경우에는 NIS (NIS(네트워크 정보 서비스)) 서버를 사용 하 여 UNIX 환경에 대 한 사용자 인증 정보를 제공할 수 있습니다. 또는 원하는 경우 사용자 이름 매핑 서비스를 실행 하는 컴퓨터에 저장 된 암호 및 그룹 파일을 사용할 수 있습니다.

### <a name="install-network-file-system-on-the-server-with-server-manager"></a>서버 관리자를 사용 하 여 서버에 네트워크 파일 시스템 설치

1. 역할 및 기능 추가 마법사의 서버 역할에서 **파일 및 저장소 서비스** 를 선택합니다(아직 설치하지 않은 경우).
2. **파일 및 ISCSI 서비스**에서 **파일 서버** 및 **NFS 용 서버**를 선택 합니다. 선택한 NFS 기능을 포함 하려면 **기능 추가** 를 선택 합니다.
3. 서버에 NFS 구성 요소를 설치 하려면 **설치** 를 선택 합니다.

### <a name="install-network-file-system-on-the-server-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 서버에 네트워크 파일 시스템 설치

1. Windows PowerShell을 시작합니다. 작업 표시줄에서 PowerShell을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 선택합니다.
2. 다음 Windows PowerShell 명령을 실행합니다.

```PowerShell
Import-Module ServerManager
Add-WindowsFeature FS-NFS-Service
Import-Module NFS
```

## <a name="configure-nfs-authentication"></a>NFS 인증 구성

NFS 버전 4.1 및 NFS 버전 3.0 프로토콜을 사용 하는 경우 다음과 같은 인증 및 보안 옵션이 있습니다.

- RPCSEC\_GSS
  - **Krb5**. 는 Kerberos 버전 5 프로토콜을 사용 하 여 파일 공유에 대 한 액세스 권한을 부여 하기 전에 사용자를 인증 합니다.
  - **Krb5i**. 에서는 Kerberos 버전 5 프로토콜을 사용 하 여 무결성 검사 (체크섬)로 인증 하 고이로 인해 데이터가 변경 되지 않았는지 확인 합니다.
  - **Krb5p** 는 개인 정보 보호를 위해 암호화를 사용 하 여 NFS 트래픽을 인증 하는 Kerberos 버전 5 프로토콜을 사용 합니다.
- 인증\_SYS

매핑되지 않은 사용자 액세스를 사용 하도록 설정 하는 옵션\_을 제공 하는 서버 권한 부여 (AUTH SYS)를 사용 하지 않도록 선택할 수도 있습니다. 매핑되지 않은 사용자 액세스를 사용 하는 경우 기본값 인 UID/GID로 매핑되지 않은 사용자 액세스를 허용 하도록 지정 하거나 익명 액세스를 허용할 수 있습니다.

NFS 인증 구성에 대 한 지침은 다음 섹션에서 설명 합니다.

## <a name="create-an-nfs-file-share"></a>NFS 파일 공유 만들기

서버 관리자 또는 Windows PowerShell NFS cmdlet 중 하나를 사용 하 여 NFS 파일 공유를 만들 수 있습니다.

### <a name="create-an-nfs-file-share-with-server-manager"></a>서버 관리자를 사용 하 여 NFS 파일 공유 만들기

1. 서버에 로컬 관리자 그룹의 구성원으로 로그온합니다.
2. 서버 관리자가 자동으로 시작됩니다. 자동으로 시작 되지 않으면 **시작**을 선택 하 고 **servermanager**를 입력 한 다음 **서버 관리자**를 선택 합니다.
3. 왼쪽에서 **파일 및 저장소 서비스**를 선택 하 고 **공유**를 선택 합니다.
4. **파일 공유를 만들려면 선택 하 고 새 공유 마법사를 시작**합니다.
5. **프로필 선택** 페이지에서 **NFS 공유 – 빠른** 또는 **nfs 공유-고급**을 선택 하 고 **다음**을 선택 합니다.
6. **공유 위치** 페이지에서 서버 및 볼륨을 선택 하 고 **다음**을 선택 합니다.
7. **공유 이름** 페이지에서 새 공유의 이름을 지정 하 고 **다음**을 선택 합니다.
8. **인증** 페이지에서이 공유에 사용할 인증 방법을 지정 합니다.
9. **공유 권한** 페이지에서 **추가**를 선택한 다음, 공유에 사용 권한을 부여 하려는 호스트, 클라이언트 그룹 또는 netgroup을 지정 합니다.
10. **권한**에서 사용자에 게 부여할 액세스 제어의 유형을 구성 하 고 **확인**을 선택 합니다.
11. **확인** 페이지에서 구성을 검토 하 고 **만들기** 를 선택 하 여 NFS 파일 공유를 만듭니다.

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet은 NFS 파일 공유를 만들 수도 있습니다. 여기서 `nfs1` 은 공유의 이름이 고 `C:\\shares\\nfsfolder` 은 파일 경로입니다.

```PowerShell
New-NfsShare -name nfs1 -Path C:\shares\nfsfolder
```

### <a name="known-issue"></a>알려진 문제
NFS 버전 4.1에서는 잘못 된 문자를 사용 하 여 파일 이름을 만들거나 복사할 수 있습니다. Vi 편집기를 사용 하 여 파일을 열려고 하면 손상 된 것으로 표시 됩니다. Vi에서 파일을 저장 하거나 이름을 바꾸거나 이동 하거나 사용 권한을 변경할 수 없습니다. 잘못 된 문자를 사용 하지 마십시오.
