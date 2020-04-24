---
title: 일반 원격 데스크톱 연결 문제 해결
description: 원격 데스크톱 연결과 관련된 "클래스가 등록되지 않았습니다" 오류를 해결합니다.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 03c3c8daa8dc4bea0e03ed285a98401f91cdf1cb
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857216"
---
# <a name="general-remote-desktop-connection-troubleshooting"></a>일반 원격 데스크톱 연결 문제 해결

원격 데스크톱 클라이언트에서 원격 데스크톱에 연결할 수 없지만 원인을 파악하는 데 도움이 되는 메시지 또는 다른 증상이 제공되지 않는 경우 다음 단계를 사용합니다.

## <a name="check-the-status-of-the-rdp-protocol"></a>RDP 프로토콜의 상태 확인

### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>로컬 컴퓨터의 RDP 프로토콜 상태 확인

로컬 컴퓨터의 RDP 프로토콜 상태를 확인하고 변경하려면 [원격 데스크톱을 사용하도록 설정하는 방법](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)을 참조하세요.

> [!NOTE]  
> 원격 데스크톱 옵션을 사용할 수 없는 경우 [그룹 정책 개체가 RDP를 차단하고 있는지 확인](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)을 참조하세요.

### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>원격 컴퓨터의 RDP 프로토콜 상태 확인

