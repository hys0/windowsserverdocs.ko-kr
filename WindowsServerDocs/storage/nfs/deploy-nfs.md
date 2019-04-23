---
title: 네트워크 파일 시스템 배포
description: 네트워크 파일 시스템을 배포 하는 방법에 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2f3671283720d515cd3e3e609d98e02343c15892
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860774"
---
# <a name="deploy-network-file-system"></a>네트워크 파일 시스템 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네트워크 파일 시스템 (NFS) 파일 공유 Windows 서버와 NFS 프로토콜을 사용 하 여 UNIX 운영 체제를 실행 하는 컴퓨터 간에 파일을 전송할 수 있는 솔루션을 제공 합니다. 이 항목에서는 NFS를 배포 하기 위해 따라야 하는 단계를 설명 합니다.

## <a name="whats-new-in-network-file-system"></a>네트워크 파일 시스템의 새로운 기능

Windows Server 2012의 NFS에 대 한 변경 내용 다음과 같습니다.

- **NFS 버전 4.1에 대 한 지원을**합니다. 이 프로토콜 버전에는 다음과 같은 향상 기능이 포함 됩니다.
  - 방화벽을 탐색 하는 것이 쉽습니다 내게 필요한 옵션 개선입니다.
  - RPCSEC 지원\_GSS 프로토콜, 보다 강력한 보안을 제공 하 고 클라이언트 및 서버 보안 협상을 허용 합니다.
  - UNIX 및 Windows 파일 의미 체계를 지원합니다.
  - 클러스터 된 파일 서버 배포의 이점을 활용 합니다.
  - WAN에 게 친숙 한 복합 프로시저를 지원합니다.

- **Windows PowerShell 용 NFS 모듈**합니다. 기본 제공 NFS cmdlet의 가용성을 쉽게 다양 한 작업을 자동화할 수 있습니다. Cmdlet 이름은 다른 Windows PowerShell cmdlet ("Get" 및 "Set"와 같은 동사 사용)를 보다 쉽게 사용자에 대 한 새 cmdlet을 사용 하는 방법을 배우는 Windows PowerShell에 익숙한와 일치 합니다.
- **NFS 관리 향상**합니다. 새 중앙 집중식된 UI 기반 관리 콘솔의 SMB 및 NFS 공유, 할당량, 파일 차단 및 클러스터 된 파일 서버를 관리 하는 것 외에도 분류, 구성 및 관리를 간소화 합니다.
- **향상 된 기능 Mapping identity**합니다. 관리자가 신속 하 게는 id 매핑 소스를 구성 하 고 만든 다음 사용자에 대 한 개별 매핑된 id를 허용 하는 id 매핑을 구성 하기 위한 작업 기반 Windows PowerShell cmdlet 및 새 UI 지원 합니다. 향상 된 SMB 및 NFS를 통해 다중 프로토콜 액세스를 위해 공유를 설정 하려면 관리자가 쉽게 있습니다.
- **클러스터 리소스 모델 재구성**합니다. 이러한 향상 된이 기능 Windows NFS에 대 한 클러스터 리소스 모델 및 SMB 프로토콜 서버 간의 일관성을 제공 하 고 관리를 간소화 합니다. 많은 공유에 있는 NFS 서버에 대 한 리소스 네트워크 및 필요한 WMI 호출 횟수는 장애 조치 볼륨 포함 하는 많은 수의 NFS 공유 줄어듭니다.
- **다시 시작 키 관리자와의 통합**합니다. 다시 시작 키 관리자는 파일 서버 및 파일 시스템 상태를 추적 하 고 클라이언트 또는 파일 서버의 데이터를 저장 하는 서버 응용 프로그램을 방해 하지 않고 장애 조치할 Windows SMB 및 NFS 프로토콜 서버를 사용 하도록 설정 하는 구성 요소입니다. 이러한 향상은 Windows Server 2012를 실행 하는 파일 서버의 지속적인 가용성 기능의 핵심 구성 요소.

## <a name="scenarios-for-using-network-file-system"></a>네트워크 파일 시스템을 사용 하는 시나리오

NFS 혼합된 된 환경의 Windows 및 UNIX 기반 운영 체제를 지원합니다. 다음 배포 시나리오는 NFS를 사용 하 여 지속적으로 사용 가능한 Windows Server 2012 파일 서버를 배포 하는 방법의 예입니다.

### <a name="provision-file-shares-in-heterogeneous-environments"></a>이종 시스템 환경에서 프로 비전 파일 공유

이 시나리오는 Windows와 UNIX 또는 Linux 기반 클라이언트와 같은 다른 운영 체제의 구성 된 이기종 환경의 사용 하 여 조직에 적용 됩니다. 컴퓨터. 이 시나리오에서는 SMB 및 NFS 프로토콜을 통해 동일한 파일 공유에 대 한 다중 프로토콜 액세스를 제공할 수 있습니다. 일반적으로이 시나리오에서 Windows 파일 서버를 배포할 때 Windows에서 사용자와 UNIX 기반 컴퓨터 간의 공동 작업을 지원 해야 합니다. 파일 공유를 구성 된 경우 SMB 및 NFS 프로토콜을 사용 하 여 해당 파일에서 SMB 프로토콜을 통해 액세스 하는 Windows 사용자와 공유 및 UNIX 기반 컴퓨터의 사용자가 NFS 프로토콜을 통해 일반적으로 해당 파일에 액세스 합니다.

