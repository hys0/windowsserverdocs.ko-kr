---
title: 서비스 채널
description: 'Windows Server 서비스 채널 설명: LTSC 및 SAC'
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: high
ms.openlocfilehash: c4329339e37acbb0b589e767a570073f4ae1363f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848734"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server 서비스 채널: LTSC 및 SAC

>적용 대상: Windows Server 2019, Windows Server 2016


**Windows Server 고객에 게 장기 서비스 채널 및 반기 채널을 사용할 수 있는 두 개의 주 릴리스 채널 있습니다.** 

장기 서비스 채널(LTSC)에서 서버를 유지하고, 사용자의 요구에 따라 반기 채널로 이동하거나, 두 트랙에 일부 서버를 보유할 수 있습니다.


## <a name="long-term-servicing-channel-ltsc"></a>장기 서비스 채널(LTSC)
이는 2~3년마다 Windows Server의 주 버전이 출시되는, 이미 여러분에게 친숙한 릴리스 모델(이전의 “장기 서비스 *분기*”)입니다. 사용자는 5년 동안 일반 지원을 받고 지원 기간을 5년 연장할 수 있습니다. 이 채널은 보다 장기적인 서비스 옵션과 기능적 안정성이 요구되는 시스템에 적절합니다. Windows Server 2016 이하 버전의 Windows Server 배포는 새로운 반기 채널 릴리스의 영향을 받지 않습니다. 장기 서비스 채널은 보안 및 비보안 업데이트를 계속해서 수신하지만, 새로운 기능은 수신하지 않습니다.

> [!Note]  
> **현재 LTSC 제품은 Windows Server 2019입니다**. 이 채널을 유지하고자 하는 경우 Windows Server 2019를 설치(또는 계속 사용)해야 하고, Server Core 설치 옵션 또는 Desktop 환경 포함 서버 설치 옵션으로 설치할 수 있습니다.

## <a name="semi-annual-channel"></a>반기 채널 
반기 채널은 신속 하 게 활용 하려면 새 운영 체제 기능 둘 다 응용 프로그램에서 더 빠른 속도로 특히 소프트웨어 정의 뿐만 아니라 컨테이너 및 마이크로 서비스에 구축 된 혁신은 고객을 위한 완벽 한 하이브리드 데이터 센터입니다. 반기 채널의 Windows Server 제품은 1년에 두 번, 봄과 가을에 새 릴리스가 제공됩니다. 이 채널의 각 릴리스는 최초 릴리스 후 18개월 동안 지원됩니다.

반기 채널에 도입된 대부분의 기능은 Windows Server의 차기 LTSC 릴리스로 롤업됩니다. 에디션, 기능 및 지원 내용은 고객 피드백에 따라 릴리스마다 달라질 수 있습니다.

반기 채널은 [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)가 포함된 볼륨 라이선스 고객에게 제공되며, Azure Marketplace 또는 기타 클라우드/호스팅 서비스 공급자와 Visual Studio 구독과 같은 구독 프로그램을 통해서도 이용할 수 있습니다.

> [!Note]  
> **현재 반기 채널 릴리스는 Windows Server 버전 1809입니다**. 이 채널에 서버를 배치하려는 경우 Server Core 모드에서 또는 컨테이너에서 Nano 서버 실행으로 설치할 수 있는 Windows Server 버전 1809를 설치해야 합니다. Windows Server 2016에서 Windows Server 버전 1809로 현재 위치 업그레이드는 지원되지 않습니다. 두 버전이 **다른 릴리스 채널**에 있기 때문입니다. Windows Server 버전 1809는 Windows Server 2016에 대한 업데이트가 아니라 반기 채널의 다음 Windows Server 릴리스입니다.



이 모델에서는 Windows Server 릴리스는 릴리스의 연도 및 월에 의해 식별됩니다. 예를 들어 2017년에 9번째 달(9월)의 릴리스는 **버전 1709**로 식별됩니다. 반기 채널에서 Windows Server 릴리스는 연간 두 번 업데이트됩니다. 각 릴리스의 지원 수명 주기는 18개월입니다.

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>서버를 LTSC에 유지하거나 반기 채널로 이동시켜야 합니까?
다음과 같은 주요 차이점을 고려해야 합니다.

