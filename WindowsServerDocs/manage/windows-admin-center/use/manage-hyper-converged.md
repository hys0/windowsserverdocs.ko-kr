---
title: Windows Admin Center를 사용 하 여 하이퍼 컨 버 지 드 인프라 관리
description: Windows Admin Center (Project Honolulu)를 사용 하 여 하이퍼 컨 버 지 드 인프라 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9ce4381735746ace6358aa2cb30f8b341c576054
ms.sourcegitcommit: e558dda2774345e9ad17ff04b759f68c59d88139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "9262846"
---
# Windows Admin Center를 사용 하 여 하이퍼 컨 버 지 드 인프라 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

## 컨 버 지 드 인프라 란

소프트웨어 정의 컴퓨팅, 저장소 및 네트워킹 고성능, 효과적인를 제공 하기 위해 하나의 클러스터를 쉽게 확장할 가상화 하이퍼 컨 버 지 드 인프라에 통합 되어 있습니다. 이 접근 권한이 값은 [저장소 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview), [소프트웨어 정의 네트워킹](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking) 및 [Hyper-v](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)를 사용 하 여 Windows Server 2016에 도입 되었습니다.

> [!Tip]
> 취득 컨 버 지 드 인프라를 찾고 계신가요? Microsoft은 파트너 로부터 이러한 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd) 솔루션을 권장합니다. 설계, 조립 되며 호환성 및 안정성 얻기 및 신속 하 게 실행 되도록 하는 참조 아키텍처에 대해 유효성이 검사 됩니다.

