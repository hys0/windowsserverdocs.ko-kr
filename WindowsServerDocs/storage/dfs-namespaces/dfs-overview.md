---
title: DFS 네임 스페이스 개요
ms.prod: windows-server
ms.author: jgerend
manager: daveba
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 06/07/2019
description: 이 항목에서는 서로 다른 서버에 있는 공유 폴더를 논리적으로 구성 된 하나 이상의 네임 스페이스로 그룹화 할 수 있도록 하는 Windows Server의 역할 서비스인 DFS 네임 스페이스에 대해 설명 합니다.
ms.openlocfilehash: fd02f0b65cc57300c673d72c7879a80d48747fa2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471887"
---
# <a name="dfs-namespaces-overview"></a>DFS 네임 스페이스 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server(반기 채널)

DFS 네임 스페이스는 여러 서버에 있는 공유 폴더를 논리적으로 구성 된 하나 이상의 네임 스페이스로 그룹화 할 수 있도록 하는 Windows Server의 역할 서비스입니다. 이를 통해 사용자에 게 공유 폴더에 대 한 가상 보기를 제공할 수 있습니다 .이 경우 다음 그림과 같이 단일 경로에서 여러 서버에 있는 파일로 이동할 수 있습니다.

![DFS 네임스페이스 기술 요소](media/dfs-overview.png)

DFS 네임 스페이스를 구성 하는 요소에 대 한 설명은 다음과 같습니다.

- 네임 스페이스 **서버** -네임 스페이스 서버는 네임 스페이스를 호스팅합니다. 네임 스페이스 서버는 구성원 서버 또는 도메인 컨트롤러일 수 있습니다.
- **네임 스페이스 루트** -네임 스페이스 루트는 네임 스페이스의 시작 지점입니다. 위의 그림에서 루트의 이름은 Public이 고 네임 스페이스 경로는 \\ \\ Contoso \\ public입니다. 이 형식의 네임 스페이스는 도메인 이름 (예: Contoso)으로 시작 하 고 해당 메타 데이터가 Active Directory Domain Services (AD DS)에 저장 되기 때문에 도메인 기반 네임 스페이스입니다. 위의 그림에서 단일 네임 스페이스 서버를 보여 주지만 여러 네임 스페이스 서버에서 도메인 기반 네임 스페이스를 호스트 하 여 네임 스페이스의 가용성을 높일 수 있습니다.
- **폴더-폴더** 대상이 없는 폴더는 네임 스페이스에 구조 및 계층 구조를 추가 하 고 폴더 대상이 있는 폴더는 사용자에 게 실제 콘텐츠를 제공 합니다. 사용자가 네임 스페이스에 폴더 대상이 있는 폴더를 검색 하면 클라이언트 컴퓨터는 클라이언트 컴퓨터를 폴더 대상 중 하나로 투명 하 게 리디렉션하는 조회를 수신 합니다.
- **폴더** 대상-폴더 대상은 공유 폴더의 UNC 경로 또는 네임 스페이스의 폴더와 연결 된 다른 네임 스페이스입니다. 폴더 대상은 데이터와 콘텐츠가 저장 되는 위치입니다. 위의 그림에서 이름이 Tools 인 폴더에는 런던에 하나, 뉴욕에 있는 폴더 대상이 두 개 있으며, 학습 가이드 라는 폴더에는 뉴욕의 단일 폴더 대상이 있습니다. Contoso 공용 소프트웨어 도구를 검색 하는 사용자는 \\ \\ \\ \\ \\ \\ \\ \\ \\ \\ \\ 현재 사용자가 있는 사이트에 따라 공유 폴더 LDN 도구 또는 NYC 도구에 투명 하 게 리디렉션됩니다.

이 항목에서는 DFS 설치 방법, 새로운 기능 및 평가 및 배포 정보를 찾을 수 있는 위치에 대해 설명 합니다.

DFS 관리, [Windows PowerShell의 DFSN (Dfs 네임 스페이스) cmdlet](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps), **DFSUTIL** 명령 또는 WMI를 호출 하는 스크립트를 사용 하 여 네임 스페이스를 관리할 수 있습니다.

## <a name="server-requirements-and-limits"></a>서버 요구 사항 및 제한

DFS 관리 실행 또는 DFS 네임스페이스 사용을 위한 추가 하드웨어 또는 소프트웨어 요구 사항은 없습니다.

네임 스페이스 서버는 네임 스페이스를 호스트 하는 도메인 컨트롤러 또는 멤버 서버입니다. 서버에서 호스팅할 수 있는 네임 스페이스 수는 네임 스페이스 서버에서 실행 중인 운영 체제에 의해 결정 됩니다.

다음 운영 체제를 실행 하는 서버는 단일 독립 실행형 네임 스페이스 외에 여러 도메인 기반 네임 스페이스를 호스트할 수 있습니다.

- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 Datacenter 및 Enterprise Edition
- Windows Server(반기 채널)

다음 운영 체제를 실행 하는 서버는 단일 독립 실행형 네임 스페이스를 호스트할 수 있습니다.

- Windows Server 2008 R2 Standard

다음 표에서는 네임 스페이스를 호스트할 서버를 선택 하는 경우 고려해 야 할 추가 요소에 대해 설명 합니다.

