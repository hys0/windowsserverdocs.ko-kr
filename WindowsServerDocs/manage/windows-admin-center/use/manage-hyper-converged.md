---
title: Windows 관리 센터를 사용 하 여 하이퍼 수렴 형 인프라 관리
description: Windows 관리 센터 (Project Honolulu)를 사용 하 여 하이퍼 수렴 형 인프라 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d692251e1ba0fef43e4eeee6f259f26f4347f3c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356880"
---
# <a name="manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 하이퍼 수렴 형 인프라 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## <a name="what-is-hyper-converged-infrastructure"></a>하이퍼 수렴 형 인프라 란?

하이퍼 수렴 형 인프라는 소프트웨어 정의 계산, 저장소 및 네트워킹을 하나의 클러스터로 통합 하 여 고성능, 비용 효율적이 고 쉽게 확장할 수 있는 가상화를 제공 합니다. 이 기능은 [스토리지 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview), [소프트웨어 정의 네트워킹](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking) 및 [hyper-v](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)와 함께 Windows Server 2016에서 도입 되었습니다.

> [!Tip]
> 하이퍼 수렴 형 인프라를 획득 하 고 싶으십니까? Microsoft는 파트너의 이러한 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd) 솔루션을 권장 합니다. 이러한 기능은 호환성 및 안정성을 보장 하기 위해 참조 아키텍처에 대해 디자인, 조합 및 유효성 검사를 수행 하므로 신속 하 게 시작 하 고 실행할 수 있습니다.