> [!IMPORTANT]  
> 이 섹션의 지침은 주의 깊게 수행해야 합니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 문제가 발생하는 경우에 대비하여 복원할 수 있도록 레지스트리 수정을 시작하기 전에 해당 [레지스트리를 백업](https://support.microsoft.com/help/322756)하세요.

원격 컴퓨터의 RDP 프로토콜 상태를 확인하고 변경하려면 네트워크 레지스트리 연결을 사용합니다.

1. 먼저 **시작** 메뉴로 이동한 다음, **실행**을 선택합니다. 표시되는 텍스트 상자에서 **regedt32**를 입력합니다.
2. 레지스트리 편집기에서 **파일**을 선택한 다음, **네트워크 레지스트리 연결**을 선택합니다.
3. **컴퓨터 선택** 대화 상자에서 원격 컴퓨터의 이름을 입력하고 **이름 확인**을 선택한 다음, **확인**을 선택합니다.
4. **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**로 이동합니다.  
   ![fDenyTSConnections 항목을 표시하는 레지스트리 편집기](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - **fDenyTSConnections** 키 값이 **0**이면 RDP를 사용할 수 있습니다.
   - **fDenyTSConnections** 키 값이 **1**이면 RDP를 사용할 수 없습니다.
5. RDP를 사용하려면 **fDenyTSConnections** 값을 **1**에서 **0**으로 변경합니다.

### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>GPO(그룹 정책 개체)가 로컬 컴퓨터의 RDP를 차단하고 있는지 확인합니다.

사용자 인터페이스에서 RDP를 켤 수 없거나 **fDenyTSConnections** 값을 변경한 후에 **1**로 되돌리면 GPO에서 컴퓨터 수준 설정을 재정의할 수 있습니다.

로컬 컴퓨터의 그룹 정책 구성을 확인하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력합니다.

```cmd
gpresult /H c:\gpresult.html
```

이 명령이 완료된 후 gpresult.html 파일을 엽니다. **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결**에서 **Allow users to connect remotely by using Remote Desktop Services**(원격 데스크톱 서비스를 사용한 원격 연결 허용) 정책을 찾습니다.

- 이 정책을 **사용**으로 설정하면 그룹 정책에서 RDP 연결을 차단하지 않습니다.
- 이 정책이 **사용 안 함**으로 설정된 경우 **최우선 GPO**를 확인합니다. 이것이 바로 RDP 연결을 차단하는 GPO입니다.
  ![도메인 수준 GPO **RDP 차단**이 RDP를 차단하는 gpresult.html 세그먼트 예제](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![**로컬 그룹 정책**이 RDP를 차단하는 gpresult.html 세그먼트 예제](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>GPO가 원격 컴퓨터의 RDP를 차단하는지 확인

원격 컴퓨터의 그룹 정책 구성을 확인하는 명령은 로컬 컴퓨터와 거의 동일합니다.

```cmd
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```

이 명령이 생성하는 파일(**gpresult-\<컴퓨터 이름\>.html**)은 로컬 컴퓨터 버전(**gpresult.html**)이 사용하는 것과 동일한 정보 형식을 사용합니다.

### <a name="modifying-a-blocking-gpo"></a>차단 GPO 수정

GPE(그룹 정책 개체 편집기) 및 GPM(그룹 정책 관리 콘솔)에서 이러한 설정을 수정할 수 있습니다. 그룹 정책을 사용하는 방법에 대한 자세한 내용은 [고급 그룹 정책 관리](https://docs.microsoft.com/microsoft-desktop-optimization-pack/agpm/)를 참조하세요.

차단 정책을 수정하려면 다음 방법 중 하나를 사용합니다.

- GPE에서 적절한 GPO 수준(예: 로컬 또는 도메인)에 액세스하고, **컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소** > **원격 데스크톱 서비스** > **원격 데스크톱 세션 호스트** > **연결** > **Allow users to connect remotely by using Remote Desktop Services**(원격 데스크톱 서비스를 사용한 원격 연결 허용) 정책으로 이동합니다.  
   1. 정책을 **사용** 또는 **구성되지 않음**으로 설정합니다.
   2. 영향을 받는 컴퓨터에서 관리자 권한으로 명령 프롬프트 창을 열고, **gpupdate /force** 명령을 실행합니다.
- GPM에서 차단 정책이 영향을 받는 컴퓨터에 적용되는 OU(조직 구성 단위)로 이동한 다음, 해당 OU의 정책을 삭제합니다.

## <a name="check-the-status-of-the-rdp-services"></a>RDP 서비스의 상태 확인

로컬(클라이언트) 컴퓨터와 원격(대상) 컴퓨터에서 다음 서비스가 실행 중이어야 합니다.

- 원격 데스크톱 서비스(TermService)
- 원격 데스크톱 서비스 UserMode 포트 리디렉터(UmRdpService)

서비스 MMC 스냅인을 사용하여 로컬로 또는 원격으로 서비스를 관리할 수 있습니다. 또한 PowerShell을 사용하여 서비스를 로컬 또는 원격으로 관리할 수도 있습니다(원격 컴퓨터가 원격 PowerShell cmdlet을 허용하도록 구성된 경우).

![서비스 MMC 스냅인의 원격 데스크톱 서비스. 기본 서비스 설정을 수정하지 마세요.](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

두 컴퓨터 중 하나 또는 둘 다 실행되고 있지 않으면 해당 컴퓨터를 시작합니다.

> [!NOTE]  
> 원격 데스크톱 서비스를 시작할 때 원격 데스크톱 서비스 UserMode 포트 리디렉터 서비스를 자동으로 다시 시작하도록 **예**를 클릭합니다.

## <a name="check-that-the-rdp-listener-is-functioning"></a>RDP 수신기가 작동하는지 확인

> [!IMPORTANT]  
> 이 섹션의 지침은 주의 깊게 수행해야 합니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 문제가 발생하는 경우에 대비하여 복원할 수 있도록 레지스트리 수정을 시작하기 전에 해당 [레지스트리를 백업](https://support.microsoft.com/help/322756)하세요.

### <a name="check-the-status-of-the-rdp-listener"></a>RDP 수신기의 상태 확인

이 절차에서는 관리자 권한이 있는 PowerShell 인스턴스를 사용합니다. 로컬 컴퓨터의 경우 관리자 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 그러나 동일한 cmdlet이 로컬 및 원격으로 작동하므로 이 절차에서는 PowerShell를 사용합니다.

1. 원격 컴퓨터에 연결하려면 다음 cmdlet을 실행합니다.

   ```powershell
   Enter-PSSession -ComputerName <computer name>
   ```

2. **qwinsta**를 입력합니다. 
    ![qwinsta 명령은 컴퓨터의 포트에서 수신 대기하는 프로세스를 나열합니다.](../media/troubleshoot-remote-desktop-connections/WPS_qwinsta.png)
3. 목록에 상태가 **수신 대기**인 **rdp-tcp**가 포함된 경우 RDP 수신기가 작동합니다. [RDP 수신기 포트 확인](#check-the-rdp-listener-port)을 진행합니다. 그렇지 않으면 4단계를 진행합니다.
4. 작동 중인 컴퓨터에서 RDP 수신기 구성을 내보냅니다.
    1. 영향을 받는 컴퓨터와 동일한 운영 체제 버전을 사용하는 컴퓨터에 로그인하고, 해당 컴퓨터의 레지스트리에 액세스합니다(예를 들어 레지스트리 편집기를 사용하여).
    2. 다음 레지스트리 항목으로 이동합니다.  
        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp**
    3. 이 항목을 .reg 파일로 내보냅니다. 예를 들어 레지스트리 편집기에서 항목을 마우스 오른쪽 단추로 클릭하고 **내보내기**를 선택한 다음, 내보낸 설정의 파일 이름을 입력합니다.
    4. 내보낸 .reg 파일을 영향을 받는 컴퓨터에 복사합니다.
5. RDP 수신기 구성을 가져오려면 영향을 받는 컴퓨터에서 관리자 권한이 있는 PowerShell 창을 엽니다(또는 PowerShell 창을 열고 영향을 받는 컴퓨터에 원격으로 연결).
   1. 기존 레지스트리 항목을 백업하려면 다음 cmdlet을 입력합니다.  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 기존 레지스트리 항목을 제거하려면 다음 cmdlet을 입력합니다.  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 새 레지스트리 항목을 가져오고 서비스를 다시 시작하려면 다음 cmdlet을 입력합니다.  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```
      
      \<filename\>을 내보낸 .reg 파일의 이름으로 바꿉니다.

6. 원격 데스크톱 연결을 다시 시도하여 구성을 테스트합니다. 여전히 연결할 수 없는 경우 영향을 받는 컴퓨터를 다시 시작합니다.
7. 여전히 연결할 수 없는 경우 [RDP 자체 서명된 인증서의 상태를 확인](#check-the-status-of-the-rdp-self-signed-certificate)합니다.

### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>RDP 자체 서명된 인증서의 상태 확인

1. 여전히 연결할 수 없는 경우 인증서 MMC 스냅인을 엽니다. 관리할 인증서 저장소를 선택하라는 메시지가 표시되면 **컴퓨터 계정**을 선택한 다음, 영향을 받는 컴퓨터를 선택합니다.
2. **원격 데스크톱** 아래의 **Certificates** 폴더에서 RDP 자체 서명된 인증서를 삭제합니다. 
    ![MMC 인증서 스냅인에서 원격 데스크톱 인증서를 제거합니다.](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. 영향을 받는 컴퓨터에서 원격 데스크톱 서비스를 다시 시작합니다.
4. 인증서 스냅인을 새로 고칩니다.
5. RDP 자체 서명된 인증서를 다시 만들지 않은 경우 [MachineKeys 폴더의 권한을 확인](#check-the-permissions-of-the-machinekeys-folder)합니다.

### <a name="check-the-permissions-of-the-machinekeys-folder"></a>MachineKeys 폴더의 권한 확인

1. 영향을 받는 컴퓨터에서 탐색기를 열고 **C:\\ProgramData\\Microsoft\\Crypto\\RSA\\** 로 이동합니다.
2. **MachineKeys**를 마우스 오른쪽 단추로 클릭하고 **속성**, **보안**, **고급**을 차례로 선택합니다.
3. 다음 권한이 구성되었는지 확인합니다.
      - Builtin\\Administrators: 모든 권한
      - Everyone: 읽기, 쓰기

## <a name="check-the-rdp-listener-port"></a>RDP 수신기 포트 확인

로컬(클라이언트) 컴퓨터와 원격(대상) 컴퓨터에서 RDP 수신기가 3389 포트에서 수신 대기 중이어야 합니다. 다른 애플리케이션은 이 포트를 사용하면 안 됩니다.

> [!IMPORTANT]  
> 이 섹션의 지침은 주의 깊게 수행해야 합니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 문제가 발생하는 경우에 대비하여 복원할 수 있도록 레지스트리 수정을 시작하기 전에 해당 [레지스트리를 백업](https://support.microsoft.com/help/322756)하세요.

RDP 포트를 확인하거나 변경하려면 레지스트리 편집기를 사용합니다.

1. [시작] 메뉴로 이동하여 **실행**을 선택한 다음, 표시되는 텍스트 상자에서 **regedt32**를 입력합니다.
      - 원격 컴퓨터에 연결하려면 **파일**을 선택한 다음, **네트워크 레지스트리 연결**을 선택합니다.
      - **컴퓨터 선택** 대화 상자에서 원격 컴퓨터의 이름을 입력하고 **이름 확인**을 선택한 다음, **확인**을 선택합니다.
2. 레지스트리를 열고 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** 로 이동합니다. 
    ![RDP 프로토콜의 PortNumber 하위 키.](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. **PortNumber**의 값이 **3389**가 아니면 **3389**로 변경합니다. 
   > [!IMPORTANT]  
    > 다른 포트를 사용하여 원격 데스크톱 서비스를 작동할 수 있습니다. 그러나 이 작업은 수행하지 않는 것이 좋습니다. 이러한 유형의 구성 문제를 해결하는 방법은 이 문서에서 다루지 않습니다.
4. 포트 번호를 변경한 후 원격 데스크톱 서비스를 다시 시작합니다.

### <a name="check-that-another-application-isnt-trying-to-use-the-same-port"></a>다른 애플리케이션에서 동일한 포트를 사용하지 않는지 확인

이 절차에서는 관리자 권한이 있는 PowerShell 인스턴스를 사용합니다. 로컬 컴퓨터의 경우 관리자 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 그러나 동일한 cmdlet이 로컬 및 원격으로 작동하므로 이 절차에서는 PowerShell를 사용합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결하려면 입력 **Enter-PSSession -ComputerName \<컴퓨터 이름\>** 을 입력합니다.
2. 다음 명령을 입력합니다.  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![netstat 명령은 포트 및 포트에서 수신 대기하는 서비스 목록을 생성합니다.](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. 상태가 **Listening**인 TCP 포트 3389 또는 할당된 RDP 포트의 항목을 찾습니다. 
    > [!NOTE]  
   > 해당 포트를 사용하는 프로세스 또는 서비스의 PID(프로세스 식별자)가 PID 열 아래에 나타납니다.
4. 포트 3389(또는 할당된 RDP 포트)를 사용하는 애플리케이션을 확인하려면 다음 명령을 입력합니다.  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![tasklist 명령은 특정 프로세스의 세부 정보를 보고합니다.](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. 포트와 연결된 PID 번호의 항목을 찾습니다(**netstat** 출력에 표시됨). 해당 PID와 연결된 서비스 또는 프로세스가 오른쪽 열에 나타납니다.
6. 원격 데스크톱 서비스(TermServ.exe) 이외의 애플리케이션 또는 서비스가 이 포트를 사용하는 경우 다음 방법 중 하나를 사용하여 충돌을 해결할 수 있습니다.
      - 다른 애플리케이션 또는 서비스가 다른 포트를 사용하도록 구성합니다(권장).
      - 다른 애플리케이션 또는 서비스를 제거합니다.
      - 다른 포트를 사용하도록 RDP를 구성한 다음, 원격 데스크톱 서비스를 다시 시작합니다(권장하지 않음).

### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>방화벽이 RDP 포트를 차단하는지 확인

**psping** 도구를 사용하여 포트 3389를 통해 영향을 받는 컴퓨터에 연결할 수 있는지 테스트합니다.

1. 영향을 받지 않는 다른 컴퓨터로 이동하여 <https://live.sysinternals.com/psping.exe>에서 **pspping**을 다운로드합니다.
2. 명령 프롬프트 창을 관리자 권한으로 열고, **psping**을 설치한 디렉터리로 변경하고, 다음 명령을 입력합니다.  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. **psping** 명령의 출력에서 다음과 같은 결과를 확인합니다.  
      - **Connecting to \<computer IP\>** : 원격 컴퓨터에 연결할 수 있습니다.
      - **(0% loss)** : 모든 연결 시도가 성공했습니다.
      - **The remote computer refused the network connection**: 원격 컴퓨터에 연결할 수 없습니다.
      - **(100% loss)** : 모든 연결 시도가 실패했습니다.
1. 여러 컴퓨터에서 **psping**을 실행하여 영향을 받는 컴퓨터에 연결할 수 있는지 테스트합니다.
1. 영향을 받는 컴퓨터가 다른 컴퓨터의 연결을 모조리 차단하는지, 그 중 일부 컴퓨터만 차단하는지 또는 그 중 오직 한 컴퓨터만 차단하는지 확인합니다.
1. 다음 단계를 권장합니다.
      - 네트워크 관리자에게 연락하여 네트워크에서 영향을 받는 컴퓨터로 RDP 트래픽을 보낼 수 있는지 확인합니다.
      - 원본 컴퓨터와 영향을 받는 컴퓨터(영향을 받는 컴퓨터의 Windows 방화벽 포함) 간의 모든 방화벽 구성을 조사하여 방화벽이 RDP 포트를 차단하는지 확인합니다.
