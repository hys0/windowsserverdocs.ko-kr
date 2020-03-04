---
title: DFS 복제 개요
ms.date: 03/08/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: c17fd78a2cf726ab156d3eda09b9c0e2d4ed6a75
ms.sourcegitcommit: aaae95cb05c44232099ec46b04a127c77a3f486e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77520359"
---
# <a name="dfs-replication-overview"></a>DFS 복제 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server(반기 채널)

DFS 복제는 Windows Server의 역할 서비스로, 여러 서버 및 사이트의 폴더(DFS 네임스페이스 경로에 참조된 폴더 포함)를 효율적으로 복제할 수 있습니다. DFS 복제는 제한된 대역폭 네트워크 연결을 통해 서버 간에 폴더를 동기화 상태로 유지하는 데 사용할 수 있는 효율적인 다중 마스터 복제 엔진입니다. FRS(파일 복제 서비스)를 DFS 네임스페이스에 대한 복제 엔진으로 바꾸고, Windows Server 2008 이상 도메인 기능 수준을 사용하는 도메인의 AD DS(Active Directory Domain Services) SYSVOL 폴더를 복제합니다.

DFS 복제에서는 RDC(원격 차등 압축)라는 압축 알고리즘을 사용합니다. RDC는 파일의 데이터에 대한 변경 내용을 검색하고 DFS 복제가 전체 파일 대신 변경된 파일 블록만 복제할 수 있게 합니다.

DFS 복제를 사용하여 SYSVOL을 복제하는 방법에 대한 자세한 내용은 [DFS 복제로 SYSVOL 복제 마이그레이션](migrate-sysvol-to-dfsr.md)을 참조하세요.

DFS 복제를 사용하려면 복제 그룹을 만들고 그룹에 복제된 폴더를 추가해야 합니다. 복제 그룹, 복제된 폴더 및 구성원이 다음 그림에 나와 있습니다.

![두 구성원 간의 연결을 포함하는 복제 그룹. 각각 복제된 폴더가 두 개 있음.](media/dfsr-overview.gif)

이 그림에서는 복제 그룹이 하나 이상의 복제된 폴더의 복제에 참여하는 서버 세트(구성원이라고 함)를 보여줍니다. 복제된 폴더는 각 구성원에서 동기화 상태를 유지하는 폴더입니다. 그림에는 두 개의 복제된 폴더가 있습니다. 프로젝트 및 제안. 데이터가 복제된 각 폴더에서 변경되면 복제 그룹의 구성원 간 연결을 통해 변경 내용이 복제됩니다. 모든 멤버 간의 연결은 복제 토폴로지를 형성합니다.
복제 그룹에 대한 토폴로지, 예약 및 대역폭 제한이 복제된 각 폴더에 적용되기 때문에 단일 복제 그룹에 여러 개의 복제된 폴더를 생성하면 복제된 폴더의 배포 프로세스가 간소화됩니다. 복제된 폴더를 추가로 배포하려면 Dfsradmin.exe를 사용하거나 마법사의 지시에 따라 새로 복제된 폴더에 대한 로컬 경로 및 사용 권한을 정의할 수 있습니다.

복제된 각 폴더에는 파일 및 하위 폴더 필터와 같은 고유한 설정이 있으므로 복제된 각 폴더에 대해 서로 다른 파일과 하위 폴더를 필터링할 수 있습니다.

각 구성원에 저장된 복제된 폴더는 구성원의 다른 볼륨에 있을 수 있으며 복제된 폴더는 공유 폴더 또는 네임스페이스의 일부가 될 필요가 없습니다. 그러나 DFS 관리 스냅인을 사용하면 복제된 폴더를 쉽게 공유하고 필요에 따라 기존 네임스페이스에 게시할 수 있습니다.

DFS 관리, DfsrAdmin 및 Dfsrdiag 명령 또는 WMI를 호출하는 스크립트를 사용하여 DFS 복제를 관리할 수 있습니다.

## <a name="requirements"></a>요구 사항

DFS 복제를 배포하려면 다음과 같이 서버를 구성해야 합니다.

- Windows Server 2003 R2 이상 스키마 추가를 포함하도록 AD DS(Active Directory Domain Services) 스키마를 업데이트합니다. 읽기 전용 복제된 폴더는 Windows Server 2003 R2 이전 스키마 추가와 함께 사용할 수 없습니다.
- 복제 그룹에 있는 모든 서버가 같은 포리스트에 있는지 확인합니다. 다른 포리스트에 있는 서버에서 복제를 사용할 수 없습니다.
- 복제 그룹의 구성원 역할을 하게 되는 모든 서버에 DFS 복제를 설치합니다.
- 바이러스 백신 소프트웨어 공급업체에 문의하여 바이러스 백신 소프트웨어가 DFS 복제와 호환되는지 확인합니다.
- NTFS 파일 시스템으로 포맷된 볼륨에서 복제할 폴더를 찾습니다. DFS 복제는 ReFS(복원 파일 시스템) 또는 FAT 파일 시스템을 지원하지 않습니다. 또한 DFS 복제는 클러스터 공유 볼륨에 저장된 콘텐츠 복제를 지원하지 않습니다.