> [!IMPORTANT]
> 이 문서에서 설명 하는 일부 기능은 Windows 관리 센터 미리 보기 에서만 사용할 수 있습니다. [이 버전을 가져올 어떻게 할까요? 있나요?](http://aka.ms/windowsadmincenter)

## <a name="what-is-windows-admin-center"></a>Windows Admin Center란

[Windows 관리 센터](../understand/windows-admin-center.md) 는 windows Server를 위한 차세대 관리 도구로 서, 서버 관리자와 같은 기존의 후속 "도구"입니다. 무료 이며 인터넷 연결 없이 설치 하 고 사용할 수 있습니다. Windows 관리 센터를 사용 하 여 Windows Server 2016 또는 Windows Server 2019를 실행 하는 하이퍼 수렴 형 인프라를 관리 하 고 모니터링할 수 있습니다.

![하이퍼 수렴 형 클러스터 대시보드](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## <a name="key-features"></a>주요 기능

하이퍼 수렴 형 인프라의 Windows 관리 센터에 대 한 주요 사항은 다음과 같습니다.

- **계산, 저장소 및 빠른 네트워킹을 위한 통일 된 단일 창** 한 가지 용도, 일관 되 고 상호 연결 된 환경에서 가상 머신, 호스트 서버, 볼륨, 드라이브 등을 확인 하세요.
- **저장소 공간 및 Hyper-v 가상 머신을 만들고 관리 합니다.** 볼륨 만들기, 열기, 크기 조정 및 삭제를 위한 매우 간단한 워크플로 그리고 가상 컴퓨터를 만들고, 시작 하 고, 연결 하 고, 이동 합니다. 훨씬 더 많은 것이 있습니다.
- **강력한 클러스터 전체 모니터링.** 대시보드는 클러스터의 모든 서버에서 메모리와 CPU 사용량, 저장소 용량, IOPS, 처리량 및 대기 시간을 실시간으로 그래프로, 무언가가 적절 하지 않은 경우 명확한 경고를 포함 합니다.
- **SDN (소프트웨어 정의 네트워킹) 지원.** 가상 네트워크, 서브넷을 관리 및 모니터링 하 고 가상 컴퓨터를 가상 네트워크에 연결 하 고 SDN 인프라를 모니터링 합니다.

하이퍼 수렴 형 인프라의 Windows 관리 센터는 Microsoft에서 적극적으로 개발 하 고 있습니다. 기존 기능을 개선 하 고 새로운 기능을 추가 하는 빈번한 업데이트를 받습니다.

## <a name="before-you-start"></a>시작하기 전 주의 사항

Windows 관리 센터에서 클러스터를 하이퍼 수렴 형 인프라로 관리 하려면 Windows Server 2016 또는 Windows Server 2019를 실행 하 고 Hyper-v를 사용 하도록 설정 하 고 스토리지 공간 다이렉트를 사용 하도록 설정 해야 합니다. 필요에 따라 Windows 관리 센터를 통해 소프트웨어 정의 네트워킹을 사용 하도록 설정 하 고 관리할 수도 있습니다.

> [!Tip]
> Windows 관리 센터는 Windows Server 2012 이상에서 사용할 수 있는 모든 작업을 지 원하는 모든 클러스터에 대 한 범용 관리 환경을 제공 합니다. 이 소리가 더 적합 한 경우 Windows 관리 센터에 클러스터를 추가할 때 **하이퍼 수렴 형 클러스터**대신 [**장애 조치 (Failover) 클러스터**](manage-failover-clusters.md) 를 선택 합니다.

### <a name="prepare-your-windows-server-2016-cluster-for-windows-admin-center"></a>Windows 관리 센터에 대 한 Windows Server 2016 클러스터 준비

하이퍼 수렴 형 인프라를 위한 windows 관리 센터는 Windows Server 2016이 출시 된 후 추가 된 관리 Api에 따라 달라 집니다. Windows 관리 센터를 사용 하 여 Windows Server 2016 클러스터를 관리 하려면 먼저 다음 두 단계를 수행 해야 합니다.

1. 클러스터의 모든 서버에서 [KB4103723 (Windows server 2016 용 2018-05 누적 업데이트)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723) 이상을 설치 했는지 확인 합니다. 이 업데이트를 다운로드 하 고 설치 하려면 **설정** > **업데이트 & 보안** > **Windows 업데이트** 로 이동 하 고 **Microsoft 업데이트에서 온라인 업데이트 확인**을 선택 합니다.
2. 클러스터에서 관리자 권한으로 다음 PowerShell cmdlet을 실행 합니다.

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> 이 cmdlet은 클러스터의 모든 서버에서 한 번만 실행 해야 합니다. Windows PowerShell에서 로컬로 실행 하거나 CredSSP (Credential Security Service Provider)를 사용 하 여 원격으로 실행할 수 있습니다. 구성에 따라 Windows 관리 센터 내에서이 cmdlet을 실행 하지 못할 수 있습니다.

### <a name="prepare-your-windows-server-2019-cluster-for-windows-admin-center"></a>Windows 관리 센터에 대 한 Windows Server 2019 클러스터 준비

클러스터가 Windows Server 2019를 실행 하는 경우 위의 단계는 필요 하지 않습니다. 다음 섹션에 설명 된 대로 Windows 관리 센터에 클러스터를 추가 하기만 하면 좋습니다.

### <a name="configure-software-defined-networking-optional"></a>소프트웨어 정의 네트워킹 구성 (선택 사항) ###

다음 단계로 SDN (소프트웨어 방식 네트워킹)을 사용 하도록 Windows Server 2016 또는 2019를 실행 하는 하이퍼 수렴 형 인프라를 구성할 수 있습니다.

1. 하이퍼 수렴 형 인프라 호스트에 설치한 os와 동일한 OS의 VHD를 준비 합니다. 이 VHD는 모든 NC/SLB/GW Vm에 사용 됩니다.
2. SDN Express에서 [https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress)모든 폴더와 파일을 다운로드 합니다.
3. 배포 콘솔을 사용 하 여 다른 VM을 준비 합니다. 이 VM은 SDN 호스트에 액세스할 수 있어야 합니다. 또한 VM에는 RSAT Hyper-v 도구가 설치 되어 있어야 합니다.
4. SDN Express에 대해 다운로드 한 모든 항목을 배포 콘솔 VM에 복사 합니다. 및은이 **Sdnexpress** 폴더를 공유 합니다. 구성 파일 줄 8에서 정의한 대로 모든 호스트가 **Sdnexpress** 공유 폴더에 액세스할 수 있는지 확인 합니다.
   ```
    \\$env:Computername\SDNExpress
   ```
5. 배포 콘솔 VM의 **Sdnexpress** 폴더 아래에 있는 **IMAGES** 폴더에 OS의 VHD를 복사 합니다.
6. 사용자 환경 설정으로 SDN Express 구성을 수정 합니다. 사용자 환경 정보에 따라 SDN Express 구성을 수정한 후 다음 두 단계를 완료 합니다.
7. 관리자 권한으로 PowerShell을 실행 하 여 SDN을 배포 합니다.

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

배포에는 약 30 ~ 45 분이 소요 됩니다.

## <a name="get-started"></a>시작

하이퍼 수렴 형 인프라를 배포한 후에는 Windows 관리 센터를 사용 하 여 관리할 수 있습니다.

### <a name="install-windows-admin-center"></a>Windows Admin Center 설치

아직 설치 하지 않은 경우 Windows 관리 센터를 다운로드 하 여 설치 합니다. 가장 빠르게 시작 하 고 실행 하는 방법은 Windows 10 컴퓨터에 설치 하 고 서버를 원격으로 관리 하는 것입니다. 이 작업은 5 분 이내에 수행 됩니다. [지금 다운로드](https://aka.ms/windowsadmincenter) 하거나 [다른 설치 옵션에 대해 자세히 알아보세요](../deploy/install.md).

### <a name="add-hyper-converged-cluster"></a>하이퍼 수렴 형 클러스터 추가

Windows 관리 센터에 클러스터를 추가 하려면 다음을 수행 합니다.

1. 모든 연결에서 **+ 추가** 를 클릭 합니다.
2. **하이퍼 수렴 형 클러스터 연결**을 추가 하도록 선택 합니다.
3. 클러스터의 이름을 입력 하 고, 메시지가 표시 되 면 사용할 자격 증명을 입력 합니다.
4. **추가** 를 클릭 하 여 완료 합니다.

클러스터는 연결 목록에 추가 됩니다. 대시보드를 시작 하려면 클릭 합니다.

![하이퍼 수렴 형 클러스터 연결 추가](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### <a name="add-sdn-enabled-hyper-converged-cluster-windows-admin-center-preview"></a>SDN 사용 하이퍼 수렴 형 클러스터 추가 (Windows 관리 센터 미리 보기)

최신 Windows 관리 센터 미리 보기는 하이퍼 수렴 형 인프라를 위한 소프트웨어 정의 네트워킹 관리를 지원 합니다. 하이퍼 수렴 형 클러스터 연결에 네트워크 컨트롤러 REST URI를 추가 하 여 하이퍼 수렴 형 클러스터 관리자를 사용 하 여 SDN 리소스를 관리 하 고 SDN 인프라를 모니터링할 수 있습니다.

1. 모든 연결에서 **+ 추가** 를 클릭 합니다.
2. **하이퍼 수렴 형 클러스터 연결**을 추가 하도록 선택 합니다.
3. 클러스터의 이름을 입력 하 고, 메시지가 표시 되 면 사용할 자격 증명을 입력 합니다.
4. **네트워크 컨트롤러 구성** 을 선택 하 여 계속 합니다.
5. **네트워크 컨트롤러 URI** 를 입력 하 고 **유효성 검사**를 클릭 합니다.
6. **추가** 를 클릭 하 여 완료 합니다.

클러스터는 연결 목록에 추가 됩니다. 대시보드를 시작 하려면 클릭 합니다.

![SDN 사용 하이퍼-수렴 형 클러스터 연결 추가](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> Northbound 통신용 Kerberos 인증이 포함 된 SDN 환경은 현재 지원 되지 않습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="are-there-differences-between-managing-windows-server-2016-and-windows-server-2019"></a>Windows Server 2016 및 Windows Server 2019를 관리 하는 데 차이가 있나요?

예. 하이퍼 수렴 형 인프라를 위한 windows 관리 센터는 Windows Server 2016 및 Windows Server 2019의 환경을 개선 하는 빈번한 업데이트를 받습니다. 그러나 일부 새로운 기능은 Windows Server 2019에만 사용할 수 있습니다. 예를 들어, 중복 제거 및 압축을 위한 토글 스위치를 사용할 수 있습니다.

### <a name="can-i-use-windows-admin-center-to-manage-storage-spaces-direct-for-other-use-cases-not-hyper-converged-such-as-converged-scale-out-file-server-sofs-or-microsoft-sql-server"></a>Windows 관리 센터를 사용 하 여 수렴 형 스케일 아웃 파일 서버 (SoFS) 또는 Microsoft SQL Server 같은 다른 사용 사례 (하이퍼 수렴 안 함)에 대 한 스토리지 공간 다이렉트를 관리할 수 있나요?

하이퍼 수렴 형 인프라를 위한 Windows 관리 센터에서는 특히 스토리지 공간 다이렉트의 다른 사용 사례에 대 한 관리 또는 모니터링 옵션을 제공 하지 않습니다. 예를 들어 파일 공유를 만들 수 없습니다. 그러나 볼륨 만들기 또는 드라이브 교체와 같은 대시보드 및 핵심 기능은 스토리지 공간 다이렉트 클러스터에 대해 작동 합니다.

### <a name="whats-the-difference-between-a-failover-cluster-and-a-hyper-converged-cluster"></a>장애 조치 (Failover) 클러스터와 하이퍼 수렴 형 클러스터 간의 차이점은 무엇 인가요?

일반적으로 "하이퍼 수렴 형" 이라는 용어는 동일한 클러스터 된 서버에서 Hyper-v를 실행 하 고 스토리지 공간 다이렉트 하 여 계산 및 저장소 리소스를 가상화 하는 것을 의미 합니다. Windows 관리 센터의 컨텍스트에서 연결 목록에서 **+ 추가** 를 클릭 하면 **장애 조치 (Failover) 클러스터 연결** 또는 **하이퍼 수렴 형 클러스터 연결**중에서 선택할 수 있습니다.

- **장애 조치 (Failover) 클러스터 연결은** 장애 조치(Failover) 클러스터 관리자 desktop 응용 프로그램의 후속 작업입니다. Microsoft SQL Server를 포함 하 여 모든 워크 로드를 지 원하는 모든 클러스터에 대 한 친숙 한 범용 관리 환경을 제공 합니다. Windows Server 2012 이상 버전에서 사용할 수 있습니다.

- **하이퍼 수렴 형 클러스터 연결은** 스토리지 공간 다이렉트 및 hyper-v에 맞게 조정 된 새로운 환경입니다. 대시보드 기능과 차트 및 모니터링 알림을 강조합니다. Windows Server 2016 및 Windows Server 2019에서 사용할 수 있습니다.

### <a name="why-do-i-need-the-latest-cumulative-update-for-windows-server-2016"></a>Windows Server 2016에 대 한 최신 누적 업데이트가 필요한 이유는 무엇 인가요?

하이퍼 수렴 형 인프라를 위한 windows 관리 센터는 Windows Server 2016이 출시 된 이후 개발 된 관리 Api에 따라 달라 집니다. 이러한 Api는 2018-05 2018 년 5 월 8 일에 제공 되는 [누적 2016 업데이트 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)에 추가 되었습니다.

### <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Windows Admin Center를 사용하는 비용은 얼마입니까?

Windows Admin Center는 Windows 이외에 추가 비용이 들지 않습니다.

유효한 Windows Server 또는 Windows 10 라이선스를 가지고 추가 비용 없이 Windows Admin Center(별도 다운로드를 통해 사용 가능)를 사용할 수 있습니다. Windows 추가 EULA에 의해 사용권이 부여됩니다.

### <a name="does-windows-admin-center-require-system-center"></a>Windows Admin Center에 System Center가 필요합니까?

아니요.

### <a name="does-it-require-an-internet-connection"></a>인터넷 연결이 필요 한가요?

아니요.

Windows 관리 센터는 Microsoft Azure 클라우드와 강력 하 고 편리한 통합 기능을 제공 하지만 하이퍼 수렴 형 인프라의 핵심 관리 및 모니터링 환경은 완전히 온-프레미스입니다. 인터넷 연결 없이 설치 하 고 사용할 수 있습니다.

## <a name="things-to-try"></a>시도할 작업

처음 시작 하는 경우 하이퍼 수렴 형 인프라의 Windows 관리 센터를 구성 하 고 작동 하는 방법을 배우는 데 도움이 되는 간략 한 자습서는 다음과 같습니다. 좋은 judgement을 연습 하 고 프로덕션 환경에 주의 하세요. 이러한 비디오는 windows 관리 센터 버전 1804 및 Windows Server 2019의 Insider Preview 빌드를 사용 하 여 기록 되었습니다.

### <a name="manage-storage-spaces-direct-volumes"></a>스토리지 공간 다이렉트 볼륨 관리

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">3 방향 미러 볼륨을 만드는 방법</a></li>
               <li>(1:17) <a href="https://youtu.be/R72QHudqWpE">미러 가속 패리티 볼륨을 만드는 방법</a></li>
               <li>(1:02) <a href="https://youtu.be/j59z7ulohs4">볼륨을 열고 파일을 추가 하는 방법</a></li>
               <li>(0:51) <a href="https://youtu.be/PRibTacyKko">중복 제거 및 압축을 켜는 방법</a></li>
               <li>(0:47) <a href="https://youtu.be/hqyBzipBoTI">볼륨을 확장 하는 방법</a></li>
               <li>(0:26) <a href="https://youtu.be/DbjF8r2F6Jo">볼륨을 삭제 하는 방법</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>볼륨 만들기, 3 방향 미러</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>볼륨 만들기, 미러 가속 패리티</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>볼륨을 열고 파일 추가</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>중복 제거 및 압축 설정</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>볼륨 확장</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>볼륨 삭제</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### <a name="create-a-new-virtual-machine"></a>새 가상 컴퓨터 만들기

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 맨 위에서 **인벤토리** 탭을 선택한 다음 **새로** 만들기를 클릭 하 여 새 가상 컴퓨터를 만듭니다.
3. 가상 컴퓨터 이름을 입력 하 고 1 세대와 2 세대 가상 컴퓨터를 선택 합니다.
4. 그런 다음 uou는 처음에 가상 머신을 만들거나 권장 호스트를 사용할 호스트를 선택할 수 있습니다.
5. 가상 컴퓨터 파일의 경로를 선택 하십시오. 드롭다운 목록에서 볼륨을 선택 하거나 **찾아보기** 를 클릭 하 여 폴더 선택기를 사용 하 여 폴더를 선택 합니다. 가상 컴퓨터 구성 파일 및 가상 하드 디스크 파일은 선택한 볼륨 또는 경로의 `\Hyper-V\[virtual machine name]` 경로 아래에 있는 단일 폴더에 저장 됩니다.
6. 가상 프로세서 수를 선택 하 고, 중첩 된 가상화를 사용 하도록 설정할지 여부를 선택 하 고, 메모리 설정, 네트워크 어댑터, 가상 하드 디스크를 구성 하 고, .iso 이미지 파일이 나 네트워크에서 운영 체제를 설치할지 여부를 선택 합니다.
7. **만들기**를 클릭하여 가상 컴퓨터를 만듭니다.
8. 가상 컴퓨터를 만들고 가상 컴퓨터 목록에 표시 되 면 가상 컴퓨터를 시작할 수 있습니다.
9. 가상 컴퓨터가 시작 되 면 VMConnect를 통해 가상 컴퓨터의 콘솔에 연결 하 여 운영 체제를 설치할 수 있습니다. 목록에서 가상 컴퓨터를 선택 하 고 **추가** > **연결** 을 클릭 하 여 .rdp 파일을 다운로드 합니다. 원격 데스크톱 연결 앱에서 .rdp 파일을 엽니다. 가상 컴퓨터의 콘솔에 연결 하는 중 이므로 Hyper-v 호스트의 관리자 자격 증명을 입력 해야 합니다.

[Windows 관리 센터를 사용 하 여 가상 머신 관리에 대해 자세히 알아보세요](manage-virtual-machines.md).

### <a name="pause-and-safely-restart-a-server"></a>서버 일시 중지 및 안전 하 게 다시 시작

1. **대시보드의**왼쪽 탐색 영역에서 **서버** 를 선택 하거나 대시보드의 오른쪽 아래에 있는 타일에서 **서버 > 보기** 링크를 클릭 합니다.
2. 위쪽의 **요약** 에서 **인벤토리** 탭으로 전환 합니다.
3. 서버 이름을 클릭 하 여 **서버 세부 정보** 페이지를 엽니다.
4. **유지 관리를 위해 서버 일시 중지를**클릭 합니다. 계속 하는 것이 안전 하면 가상 컴퓨터를 클러스터의 다른 서버로 이동 합니다. 이 경우 서버는 상태 드레이닝을 갖습니다. 원하는 경우 **virtual machines > Inventory** 페이지에서 가상 컴퓨터 이동을 볼 수 있습니다. 여기서 호스트 서버는 표에서 명확 하 게 표시 됩니다. 모든 가상 머신이 이동 하면 서버 상태가 **일시 중지**됩니다.
5. **서버 관리** 를 클릭 하 여 Windows 관리 센터의 모든 서버 관리 도구에 액세스 합니다.
6. **다시 시작**을 클릭 한 다음 **예**를 클릭 합니다. 연결 목록으로 돌아갑니다.
7. **대시보드**로 돌아가서 종료 되는 동안 서버에 빨간색으로 색이 지정 됩니다.
8. 백업 된 후에는 **서버** 페이지로 다시 이동 하 고, **유지 관리에서 서버 다시 시작** 을 클릭 하 여 서버 상태를 간단 하 게 다시 설정 합니다. 시간에 가상 컴퓨터는 다시 이동 합니다. 사용자 작업이 필요 하지 않습니다.

### <a name="replace-a-failed-drive"></a>실패 한 드라이브 바꾸기

1. 드라이브에 오류가 발생 하면 **대시보드의**왼쪽 상단 **경고** 영역에 경고가 표시 됩니다.
2. 왼쪽의 탐색에서 **드라이브** 를 선택 하거나 오른쪽 아래 모서리의 타일에서 드라이브 **> 보기** 링크를 클릭 하 여 드라이브를 찾아보고 자신의 상태를 확인할 수도 있습니다. **인벤토리** 탭에서 그리드는 정렬, 그룹화 및 키워드 검색을 지원 합니다.
3. **대시보드에서**경고를 클릭 하 여 드라이브의 실제 위치와 같은 세부 정보를 확인 합니다.
4. 자세히 **알아보려면 드라이브 세부 정보 페이지** 의 **드라이브로 이동** 바로 가기를 클릭 합니다.
5. 하드웨어에서 지 원하는 경우 **라이트 켜기/끄기를** 클릭 하 여 드라이브의 표시기 조명을 제어할 수 있습니다.
6. 스토리지 공간 다이렉트 자동으로 실패 한 드라이브를 받아볼 및 evacuates 합니다. 이 문제가 발생 하면 드라이브 상태는 사용 중지 되며, 저장소 용량 표시줄이 비어 있습니다.
7. 실패 한 드라이브를 제거 하 고 교체를 삽입 합니다.
8. **드라이브 > 인벤토리에**는 새 드라이브가 표시 됩니다. 시간이 되 면 경고가 지워집니다. 볼륨은 정상 상태로 복구 되 고, 저장소는 새 드라이브에 균형을 다시 조정 합니다. 사용자 작업은 필요 하지 않습니다.

### <a name="manage-virtual-networks-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>가상 네트워크 관리 (Windows 관리 센터 미리 보기를 사용 하 여 SDN 지원 HCI 클러스터)

1. 왼쪽의 탐색 영역에서 **가상 네트워크** 를 선택 합니다.
2. **새로** 만들기를 클릭 하 여 새 가상 네트워크 및 서브넷을 만들거나 기존 가상 네트워크를 선택 하 고 **설정** 을 클릭 하 여 구성을 수정 합니다.
3. 가상 네트워크 서브넷에 적용 된 액세스 제어 목록과 가상 네트워크 서브넷에 대 한 VM 연결을 보려면 기존 가상 네트워크를 클릭 합니다.

![가상 네트워크 관리](../media/manage-hyper-converged/manage-virtual-networks.png)

### <a name="connect-a-virtual-machine-to-a-virtual-network-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>가상 컴퓨터를 가상 네트워크에 연결 (Windows 관리 센터 미리 보기를 사용 하 여 SDN 지원 HCI 클러스터)

1. 왼쪽의 탐색 영역에서 **Virtual Machines** 를 선택 합니다.
2. 기존 가상 머신을 선택 > **설정** > 클릭 하 여 **설정**에서 **네트워크** 탭을 엽니다.
3. 가상 컴퓨터를 가상 네트워크에 연결 하려면 **Virtual Network** 및 **가상 서브넷** 필드를 구성 합니다.

가상 컴퓨터를 만들 때 가상 네트워크를 구성할 수도 있습니다.

![가상 컴퓨터를 가상 네트워크에 연결](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### <a name="monitor-software-defined-networking-infrastructure-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>소프트웨어 정의 네트워킹 인프라 모니터링 (Windows 관리 센터 미리 보기를 사용 하 여 SDN 지원 HCI 클러스터)

1. 왼쪽 탐색 영역에서 **SDN 모니터링** 을 선택 합니다.
2. 네트워크 컨트롤러, 소프트웨어 Load Balancer, 가상 게이트웨이의 상태에 대 한 자세한 정보를 보고 가상 게이트웨이 풀, 공용 및 개인 IP 풀 사용량 및 SDN 호스트 상태를 모니터링 합니다.

![SDN 인프라 모니터링](../media/manage-hyper-converged/sdn-monitoring.png)

## <a name="feedback"></a>사용자 의견

사용자 의견에 대 한 모든 것입니다. 자주 업데이트 하는 가장 중요 한 혜택은 작업 및 개선 해야 할 작업을 파악 하는 것입니다. 다음은 사용자가 생각 하는 내용을 알려 주는 몇 가지 방법입니다.

- [UserVoice의 기능 요청 제출 및 투표](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft 기술 커뮤니티의 Windows 관리 센터 포럼 참여](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- 트 윗`@servermgmt`

### <a name="see-also"></a>참조

- [Windows Admin Center](../understand/windows-admin-center.md)
- [스토리지 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [소프트웨어 정의 네트워킹](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
