---
title: 서비스 채널
description: 'Windows Server 서비스 채널 설명: LTSC 및 SAC'
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 05/21/2019
ms.openlocfilehash: 3d443ff123cc041196f59d93d156415c34bdf70f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947878"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server 서비스 채널: LTSC 및 SAC

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

Windows Server 고객, 장기 서비스 채널 및 반기 채널에 사용할 수 있는 두 기본 릴리스 채널이 있습니다.

장기 서비스 채널(LTSC)에서 서버를 유지하고, 사용자의 요구에 따라 반기 채널로 이동하거나, 두 트랙에 일부 서버를 보유할 수 있습니다.

## <a name="long-term-servicing-channel-ltsc"></a>장기 서비스 채널(LTSC)

이는 2~3년마다 새로운 Windows Server의 주 버전이 출시되는, 이미 여러분에게 친숙한 릴리스 모델(이전의 “장기 서비스 *분기*”라고 함)입니다. 사용자는 5년 동안 일반 지원을 받고 지원 기간을 5년 연장할 수 있습니다. 이 채널은 보다 장기적인 서비스 옵션과 기능적 안정성이 요구되는 시스템에 적절합니다. Windows Server 2016 이하 버전의 Windows Server 배포는 새로운 반기 채널 릴리스의 영향을 받지 않습니다. 장기 서비스 채널은 보안 및 비보안 업데이트를 계속해서 수신하지만, 새로운 기능은 수신하지 않습니다.

> [!Note]  
> **현재 LTSC 제품은 Windows Server 2019입니다**. 이 채널을 유지하고자 하는 경우 Windows Server 2019를 설치(또는 계속 사용)해야 하고, Server Core 설치 옵션 또는 Desktop 환경 포함 서버 설치 옵션으로 설치할 수 있습니다.

## <a name="semi-annual-channel"></a>반기 채널

반기 채널은 컨테이너 및 마이크로서비스에 빌드된 애플리케이션은 물론이고 소프트웨어 정의 하이브리드 데이터 센터에서 새로운 운영 체제 기능을 보다 신속하게 활용할 수 있도록 혁신에 박차를 가하고 있는 고객에게 가장 적합합니다. 반기 채널의 Windows Server 제품은 1년에 두 번, 봄과 가을에 새 릴리스가 제공됩니다. 이 채널의 각 릴리스는 최초 릴리스 후 18개월 동안 지원됩니다.

반기 채널에 도입된 대부분의 기능은 Windows Server의 차기 LTSC 릴리스로 롤업됩니다. 버전, 기능 및 지원 내용은 고객 피드백에 따라 릴리스마다 달라질 수 있습니다.

반기 채널은 [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx)가 포함된 볼륨 라이선스 고객에게 제공되며, Azure Marketplace 또는 기타 클라우드/호스팅 서비스 공급자와 Visual Studio 구독과 같은 구독 프로그램을 통해서도 이용할 수 있습니다.

> [!Note]  
> **현재 반기 채널 릴리스는 Windows Server 버전 1903입니다**. 이 채널에 서버를 배치하려는 경우 Server Core 모드에서 또는 컨테이너에서 Nano 서버 실행으로 설치할 수 있는 Windows Server 버전 1903을 설치해야 합니다. 장기 서비스 채널 릴리스는 **여러 릴리스 채널**에 있기 때문에 현재 위치 업그레이드가 지원되지 않습니다. 반기 채널 릴리스는 업데이트가 아니며, 반기 채널의 다음 Windows Server 릴리스입니다.

이 모델에서는 Windows Server 릴리스는 릴리스의 연도 및 월에 의해 식별됩니다. 예를 들어 2017년에 9번째 달(9월)의 릴리스는 **버전 1709**로 식별됩니다. 반기 채널에서 Windows Server 릴리스는 연간 두 번 업데이트됩니다. 각 릴리스의 지원 수명 주기는 18개월입니다.

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>서버를 LTSC에 유지하거나 반기 채널로 이동시켜야 합니까?

다음과 같은 주요 차이점을 고려해야 합니다.