- 혁신에 박차를 가해야 합니까? 최신 Windows Server 기능을 먼저 이용해야 합니까? 릴리스 흐름이 빠른 하이브리드 응용 프로그램, DevOps 및 Hyper-V 패브릭을 지원해야 합니까? 이럴 경우 **Windows Server, 버전 1809**를 설치하여 **반기 채널에 가입**하는 방법을 고려해야 합니다. 이 항목에서 설명하는 것과 같이 1년에 두 번 새로운 버전을 받아보고 릴리스당 18개월 동안 프로덕션 환경에서 일반 지원을 받게 됩니다. 볼륨 라이선스, Azure 또는 Visual Studio 구독 서비스를 통해 이용이 가능합니다. 현재, 반기 채널의 릴리스들은 프로덕션 환경에서 제품을 실행하고자 할 경우 볼륨 라이선스와 Software Assurance가 필요합니다.
- 안정성과 예측 가능성이 필요합니까? VM 및 실제 서버의 기존 워크로드를 실행해야 합니까? 이러한 경우 **LTSC에 서버를 유지**하는 방법을 고려해야 합니다. 최신 LTSC 릴리스는 **Windows Server 2019**입니다. 이 항목에 설명된 대로, 2~3년마다 새로운 버전에 액세스할 수 있고 5년 동안 일반 지원을 받으며, 릴리스당 5년까지 지원 기간을 연장할 수 있습니다. LTSC 릴리스는 모든 릴리스 메커니즘을 통해 사용할 수 있습니다. LTSC 릴리스는 사용 중인 라이선스 모델에 관계 없이 모든 사용자에게 제공됩니다. 

다음 표에는 채널 간 주요 차이점이 요약되어 있습니다.

|  | 장기 서비스 채널(Windows Server 2019) |반기 채널(Windows Server) |
| ------------------- | ------------------------------------ | ------------------------------------------------- |
|권장 시나리오 | 일반 목적의 파일 서버, Microsoft 및 비 Microsoft 워크로드, 기존 앱, 인프라 역할, 소프트웨어 정의 데이터 센터 및 하이퍼 컨버지드 인프라 | 더 빠른 혁신을 통해 혜택을 얻는 컨테이너화된 응용 프로그램, 컨테이너 호스트 및 응용 프로그램 시나리오 |
| 새 릴리스 | 2~3년마다 |6개월마다 |
| 지원 |일반 지원 5년 + 연장 지원 5년 | 18개월 |
| 버전 | 모든 Windows Server 에디션 사용 가능 | Standard 및 Datacenter 에디션 |
| 사용할 수 있는 사람 | 모든 채널을 통한 모든 고객 | Software Assurance 및 클라우드 고객만 |
| 설치 옵션 | Server Core 및 데스크톱 환경 포함 서버 | 컨테이너 호스트 및 이미지 및 Nano 서버 컨테이너 이미지용 Server Core |                |


## <a name="device-compatibility"></a>디바이스 호환성
다른 전달 사항이 없는 한, 반기 채널 릴리스를 실행하기 위한 최소 하드웨어 요구 사항은 최신 버전의 Windows Server용 LTSC 릴리스와 동일합니다. 예를 들어, **현재 장기 서비스 채널 릴리스 Windows Server 2019**입니다. 대부분의 하드웨어 드라이버가 이러한 릴리스에서 계속 작동합니다.

## <a name="servicing"></a>서비스
LTSC 및 반기 채널 릴리스 모두 보안 업데이트와 비보안 업데이트에서 지원됩니다. 차이는 위에서 설명한 대로 릴리스가 지원되는 기간입니다.

### <a name="servicing-tools"></a>서비스 도구
IT 전문가가 Windows Server를 서비스하는 데 사용할 수 있는 도구가 많이 있습니다. 각 옵션에는 기능과 컨트롤부터 단순성과 낮은 관리 요구 사항에 이르는 장단점이 있습니다. 다음은 서비스 업데이트를 관리하는 데 사용할 수 있는 서비스 도구의 예입니다.

- **Windows 업데이트 (독립 실행형)**: 이 옵션은 인터넷에 연결 되어 있고 Windows 업데이트가 사용 하도록 설정 하는 서버에 사용할 수만 있습니다.
- **WSUS(Windows Server Update Services)** 는 Windows 10 및 Windows Server 업데이트에 대한 포괄적인 제어를 제공하며 Windows Server 운영 체제에서 기본적으로 사용 가능합니다. 업데이트 지연 기능 외에도 조직에서는 업데이트의 승인 계층을 추가하고 준비될 때마다 특정 컴퓨터나 컴퓨터 그룹에 업데이트를 배포하도록 선택할 수 있습니다.
- **System Center Configuration Manager**는 서비스에 대한 최상의 컨트롤을 제공합니다. IT 전문가가 업데이트를 지연하고 승인할 수 있으며, 배포의 대상을 지정하고 대역폭 사용 및 배포 시간을 관리하는 여러 옵션이 있습니다.