## <a name="interoperability-with-azure-virtual-machines"></a>Azure 가상 컴퓨터와의 상호 운용성

Azure의 가상 머신에서 DFS 복제 사용이 Windows Server에서 테스트되었지만 몇 가지 제한 사항 및 요구 사항을 따라야 합니다.

- SYSVOL 폴더 외 모든 것을 복제하기 위해 DFS 복제를 실행하는 서버를 복원하는 데 스냅샷 또는 저장된 상태를 사용하면 DFS 복제가 실패할 수 있는데, 이 경우 특별한 데이터베이스 복구 단계가 필요합니다. 마찬가지로, 가상 머신을 내보내거나, 복제 또는 복사하지 마세요. 자세한 내용은 Microsoft 기술 자료 문서 [2517913](https://support.microsoft.com/kb/2517913) 및 [안전하게 DFSR 가상화](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)를 참조하세요.
- 가상 머신에 있는 복제된 폴더의 데이터를 백업하는 경우, 게스트 가상 머신 내에서 백업 소프트웨어를 사용해야 합니다.
- DFS 복제를 사용하려면 물리적 또는 가상화된 도메인 컨트롤러에 액세스해야 합니다. DFS 복제는 직접 Azure AD와 통신할 수 없습니다.
- DFS 복제에는 온-프레미스 복제 그룹 구성원과 Azure VM에서 호스트팅되는 구성원 간에 VPN 연결이 필요합니다. 또한 RPC 엔드포인트 매퍼(포트 135) 및 49152와 65535 사이에 임의로 할당된 포트가 VPN 연결을 통과할 수 있도록 온-프레미스 라우터(예: Forefront Threat Management Gateway)를 구성해야 합니다. Set-DfsrMachineConfiguration cmdlet 또는 Dfsrdiag 명령줄 도구를 사용하여 임의 포트 대신 고정 포트를 지정할 수 있습니다. DFS 복제에 고정 포트를 지정하는 방법에 대한 자세한 내용은 [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration)을 참조하세요. Windows Server를 관리하기 위해 열려는 관련 포트에 대한 자세한 내용은 Microsoft 기술 자료 문서 [832017](https://support.microsoft.com/kb/832017) 을 참조하세요.

Azure 가상 컴퓨터를 시작하는 방법에 대해 자세히 알아보려면 [Microsoft Azure 웹 사이트](https://docs.microsoft.com/azure/virtual-machines/)를 방문하세요.

## <a name="installing-dfs-replication"></a>DFS 복제 설치

DFS 복제는 파일 및 스토리지 서비스 역할의 일부입니다. DFS 관리 도구(DFS 관리, Windows PowerShell용 DFS 복제 모듈 및 명령줄 도구)는 원격 서버 관리 도구의 일부로 별도로 설치됩니다.

다음 섹션에 설명된 대로 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md), 서버 관리자 또는 PowerShell을 사용하여 DFS 복제를 설치합니다.

### <a name="to-install-dfs-by-using-server-manager"></a>서버 관리자를 사용하여 DFS를 설치하려면

1. 서버 관리자를 열고 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 나타납니다.

2. **서버 선택** 페이지에서 DFS를 설치할 오프라인 가상 머신의 서버 또는 VHD(가상 하드 디스크)를 허용하려면.

3. 설치할 역할 서비스 및 기능을 선택합니다.

    - DFS 복제 서비스를 설치하려면 **서버 역할** 페이지에서 **DFS 복제**를 선택합니다.

    - DFS 관리 도구만 설치하려면 **기능** 페이지에서 **원격 서버 관리 도구**, **원격 관리 도구**, **파일 서비스 도구**를 차례로 확장하고 **DFS 관리 도구**를 선택합니다.

         **DFS 관리 도구**는 DFS 관리 스냅인, Windows PowerShell용 DFS 복제 및 DFS 네임스페이스 모듈 및 명령줄 도구를 설치하지만 DFS 서비스를 서버에 설치하지는 않습니다.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 DFS 복제를 설치하려면 다음을 수행합니다.

관리자 권한으로 Windows PowerShell 세션을 연 다음, 다음 명령을 입력합니다. 여기서 <name\>은 설치할 역할 서비스 또는 기능입니다. 관련 역할 서비스 또는 기능 이름 목록은 다음 표를 참조하세요.

```PowerShell
Install-WindowsFeature <name>
```

|역할 서비스 또는 기능|이름|
|---|---|
|DFS 복제|`FS-DFS-Replication`|
|DFS 관리 도구|`RSAT-DFS-Mgmt-Con`|

예를 들어 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치하려면 다음을 입력합니다.

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

DFS 복제 및 원격 서버 관리 도구 기능의 분산 파일 시스템 도구 부분을 설치하려면 다음을 입력합니다.

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>참고 항목

- [DFS 네임스페이스 및 DFS 복제 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [검사 목록: DFS 복제 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [검사 목록: DFS 복제 관리](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [DFS 복제 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS 복제 관리](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS 복제 문제 해결](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
