---
title: Server Core 관리
description: Windows Server의 Server Core 설치를 관리 하는 방법을 설명 합니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 6836e5db36727294d215f7f98e0faeede55a612a
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1718713"
---
# <a name="manage-a-server-core-server"></a>Server Core 서버 관리
 
> 적용 대상: Windows Server (세미콜론 연간 회의 채널) 및 Windows Server 2016

다음과 같은 방법으로의 Server Core 서버를 관리할 수 있습니다.
- [Windows 관리 센터](../../manage/windows-admin-center/overview.md) 를 사용 하 여
- Windows 10에서 실행 되는 [원격 서버 관리 도구](../../remote/remote-server-administration-tools.md) 를 사용 하 여
- 로컬 및 원격 Windows PowerShell을 사용 하 여
- [서버 관리자](../server-manager/server-manager.md) 를 사용 하 여 원격으로
- [MMC 스냅인](#managing-with-microsoft-management-console) 사용 하 여 원격으로
- [원격 데스크톱 서비스](#managing-with-remote-desktop-services) 와 원격으로

도 하드웨어를 추가 하 고 명령줄에서 이렇게으로 드라이버를 로컬로,를 관리할 수 있습니다.

일부 중요 한 제한 사항 및 Server Core를 사용 하 여 작업할 때 주의 해야할 팁 가지가 있습니다.

- 모든 명령 프롬프트 창을 닫아야 하 고 새 명령 프롬프트 창을 열고 하려면 수 작업을 수행 하는 작업 관리자에서. **CTRL\ + ALT\ + DELETE**를, **작업 관리자 시작**을 클릭 하 고, 클릭 **자세한 내용 > 파일 > 실행**, 하 고 **cmd.exe**를 입력 합니다. ( **Powershell.exe** PowerShell 명령 창을 열 수를 입력 합니다.) 또는 로그 아웃 한 다음 다시 로그인 수 있습니다.
- 모든 명령 또는 Windows 탐색기를 시작 하려고 하는 도구 작동 하지 않습니다. 예를 실행 하 **시작.** 명령 프롬프트에서 작동 하지 않습니다.
- HTML 렌더링 또는 Server Core에서 HTML 도움말에 대 한 지원은 없습니다.
- Server Core Windows Installer 파일에서 도구 및 유틸리티를 설치할 수 있도록 자동 모드에서 Windows Installer를 지원 합니다. Server Core에서 Windows Installer 패키지를 설치할 때 기본 사용자 인터페이스를 표시 하 **는 /qb** 옵션을 사용 합니다.
- 표준 시간대를 변경 하려면 **집합 날짜**를 실행 합니다.
- 국가별 설정을 변경 하려면 **컨트롤 intl.cpl**를 실행 합니다.
- **Control.exe** 실행 되지 않음 해당 합니다. **Timedate.cpl** 또는 **Intl.cpl**중 하나를 실행 해야 합니다.
- **Winver.exe** Server Core에서 사용할 수 없습니다. 버전 정보를 가져오려면 **Systeminfo.exe**를 사용 합니다.

## <a name="managing-server-core-with-windows-admin-center"></a>Windows 관리 센터와 Server Core 관리
[Windows 관리 센터](../../manage/windows-admin-center/overview.md) 는 온-프레미스 없는 Azure 또는 클라우드 의존 관계와 Windows 서버 관리를 사용 하도록 설정 하는 브라우저 기반 관리 응용 프로그램입니다. Windows 관리 센터 서버 인프라의 모든 측면에 대해 모든 권한을 제공 하 고 인터넷에 연결 되지 않은 개인 네트워크에서 관리를 위한 특히 유용 합니다. Windows 10, 게이트웨이 서버 또는 데스크톱 경험을 갖춘 Windows Server의 설치에 Windows 관리 센터를 설치할 수 있으며 관리 하려는 서버 핵심 시스템에 연결 합니다.

## <a name="managing-server-core-remotely-with-server-manager"></a>Server Core 원격으로 서버 관리자와 함께 관리

서버 관리자는 프로 비전 하 고 서버에 대 한 물리적 액세스 또는 원격 데스크톱 프로토콜 (RDP)를 사용 하도록 설정할 필요가 없이 사용자 데스크톱에서 로컬 및 원격 Windows 기반 서버를 관리 하는데 도움이 되는 Windows Server의 관리 콘솔 각 서버에 연결 합니다. 서버 관리자는 원격, 다중 서버 관리를 지원합니다.

원격 서버에서 실행 되는 서버 관리자가 관리 하 여 로컬 서버를 사용 하도록 설정 하려면 Windows PowerShell cmdlet을 실행 **구성 SMRemoting.exe – 사용**합니다.

## <a name="managing-with-microsoft-management-console"></a>Microsoft Management Console을 사용 하 여 관리

Server Core 서버를 관리 하려면 많은 스냅인에 대 한 관리 콘솔 MMC (Microsoft)를 원격으로 사용할 수 있습니다.

사용 하려면 MMC 스냅인을 사용 하는 도메인 구성원 인 Server Core 서버를 관리 하려면: 

1. MMC 스냅인을 같은 컴퓨터 관리를 시작 합니다.
2. 스냅인을 마우스 오른쪽 단추로 클릭 하 고 **다른 컴퓨터에 연결**을 클릭 합니다.
2. Server Core 서버의 컴퓨터 이름을 입력 한 다음 **확인**을 클릭 합니다. 이제 다른 PC 또는 서버와 마찬가지로 Server Core 서버를 관리 하려면 MMC 스냅인을 사용 하 여 사용할 수 있습니다.

Server Core 서버를 관리 하는 MMC 스냅인을 사용 하려면 즉 *하지* 도메인 구성원: 

1. 원격 컴퓨터에서 명령 프롬프트에서 다음 명령을 입력 하 여 Server Core 컴퓨터에 연결 하는데 사용할 대체 자격 증명을 설정 합니다.
   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```
   암호를 묻는 메시지가 표시 하려는 경우 **** 전달/옵션을 생략 합니다.

2. 대화 상자가 나타나면 지정한 사용자 이름에 대 한 암호를 입력 합니다.
   Server Core 서버에서 방화벽 MMC 스냅인과 연결할 수 있도록 아직 구성 되지 않은 경우 MMC 스냅인을 허용 하도록 Windows 방화벽을 구성 하려면 다음 단계를 수행 합니다. 3 단계를 계속 합니다.
3. 다른 컴퓨터에는 MMC 스냅인을 같은 **컴퓨터 관리**를 시작 합니다.
4. 왼쪽된 창에서 스냅인을 마우스 오른쪽 단추로 클릭 하 고 **다른 컴퓨터에 연결**을 클릭 합니다. (등 컴퓨터 관리 예제에서는 마우스 오른쪽 단추로 클릭할 **컴퓨터 관리 (로컬)** 입니다.)
5. **다른 컴퓨터**Server Core 서버의 컴퓨터 이름을 입력 한 다음 **확인**을 클릭 합니다. 이제 MMC 스냅인을 사용 하는 Windows Server 운영 체제를 실행 하는 다른 모든 컴퓨터의 경우와 마찬가지로 Server Core 서버를 관리 하는데 사용할 수 있습니다.

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>MMC 스냅인 (s) 연결을 허용 하도록 Windows 방화벽을 구성 하려면
모든 MMC 스냅인과 연결을 허용 하려면 다음 명령을 실행 합니다.

```
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

특정 MMC 스냅인만 연결을 허용 하려면 다음을 실행 합니다.
```
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

여기서 *rulegroup* 은 연결 하려는 스냅인에 따라 다음 중 하나입니다.

| MMC 스냅인                            | 규칙 그룹                                            |
|----------------------------------------|-------------------------------------------------------|
| 이벤트 뷰어                           | 원격 이벤트 로그 관리                           |
| Services                               | 원격 서비스 관리                             |
| 공유 폴더                         | 파일 및 프린터 공유                              |
| 작업 스케줄러                         | 성능 로그 및 알림, 파일 및 프린터 공유 |
| 디스크 관리                        | 원격 볼륨 관리                              |
| Windows 방화벽 및 고급 보안 | Windows 방화벽에 대 한 원격 관리                    |


> [!NOTE] 
> 일부 MMC 스냅인 방화벽을 통해 연결을 허용 하는 해당 규칙 그룹이 필요는 없습니다. 이벤트 뷰어, 서비스 또는 공유 폴더에 대 한 규칙 그룹을 사용 하면 대부분의 다른 스냅인과 연결할 수 있도록 됩니다. 
>
> 또한 특정 스냅인 추가 전에 구성을 해야 Windows 방화벽을 통해 연결할 수 있습니다.
>
> - 디스크 관리 합니다. 먼저 Server Core 컴퓨터에서 가상 디스크 서비스 (VDS)를 시작 해야 합니다. 또한 MMC 스냅인을 사용 하 여 실행 중인 컴퓨터에서 디스크 관리 규칙을 적절 하 게 구성 해야 있습니다.
> - IP 보안 모니터 합니다. 이 스냅인의 원격 관리를 사용 하려면 먼저 해야 합니다. **Cscript \windows\system32\scregedit.wsf /im 1** 확인 하려면 명령 프롬프트에서 입력
> - 안정성 및 성능입니다. 스냅인에서 구성이 필요 하지 않습니다 더 이상, 하지만 Server Core 컴퓨터를 모니터링 하려면이 옵션을 사용할 때 성능 데이터를만 모니터링할 수 있습니다. 안정성 데이터를 사용할 수 없습니다.

## <a name="managing-with-remote-desktop-services"></a>원격 데스크톱 서비스를 사용 하 여 관리

원격 컴퓨터에서 Server Core 서버를 관리 하려면 [원격 데스크톱](../../remote/remote-desktop-services/welcome-to-rds.md) 을 사용할 수 있습니다.

Server Core에 액세스 하기 전에 다음 명령을 실행 해야 합니다. 
```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```
이 통해 관리 모드에 대 한 원격 데스크톱 연결을 수락 하도록 합니다.

## <a name="add-hardware-and-manage-drivers-locally"></a>하드웨어를 추가 하 고 드라이버를 로컬로 관리 합니다.

하드웨어에 Server Core 서버를 추가 하려면 새 하드웨어를 설치 하기 위한 하드웨어 공급 업체에서 제공 하는 지침을 따릅니다. 

하드웨어 플러그앤플레이 하지 않으면 드라이버를 수동으로 설치에 필요 합니다. 이렇게 하려면 드라이버 파일을 서버에서 임시 위치에 복사 하 고 다음 명령을 실행 하.
```
pnputil –i –a <driverinf>
```
여기서 *driverinf* 은 드라이버에 대 한.inf 파일의 파일 이름입니다.

메시지가 표시 되 면 컴퓨터를 다시 시작 합니다.

어떤 드라이버를 설치를 보려면 다음 명령을 실행 합니다. 
```
sc query type= driver
```

> [!NOTE] 
> 성공적으로 완료 하려면 명령에 대 한 등호 뒤 간격을 포함 해야 합니다.

장치 드라이버를 사용 하지 않으려면 다음을 실행 합니다. 
```
sc delete <service_name>
```

여기서 *미러링* 을는 실행 했을 때 얻은 하는 서비스의 이름을 **sc 쿼리 유형 드라이버 =** 합니다.