- 혁신에 박차를 가해야 합니까? 최신 Windows Server 기능을 먼저 이용해야 합니까? 릴리스 흐름이 빠른 하이브리드 애플리케이션, DevOps 및 Hyper-V 패브릭을 지원해야 합니까? 이럴 경우 **Windows Server, 버전 1903**을 설치하여 **반기 채널에 가입**하는 방법을 고려해야 합니다. 이 항목에서 설명하는 것과 같이 1년에 두 번 새로운 버전을 받아보고 릴리스당 18개월 동안 프로덕션 환경에서 일반 지원을 받게 됩니다. 볼륨 라이선스, Azure 또는 Visual Studio Subscription 서비스를 통해 이용이 가능합니다. 현재, 반기 채널의 릴리스들은 프로덕션 환경에서 제품을 실행하고자 할 경우 볼륨 라이선스와 Software Assurance가 필요합니다.
- 안정성과 예측 가능성이 필요합니까? 가상 머신 및 실제 서버의 기존 워크로드를 실행해야 합니까? 이러한 경우 **LTSC에 서버를 유지**하는 방법을 고려해야 합니다. 최신 LTSC 릴리스는 **Windows Server 2019**입니다. 이 항목에 설명된 대로, 2~3년마다 새로운 버전에 액세스할 수 있고 5년 동안 일반 지원을 받으며, 릴리스당 5년까지 지원 기간을 연장할 수 있습니다. LTSC 릴리스는 모든 릴리스 메커니즘을 통해 사용할 수 있습니다. LTSC 릴리스는 사용 중인 라이선스 모델에 관계없이 모든 사용자에게 제공됩니다. 

다음 표에는 채널 간 주요 차이점이 요약되어 있습니다.


|                       |                                                              장기 서비스 채널(Windows Server 2019)                                                               |                                   반기 채널(Windows Server)                                   |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| 권장 시나리오 | 범용 파일 서버, Microsoft 및 비 Microsoft 워크로드, 기존 앱, 인프라 역할, 소프트웨어 정의 데이터 센터 및 하이퍼 컨버지드 인프라 | 더 빠른 혁신을 통해 혜택을 얻는 컨테이너화된 애플리케이션, 컨테이너 호스트 및 애플리케이션 시나리오 |
|     새 릴리스      |                                                                               2~3년마다                                                                                |                                              6개월마다                                              |
|        Support(지원)        |                                                       일반 지원 5년 + 연장 지원 5년                                                        |                                                18개월                                                 |
|       버전        |                                                                    모든 Windows Server 버전 사용 가능                                                                     |                                     Standard 및 Datacenter 버전                                     |
|      사용할 수 있는 사람      |                                                                      모든 채널을 통한 모든 고객                                                                      |                               Software Assurance 및 클라우드 고객만                                |
| 설치 옵션  |                                                                Server Core 및 데스크톱 환경 포함 서버                                                                |                 컨테이너 호스트 및 이미지 및 Nano 서버 컨테이너 이미지용 Server Core                 |

## <a name="device-compatibility"></a>디바이스 호환성

다른 전달 사항이 없는 한, 반기 채널 릴리스를 실행하기 위한 최소 하드웨어 요구 사항은 최신 버전의 Windows Server용 LTSC 릴리스와 동일합니다. 예를 들어, **현재 장기 서비스 채널 릴리스 Windows Server 2019**입니다. 대부분의 하드웨어 드라이버가 이러한 릴리스에서 계속 작동합니다.

## <a name="servicing"></a>서비스

LTSC 및 반기 채널 릴리스 모두 보안 업데이트와 비보안 업데이트에서 지원됩니다. 차이는 위에서 설명한 대로 릴리스가 지원되는 기간입니다.

### <a name="servicing-tools"></a>서비스 도구

IT 전문가가 Windows Server를 서비스하는 데 사용할 수 있는 도구가 많이 있습니다. 각 옵션에는 기능과 컨트롤부터 단순성과 낮은 관리 요구 사항에 이르는 장단점이 있습니다. 다음은 서비스 업데이트를 관리하는 데 사용할 수 있는 서비스 도구의 예입니다.

- **Windows 업데이트(독립 실행형)** : 이 옵션은 인터넷에 연결되어 있고 Windows 업데이트를 사용하도록 설정된 서버에만 사용할 수 있습니다.
- **WSUS(Windows Server Update Services)** 는 Windows 10 및 Windows Server 업데이트에 대한 포괄적인 제어를 제공하며 Windows Server 운영 체제에서 기본적으로 사용 가능합니다. 업데이트 지연 기능 외에도 조직에서는 업데이트의 승인 계층을 추가하고 준비될 때마다 특정 컴퓨터나 컴퓨터 그룹에 업데이트를 배포하도록 선택할 수 있습니다.
- **System Center Configuration Manager**는 서비스에 대한 최상의 컨트롤을 제공합니다. IT 전문가가 업데이트를 지연하고 승인할 수 있으며, 배포의 대상을 지정하고 대역폭 사용 및 배포 시간을 관리하는 여러 옵션이 있습니다.

