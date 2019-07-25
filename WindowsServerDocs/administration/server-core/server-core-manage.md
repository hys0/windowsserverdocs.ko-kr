---
title: Server Core 관리
description: Windows Server의 Server Core 설치를 관리 하는 방법 알아보기
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 07/23/2019
ms.openlocfilehash: bbb04e761dbb1dd48d95e15d11c91608f4d6c240
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476543"
---
# <a name="manage-a-server-core-server"></a>Server Core 서버 관리
 
> 적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

다음과 같은 방법으로 Server Core 서버를 관리할 수 있습니다.
- [Windows 관리 센터](../../manage/windows-admin-center/overview.md) 사용
- Windows 10에서 실행 되는 [원격 서버 관리 도구](../../remote/remote-server-administration-tools.md) 사용
- Windows PowerShell을 사용하여 로컬 및 원격으로
- 원격으로 [서버 관리자](../server-manager/server-manager.md) 사용
- [MMC 스냅인](#managing-with-microsoft-management-console) 을 사용 하 여 원격으로
- 원격으로 [원격 데스크톱 서비스](#managing-with-remote-desktop-services)

또한 명령줄에서 하드웨어를 추가 하 고 드라이버를 로컬로 관리할 수 있습니다.

Server Core로 작업할 때 유의 해야 할 몇 가지 중요 한 제한 사항과 팁이 있습니다.

- 모든 명령 프롬프트 창을 닫고 새로운 명령 프롬프트 창을 열려면 작업 관리자에서 수행할 수 있습니다. **Ctrl\+ALT\+delete**를 누르고 **작업 관리자 시작**, **자세한 내용 > 파일 > 실행**을 차례로 클릭 한 다음 **cmd.exe**를 입력 합니다. Powershell 명령 창을 열려면 **debug.exe** 를 입력 합니다. 또는 로그 아웃 한 다음 다시 로그인 할 수 있습니다.
- Windows Explorer를 시작하려는 모든 명령이나 도구는 작동하지 않습니다. 예를 들어 start를 실행 **합니다.** 명령 프롬프트에서가 작동 하지 않습니다.
- Server Core에서는 HTML 렌더링 이나 HTML 도움말이 지원 되지 않습니다.
- Server Core는 Windows Installer 파일에서 도구와 유틸리티를 설치할 수 있도록 자동 모드의 Windows Installer을 지원 합니다. Server Core에 Windows Installer 패키지를 설치 하는 경우 **/qb** 옵션을 사용 하 여 기본 사용자 인터페이스를 표시 합니다.
- 표준 시간대를 변경 하려면 **설정 날짜**를 실행 합니다.
- 국가별 설정을 변경 하려면 **control**을 실행 합니다.
- **컨트롤** 은 자체적으로 실행 되지 않습니다. 이 파일은 **Timedate .cpl** **또는 node.js**를 사용 하 여 실행 해야 합니다.
- **Winver** 는 Server Core에서 사용할 수 없습니다. 버전 정보를 가져오려면 **printbrm.exe**를 사용 합니다.

## <a name="managing-server-core-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 Server Core 관리
[Windows Admin Center](../../manage/windows-admin-center/overview.md)는 Azure 또는 클라우드 종속성 없이 Windows Server의 온-프레미스 관리를 지원하는 브라우저 기반 관리 앱입니다. Windows Admin Center는 서버 인프라의 모든 측면에 대한 완전한 권한을 부여하며 특히 인터넷에 연결되지 않은 개인 네트워크의 관리에 유용합니다. Windows 10, 게이트웨이 서버 또는 데스크톱 경험을 사용 하는 Windows Server 설치에서 windows 관리 센터를 설치 하 고 관리 하려는 Server Core 시스템에 연결할 수 있습니다.

## <a name="managing-server-core-remotely-with-server-manager"></a>서버 관리자를 사용 하 여 원격으로 Server Core 관리

서버 관리자는 서버에 물리적으로 액세스 하거나 RDP (원격 데스크톱 프로토콜)를 사용 하도록 설정 하지 않고도 데스크톱에서 로컬 및 원격 Windows 기반 서버를 프로 비전 하 고 관리 하는 데 도움이 되는 Windows Server의 관리 콘솔입니다. 각 서버에 대 한 연결입니다. 서버 관리자은 원격 다중 서버 관리를 지원 합니다.

원격 서버에서 실행 되는 서버 관리자에서 로컬 서버를 관리할 수 있도록 하려면 Windows PowerShell cmdlet **configure-smremoting.exe – enable**을 실행 합니다.

## <a name="managing-with-microsoft-management-console"></a>Microsoft Management Console을 사용 하 여 관리

MMC (Microsoft Management Console) 용 대부분의 스냅인을 원격으로 사용 하 여 Server Core 서버를 관리할 수 있습니다.

MMC 스냅인을 사용 하 여 도메인 구성원 인 Server Core 서버를 관리 하려면 다음을 수행 합니다. 

1. MMC 스냅인 (예: 컴퓨터 관리)을 시작 합니다.
2. 스냅인을 마우스 오른쪽 단추로 클릭 한 다음 **다른 컴퓨터에 연결**을 클릭 합니다.
2. Server Core 서버의 컴퓨터 이름을 입력 하 고 **확인**을 클릭 합니다. 이제 다른 PC 또는 서버와 마찬가지로 MMC 스냅인을 사용 하 여 Server Core 서버를 관리할 수 있습니다.

MMC 스냅인을 사용 하 여 도메인 구성원이 *아닌* server Core 서버를 관리 하려면 다음을 수행 합니다. 

1. 원격 컴퓨터의 명령 프롬프트에서 다음 명령을 입력 하 여 Server Core 컴퓨터에 연결 하는 데 사용할 대체 자격 증명을 설정 합니다.

   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```

   암호를 묻는 메시지를 표시 하려면 **/pass** 옵션을 생략 합니다.

2. 메시지가 표시 되 면 지정한 사용자 이름의 암호를 입력 합니다.
   Server Core 서버의 방화벽이 MMC 스냅인의 연결을 허용 하도록 아직 구성 되지 않은 경우 아래 단계를 수행 하 여 MMC 스냅인을 허용 하도록 Windows 방화벽을 구성 합니다. 그런 다음 3 단계를 계속 합니다.
3. 다른 컴퓨터에서 MMC 스냅인 (예: **컴퓨터 관리**)을 시작 합니다.
4. 왼쪽 창에서 스냅인을 마우스 오른쪽 단추로 클릭 한 다음 **다른 컴퓨터에 연결**을 클릭 합니다. 예를 들어 컴퓨터 관리 예제에서는 **컴퓨터 관리 (로컬)** 를 마우스 오른쪽 단추로 클릭 합니다.
5. **다른 컴퓨터**에 server Core 서버의 컴퓨터 이름을 입력 하 고 **확인**을 클릭 합니다. 이제 Windows Server 운영 체제를 실행하는 다른 컴퓨터와 마찬가지로 MMC 스냅인을 사용하여 Server Core 서버를 관리할 수 있습니다.

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>MMC 스냅인의 연결을 허용하도록 Windows 방화벽을 구성하려면
모든 MMC 스냅인의 연결을 허용 하려면 다음 명령을 실행 합니다.

```PowerShell
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

특정 MMC 스냅인의 연결만 허용 하려면 다음을 실행 합니다.

```PowerShell
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

여기서 *rulegroup* 은 연결 하려는 스냅인에 따라 다음 중 하나입니다.

| MMC 스냅인                            | 규칙 그룹                                            |
| ---------------------------------------- | ------------------------------------------------------- |
| 이벤트 뷰어                           | 원격 이벤트 로그 관리                           |
| 서비스                               | 원격 서비스 관리                             |
| 공유 폴더                         | 파일 및 프린터 공유                              |
| 작업 스케줄러                         | 성능 로그 및 경고, 파일 및 프린터 공유 |
| 디스크 관리                        | 원격 볼륨 관리                              |
| Windows 방화벽 및 고급 보안 | Windows 방화벽 원격 관리                    |


> [!NOTE] 
> 일부 MMC 스냅인은 방화벽을 통해 연결할 수 있는 해당 규칙 그룹을 포함 하지 않습니다. 이벤트 뷰어, 서비스 또는 공유 폴더에 대한 규칙 그룹을 사용하도록 설정하면 대부분의 다른 스냅인의 연결을 허용합니다. 
>
> 또한 방화벽을 통해 연결하려면 추가 구성이 필요한 스냅인도 있습니다.
>
> - 디스크 관리. 먼저 Server Core 컴퓨터에서 VDS(가상 디스크 서비스)를 시작해야 합니다. MMC 스냅인을 실행하는 컴퓨터에서 디스크 관리 규칙도 절적하게 구성해야 합니다.
> - IP 보안 모니터. 먼저 이 스냅인의 원격 관리를 사용하도록 설정해야 합니다. 이렇게 하려면 명령 프롬프트에서 **Cscript \windows\system32\scregedit.wsf/im 1** 을 입력 합니다.
> - 안정성 및 성능. 스냅인을 위해 추가 구성이 필요하지 않지만, 스냅인을 사용하여 Server Core 컴퓨터를 모니터링할 경우 성능 데이터만 모니터링할 수 있습니다. 안정성 데이터는 사용할 수 없습니다.

## <a name="managing-with-remote-desktop-services"></a>원격 데스크톱 서비스로 관리

원격 [데스크톱](../../remote/remote-desktop-services/welcome-to-rds.md) 을 사용 하 여 원격 컴퓨터에서 server Core 서버를 관리할 수 있습니다.

Server Core에 액세스 하려면 다음 명령을 실행 해야 합니다. 

```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```

그러면 관리용 원격 데스크톱 모드에서 연결을 수락합니다.

## <a name="add-hardware-and-manage-drivers-locally"></a>로컬로 하드웨어 추가 및 드라이버 관리

Server Core 서버에 하드웨어를 추가 하려면 하드웨어 공급 업체에서 제공 하는 지침에 따라 새 하드웨어를 설치 합니다. 

하드웨어가 플러그 앤 플레이를 수행 하지 않는 경우 드라이버를 수동으로 설치 해야 합니다. 이렇게 하려면 드라이버 파일을 서버의 임시 위치에 복사 하 고 다음 명령을 실행 합니다.

```
pnputil –i –a <driverinf>
```

여기서 *driverinf* 는 드라이버에 대 한 .inf 파일의 파일 이름입니다.

메시지가 표시되면 컴퓨터를 다시 시작합니다.

설치 된 드라이버를 확인 하려면 다음 명령을 실행 합니다. 

```
sc query type= driver
```

> [!NOTE] 
> 명령이 완료되려면 등호 뒤에 공백을 포함해야 합니다.

장치 드라이버를 사용 하지 않도록 설정 하려면 다음을 실행 합니다.

```
sc delete <service_name>
```

여기서 *service_name* 은 **sc query type = driver**를 실행할 때 가져온 서비스의 이름입니다.