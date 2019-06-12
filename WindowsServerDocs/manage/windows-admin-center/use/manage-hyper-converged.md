---
title: Windows Admin Center 사용 하 여 하이퍼 수렴 형 인프라 관리
description: Windows Admin Center (프로젝트 브라 티)를 사용 하 여 하이퍼 수렴 형 인프라 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fe00072932d9c7f283ebd887a5292ac9a9d0e37f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446034"
---
# <a name="manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 하이퍼 수렴 형 인프라 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## <a name="what-is-hyper-converged-infrastructure"></a>Hyper-Converged 인프라란

하이퍼 수렴 형 인프라는 소프트웨어 정의 계산, 저장소 및 네트워킹 고성능, 경제적이 고 제공 하기 위해 하나의 클러스터를 쉽게 확장할 수 있는 가상화를 통합 합니다. 이 기능은 Windows Server 2016에서 도입 되었습니다 [저장소 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)를 [소프트웨어 정의 네트워킹](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking) 하 고 [하이퍼-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)합니다.

> [!Tip]
> Hyper-Converged 인프라를 획득 하려고 하나요? 이러한 것이 좋습니다 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd) 파트너의 솔루션입니다. 이러한 설계, 조립 및 호환성 및 안정성 얻게 되므로 신속 하 게 실행 하기 위한이 참조 아키텍처에 대해 유효성을 검사 합니다.