이 시나리오에 대 한 올바른 id 매핑 소스 구성을 해야 합니다. Windows Server 2012는 다음 id 매핑 저장소를 지원합니다.

- 매핑 파일
- AD DS(Active Directory 도메인 서비스)
- Active Directory Lightweight Directory Services (AD LDS)와 같은 RFC 2307 규격 LDAP 저장
- 사용자 이름 매핑 (UNM) 서버

### <a name="provision-file-shares-in-unix-based-environments"></a>UNIX 기반 환경에서 프로 비전 파일 공유

이 시나리오에서는 Windows 파일 서버 클라이언트 UNIX 기반 컴퓨터에 대 한 NFS 파일 공유에 대 한 액세스를 제공 하는 대부분의 UNIX 기반 환경에 배포 됩니다. UNIX-Windows를 만들지 않고 NFS 데이터를 저장 하기 위한 서버를 사용할 수 있습니다 Windows 계정 매핑 있도록에 처음에 매핑되지 않은 UNIX 사용자 액세스 (UUUA) 옵션 Windows Server 2008 R2에서 NFS 공유에 대 한 구현 되었습니다. UUUA 신속 하 게 프로 비전 하 고 NFS 계정 매핑을 구성 하지 않고도 배포에 할당할 수 있습니다. NFS 용 사용 하도록 설정 하면 사용자 지정 보안 식별자 (Sid) 매핑되지 않은 사용자를 나타내는 UUUA에 만듭니다. 매핑된 사용자 계정이 표준 Windows Sid (보안 식별자)를 사용 하 고 매핑되지 않은 사용자가 사용자 지정 NFS Sid를 사용 합니다.

## <a name="system-requirements"></a>시스템 요구 사항

Windows Server 2012 버전에서 NFS 용 서버를 설치할 수 있습니다. UNIX 기반 컴퓨터에서 실행 하는 NFS 서버 또는 NFS 클라이언트를 이러한 NFS 서버 및 클라이언트 구현은 준수 하는 경우 다음 프로토콜 사양 중 하나를 사용 하 여 NFS를 사용할 수 있습니다.