| 독립 실행형 네임 스페이스를 호스팅하는 서버 | 도메인 기반 네임 스페이스를 호스팅하는 서버 |
| ---                                   |        ---                                |
| 네임 스페이스를 호스트할 NTFS 볼륨을 포함 해야 합니다.|네임 스페이스를 호스트할 NTFS 볼륨을 포함 해야 합니다. |
| 는 구성원 서버나 도메인 컨트롤러가 될 수 있습니다.|는 네임 스페이스를 구성 하는 도메인의 구성원 서버 또는 도메인 컨트롤러 여야 합니다. 이 요구 사항은 지정 된 도메인 기반 네임 스페이스를 호스팅하는 모든 네임 스페이스 서버에 적용 됩니다. |
| 장애 조치 (failover) 클러스터에서 호스트 하 여 네임 스페이스의 가용성을 높일 수 있습니다.|네임 스페이스는 장애 조치 (failover) 클러스터의 클러스터 된 리소스가 될 수 없습니다. 그러나 해당 서버에서 로컬 리소스만 사용 하도록 네임 스페이스를 구성 하는 경우에는 장애 조치 (failover) 클러스터의 노드 역할을 하는 서버에서 네임 스페이스를 찾을 수 있습니다. |

## <a name="installing-dfs-namespaces"></a>DFS 네임 스페이스 설치

DFS 네임스페이스 및 DFS 복제는 파일 및 스토리지 서비스 역할의 일부입니다. DFS 관리 도구(DFS 관리, Windows PowerShell용 DFS 네임스페이스 모듈 및 명령줄 도구)는 원격 서버 관리 도구의 일부로 별도로 설치됩니다.

다음 섹션에 설명 된 대로 [Windows 관리 센터](../../manage/windows-admin-center/understand/windows-admin-center.md), 서버 관리자 또는 PowerShell을 사용 하 여 DFS 네임 스페이스를 설치 합니다.

### <a name="to-install-dfs-by-using-server-manager"></a>서버 관리자를 사용하여 DFS를 설치하려면

1. 서버 관리자를 열고 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 나타납니다.

2. **서버 선택** 페이지에서 DFS를 설치할 오프라인 가상 머신의 서버 또는 VHD(가상 하드 디스크)를 허용하려면.

3. 설치할 역할 서비스 및 기능을 선택합니다.

    - DFS 네임 스페이스 서비스를 설치 하려면 **서버 역할** 페이지에서 **dfs 네임 스페이스**를 선택 합니다.

    - DFS 관리 도구만 설치하려면 **기능** 페이지에서 **원격 서버 관리 도구**, **원격 관리 도구**, **파일 서비스 도구**를 차례로 확장하고 **DFS 관리 도구**를 선택합니다.

         **DFS 관리 도구**는 DFS 관리 스냅인, Windows PowerShell용 DFS 네임스페이스 모듈 및 명령줄 도구를 설치하지만 DFS 서비스를 서버에 설치하지는 않습니다.

### <a name="to-install-dfs-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 DFS를 설치하려면

관리자 권한으로 Windows PowerShell 세션을 연 다음, 다음 명령을 입력합니다. 여기서 <name\>은 설치할 역할 서비스 또는 기능입니다. 관련 역할 서비스 또는 기능 이름 목록은 다음 표를 참조하세요.

```PowerShell
Install-WindowsFeature <name>
```

| 역할 서비스 또는 기능 | 이름 |
| ----------------------- | ---- |
| DFS 네임스페이스          | `FS-DFS-Namespace` |
| DFS 관리 도구    | `RSAT-DFS-Mgmt-Con` |

예를 들어 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치하려면 다음을 입력합니다.

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

DFS 네임 스페이스 및 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치 하려면 다음을 입력 합니다.

```PowerShell
Install-WindowsFeature "FS-DFS-Namespace", "RSAT-DFS-Mgmt-Con"
```

## <a name="interoperability-with-azure-virtual-machines"></a>Azure 가상 컴퓨터와의 상호 운용성

Microsoft Azure의 가상 머신에서 DFS 네임 스페이스를 사용 하는 것은 테스트 되었습니다. 그러나 몇 가지 제한 사항 및 요구 사항을 따라야 합니다.

- Azure 가상 컴퓨터에서 독립 실행형 네임 스페이스를 클러스터링 할 수 없습니다.

- Azure Active Directory 환경을 포함 하 여 Azure virtual machines에서 도메인 기반 네임 스페이스를 호스트할 수 있습니다.

Azure virtual machines를 시작 하는 방법에 대 한 자세한 내용은 [azure virtual machines 설명서](https://docs.microsoft.com/azure/virtual-machines/)를 참조 하세요.

## <a name="additional-references"></a>추가 참조

자세한 내용은 다음 리소스를 참조하세요.

| 콘텐츠 유형        | 참조 |
| ------------------  | ----------------|
| **제품 평가** | [Windows Server에서 제공 하는 DFS 네임 스페이스 및 DFS 복제의 새로운 기능](https://technet.microsoft.com/library/dn281957(v=ws.11).aspx) |
| **배포**    | [DFS 네임 스페이스 확장성 고려 사항](https://blogs.technet.com/b/filecab/archive/2012/08/26/dfs-namespace-scalability-considerations.aspx) |
| **작업**    | [DFS 네임스페이스: 질문과 대답](https://technet.microsoft.com/library/ee404780.aspx) |
| **커뮤니티 리소스** | [File 서비스 및 스토리지 TechNet 포럼](https://social.technet.microsoft.com/forums/winserverfiles/threads/) |
| **프로토콜**        | [Windows Server의 파일 서비스 프로토콜](https://msdn.microsoft.com/library/cc239318.aspx) (사용 되지 않음) |
| **관련 기술** | [장애 조치 클러스터링](../../failover-clustering/failover-clustering-overview.md)|
| **지원** | [Windows IT 전문가 지원](https://www.microsoft.com/itpro/windows/support)|