> [!IMPORTANT]
> 이 문서에 설명 된 기능 중 일부가 Windows Admin Center 미리 보기에서 사용할 수 있습니다. [이 버전 가져오기](http://aka.ms/windowsadmincenter)

## <a name="what-is-windows-admin-center"></a>Windows Admin Center란

[Windows Admin Center](../understand/windows-admin-center.md) 기존의 "기본" 서버 관리자와 같은 도구에 대 한 후속 Windows Server의 차세대 관리 도구입니다. 무료 설치 및 인터넷에 연결 하지 않고 사용할 수 있습니다. 관리 및 Windows Server 2016 또는 Windows Server 2019 실행 Hyper-Converged 인프라를 모니터링 하려면 Windows Admin Center 사용할 수 있습니다.

![하이퍼 수렴 형 클러스터 대시보드](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## <a name="key-features"></a>주요 기능

Hyper-Converged 인프라에 대 한 Windows Admin Center 주요 기능은 다음과 같습니다.

- **통합 된 단일-창-의-투명 계산, 저장소 및 네트워킹 예정입니다.** 가상 컴퓨터, 호스트 서버, 볼륨, 드라이브 및 하나의 특화 된, 일관성, 상호 연결 된 환경 내에서 자세히 보기
- **저장소 공간 및 Hyper-v virtual machines를 만들고 설정 합니다.** 근본적으로 간단한 워크플로를 만들고, 열고, 크기 조정; 볼륨을 삭제 및 만들기, 시작, 연결 및 가상 컴퓨터를 이동 합니다. 그 밖의 기능입니다.
- **강력한 클러스터 전체의 모니터링 합니다.** 대시보드 그래프 메모리 및 CPU 사용량, 저장소 용량, IOPS, 처리량 및 대기 시간에 오류가 발생 하는 경우 일반 경고를 사용 하 여 클러스터의 모든 서버에서 실시간으로 합니다.
- **소프트웨어 정의 네트워킹 (SDN) 지원 합니다.** 관리 가상 네트워크, 서브넷, 가상 컴퓨터를 가상 네트워크에 연결 및 모니터링 SDN 인프라를 모니터링 합니다.

Windows Admin Center Hyper-Converged 인프라에 대 한 Microsoft에서 적극적으로 개발 되는 합니다. 기존 기능을 개선 하 고 새 기능을 추가 하는 자주 업데이트를 수신 합니다.

## <a name="before-you-start"></a>시작하기 전 주의 사항

클러스터에서 Windows Admin Center Hyper-Converged 인프라를 관리 하려면 Windows Server 2016 또는 Windows Server 2019 실행 해야 하 고 Hyper-v 및 저장소 공간 다이렉트 사용 하도록 설정 합니다. 필요에 따라는 사용 하도록 설정 하 고 Windows Admin Center 통해 관리 되는 소프트웨어 정의 네트워킹도 하는 것이 있습니다.

> [!Tip]
> 또한 Windows Admin Center Windows Server 2012 이상에 사용 가능한 모든 워크 로드를 지 원하는 모든 클러스터에 대 한 범용 관리 환경을 제공 합니다. Windows Admin Center 클러스터를 추가 하는 경우 적합 한 처럼 생각을 하는 경우 선택할 [ **장애 조치 클러스터** ](manage-failover-clusters.md) 대신 **Hyper-Converged 클러스터**합니다.

### <a name="prepare-your-windows-server-2016-cluster-for-windows-admin-center"></a>Windows Admin Center 대 한 Windows Server 2016 클러스터 준비

Windows Admin Center Hyper-Converged 인프라에 대 한 관리 Api 추가 Windows Server 2016가 출시 된 후에 따라 달라 집니다. Windows Admin Center 사용 하 여 Windows Server 2016 클러스터를 관리 하기 전에 이러한 두 단계를 수행 해야 합니다.

1. 클러스터의 모든 서버에 설치 되어 있는지 확인 합니다 [Windows Server 2016 (KB4103723)에 대 한 누적 업데이트 2018-05](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723) 이상. 을 다운로드 하 고이 업데이트를 설치 하려면로 이동 **설정을** > **업데이트 및 보안** > **Windows 업데이트** 선택 하 고  **Microsoft Update에서 업데이트에 대 한 온라인 확인**합니다.
2. 클러스터에서 관리자 권한으로 다음 PowerShell cmdlet을 실행 합니다.

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> 클러스터의 모든 서버에서 cmdlet을 한 번 실행 해야 합니다. Windows PowerShell에서 로컬로 실행할 수도 있고 Credential Security Service Provider (CredSSP)를 사용 하 여 원격으로 실행할 수 있습니다. 구성에 따라 Windows Admin Center 내에서이 cmdlet을 실행 하려면 못할 수 있습니다.

### <a name="prepare-your-windows-server-2019-cluster-for-windows-admin-center"></a>Windows Admin Center 대 한 Windows Server 2019 클러스터 준비

클러스터에서 Windows Server 2019를 실행 하는 경우에 위의 단계를 필요 하지 않습니다. 다음 섹션에 설명 된 대로 Windows Admin Center 클러스터 추가 계속 진행 하세요!

### <a name="configure-software-defined-networking-optional"></a>소프트웨어 방식 네트워킹 (선택 사항)를 구성 합니다. ###

다음 단계를 사용 하 여 소프트웨어 정의 네트워킹 (SDN)을 사용 하는 Windows Server 2016 또는 2019 실행 Hyper-Converged 인프라를 구성할 수 있습니다.

1. 하이퍼 수렴 형 인프라 호스트에 설치 된 동일한 OS는 os VHD를 준비 합니다. 이 VHD 모든 NC/SLB/GW Vm에 대해 사용 됩니다.
2. 모든 폴더 및 SDN Express에서 파일을 다운로드 [ https://github.com/Microsoft/SDN/tree/master/SDNExpress ](https://github.com/Microsoft/SDN/tree/master/SDNExpress)합니다.
3. 배포 콘솔을 사용 하 여 다른 VM을 준비 합니다. 이 VM은 SDN 호스트에 액세스할 수 있어야 합니다. 또한 VM이 RSAT Hyper-v 도구가 설치 되어 있어야 합니다.
4. VM 배포 콘솔로 SDN Express에 대 한 다운로드 한 모든 내용을 복사 합니다. 이 공유 하 고 **SDNExpress** 폴더입니다. 모든 호스트에 액세스할 수 있는지 확인 합니다 **SDNExpress** 구성 파일 줄 8에서에서 정의 된 대로 폴더를 공유:
   ```
    \\$env:Computername\SDNExpress
   ```
5. 에 os VHD를 복사 합니다 **이미지** 아래에 폴더를 **SDNExpress** VM 배포 콘솔에는 폴더.
6. 환경 설치를 사용 하 여 SDN Express 구성을 수정 합니다. 환경 정보에 따라 SDN Express 구성을 수정한 후에 다음 두 단계를 완료 합니다.
7. SDN을 배포 하려면 관리자 권한으로 PowerShell을 실행 합니다.

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

배포에는 약 30 ~ 45 분 소요 됩니다.

## <a name="get-started"></a>시작

Hyper-Converged 인프라 배포 되 면 Windows Admin Center 사용 하 여 관리할 수 있습니다.

### <a name="install-windows-admin-center"></a>Windows Admin Center 설치

아직 하지 않은 경우 다운로드 하 고 Windows Admin Center 설치 합니다. 빠른 시작 방법 및 실행 중인 Windows 10 컴퓨터에 설치 하 고 서버를 원격으로 관리 하는 것입니다. 그러면 5 분 이내입니다. [지금 다운로드](https://aka.ms/windowsadmincenter) 나 [다른 설치 옵션에 자세히 알아보려면](../deploy/install.md)합니다.

### <a name="add-hyper-converged-cluster"></a>하이퍼 수렴 형 클러스터를 추가 합니다.

Windows Admin Center 클러스터를 추가 합니다.

1. 클릭 **+ 추가** 모든 연결 합니다.
2. 추가 하도록 선택 된 **Hyper-Converged 클러스터 연결**합니다.
3. 클러스터의 이름을 입력 하 고 메시지가 표시 되 면 사용할 자격 증명입니다.
4. 클릭 **추가** 완료 합니다.

클러스터 연결 목록에 추가 됩니다. 대시보드를 시작 하려면 클릭 합니다.

![하이퍼 수렴 형 클러스터 연결 추가](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### <a name="add-sdn-enabled-hyper-converged-cluster-windows-admin-center-preview"></a>SDN 사용이 가능한 하이퍼 수렴 형 클러스터 (Windows Admin Center 미리 보기)를 추가 합니다.

최신 Windows Admin Center 미리 보기는 Hyper-Converged 인프라에 대 한 소프트웨어 정의 네트워킹 관리를 지원합니다. 하이퍼 수렴 형 클러스터 연결에 네트워크 컨트롤러 REST URI를 더하여 SDN 리소스 관리 및 SDN 인프라를 모니터링 하려면 하이퍼 수렴 형 클러스터 관리자를 사용할 수 있습니다.

1. 클릭 **+ 추가** 모든 연결 합니다.
2. 추가 하도록 선택 된 **Hyper-Converged 클러스터 연결**합니다.
3. 클러스터의 이름을 입력 하 고 메시지가 표시 되 면 사용할 자격 증명입니다.
4. 확인할 **네트워크 컨트롤러 구성** 계속 합니다.
5. 입력 된 **네트워크 컨트롤러 URI** 클릭 **유효성 검사**합니다.
6. 클릭 **추가** 완료 합니다.

클러스터 연결 목록에 추가 됩니다. 대시보드를 시작 하려면 클릭 합니다.

![하이퍼 수렴 형 클러스터 SDN 사용이 가능한 연결 추가](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> SDN 환경 Northbound 통신에 대 한 Kerberos 인증을 사용 하 여 현재 지원 되지 않습니다.

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="are-there-differences-between-managing-windows-server-2016-and-windows-server-2019"></a>Windows Server 2016 및 Windows Server 2019 관리 간의 차이점과 있습니까?

예 Windows Admin Center Hyper-Converged 인프라에 대 한 Windows Server 2016 및 Windows Server 2019에 대 한 환경을 개선 하는 자주 업데이트를 받습니다. 그러나 특정 새 기능은 Windows Server 2019 – 예를 들어, 중복 제거 및 압축에 대 한 토글 스위치를 사용할 수 있습니다.

### <a name="can-i-use-windows-admin-center-to-manage-storage-spaces-direct-for-other-use-cases-not-hyper-converged-such-as-converged-scale-out-file-server-sofs-or-microsoft-sql-server"></a>다른 사용 사례 (없습니다 하이퍼 수렴 형), 수렴 형 스케일 아웃 파일 서버 (SoFS) 또는 Microsoft SQL Server와 같은 저장소 공간 다이렉트를 관리 하려면 Windows Admin Center 사용할 수 있나요?

Windows Admin Center Hyper-Converged 인프라에 대 한 관리 또는 저장소 공간 다이렉트의 다른 사용 사례에 맞게 모니터링 옵션을 제공 하지 않습니다 – 예를 들어,이 파일 공유를 만들 수 없습니다. 그러나 모든 저장소 공간 다이렉트 클러스터에 대 한 볼륨 만들기 또는 드라이브를 교체 하는 등의 대시보드 및 핵심 기능 작동 합니다.

### <a name="whats-the-difference-between-a-failover-cluster-and-a-hyper-converged-cluster"></a>장애 조치 클러스터와 Hyper-Converged 클러스터 간의 차이 무엇입니까?

일반적으로 동일한 Hyper-v 및 저장소 공간 다이렉트를 실행 "하이퍼 수렴 형" 이란 용어는 계산 및 저장소 리소스를 가상화 하는 서버를 클러스터링. Windows Admin Center 클릭할 때의 컨텍스트에서 **+ 추가** 연결 목록에서 선택할 수 있습니다 추가 된 **장애 조치 클러스터 연결** 또는 **Hyper-Converged 클러스터 연결**:

- 합니다 **장애 조치 클러스터 연결** 데스크톱 응용 프로그램을 장애 조치 클러스터 관리자의 후속 버전입니다. Microsoft SQL Server를 포함 하 여 모든 워크 로드를 지 원하는 모든 클러스터에 대 한 친숙 하 고 범용 관리 환경을 제공 합니다. 것이 이상 Windows Server 2012에 사용할 수 있습니다.

- 합니다 **Hyper-Converged 클러스터 연결** 는 완전히 새로운 환경에 맞게 조정 됩니다 저장소 공간 다이렉트 및 Hyper-v입니다. 대시보드 기능과 차트 및 모니터링 알림을 강조합니다. Windows Server 2016 및 Windows Server 2019에 대해 제공 됩니다.

### <a name="why-do-i-need-the-latest-cumulative-update-for-windows-server-2016"></a>Windows Server 2016에 대 한 최신 누적 업데이트를 필요한 이유

Windows Admin Center Hyper-Converged 인프라에 대 한 관리 Api는 Windows Server 2016이 릴리스된 이후 개발에 따라 달라 집니다. 이러한 Api에 추가 되는 [2018-05 Windows Server 2016 (KB4103723)에 대 한 누적 업데이트](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723), 2018 년 5 월 8 일부 터 사용할 수 있습니다.

### <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Windows Admin Center를 사용하는 비용은 얼마입니까?

Windows Admin Center는 Windows 이외에 추가 비용이 들지 않습니다.

Windows Admin Center (별도 다운로드로 제공)를 사용 하 여 추가 비용 없이 Windows Server 또는 Windows 10의 유효한 라이선스가 있는-Windows 추가 사용권 계약서에서 사용이 허가 됩니다.

### <a name="does-windows-admin-center-require-system-center"></a>Windows Admin Center에 System Center가 필요합니까?

아니요.

### <a name="does-it-require-an-internet-connection"></a>인터넷에 연결 하기 필요 합니까?

아니요.

Windows Admin Center 강력한 제공 및 Microsoft Azure 클라우드, 핵심 관리 및 모니터링 환경을 Hyper-Converged 인프라에 대 한 편리한 통합을 완전히 하지만 온-프레미스. 설치 고 인터넷에 연결 하지 않고 사용할 수 있습니다.

## <a name="things-to-try"></a>시도할 작업

하면 이제 막 시작, Hyper-Converged 인프라에 대 한 Windows Admin Center 구성 되 고 작동 하는 방법을 배울 수 있도록 하는 간단한 자습서를 같습니다. 좋은 관행을 연습 하 고 프로덕션 환경에 주의 하세요. 이러한 비디오는 Windows Admin Center 버전 1804 및 Windows Server 2019의 Insider Preview 빌드를 사용 하 여 기록 되었습니다.

### <a name="manage-storage-spaces-direct-volumes"></a>저장소 공간 다이렉트 볼륨 관리

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">3 방향 미러 볼륨을 만드는 방법</a></li>
               <li>(1:17) <a href="https://youtu.be/R72QHudqWpE">미러 가속 패리티 볼륨을 만드는 방법</a></li>
               <li>(1:02) <a href="https://youtu.be/j59z7ulohs4">볼륨을 열고 파일을 추가 하는 방법</a></li>
               <li>(0:51) <a href="https://youtu.be/PRibTacyKko">중복 제거 및 압축 설정 하는 방법</a></li>
               <li>(0:47) <a href="https://youtu.be/hqyBzipBoTI">볼륨을 확장 하는 방법</a></li>
               <li>(0:26) <a href="https://youtu.be/DbjF8r2F6Jo">볼륨을 삭제 하는 방법</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>3 방향 미러 볼륨 만들기</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>미러 가속 패리티 볼륨 만들기</strong>
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

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 합니다 **인벤토리** 탭을 클릭 한 다음 **새로 만들기** 새 가상 머신을 만들려면.
3. 가상 컴퓨터 이름을 입력 하 고 1 및 2 세대 가상 컴퓨터 중에서 선택 합니다.
4. 열리는 처음에 가상 컴퓨터를 만들 하거나 권장 되는 호스트를 사용 하 여 호스트를 선택할 수 있습니다.
5. 가상 머신 파일에 대 한 경로 선택 합니다. 드롭다운 목록에서 볼륨을 선택 하거나 클릭 **찾아보기** 폴더 선택기를 사용 하 여 폴더를 선택 합니다. 가상 머신 구성 파일과 가상 하드 디스크 파일에서 단일 폴더에 저장 됩니다는 `\Hyper-V\[virtual machine name]` 선택한 볼륨의 경로 경로입니다.
6. 중첩 된 가상화를 사용 하려면, 메모리 설정, 네트워크 어댑터, 가상 하드 디스크를 구성 하 고.iso 이미지 파일에서 또는 네트워크에서 운영 체제를 설치할 것인지 여부를 선택 하는지 여부를 가상 프로세서의 수를 선택 합니다.
7. **만들기**를 클릭하여 가상 컴퓨터를 만듭니다.
8. 가상 머신을 만들고 가상 컴퓨터 목록에 표시 됩니다, 가상 컴퓨터를 시작할 수 있습니다.
9. 가상 머신이 시작 되 면 운영 체제를 설치 하는 VMConnect 통해 가상 머신의 콘솔에 연결할 수 있습니다. 목록에서 가상 컴퓨터를 선택, 클릭 **자세한** > **Connect** .rdp 파일을 다운로드 합니다. 원격 데스크톱 연결 앱에.rdp 파일을 엽니다. 가상 머신의 콘솔에 연결할은이 때문에 Hyper-v 호스트의 관리자 자격 증명을 입력 해야 합니다.

[Windows Admin Center 사용 하 여 가상 머신 관리에 자세히 알아보려면](manage-virtual-machines.md)합니다.

### <a name="pause-and-safely-restart-a-server"></a>일시 중지 하 고 안전 하 게 서버를 다시 시작

1. **대시보드**를 선택 **서버** 를 클릭 하 여 또는 왼쪽 탐색 모음에서를 **서버 보기 >** 대시보드의 오른쪽 아래 모퉁이의 타일에 대 한 링크 .
2. 맨 위에 있는 전환 **요약** 에 **인벤토리** 탭 합니다.
3. 열려면 해당 이름을 클릭 하 여 서버를 선택 합니다 **Server** 세부 정보 페이지입니다.
4. 클릭 **유지 관리에 대 한 일시 중지 server**합니다. 계속 진행 하면 안전 인 경우 가상 머신을 클러스터의 다른 서버로 이동 됩니다. 서버 상태에 이렇게 하는 동안 드레이닝 해야 합니다. 원한다 면 이동 된 가상 컴퓨터를 볼 수 있습니다 합니다 **Virtual machines > 인벤토리** 페이지에서 해당 호스트 서버 그리드에서 명확 하 게 표시 됩니다. 모든 가상 컴퓨터를 이동 하는 경우 서버 상태 됩니다 **일시 중지 됨**합니다.
5. 클릭 **관리 서버** Windows Admin Center 모든 서버 관리 도구를 액세스할 수 있습니다.
6. 클릭 **다시 시작**, 한 다음 **예**합니다. 하는 연결 목록에 다시 종료 될 것입니다.
7. 다시 합니다 **대시보드**를 중단 하는 동안 서버는 빨간색으로 표시 합니다.
8. 백업 있으면 다시 이동 합니다 **Server** 페이지를 클릭 **유지 관리에서 서버 다시 시작** 를 단순히 최신 서버 상태를 설정 하려면. 시간 내에 가상 컴퓨터를 다시 이동 – 사용자 동작은 필요 하지 않습니다.

### <a name="replace-a-failed-drive"></a>실패 한 드라이브 교체

1. 드라이브를 실패할 경우 홈페이지에서 경고가 나타날 **경고** 영역의 합니다 **대시보드**합니다.
2. 선택할 수도 있습니다 **드라이브** 클릭 또는 왼쪽 탐색 영역에서 합니다 **보기 드라이브 >** 드라이브를 찾아보고 해당 상태를 직접 보려면 오른쪽 아래 모퉁이의 타일에 대 한 링크입니다. 에 **인벤토리** 탭 모눈 정렬, 그룹화 및 키워드 검색 지원 합니다.
3. **대시보드**를 드라이브의 물리적 위치와 같은 세부 정보를 보려면 경고를 클릭 합니다.
4. 자세히 알아보려면 클릭 합니다 **드라이브로 이동** 바로 가기를 합니다 **드라이브** 세부 정보 페이지입니다.
5. 하드웨어에서 지 원하는 경우 클릭할 수 있습니다 **표시등 켜기/끄기** 드라이브 표시등을 제어할 수 있습니다.
6. 저장소 공간 다이렉트 자동으로 재시도 및 실패 한 드라이브 evacuates 합니다. 이 드라이브 상태 않으며 해당 저장소 용량 막대 비어 있습니다.
7. 실패 한 드라이브를 제거 하 고 대체를 삽입 합니다.
8. **드라이브 > 인벤토리**, 새 드라이브가 표시 됩니다. 시간 내에 경고가 지워집니다, 그리고 정상 상태를 다시 복구 하는 볼륨 및 저장소를 새 드라이브로 균형 다시 맞추기 – 사용자 동작은 필요 하지 않습니다.

### <a name="manage-virtual-networks-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>가상 네트워크 (Windows Admin Center 미리 보기를 사용 하 여 SDN 사용이 가능한 HCI 클러스터)를 관리 합니다.

1. 선택 **가상 네트워크** 왼쪽 탐색 영역에서 합니다.
2. 클릭 **새로 만들기** 새 가상 네트워크 및 서브넷 만들기 또는 기존 가상 네트워크를 선택 하 고, 클릭 하 **설정** 해당 구성을 수정할 수 있습니다.
3. 가상 네트워크 서브넷에 VM 연결 보기 및 액세스 제어 목록 가상 네트워크 서브넷에 적용 하려면 기존 가상 네트워크를 클릭 합니다.

![가상 네트워크 관리](../media/manage-hyper-converged/manage-virtual-networks.png)

### <a name="connect-a-virtual-machine-to-a-virtual-network-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>가상 머신을 가상 네트워크 (Windows Admin Center 미리 보기를 사용 하 여 SDN 사용이 가능한 HCI 클러스터)에 연결

1. 선택 **가상 머신** 왼쪽 탐색 영역에서 합니다.
2. 기존 가상 머신을 선택 > 클릭 **설정을** > 열기를 **네트워크** 탭에서 **설정**합니다.
3. 구성 합니다 **가상 네트워크** 하 고 **가상 서브넷** 가상 머신을 가상 네트워크에 연결 하는 필드입니다.

또한 가상 머신을 만들 때 가상 네트워크를 구성할 수 있습니다.

![가상 머신을 가상 네트워크에 연결](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### <a name="monitor-software-defined-networking-infrastructure-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>소프트웨어 정의 네트워킹 인프라 모니터링 (Windows Admin Center 미리 보기를 사용 하 여 SDN 사용이 가능한 HCI 클러스터)

1. 선택 **SDN 모니터링** 왼쪽 탐색 영역에서 합니다.
2. 네트워크 컨트롤러, 소프트웨어 부하 분산 장치 가상 게이트웨이 상태에 대 한 자세한 정보를 확인 하 고 가상 게이트웨이 풀, 공용 및 개인 IP 풀 사용량 및 SDN 호스트 상태를 모니터링 합니다.

![SDN 인프라 모니터링](../media/manage-hyper-converged/sdn-monitoring.png)

## <a name="feedback"></a>사용자 의견

여러분의 의견에 대 한 모든 것! 잦은 업데이트의 가장 중요 한 장점은 무엇 작동 하 고 개선 하는 사항 들을 합니다. 여러분은 아마도 알리는 방법은 다음과 같습니다.

- [제출 하 고 UserVoice에서 기능 요청에 대 한 투표](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft 기술 커뮤니티에서 Windows Admin Center 포럼 가입](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- 에 트 윗 `@servermgmt`

### <a name="see-also"></a>참조

- [Windows Admin Center](../understand/windows-admin-center.md)
- [스토리지 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [소프트웨어 정의 네트워킹](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