아마도 이미 리소스, 직원 및 전문성에 따라 이러한 옵션 중 하나를 사용하도록 선택했을 것입니다. 반기 채널 릴리스에도 같은 프로세스를 계속 사용할 수 있습니다. 예를 들어 이미 System Center Configuration Manager를 사용하여 업데이트를 관리한다면, 계속 사용할 수 있습니다. 마찬가지로 WSUS를 사용한다면, 계속 사용하면 됩니다.

## <a name="where-to-obtain-semi-annual-channel-releases"></a>반기 채널 릴리스를 받을 수 있는 곳

반기 채널 릴리스는 새로 설치로 설치되어야 합니다.

- VLSC(볼륨 라이선스 서비스 센터): [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx)를 사용하는 볼륨 라이선스 고객은 [볼륨 라이선싱 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)로 이동하고 **로그인**을 클릭하여 이 릴리스를 받을 수 있습니다. 그런 다음, **다운로드 및 키**를 클릭하고 이 릴리스를 검색합니다. 

- 반기 채널 릴리스도 [Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview)에서 사용할 수 있습니다.

- Visual Studio 구독: Visual Studio 구독자는 [Visual Studio 구독자 다운로드 페이지](https://my.visualstudio.com/downloads?pid=2347)에서 반기 채널 릴리스를 다운로드할 수 있습니다. 이미 구독자가 아닌 경우 [Visual Studio 구독](https://www.visualstudio.com/subscriptions/) 페이지로 이동하고 가입한 다음, 위와 같이 [Visual Studio 구독자 다운로드 페이지](https://my.visualstudio.com/downloads?pid=2347)로 이동합니다. Visual Studio 구독을 통해 얻은 릴리스는 개발 및 테스트용으로만 사용됩니다.

- Windows 참가자 프로그램을 통해 미리 보기 릴리스 받기: Windows Server의 초기 빌드를 테스트하는 것은 릴리스 전에 가능한 문제를 발견할 수 있는 기회이기 때문에 Microsoft와 고객 모두에게 도움이 됩니다. 또한 고객이 제품의 기능에 직접 영향을 줄 수 있는 특별한 기회도 제공합니다.   
Microsoft는 개발 프로세스 전체 동안 피드백을 받아 최대한 빨리 조정될 수 있도록 합니다. 초기 테스트와 피드백은 신속한 릴리스 모델에 필수적입니다. Windows 참가자 프로그램에 참여하려면 [서버용 Windows 참가자 프로그램 문서](https://docs.microsoft.com/windows-insider/at-work/)를 참조하세요.

## <a name="activating-semi-annual-channel-releases"></a>반기 채널 릴리스 정품 인증

- Microsoft Azure를 사용하고 있는 경우에는 이 릴리스가 자동으로 정품 인증됩니다.
- 볼륨 라이선스 서비스 센터 또는 Visual Studio 구독에서 이 릴리스를 받은 경우 키 관리 시스템(KMS) 환경에서 Windows Server 2019 CSVLK를 사용하여 정품 인증할 수 있습니다. 자세한 내용은 [KMS 클라이언트 설정 키](../get-started/kmsclientkeys.md)를 참조하세요.

Windows Server 2019 이전에 출시된 반기 채널 릴리스는 Windows Server 2016 CSVLK를 사용합니다.

## <a name="why-do-semi-annual-channel-releases-offer-only-the-server-core-installation-option"></a>반기 채널 릴리스가 Server Core 설치 옵션만 제공하는 이유는 무엇입니까?

Windows Server의 각 릴리스를 계획할 때 중요한 단계 중 하나는 고객의 피드백을 듣는 것입니다. Windows Server를 어떻게 사용하고 계신가요? Windows Server 배포, 그리고 더 나아가 일상적인 비즈니스에 가장 큰 영향을 미치는 새 기능은 무엇인가요? 고객 피드백에 따르면 새로운 혁신 기술을 가급적 빠르고 효율적으로 제공하는 것이 최우선 과제입니다. 동시에 혁신 속도가 두드러지는 고객은 주로 PowerShell 명령줄 스크립팅을 사용하여 데이터 센터를 관리하므로, 데스크톱 환경 포함 Windows Server 설치 시 이용 가능한 데스크톱 GUI를 강하게 요구하진 않습니다. 특히 [Windows Admin Center](../manage/windows-admin-center/overview.md)를 이용해 서버를 원격으로 관리하게 된 후로는 더더욱 그러합니다.

Server Core 설치 옵션에 집중함으로써 기존 Windows Server 플랫폼 기능 및 애플리케이션 호환성을 유지하면서 더 많은 리소스를 새로운 혁신에 제공할 수 있습니다. 이에 관한 문제 또는 Windows Server 및 향후 릴리스에 관한 다른 피드백이 있는 경우 [피드백 허브](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)를 통해 의견이나 제안 사항을 보낼 수 있습니다.

## <a name="what-about-nano-server"></a>Nano 서버는 어떤가요?

Nano 서버는 반기 채널에서 컨테이너 운영 체제로 이용 가능합니다. 자세한 내용은 [Windows Server 반기 채널 내 Nano 서버 변경 사항](../get-started/nano-in-semi-annual-channel.md)을 참조하세요.

## <a name="how-to-tell-whether-a-server-is-running-an-ltsc-or-sac-release"></a>서버가 LTSC 또는 SAC 릴리스 중 무엇을 실행 중인지 확인하는 방법

일반적으로 장기 서비스 채널 릴리스(예: Windows Server 2019)는 반기 채널의 새 버전(예: Windows Server, 버전 1809)과 동시에 출시됩니다. 따라서 서버가 반기 채널 릴리스를 실행 중인지 확인하기가 약간 까다로울 수 있습니다. 빌드 번호를 확인하는 대신 제품 이름을 확인해야 합니다. 반기 채널 릴리스는 버전 번호 없이 "Windows Server Standard" 또는 "Windows Server Datacenter" 제품 이름을 사용하지만 장기 서비스 채널 릴리스에는 버전 번호가 포함됩니다(예: "Windows Server 2019 Datacenter").

>[!Note]  
> 아래 지침은 수명 주기 및 일반 인벤토리만을 목적으로 하는 LTSC 및 SAC의 식별 및 차별화를 돕는 것입니다.  애플리케이션 호환성 용도 또는 특정 API 표면을 나타내는 것을 목적으로 하지 않습니다.  앱 개발자는 지침을 활용하여 구성 요소로서의 호환성, API 및 기능이 시스템 수명 주기에 걸쳐 추가될 수 있거나 아직 추가될 수 없도록 해야 합니다. [운영 체제 버전](https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version)은 앱 개발자에게 있어 좋은 출발점입니다.

PowerShell을 열고 Get-ItemProperty Cmdlet 또는 Get-ComputerInfo Cmdlet을 사용하여 레지스트리에서 속성을 확인합니다.  빌드 번호와 함께 브랜딩 연도(예: 2019)의 유무 여부에 따라 LTSC 또는 SAC가 표시됩니다.  LTSC에는 있고, SAC에는 없습니다.  ReleaseId 또는 WindowsVersion의 릴리스 시점(예: 1809)과 설치가 Server Core 또는 데스크톱 환경 포함 서버인지 여부를 반환합니다. 

**데스크톱 환경 포함 Windows Server 2019 Datacenter Edition(LTSC) 예시:**

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

**Windows Server 버전 1809(SAC) Standard Edition Server Core 예시:**

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

**Windows Server 2019 Standard Edition(LTSC) Server Core 예시:**


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

새로운 [Server Core 앱 호환성 FOD](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19)가 서버에 존재하는지 여부를 쿼리하려면 [Get-WindowsCapability](https://docs.microsoft.com/powershell/module/dism/get-windowscapability?view=win10-ps) Cmdlet을 사용하고 다음을 찾으세요.
````
Name    :     ServerCore.AppCompatibility~~~~0.0.1.0
State   :     Installed
````

## <a name="see-also"></a>참고 항목

[Windows Server 반기 채널의 Nano 서버 변경 사항](../get-started/nano-in-semi-annual-channel.md)

[Windows Server 지원 수명 주기](https://support.microsoft.com/lifecycle)

[Server Core가 실행 중인지 여부 확인](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo 함수](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[소프트웨어 인벤토리 로깅 Cmdlet](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
