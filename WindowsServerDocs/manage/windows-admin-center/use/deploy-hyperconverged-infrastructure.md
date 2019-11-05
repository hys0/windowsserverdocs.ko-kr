---
title: Windows 관리 센터를 사용 하 여 하이퍼 수렴 형 인프라 배포
ms.topic: article
author: cosmosdarwin
ms.author: cosdar
ms.prod: windows-server
ms.technology: manage
ms.date: 11/04/2019
ms.openlocfilehash: 62bf21dd0afcb99aa77cff8a733e80fc4cffe2fb
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73587233"
---
# <a name="deploy-hyperconverged-infrastructure-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 하이퍼 수렴 형 인프라 배포

> 적용 대상: Windows 관리 센터, Windows 관리 센터 미리 보기

Windows 관리 센터 [버전 1910](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) 이상을 사용 하 여 두 개 이상의 적합 한 windows server를 사용 하 여 하이퍼 수렴 형 인프라를 배포할 수 있습니다. 이 새로운 기능을 사용 하면 기능을 설치 하 고, 네트워킹을 구성 하 고, 클러스터를 만들고, 선택 하는 경우 스토리지 공간 다이렉트 및/또는 SDN (소프트웨어 정의 네트워킹)을 배포 하는 과정을 안내 하는 다단계 워크플로의 형태를 사용할 수 있습니다.

![클러스터 만들기 워크플로의 스크린샷](../media/deploy-hyperconverged-infrastructure/deployment-workflow-screenshot.png)

  > [!Important]
  > 이 기능은 활성 개발 중입니다. 미리 보기에서 사용할 수 있으므로 조기에 시험해 보고 사용자 의견을 공유할 수 있습니다.

## <a name="preview-the-workflow"></a>워크플로 미리 보기

### <a name="1-prerequisites"></a>1. 필수 구성 요소

Windows 관리 센터의 클러스터 만들기 워크플로는 운영 체제 미 설치 운영 체제 설치를 수행 하지 않으므로 먼저 각 서버에 Windows Server를 설치 해야 합니다. 지원 되는 버전은 Windows Server 2016, Windows Server 2019 및 Windows Server Insider Preview입니다. 또한 워크플로를 시작 하기 전에 Windows 관리 센터가 실행 되는 위치와 동일한 Active Directory 도메인에 각 서버를 조인 해야 합니다.

### <a name="2-install-windows-admin-center"></a>2. Windows 관리 센터 설치
 
지침에 따라 Windows 관리 센터의 최신 버전을 다운로드 하 여 [설치](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) 합니다.

### <a name="3-install-the-cluster-creation-extension"></a>3. 클러스터 생성 확장을 설치 합니다.

클러스터 만들기 워크플로는 Windows 관리 센터 확장 피드를 통해 배달 및 업데이트 됩니다. 이는 미리 보기 단계에서 피드백을 해결 하 고 더 빠르게 개선할 수 있도록 합니다.

확장을 설치 하려면 Windows 관리 센터를 시작 하 고 다음을 수행 합니다.

1.  오른쪽 위에서 설정 아이콘을 선택 합니다.
2.  확장으로 이동
3.  클러스터 생성 확장 프로그램 찾기
4.  설치 선택

![클러스터 생성 확장을 설치 하는 네 단계의 스크린샷](../media/deploy-hyperconverged-infrastructure/how-to-install.png)

설치 되 면 왼쪽 위의 드롭다운에서 클러스터 생성 확장을 선택 합니다.

![클러스터 생성 확장 프로그램을 시작 하는 스크린샷](../media/deploy-hyperconverged-infrastructure/how-to-launch.png)

## <a name="limitations-of-the-preview-release"></a>Preview 릴리스의 제한 사항

클러스터 만들기 워크플로는 활성 개발 중입니다. 즉, 완료 되지 않습니다.

현재 미리 보기 릴리스에 대 한 몇 가지 제한 사항은 다음과 같습니다.