1. NFS 버전 4.1 프로토콜 사양 (RFC에 정의 된 대로 [5661](https://tools.ietf.org/html/rfc5661))
2. NFS 버전 3 프로토콜 사양 (RFC에 정의 된 대로 [1813](https://tools.ietf.org/html/rfc1813))
3. NFS 버전 2 프로토콜 사양 (RFC에 정의 된 대로 [1094](https://tools.ietf.org/html/rfc1094))

## <a name="deploy-nfs-infrastructure"></a>NFS 인프라 배포

다음 컴퓨터를 배포 하 고 로컬 영역 네트워크 (LAN) 연결 해야 합니다.

- 하나 이상의 컴퓨터 NFS 구성 요소에 대 한 두 가지 주요 서비스를 설치할 Windows Server 2012를 실행 합니다. NFS 용 서버와 NFS 용 클라이언트입니다. 동일한 컴퓨터 또는 서로 다른 컴퓨터에 이러한 구성 요소를 설치할 수 있습니다.
- 하나 이상의 UNIX 기반 컴퓨터는 NFS 서버 및 NFS 클라이언트 소프트웨어를 실행 합니다. NFS 서버를 실행 하는 UNIX 기반 컴퓨터는 NFS 파일 공유 또는 NFS 용 클라이언트를 사용 하는 클라이언트와 Windows Server 2012를 실행 하는 컴퓨터에서 액세스할 수 있는 내보내기를 호스팅합니다. 필요에 따라 서로 다른 UNIX 기반 컴퓨터에 또는 동일한 UNIX 기반 컴퓨터에서 NFS 서버 및 클라이언트 소프트웨어를 설치할 수 있습니다.
- Windows Server 2008 R2 기능 수준에서 실행 하는 도메인 컨트롤러입니다. 도메인 컨트롤러에는 사용자 인증 정보와 Windows 환경에 대 한 매핑을 제공합니다.
- 도메인 컨트롤러를 배포 되지 않은 경우 UNIX 환경에 대 한 사용자 인증 정보를 제공 하는 정보 NIS (네트워크 서비스) 서버를 사용할 수 있습니다. 또는 원한다 면 사용자 이름 매핑 서비스를 실행 하는 컴퓨터에 저장 된 암호 및 그룹 파일을 사용할 수 있습니다.

### <a name="install-network-file-system-on-the-server-with-server-manager"></a>서버 관리자를 사용 하 여 서버에 네트워크 파일 시스템을 설치

1. 역할 및 기능 추가 마법사의 서버 역할에서 **파일 및 저장소 서비스** 를 선택합니다(아직 설치하지 않은 경우).
2. 아래 **파일 및 iSCSI 서비스**를 선택 **파일 서버** 하 고 **NFS 용 서버**합니다. 선택 **기능 추가** 선택한 NFS 기능을 포함 하도록 합니다.
3. 선택 **설치** 서버의 NFS 구성 요소를 설치 합니다.

### <a name="install-network-file-system-on-the-server-with-windows-powershell"></a>Windows PowerShell을 사용 하 여 서버의 네트워크 파일 시스템을 설치 합니다.

1. Windows PowerShell을 시작합니다. 작업 표시줄에서 PowerShell을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 선택합니다.
2. 다음 Windows PowerShell 명령을 실행합니다.

```PowerShell
Import-Module ServerManager
Add-WindowsFeature FS-NFS-Service
Import-Module NFS
```

## <a name="configure-nfs-authentication"></a>NFS 인증 구성

NFS 버전 4.1 및 NFS 버전 3.0 프로토콜을 사용 하는 경우 다음 인증 및 보안 옵션 해야 합니다.

- RPCSEC\_GSS
  - **Krb5**. 파일 공유에 대 한 액세스 권한을 부여 하기 전에 사용자를 인증 하는 Kerberos 버전 5 프로토콜을 사용 합니다.
  - **Krb5i**. Kerberos 버전 5 프로토콜을 사용 하 여 무결성 검사 (체크섬)을 사용 하 여 인증 하는 데이터가 변경 되지 않은 확인 합니다.
  - **Krb5p** 개인 정보 취급에 대 한 암호화로 NFS 트래픽을 인증 하는 사용 하 여 Kerberos 버전 5 프로토콜입니다.
- AUTH\_SYS

서버 권한 부여를 사용 하지 않도록 선택할 수도 있습니다 (인증\_SYS)를 제공 하는 매핑되지 않은 사용자 액세스를 사용 하도록 설정 하는 옵션입니다. 매핑되지 않은 사용자 액세스를 사용 하는 경우 UID 매핑되지 않은 사용자 액세스를 허용 하도록 지정할 수 있습니다 GID는 기본값인 또는 익명 액세스를 허용 합니다.

NFS 인증을 구성 하기 위한 지침은 다음 섹션에서 설명 합니다.

## <a name="create-an-nfs-file-share"></a>NFS 파일 공유 만들기

서버 관리자 또는 Windows PowerShell의 NFS cmdlet을 사용 하 여 NFS 파일 공유를 만들 수 있습니다.

### <a name="create-an-nfs-file-share-with-server-manager"></a>서버 관리자를 사용 하 여 NFS 파일 공유 만들기

1. 서버에 로컬 관리자 그룹의 구성원으로 로그온합니다.
2. 서버 관리자가 자동으로 시작됩니다. 자동으로 시작 되지 않으면 선택 **시작**, 형식 **servermanager.exe**를 선택한 후 **Server Manager**합니다.
3. 왼쪽에서 선택 **File and Storage Services**를 선택한 후 **공유**합니다.
4. 선택 **파일 공유를 만들려면 새 공유 마법사를 시작**합니다.
5. 에 **프로필 선택** 페이지에서 **NFS 공유 – 빠르게** 또는 **NFS 공유-고급**을 선택한 후 **다음**합니다.
6. 에 **공유 위치** 페이지는 서버 및 볼륨을 선택 하 고 선택 **다음**합니다.
7. 에 **공유 이름** 페이지에서 새 공유의 이름을 지정 하 고 선택 **다음**합니다.
8. 에 **인증** 페이지에서이 공유에 대 한 사용 하려는 인증 방법을 지정 합니다.
9. 에 **공유 사용 권한** 페이지에서 **추가**, 호스트, 클라이언트 그룹 또는 공유에 권한을 부여 하려는 netgroup을 지정 합니다.
10. **사용 권한**, 액세스 제어 사용자가 선택한를 원하는 방식으로 구성 **확인**합니다.
11. 에 **확인** 페이지에서 구성을 검토 하 고 선택 **만들기** NFS 파일 공유를 만들 수 있습니다.

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet을 NFS 파일 공유를 만들 수도 있습니다 (여기서 `nfs1` 공유의 이름 및 `C:\\shares\\nfsfolder` 파일 경로입니다):

```PowerShell
New-NfsShare -name nfs1 -Path C:\shares\nfsfolder
```

### <a name="known-issue"></a>알려진 문제
NFS 버전 4.1 허용 될 파일 이름을 생성 되거나 잘못 된 문자를 사용 하 여 복사 합니다. Vi 편집기를 사용 하 여 파일을 열려고 하는 경우 손상 된 것으로 표시 됩니다. Vi에서 파일을 저장 이름을 변경 하거나 이동 사용 권한을 변경할 수 없습니다. Illigal 문자를 사용 하지 마십시오.