> [!IMPORTANT]
> 이 문서에 설명 된 기능 중 일부는 Windows Admin Center 미리 보기에서 사용할 수만 있습니다. [이 버전 가져오기](http://aka.ms/windowsadmincenter)

## Windows Admin Center란

[Windows Admin Center](../understand/windows-admin-center.md) 는 Windows server에서 서버 관리자 같은 기존의 "기본" 도구에 대 한 후속 차세대 관리 도구입니다. 이 무료 설치 및 인터넷 연결 없이 사용 될 수 있습니다. Windows Admin Center를 사용 하 여 관리 하 고 Windows Server 2016 또는 Windows Server 2019를 실행 하는 컨 버 지 드 인프라를 모니터링 수 있습니다.

![하이퍼 컨 버 지 드 클러스터 대시보드](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## 주요 기능

컨 버 지 드 인프라에 대 한 Windows Admin Center의 주요 기능은 다음과 같습니다.

- **통합 된 단일-창-의-통한 컴퓨팅, 저장소 및 네트워킹 예정입니다.** 가상 컴퓨터, 호스트 서버, 볼륨, 드라이브 및 하나의 뛰어난 일관 되 고 상호 연결 된 환경 내에서 더 보기
- **만들기 및 저장소 공간 및 Hyper-v 가상 컴퓨터를 관리 합니다.** 만들고, 열고, 크기 조정, 고; 볼륨을 삭제 하는 간단한 워크플로 및 만들기, 시작, 연결 하 고 가상 컴퓨터; 이동 등입니다.
- **강력한 클러스터 전체의 풍부한 모니터링 합니다.** 대시보드 그래프 메모리 및 CPU 사용량, 저장소 용량, IOPS, 처리량 및 대기 시간에 올바른 점이 발견 될 경우 명확한 경고를 사용 하 여 클러스터의 모든 서버에서 실시간 합니다.
- **소프트웨어 정의 네트워킹 (SDN) 지원 합니다.** 관리 및 가상 네트워크 서브넷 모니터링, 가상 컴퓨터 가상 네트워크에 연결 및 SDN 인프라를 모니터링 합니다.

Microsoft에서 컨 버 지 드 인프라에 대 한 Windows Admin Center는 적극적으로 개발 되는 합니다. 기존 기능을 개선 하 고 새로운 기능을 추가 하는 자주 업데이트를 받습니다.

## 시작하기 전에

클러스터에서 Windows Admin Center 컨 버 지 드 인프라를 관리 하려면 Windows Server 2016 또는 Windows Server 2019를 실행 해야 하 고 Hyper-v 및 저장소 공간 다이렉트 사용 합니다. 선택적으로 사용 하도록 설정 하 고 Windows Admin Center를 통해 관리 되는 소프트웨어 정의 네트워킹 할 수도 것.

> [!Tip]
> 또한 Windows Admin Center는 Windows Server 2012 이상 사용할 수 있는 모든 워크 로드를 지 원하는 모든 클러스터에 대 한 범용 관리 환경을 제공 합니다. Windows Admin Center를 클러스터를 추가 하면 적합 한 처럼 생각을 하는 경우 **컨 버 지 드 클러스터**대신 [**장애 조치 클러스터**](manage-failover-clusters.md) 선택 합니다.

### Windows Admin Center에 대 한 Windows Server 2016 클러스터 준비

Windows Admin Center 컨 버 지 드 인프라에 대 한 Api는 Windows Server 2016 릴리스된 후 추가 관리에 따라 달라 집니다. Windows Admin Center로 Windows Server 2016 클러스터를 관리 하려면 먼저 다음 두 단계를 수행 해야 합니다.

1. 클러스터의 모든 서버가 [2018-05 Windows Server 2016 (KB4103723) 용 누적 업데이트](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723) 설치 확인 이상. **설정**으로 이동를 다운로드 하 고이 업데이트를 설치 > **& 보안 업데이트** > **Windows 업데이트** 및 **Microsoft 업데이트에서 업데이트에 대 한 온라인 검사**선택 합니다.
2. 클러스터에서 관리자 권한으로 다음 PowerShell cmdlet을 실행 합니다.

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> 클러스터의 모든 서버에서 cmdlet을 한 번 실행 해야 합니다. Windows PowerShell에서 로컬로 실행할 수도 있고 자격 증명 보안 서비스 공급자 (CredSSP)를 사용 하 여 원격으로 실행할 수 있습니다. 구성에 따라 Windows Admin Center 내에서이 cmdlet을 실행 하려면 못할 수 있습니다.

### Windows Admin Center에 대 한 Windows Server 2019 클러스터 준비

클러스터에서 Windows Server 2019를 실행 하는 경우 위의 단계 필요 하지 않습니다. 다음 섹션에 설명 된 대로 클러스터 Windows Admin Center를 추가 하 고 실습을 시작할 수 있는!

### 소프트웨어 정의 네트워킹 (선택 사항) 구성 ###

다음 단계를 사용 하 여 소프트웨어 정의 네트워킹 (SDN)를 사용 하 여 Windows Server 2016 또는 2019 실행 컨 버 지 드 인프라를 구성할 수 있습니다.

1. 하이퍼 컨 버 지 드 인프라 호스트에 설치 된 동일한 OS는 운영 체제의 VHD를 준비 합니다. 이 VHD 모든 GW/NC/SLB Vm에 대 한 사용 됩니다.
2. 모든 폴더와 파일에서 SDN Express 다운로드 [https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress).
3. 배포 콘솔을 사용 하 여 다른 VM을 준비 합니다. 이 VM SDN 호스트에 액세스할 수 있어야 합니다. 또한 RSAT Hyper-v 도구가 설치 되어 VM가 있어야 합니다.
4. VM 배포 콘솔에 SDN express 다운로드 한 모든 복사 합니다. 및이 **SDNExpress** 폴더를 공유 합니다. 구성 파일 줄 8에에서 정의 된 모든 호스트 **SDNExpress** 공유 폴더에 액세스할 수 있는지를 확인 합니다.
```
    \\$env:Computername\SDNExpress
```
5. 운영 체제의 VHD 아래의 **SDNExpress** 폴더 배포 콘솔 VM에 **이미지** 폴더에 복사 합니다.
6. 환경 설정으로 SDN Express 구성을 수정 합니다. SDN Express 구성 환경 정보에 따라 수정한 후 다음 두 단계를 완료 합니다.
7. SDN 배포 하려면 관리자 권한으로 PowerShell를 실행 합니다.

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

배포 약 30-45 분이 걸립니다.

## 시작하기

컨 버 지 드 인프라 배포 되 면 Windows Admin Center를 사용 하 여 관리할 수 있습니다.

### Windows Admin Center 설치

아직 되어 있지 않은 경우 다운로드 하 고 Windows Admin Center를 설치 합니다. 가장 빠른 시작 하는 방법 및 실행 중인 Windows 10 컴퓨터에 설치 하 고 서버를 원격으로 관리 하는 것입니다. 이 분 정도 걸립니다. [지금 다운로드](https://aka.ms/windowsadmincenter) 하거나 [다른 설치 옵션에 대 한 더 자세한](../deploy/install.md)합니다.

### 하이퍼 컨 버 지 드 클러스터를 추가 합니다.

Windows Admin Center를 클러스터를 추가 합니다.

1. 모든 연결에서 **+ 추가** 클릭 합니다.
2. **컨 버 지 드 클러스터 연결**을 추가 하려면 선택 합니다.
3. 클러스터의 이름을 입력 하 고 메시지가 표시 되 면 자격 증명을 사용 합니다.
4. 완료 하려면 **추가** 클릭 합니다.

클러스터 연결 목록에 추가 됩니다. 대시보드 시작을 클릭 합니다.

![하이퍼 컨 버 지 드 클러스터 연결 추가](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### 하이퍼 수렴 형 클러스터 SDN 사용 (Windows Admin Center 미리 보기)를 추가 합니다.

최신 Windows Admin Center 미리 보기 컨 버 지 드 인프라에 대 한 소프트웨어 정의 네트워킹 관리를 지원합니다. 네트워크 컨트롤러 REST URI 하이퍼 컨 버 지 드 클러스터 연결을 추가 하 여 SDN 리소스를 관리 하 고 SDN 인프라를 모니터링 하이퍼 컨 버 지 드 클러스터 관리자를 사용할 수 있습니다.

1. 모든 연결에서 **+ 추가** 클릭 합니다.
2. **컨 버 지 드 클러스터 연결**을 추가 하려면 선택 합니다.
3. 클러스터의 이름을 입력 하 고 메시지가 표시 되 면 자격 증명을 사용 합니다.
4. 계속 하려면 **구성 네트워크 컨트롤러** 확인 합니다.
5. **네트워크 컨트롤러 URI** 를 입력 하 고 **유효성 검사**를 클릭 합니다.
6. 완료 하려면 **추가** 클릭 합니다.

클러스터 연결 목록에 추가 됩니다. 대시보드 시작을 클릭 합니다.

![SDN 기반 하이퍼 컨 버 지 드 클러스터 연결 추가](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> SDN 환경 Northbound 통신에 대 한 Kerberos 인증을 사용 하 여 현재 지원 되지 않습니다.

## 질문과 대답

### Windows Server 2016 및 Windows Server 2019 관리 간의 차이점 있습니까?

그렇습니다. Windows Admin Center 컨 버 지 드 인프라에 대 한 Windows Server 2016 및 Windows Server 2019에 대 한 경험을 개선 하는 자주 업데이트를 받습니다. 그러나 특정 새로운 기능은 Windows Server 2019 – 중복 제거 및 압축에 대 한 예를 들어 토글 스위치에 사용할 수 있습니다.

### 다른 사용 사례에 대해 (하지 하이퍼 컨 버 지 드), 수렴 형 스케일 아웃 파일 서버 (SoFS) 또는 Microsoft SQL Server 등의 저장소 공간 다이렉트를 관리 하려면 Windows Admin Center를 사용할 수 있나요?

Windows Admin Center 컨 버 지 드 인프라에 대 한 관리 또는 저장소 공간 다이렉트의 다른 사용 사례에 대해 특별히 모니터링 옵션을 제공 하지 않습니다-예를 들어 파일 공유 만들 수 없습니다. 그러나 모든 저장소 공간 다이렉트 클러스터에 대 한 볼륨 만들기 또는 드라이브 교체와 같은 대시보드 및 핵심 기능을 작동 합니다.

### 장애 조치 클러스터 및 컨 버 지 드 클러스터 간의 차이 무엇입니까?

일반적으로 동일한에서 Hyper-v 및 저장소 공간 다이렉트 실행 "하이퍼 컨 버 지 드" 이란 용어는 클러스터 서버 가상화 컴퓨팅 및 저장소 리소스를. Windows Admin Center의 컨텍스트에서 **+ 추가** 연결 목록에서 클릭 하면 **장애 조치 클러스터 연결** 또는 **컨 버 지 드 클러스터 연결**추가 간에 선택할 수 있습니다.

- **장애 조치 클러스터 연결** 장애 조치 클러스터 관리자 데스크톱 앱에 대 한 후속입니다. Microsoft SQL Server를 비롯 한 모든 워크 로드를 지 원하는 모든 클러스터에 대 한 친숙 한, 범용 관리 환경을 제공 합니다. 이것은 Windows Server 2012에 사용할 수 있는 이후입니다.

- **컨 버 지 드 클러스터 연결** 저장소 공간 다이렉트 및 Hyper-v에 맞게 완전히 새로운 환경입니다. 대시보드 기능과 차트 및 모니터링 알림을 강조합니다. Windows Server 2016 및 Windows Server 2019에 나와 있습니다.

### Windows Server 2016에 대 한 최신 누적 업데이트를 왜 필요 한가요?

Windows Admin Center 컨 버 지 드 인프라에 대 한 관리 Api는 Windows Server 2016 릴리스된 이후 개발에 따라 달라 집니다. 이러한 Api는 [2018-05 Windows Server 2016 (KB4103723) 용 누적 업데이트를](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)사용할 수 있는 2018 년 5 월 8 일에에서 추가 됩니다.

### Windows Admin Center를 사용하는 비용은 얼마입니까?

Windows Admin Center는 Windows 이외에 추가 비용이 들지 않습니다.

Windows Admin Center (별도 다운로드 사용 가능)를 사용 하 여 추가 비용 없이 Windows Server 또는 Windows 10의 유효한 라이선스가 있는-Windows 추가 eula에 의해 사용권이 부여 됩니다.

### Windows Admin Center에 System Center가 필요합니까?

아니요.

### 인터넷 연결이 필요 하지 않습니다.

아니요.

Windows Admin Center 제공 강력 하 고 Microsoft Azure 클라우드, 핵심 관리 및 모니터링 환경을 컨 버 지 드 인프라에 대 한 편리한 통합은 완전히 온-프레미스. 설치 및 인터넷 연결 없이 사용 될 수 있습니다.

## 시도할 작업

사용자는 방금 시작 하는 경우 Windows Admin Center 컨 버 지 드 인프라에 대 한 구성 하 고 작동 하는 방법을 배울 수 있도록 하는 간단한 자습서 다음과 같습니다. 좋은 관행을 실행 하 고 프로덕션 환경에 주의 하십시오. 이 비디오는 Windows Admin Center 버전 1804 및 Windows Server 2019의 Insider Preview 빌드를 사용 하 여 기록 되었습니다.

### 저장소 공간 다이렉트 볼륨 관리

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">3 방향 미러 볼륨을 만드는 방법</a></li>
               <li>(1:17) <a href="https://youtu.be/R72QHudqWpE">미러-가속 패리티 볼륨을 만드는 방법</a></li>
               <li>(1:02) <a href="https://youtu.be/j59z7ulohs4">볼륨을 열고 파일을 추가 하는 방법</a></li>
               <li>(0:51) <a href="https://youtu.be/PRibTacyKko">중복 제거 및 압축을 켜는 방법</a></li>
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
            <strong>미러-가속 패리티 볼륨 만들기</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>볼륨을 열고 파일 추가</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>중복 제거 및 압축 켜기</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>볼륨 확장</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>볼륨을 삭제</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### 새 가상 컴퓨터 만들기

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 **인벤토리** 탭을 선택 한 다음 **새** 새 가상 컴퓨터 만들기를 클릭 합니다.
3. 가상 컴퓨터 이름을 입력 하 고 1과 2 세대 가상 컴퓨터 간에 선택 합니다.
4. Uou 처음에 가상 컴퓨터를 생성 하거나 권장된 호스트를 사용 하는 호스트를 선택할 수 있습니다.
5. 가상 컴퓨터 파일에 대 한 경로 선택 합니다. 드롭다운 목록에서 볼륨을 선택 하거나 **찾아보기** 폴더 선택기를 사용 하 여 폴더를 선택 합니다. 가상 컴퓨터 구성 파일 및 가상 하드 디스크 파일에 단일 폴더에 저장 됩니다 합니다 `\Hyper-V\[virtual machine name]` 선택한 볼륨 또는 경로 경로입니다.
6. 중첩 된 가상화를 사용 하도록 설정 하려면, 가상 하드 디스크, 네트워크 어댑터, 메모리 설정 구성 및.iso 이미지 파일에서 또는 네트워크에서 운영 체제를 설치할 것인지 선택 여부 가상 프로세서 수를 선택 합니다.
7. 가상 컴퓨터를 만들려면 **만들기** 클릭 합니다.
8. 가상 컴퓨터 만들고 가상 컴퓨터 목록에 표시, 가상 컴퓨터를 시작할 수 있습니다.
9. 가상 컴퓨터가 시작 되 면 운영 체제를 설치 하려면 VMConnect 통해 가상 컴퓨터의 콘솔에 연결할 수 있습니다. 목록에서 가상 컴퓨터를 선택, **더 많은**을 클릭 > **연결** .rdp 파일을 다운로드 합니다. 원격 데스크톱 연결 앱에서.rdp 파일을 엽니다. 이 가상 컴퓨터의 콘솔에 연결을 하므로 Hyper-v 호스트의 관리자 자격 증명을 입력 해야 합니다.

[Windows Admin Center를 사용 하 여 가상 컴퓨터 관리에 자세히 알아봅니다](manage-virtual-machines.md).

### 일시 중지 하 고 안전 하 게 하는 서버를 다시 시작

1. **대시보드**대시보드의 오른쪽 아래 모서리에서 타일에 **서버 보기 gt_** 링크를 클릭 하거나 왼쪽 탐색 창에서 **서버** 를 선택 합니다.
2. 맨 위에 있는 **인벤토리** 탭으로 **요약** 에서 전환 합니다.
3. **서버** 세부 정보 페이지를 열고 해당 이름을 클릭 하 여 서버를 선택 합니다.
4. **유지 관리를 위해 서버 일시 중지를**클릭 합니다. 계속 하려면 안전한 인 경우 가상 컴퓨터 클러스터의 다른 서버로 이동 됩니다. 이렇게 하는 동안 상태 드레이닝 서버 갖게 됩니다. 원할 경우 표에 해당 호스트 서버 명확 하 게 하 게 표시 하는 **가상 컴퓨터 gt_ 인벤토리** 페이지에서 이동 하는 가상 컴퓨터를 볼 수 있습니다. 모든 가상 컴퓨터를 이동 했을 때 서버 상태 **일시 중지**됩니다.
5. Windows Admin Center에서 모든 서버 관리 도구에 액세스 하려면 **관리 서버** 클릭 합니다.
6. **다시 시작**을 다음 **예**를 클릭 합니다. 하면 연결 목록에 다시 시작 되어야 합니다.
7. **대시보드**를 켜면 아래로 상태일 때 서버 빨간색 색입니다.
8. 백업 되 면 다시 **서버** 페이지를 탐색 하 고 **유지 관리에서 다시 시작 서버** 를 간단 하 게 최신 서버 상태를 설정할 수를 클릭 합니다. 시간 내에 가상 컴퓨터를 다시 이동 – 사용자 작업이 필요 하지 않습니다.

### 드라이브를 교체

1. 드라이브 실패할 경우, 경고 **대시보드**의 왼쪽된 위 **알림** 영역에 표시 됩니다.
2. 왼쪽 탐색 창에서 **드라이브** 를 선택 하거나 드라이브를 찾아서 해당 상태 자신에 대 한 참조를 오른쪽 아래 모서리에서 타일에 **보기 드라이브 gt_** 링크 클릭 수도 있습니다. **인벤토리** 탭에서 그리드 정렬, 그룹화 및 검색 키워드를 지원합니다.
3. **대시보드**는 드라이브의 물리적 위치와 같은 자세한 내용을 보려면 경고를 클릭 합니다.
4. 자세한 내용은 **드라이브** 세부 정보 페이지의 **드라이브로 이동** 바로 가기를 클릭 합니다.
5. 하드웨어에서 지 원하는 경우 드라이브의 표시등이 제어 하려면 **설정 켜기/끄기 빛** 클릭 수 있습니다.
6. 저장소 공간 다이렉트 자동으로 재시도 하 고 실패 한 드라이브 evacuates 합니다. 이런 드라이브 상태, 폐기 하 고의 저장소 용량 표시줄 비어 있습니다.
7. 실패 한 드라이브를 제거 하 고 해당 대체를 삽입 합니다.
8. **인벤토리 gt_ 드라이브**에서 새 드라이브로 표시 됩니다. 시간 내에 경고 지워집니다, 그리고 볼륨은 정상 상태를 다시 복구 및 저장소는 새 드라이브로 균형을 다시 조정 – 사용자 작업이 필요 하지 않습니다.

### 가상 네트워크 (SDN 지원 HCI 클러스터 Windows Admin Center 미리 보기를 사용 하 여) 관리

1. 왼쪽 탐색 창에서 **가상 네트워크** 를 선택 합니다.
2. 새 가상 네트워크를 만들고 서브넷 하거나 기존 가상 네트워크를 선택 하 고 **설정** 구성을 수정 하려면 클릭을 **새로 만들기** 클릭 합니다.
3. 가상 네트워크 서브넷에 VM 연결 보기 및 액세스 제어 목록 가상 네트워크 서브넷에 적용 하는 기존 가상 네트워크를 클릭 합니다.

![가상 네트워크 관리](../media/manage-hyper-converged/manage-virtual-networks.png)

### 가상 네트워크 (Windows Admin Center 미리 보기를 사용 하 여 SDN 지원 HCI 클러스터)에 가상 컴퓨터 연결

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 를 선택 합니다.
2. 기존 가상 컴퓨터 gt_ 클릭 선택 **설정** gt_ **설정**에서 **네트워크** 탭을 엽니다.
3. 가상 네트워크에 가상 컴퓨터를 연결 하는 **가상 네트워크** 및 **가상 서브넷** 필드를 구성 합니다.

가상 컴퓨터를 만들 때 가상 네트워크를 구성할 수도 있습니다.

![가상 네트워크에 가상 컴퓨터 연결](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### 모니터 소프트웨어 정의 네트워킹 인프라 (HCI SDN 지원 클러스터 Windows Admin Center 미리 보기를 사용 하 여)

1. 왼쪽 탐색 창에서 **SDN 모니터링** 을 선택 합니다.
2. 네트워크 컨트롤러, 소프트웨어 부하 분산 장치, 가상 게이트웨이의 상태에 대 한 자세한 내용을 보려면 하 고 가상 게이트웨이 풀, 공개 및 개인 IP 풀 사용 및 SDN 호스트 상태를 모니터링 합니다.

![SDN 인프라 모니터링](../media/manage-hyper-converged/sdn-monitoring.png)

## 피드백

피드백에 대 한 모든 것! 자주 업데이트의 가장 중요 한 장점은 들을 어떻게 작동 하 고 개선 하는 사항입니다. 하지만 이런 알려줄 하는 몇 가지는 다음과 같습니다.

- [제출 하 고, 기능 요청 UserVoice에서 투표](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft 기술 커뮤니티에서 Windows Admin Center 포럼에 가입](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- 소리를 `@servermgmt`

### 기타 참조

- [Windows Admin Center](../understand/windows-admin-center.md)
- [저장소 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [소프트웨어 정의 네트워킹](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