아마도 이미 리소스, 직원 및 전문성에 따라 이러한 옵션 중 하나를 사용하도록 선택했을 것입니다. 반기 채널 릴리스에도 같은 프로세스를 계속 사용할 수 있습니다. 예를 들어 이미 System Center Configuration Manager를 사용하여 업데이트를 관리한다면, 계속 사용할 수 있습니다. 마찬가지로 WSUS를 사용한다면, 계속 사용하면 됩니다.

## <a name="obtain-preview-releases-through-the-windows-insider-program"></a>Windows 참가자 프로그램을 통해 미리 보기 릴리스 얻기
Windows Server의 초기 빌드를 테스트하는 것은 릴리스 전에 가능한 문제를 발견할 수 있는 기회이기 때문에 Microsoft와 고객 모두에게 도움이 됩니다. 또한 고객이 제품의 기능에 직접 영향을 줄 수 있는 특별한 기회도 제공합니다. 

Microsoft는 개발 프로세스 전체 동안 피드백을 받아 최대한 빨리 조정될 수 있도록 합니다. 초기 테스트와 피드백은 신속한 릴리스 모델에 필수적입니다.

Windows 참가자 프로그램에 참여하는 방법에 대한 자세한 내용은 [서버용 Windows 참가자 프로그램 문서](https://docs.microsoft.com/windows-insider/at-work/)를 참조하십시오.

## <a name="to-identify-windows-server-2019-and-windows-server-version-1809"></a>Windows Server 2019 및 Windows Server 버전 1809 식별 방법

>[!Note]  
> 아래 지침은 수명 주기 및 일반 인벤토리만을 목적으로 하는 LTSC 및 SAC의 식별 및 차별화를 돕는 것입니다.  응용 프로그램 호환성 용도 또는 특정 API 표면을 나타내는 것을 목적으로 하지 않습니다.  앱 개발자는 지침을 활용하여 구성 요소로서의 호환성, API 및 기능이 시스템 수명 주기에 걸쳐 추가될 수 있거나 아직 추가될 수 없도록 해야 합니다. [운영 체제 버전](https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version)은 앱 개발자에게 있어 좋은 출발점입니다.

Powershell을 열고 Get-ItemProperty Cmdlet 또는 Get-ComputerInfo Cmdlet을 사용하여 레지스트리에서 속성을 확인합니다.  빌드 번호와 함께 브랜딩 연도(예: 2019)의 유무 여부에 따라 LTSC 또는 SAC가 표시됩니다.  LTSC에는 있고, SAC에는 없습니다.  ReleaseId 또는 WindowsVersion의 릴리스 시점(예: 1809)과 설치가 Server Core 또는 데스크톱 환경 포함 서버인지 여부를 반환합니다. 

**Windows Server 2019 Datacenter Edition (LTSC) 데스크톱 경험 예제:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server 2019 Datacenter
ReleaseId                 : 1809
InstallationType          : Server
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Windows Server, 버전 1809 (SAC) Standard Edition 서버 코어 예제:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server Standard
ReleaseId                 : 1809
InstallationType          : Server Core
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Windows Server 2019 Standard Edition (LTSC) Server Core 예제:**


````PowerShell
Get-ComputerInfo | Select WindowsProductName, WindowsVersion, WindowsInstallationType, OsServerLevel, OsVersion, OsHardwareAbstractionLayer
````

````
WindowsProductName            : Windows Server 2019 Standard
WindowsVersion                : 1809
WindowsInstallationType       : Server Core
OsServerLevel                 : ServerCore
OsVersion                     : 10.0.17763
OsHardwareAbstractionLayer    : 10.0.17763.107
````

새로운 [Server Core 앱 호환성 FOD](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19)가 서버에 존재하는지 여부를 쿼리하려면 [Get-WindowsCapability](https://docs.microsoft.com/powershell/module/dism/get-windowscapability?view=win10-ps) Cmdlet을 사용하고 다음을 찾으십시오.
````
Name    :     ServerCore.AppCompatibility~~~~0.0.1.0
State   :     Installed
````

# <a name="related-topics"></a>관련 항목
[Nano 서버에 Windows 서버 반기 채널 변경](../get-started/nano-in-semi-annual-channel.md)

[Windows Server 지원 수명 주기](https://support.microsoft.com/lifecycle)

[Server Core 실행 중인지 여부를 결정 합니다.](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo 함수](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[소프트웨어 인벤토리 로깅 Cmdlet](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