1.  **도메인 요구 사항.** 현재 워크플로를 사용 하려면 추가 하는 모든 서버가 Windows 관리 센터를 실행 하는 위치와 동일한 Active Directory 도메인에 이미 가입 되어 있어야 합니다.
2.  **스크립트를 표시 합니다.** 현재 미리 보기 릴리스에서는 Windows 관리 센터의 스크립트 기능 표시를 사용 하 여 워크플로가 실행 되는 스크립트를 볼 수 없으며, 마지막에 발생 한 모든 항목에 대 한 전체 보고서를 다운로드할 수 없습니다. 이는 대부분의 사용자에 게 중요 합니다. 그 동안에는 아래에 제공 된 cmdlet을 사용 하 여 무슨 일이 발생 [하는지 확인](#see-whats-happening)합니다.
3.  **다시 시작 하거나 다시 시작 합니다.** 워크플로를 통해 걸리거나를 종료할 수 있지만, 현재 미리 보기 릴리스는 중단 된 위치에서 다시 시작 하는 작업을 처리 하지 않으며 시작 하기 전에 완전히 정리할 수 없습니다. 테스트를 위해 동일한 서버에 반복적으로 배포 하려는 경우 아래 제공 된 cmdlet을 사용 하 여 [실행을 취소 하 고 다시 시작](#undo-and-start-over)합니다.
4.  **RDMA (원격 직접 메모리 액세스)** 현재 미리 보기 릴리스에서는 RDMA 네트워킹을 사용 하도록 설정할 수 없습니다 .이는 하이퍼 수렴 형 인프라에서 일반적으로 사용 됩니다. 지금은 RDMA를 사용 하도록 설정 하지 않고 워크플로를 완료 한 후 다른 도구를 사용 하 여 수행 하는 것과 같은 방법으로 RDMA를 사용 하도록 설정 합니다.

이러한 제한 사항을 해결 하는 것 외에도 향후 릴리스에 추가 될 수 있는 수많은 잠재적 기능이 있습니다. Windows 업데이트 적용, 클러스터 쿼럼에 대 한 미러링 모니터 서버 구성, 가상 컴퓨터 가져오기 등의 작업을 수행 합니다. 원하는 기능의 우선 순위를 지정 하려면 아래 설명 된 대로 [사용자 의견을 공유](#feedback) 하세요.

## <a name="see-whats-happening"></a>상황 확인

이러한 Windows PowerShell cmdlet을 사용 하 여 워크플로를 수행 하는 작업을 확인 합니다.

설치 된 Windows 기능을 확인 하려면 `Get-WindowsFeature` cmdlet을 사용 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

```PowerShell
Get-WindowsFeature "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "BitLocker"
```

![PowerShell 출력의 스크린샷](../media/deploy-hyperconverged-infrastructure/script-out-1.png)

  > [!Note]
  > 설치 되는 기능은 선택한 클러스터 유형에 따라 달라 집니다.

네트워크 어댑터 및 해당 속성 (예: 이름, IPv4 주소, VLAN ID)을 보려면 다음을 수행 합니다.

```PowerShell
Get-NetAdapter | Where Status -Eq "Up" | Sort InterfaceAlias | Format-Table Name, InterfaceDescription, Status, LinkSpeed, VLANID, MacAddress
Get-NetAdapter | Where Status -Eq "Up" | Get-NetIPAddress -AddressFamily IPv4 -ErrorAction SilentlyContinue | Sort InterfaceAlias | Format-Table InterfaceAlias, IPAddress, PrefixLength
```

![PowerShell 출력의 스크린샷](../media/deploy-hyperconverged-infrastructure/script-out-2.png)

Hyper-v 가상 스위치와 실제 네트워크 어댑터를 팀으로 구성 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

```PowerShell
Get-VMSwitch
Get-VMSwitchTeam
```

![PowerShell 출력의 스크린샷](../media/deploy-hyperconverged-infrastructure/script-out-3.png)

호스트 가상 네트워크 어댑터 (있는 경우)를 보려면 다음을 실행 합니다.

```PowerShell
Get-VMNetworkAdapter -ManagementOS | Format-Table Name, IsManagementOS, SwitchName
Get-VMNetworkAdapterTeamMapping -ManagementOS | Format-Table NetAdapterName, ParentAdapter
```

![PowerShell 출력의 스크린샷](../media/deploy-hyperconverged-infrastructure/script-out-4.png)

현재 장애 조치 (failover) 클러스터와 해당 구성원 노드를 보려면 다음을 실행 합니다.

```PowerShell
Get-Cluster
Get-ClusterNode
```

![PowerShell 출력의 스크린샷](../media/deploy-hyperconverged-infrastructure/script-out-5.png)

스토리지 공간 다이렉트를 사용할 수 있는지 여부와 자동으로 만들어진 기본 저장소 풀을 확인 하려면 다음을 수행 합니다.

```PowerShell
Get-ClusterStorageSpacesDirect
Get-StoragePool -IsPrimordial $False
```

![PowerShell 출력의 스크린샷](../media/deploy-hyperconverged-infrastructure/script-out-6.png)

## <a name="undo-and-start-over"></a>실행 취소 및 다시 시작

이러한 Windows PowerShell cmdlet을 사용 하 여 워크플로의 변경 내용을 취소 하 고 다시 시작 합니다.

### <a name="remove-virtual-machines-or-other-clustered-resources"></a>가상 컴퓨터 또는 다른 클러스터 된 리소스 제거

가상 컴퓨터 또는 다른 클러스터 된 리소스 (예: 소프트웨어 정의 네트워킹의 네트워크 컨트롤러)를 만든 경우 해당 가상 컴퓨터를 먼저 제거 합니다.

예를 들어 이름으로 리소스를 제거 하려면 다음을 사용 합니다.

```PowerShell
Get-ClusterResource -Name "<NAME>" | Remove-ClusterResource
```

### <a name="undo-the-storage-steps"></a>저장소 단계를 실행 취소 합니다.

스토리지 공간 다이렉트를 사용 하도록 설정한 경우 다음 스크립트를 사용 하 여 사용 하지 않도록 설정 합니다.

> [!Warning]
> 이러한 cmdlet은 스토리지 공간 다이렉트 볼륨의 모든 데이터를 영구적으로 삭제 합니다. 이 작업은 취소할 수 없습니다.

```PowerShell
Get-VirtualDisk | Remove-VirtualDisk
Get-StoragePool -IsPrimordial $False | Remove-StoragePool
Disable-ClusterS2D
```

### <a name="undo-the-clustering-steps"></a>클러스터링 단계 실행 취소

클러스터를 만든 경우이 cmdlet을 사용 하 여 제거 합니다.

```PowerShell
Remove-Cluster -CleanUpAD
```

클러스터 유효성 검사 보고서도 제거 하려면 클러스터의 일부인 모든 서버에서이 cmdlet을 실행 합니다.

```PowerShell
Get-ChildItem C:\Windows\cluster\Reports\ | Remove-Item
```

### <a name="undo-the-networking-steps"></a>네트워킹 단계를 실행 취소 합니다.

클러스터의 일부인 모든 서버에서 이러한 cmdlet을 실행 합니다.

Hyper-v 가상 스위치를 만든 경우:

```PowerShell
Get-VMSwitch | Remove-VMSwitch
```

> [!Note]
> `Remove-VMSwitch` cmdlet은 가상 어댑터를 자동으로 제거 하 고 실제 어댑터의 스위치 포함 팀을 실행 취소 합니다.

이름, IPv4 주소 및 VLAN ID와 같은 네트워크 어댑터 속성을 수정한 경우:

> [!Warning]
> 이러한 cmdlet은 네트워크 어댑터 이름 및 IP 주소를 제거 합니다. 아래 스크립트에서 제외 된 관리용 어댑터와 같이 나중에 연결 하는 데 필요한 정보가 있는지 확인 합니다. 또한 Windows의 어댑터 이름 뿐만 아니라 MAC 주소와 같은 실제 속성을 기준으로 서버를 연결 하는 방법을 알고 있어야 합니다.

```PowerShell
Get-NetAdapter | Where Name -Ne "Management" | Rename-NetAdapter -NewName $(Get-Random)
Get-NetAdapter | Where Name -Ne "Management" | Get-NetIPAddress -ErrorAction SilentlyContinue | Where AddressFamily -Eq IPv4 | Remove-NetIPAddress
Get-NetAdapter | Where Name -Ne "Management" | Set-NetAdapter -VlanID 0
```

이제 워크플로를 시작할 준비가 되었습니다.

## <a name="feedback"></a>Feedback

이 미리 보기 릴리스는 모든 사용자 의견을 제공 합니다. 팀에 연결할 수 있는 몇 가지 방법은 다음과 같습니다.

- [UserVoice의 기능 요청 제출 및 투표](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft 기술 커뮤니티의 Windows 관리 센터 포럼 참여](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- 전자 메일 hci [at] microsoft.com
- [@servermgmt](https://twitter.com/servermgmt) 트 윗

## <a name="report-an-issue"></a>문제 보고

위에 나열 된 채널을 사용 하 여 클러스터 만들기 워크플로와 관련 된 문제를 보고 합니다.

가능 하면 문제를 신속 하 게 재현 하 고 해결 하는 데 도움이 되도록 다음 정보를 포함 합니다.

- 선택한 클러스터의 유형 (예: *"Hyperconverged 형"* )
- 문제가 발생 한 단계 (예: *"3.2 클러스터 만들기"* )
- 클러스터 생성 확장의 버전입니다. **설정** > **확장** > **설치 된 확장** 으로 이동 하 여 **버전** 열을 확인 합니다 (예: *"1.0.30"* ).
- 화면에 있든, 브라우저 콘솔에 있든, **F12**키를 눌러 열 수 있는 오류 메시지입니다.
- 사용자 환경에 대 한 기타 관련 정보 

## <a name="see-also"></a>참고 항목

- [Hello, Windows 관리 센터](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)
- [스토리지 공간 다이렉트 배포](https://docs.microsoft.com/windows-server/storage/storage-spaces/deploy-storage-spaces-direct)
