---
title: 원격 데스크톱 연결 문제 해결
description: 증상별로 정리한 문제 해결 절차
ms.custom: na
ms.reviewer: rklemen; josh.bender
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: RobVyK
manager: ''
ms.author: kaushika; rklemen; josh.bender; v-tea
ms.date: 02/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: c6ce719ffa24cfc6704348c17548fe5cf33d9271
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284142"
---
# <a name="troubleshooting-remote-desktop-connections"></a>원격 데스크톱 연결 문제 해결
가장 많이 발생하는 여러 RDS(원격 데스크톱 서비스) 이슈에 대한 간략한 설명은 [원격 데스크톱 클라이언트에 대한 질문과 대답](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq)을 참조하세요. 이 문서에서는 연결 문제를 해결하는 고급 방법을 설명합니다. 이러한 절차 중 상당수는 한 물리적 컴퓨터를 다른 물리적 컴퓨터에 연결하는 것처럼 간단한 구성뿐 아니라 보다 복잡한 구성에도 적용됩니다. 일부 절차는 보다 복잡한 다중 사용자 시나리오에만 발생하는 이슈를 해결합니다. 원격 데스크톱 구성 요소에 대한 내용 및 이러한 구성 요소가 함께 작동하는 방식에 대한 자세한 내용은 [원격 데스크톱 서비스 아키텍처](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture)를 참조하세요.

> [!NOTE]  
> 이 문서에 설명된 절차 중 상당수는 여러 컴퓨터에 액세스해야 하며, 그 중 일부는 원격으로 액세스해야 할 수도 있습니다. 원격 관리 도구 및 구성 방법에 대한 자세한 내용은 [Windows 운영 체제용 RSAT(원격 서버 관리 도구)](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)를 참조하세요.

다음 목록에서 여러분(또는 사용자)이 겪고 있는 증상의 유형을 찾아보세요.

- [원격 데스크톱 클라이언트가 원격 데스크톱에 연결할 수 없지만, 특정 증상이 없거나 메시지(일반적인 문제 해결 단계)가 표시되지 않음](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [원격 데스크톱 클라이언트가 원격 데스크톱에 연결할 수 없으며, "클래스가 등록되지 않았습니다" 메시지가 수신됨](#client-cannot-connect-class-not-registered)
- [원격 데스크톱 클라이언트가 원격 데스크톱에 연결할 수 없으며, "사용 가능한 라이선스 없음" 또는 "보안 오류" 메시지가 수신됨](#client-cannot-connect-no-licenses-available)
- [사용자가 "액세스 거부됨" 메시지를 수신하거나 자격 증명을 두 번 입력해야 함](#user-cannot-authenticate-or-must-authenticate-twice)
- [연결하면 "원격 데스크톱 서비스가 현재 사용 중입니다" 메시지가 수신됨](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [원격 데스크톱 클라이언트의 연결이 끊어지고 동일한 세션에 다시 연결할 수 없음](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [사용자가 무선 네트워크를 통해 원격 노트북에 연결하면 노트북의 네트워크 연결이 끊어짐](#remote-laptop-disconnects-from-wireless-network)
- [사용자 환경의 성능이 저하되거나 원격 애플리케이션에서 문제 발생](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> RDP 연결 끊기 코드의 최신 목록은 [ExtendedDisconnectReasonCode 열거형](https://docs.microsoft.com/windows/desktop/TermServ/extendeddisconnectreasoncode)을 참조하세요. 

## <a name="no-specific-symptoms-or-messages-general-troubleshooting-steps"></a>특정 증상이 없거나 메시지(일반적인 문제 해결 단계)가 표시되지 않음

원격 데스크톱 클라이언트가 원격 데스크톱에 연결할 수 없지만 원인 파악에 도움이 되는 메시지가 표시되지 않거나 다른 증상이 없는 경우 다음 단계를 사용합니다. 이러한 이슈가 발생하는 가장 일반적인 원인을 해결하려면 다음 방법을 사용합니다.

- [RDP 프로토콜의 상태 확인](#check-the-status-of-the-rdp-protocol)
- [RDP 서비스의 상태 확인](#check-the-status-of-the-rdp-services)
- [RDP 수신기가 작동하는지 확인](#check-that-the-rdp-listener-is-functioning)
- [RDP 수신기 포트 확인](#check-the-rdp-listener-port)

### <a name="check-the-status-of-the-rdp-protocol"></a>RDP 프로토콜의 상태 확인

#### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>로컬 컴퓨터의 RDP 프로토콜 상태 확인

로컬 컴퓨터의 RDP 프로토콜 상태를 확인하고 변경하려면 [원격 데스크톱을 사용하도록 설정하는 방법](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)을 참조하세요.

> [!NOTE]  
> 원격 데스크톱 옵션을 사용할 수 없는 경우 [그룹 정책 개체가 RDP를 차단하고 있는지 확인](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)을 참조하세요.

#### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>원격 컴퓨터의 RDP 프로토콜 상태 확인

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)해 두세요.

원격 컴퓨터의 RDP 프로토콜 상태를 확인하고 변경하려면 네트워크 레지스트리 연결을 사용합니다.

1. **시작**을 선택하고 **실행**을 선택한 다음, **regedt32**를 입력합니다.
2. 레지스트리 편집기에서 **파일**을 선택한 다음, **네트워크 레지스트리 연결**을 선택합니다.
3. **컴퓨터 선택** 대화 상자에서 원격 컴퓨터의 이름을 입력하고 **이름 확인**을 선택한 다음, **확인**을 선택합니다.
4. **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**로 이동합니다.  
   ![fDenyTSConnections 항목을 표시하는 레지스트리 편집기](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - **fDenyTSConnections** 키 값이 **0**이면 RDP가 설정된 것입니다.
   - **fDenyTSConnections** 키 값이 **1**이면 RDP가 해제된 것입니다.
5. RDP를 사용하려면 **fDenyTSConnections** 값을 **1**에서 **0**으로 변경합니다.

#### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>GPO(그룹 정책 개체)가 로컬 컴퓨터의 RDP를 차단하고 있는지 확인합니다.

사용자 인터페이스에서 RDP를 켤 수 없거나 **fDenyTSConnections** 값을 변경한 후 다시 **1**로 되돌아가는 경우 GPO가 컴퓨터 수준 설정을 재정의하는 것일 수 있습니다.

로컬 컴퓨터의 그룹 정책 구성을 확인하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력합니다.
```
gpresult /H c:\gpresult.html
```
이 명령이 완료된 후 gpresult.html 파일을 엽니다. **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결**에서 **Allow users to connect remotely by using Remote Desktop Services**(원격 데스크톱 서비스를 사용한 원격 연결 허용) 정책을 찾습니다.

- 이 정책을 **사용**으로 설정하면 그룹 정책이 RDP 연결을 차단하지 않습니다.
- 이 정책이 **사용 안 함**으로 설정된 경우 **최우선 GPO**를 확인합니다. 이것이 바로 RDP 연결을 차단하는 GPO입니다.
  ![도메인 수준 GPO **RDP 차단**이 RDP를 차단하는 gpresult.html 세그먼트 예제](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![**로컬 그룹 정책**이 RDP를 차단하는 gpresult.html 세그먼트 예제](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

#### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>GPO가 원격 컴퓨터의 RDP를 차단하는지 확인

원격 컴퓨터의 그룹 정책 구성을 확인하는 명령은 로컬 컴퓨터와 거의 동일합니다.
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
이 명령이 생성하는 파일(**gpresult-\<컴퓨터 이름\>.html**)은 로컬 컴퓨터 버전(**gpresult.html**)이 사용하는 것과 동일한 정보 형식을 사용합니다.

#### <a name="modifying-a-blocking-gpo"></a>차단 GPO 수정

GPE(그룹 정책 개체 편집기) 및 GPM(그룹 정책 관리 콘솔)에서 이러한 설정을 수정할 수 있습니다. 그룹 정책을 사용하는 방법에 대한 자세한 내용은 [고급 그룹 정책 관리](https://docs.microsoft.com/microsoft-desktop-optimization-pack/agpm/)를 참조하세요.

차단 정책을 수정하려면 다음 방법 중 하나를 사용합니다.

- GPE에서 적절한 GPO 수준(예: 로컬 또는 도메인)에 액세스하고, **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결**\\**Allow users to connect remotely by using Remote Desktop Services**(원격 데스크톱 서비스를 사용한 원격 연결 허용) 정책으로 이동합니다.  
   1. 정책을 **사용** 또는 **구성되지 않음**으로 설정합니다.
   2. 영향을 받는 컴퓨터에서 관리자 권한으로 명령 프롬프트 창을 열고, **gpupdate /force** 명령을 실행합니다.
- GPM에서, 영향을 받는 컴퓨터에 차단 정책이 적용되는 OU로 이동한 다음, 해당 OU의 정책을 삭제합니다.

### <a name="check-the-status-of-the-rdp-services"></a>RDP 서비스의 상태 확인

로컬(클라이언트) 컴퓨터와 원격(대상) 컴퓨터에서 다음 서비스가 실행 중이어야 합니다.

- 원격 데스크톱 서비스(TermService)
- 원격 데스크톱 서비스 UserMode 포트 리디렉터(UmRdpService)

서비스 MMC 스냅인을 사용하여 로컬로 또는 원격으로 서비스를 관리할 수 있습니다. 로컬 또는 원격으로 PowerShell 사용할 수도 있습니다(원격 컴퓨터가 원격 PowerShell 명령을 수락하도록 구성된 경우).

![서비스 MMC 스냅인의 원격 데스크톱 서비스. 기본 서비스 설정을 수정하지 마세요.](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

두 컴퓨터 중 하나 또는 둘 다 실행되고 있지 않으면 해당 컴퓨터를 시작합니다.

> [!NOTE]  
> 원격 데스크톱 서비스를 시작할 때 원격 데스크톱 서비스 UserMode 포트 리디렉터 서비스를 자동으로 다시 시작하도록 **예**를 클릭합니다.

### <a name="check-that-the-rdp-listener-is-functioning"></a>RDP 수신기가 작동하는지 확인

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)해 두세요.

#### <a name="check-the-status-of-the-rdp-listener"></a>RDP 수신기의 상태 확인

이 절차에서는 관리자 권한이 있는 PowerShell 인스턴스를 사용합니다. 로컬 컴퓨터의 경우 관리자 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 하지만 같은 명령이 로컬로 그리고 원격으로 작동하므로 이 절차에서는 PowerShell를 사용합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결하려면 입력 **Enter-PSSession -ComputerName \<컴퓨터 이름\>** 을 입력합니다.
2. **qwinsta**를 입력합니다. 
    ![qwinsta 명령은 컴퓨터의 포트에서 수신 대기하는 프로세스를 나열합니다.](../media/troubleshoot-remote-desktop-connections/WPS_qwinsta.png)
3. 목록에 상태가 **수신 대기**인 **rdp-tcp**가 포함된 경우 RDP 수신기가 작동합니다. [RDP 수신기 포트 확인](#check-the-rdp-listener-port)을 진행합니다. 그렇지 않으면 4단계를 진행합니다.
4. 작동 중인 컴퓨터에서 RDP 수신기 구성을 내보냅니다.
    1. 영향을 받는 컴퓨터와 동일한 운영 체제 버전을 용하는 컴퓨터에 로그인하고, 해당 컴퓨터의 레지스트리에 액세스합니다(예를 들어 레지스트리 편집기를 사용하여).
    2. 다음 레지스트리 항목으로 이동합니다.  
        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp**
    3. 이 항목을 .reg 파일로 내보냅니다. 예를 들어 레지스트리 편집기에서 항목을 마우스 오른쪽 단추로 클릭하고 **내보내기**를 선택한 다음, 내보낸 설정의 파일 이름을 입력합니다.
    4. 내보낸 .reg 파일을 영향을 받는 컴퓨터에 복사합니다.
5. RDP 수신기 구성을 가져오려면 영향을 받는 컴퓨터에서 관리자 권한이 있는 PowerShell 창을 엽니다(또는 PowerShell 창을 열고 영향을 받는 컴퓨터에 원격으로 연결).
   1. 기존 레지스트리 항목을 백업하려면 다음 명령을 입력합니다.  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 기존 레지스트리 항목을 제거하려면 다음 명령을 입력합니다.  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 새 레지스트리 항목을 가져오고 서비스를 다시 시작하려면 다음 명령을 입력합니다.  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      \<filename\>은 내보낸 .reg 파일의 이름입니다.
6. 원격 데스크톱 연결을 다시 시도하여 구성을 테스트합니다. 여전히 연결할 수 없는 경우 영향을 받는 컴퓨터를 다시 시작합니다.
7. 여전히 연결할 수 없는 경우 [RDP 자체 서명된 인증서의 상태를 확인](#check-the-status-of-the-rdp-self-signed-certificate)합니다.

#### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>RDP 자체 서명된 인증서의 상태 확인

1. 여전히 연결할 수 없는 경우 인증서 MMC 스냅인을 엽니다. 관리할 인증서 저장소를 선택하라는 메시지가 표시되면 **컴퓨터 계정**을 선택한 다음, 영향을 받는 컴퓨터를 선택합니다.
2. **원격 데스크톱** 아래의 **Certificates** 폴더에서 RDP 자체 서명된 인증서를 삭제합니다. 
    ![MMC 인증서 스냅인에서 원격 데스크톱 인증서를 제거합니다.](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. 영향을 받는 컴퓨터에서 원격 데스크톱 서비스를 다시 시작합니다.
4. 인증서 스냅인을 새로 고칩니다.
5. RDP 자체 서명된 인증서가 다시 생성되지 않으면 [MachineKeys 폴더의 권한을 확인](#check-the-permissions-of-the-machinekeys-folder)합니다.

#### <a name="check-the-permissions-of-the-machinekeys-folder"></a>MachineKeys 폴더의 권한 확인

1. 영향을 받는 컴퓨터에서 탐색기를 열고 **C:\\ProgramData\\Microsoft\\Crypto\\RSA\\** 로 이동합니다.
2. **MachineKeys**를 마우스 오른쪽 단추로 클릭하고 **속성**, **보안**, **고급**을 차례로 선택합니다.
3. 다음 권한이 구성되었는지 확인합니다.
      - Builtin\\Administrators: 모든 권한
      - Everyone: 읽기, 쓰기

### <a name="check-the-rdp-listener-port"></a>RDP 수신기 포트 확인

로컬(클라이언트) 컴퓨터와 원격(대상) 컴퓨터에서 RDP 수신기가 3389 포트에서 수신 대기 중이어야 합니다. 다른 애플리케이션은 이 포트를 사용하면 안 됩니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)해 두세요.

RDP 포트를 확인하거나 변경하려면 레지스트리 편집기를 사용합니다.

1. [시작]을 선택하고 **실행**을 선택한 다음, **regedt32**를 입력합니다.
      - 원격 컴퓨터에 연결하려면 **파일**을 선택한 다음, **네트워크 레지스트리 연결**을 선택합니다.
      - **컴퓨터 선택** 대화 상자에서 원격 컴퓨터의 이름을 입력하고 **이름 확인**을 선택한 다음, **확인**을 선택합니다.
2. 레지스트리를 열고 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** 로 이동합니다. 
    ![RDP 프로토콜의 PortNumber 하위 키.](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. **PortNumber**의 값이 **3389**가 아니면 **3389**로 변경합니다. 
   > [!IMPORTANT]  
    > 다른 포트를 사용하여 원격 데스크톱 서비스를 작동할 수 있습니다. 그러나 이 방법은 권장하지 않습니다. 이러한 구성 문제 해결은 이 문서의 범위를 벗어납니다.
4. 포트 번호를 변경한 후 원격 데스크톱 서비스를 다시 시작합니다.

#### <a name="check-that-another-application-is-not-trying-to-use-the-same-port"></a>다른 애플리케이션이 같은 포트를 사용하려고 시도하지는 않는지 확인합니다.

이 절차에서는 관리자 권한이 있는 PowerShell 인스턴스를 사용합니다. 로컬 컴퓨터의 경우 관리자 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 하지만 같은 명령이 로컬로 그리고 원격으로 작동하므로 이 절차에서는 PowerShell를 사용합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결하려면 입력 **Enter-PSSession -ComputerName \<컴퓨터 이름\>** 을 입력합니다.
2. 다음 명령을 입력합니다.  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![netstat 명령은 포트 및 포트에서 수신 대기하는 서비스 목록을 생성합니다.](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. 상태가 **Listening**인 TCP 포트 3389 또는 할당된 RDP 포트의 항목을 찾습니다. 
    > [!NOTE]  
   > 해당 포트를 사용하는 서비스나 프로세스의 PID(프로세스 식별자)가 PID 열 아래에 나타납니다.
4. 포트 3389(또는 할당된 RDP 포트)를 사용하는 애플리케이션을 확인하려면 다음 명령을 입력합니다.  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![tasklist 명령은 특정 프로세스의 세부 정보를 보고합니다.](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. 포트와 연결된 PID 번호의 항목을 찾습니다(**netstat** 출력에 표시됨). 해당 PID와 연결된 서비스 또는 프로세스가 오른쪽에 나타납니다.
6. 원격 데스크톱 서비스(TermServ.exe) 이외의 애플리케이션 또는 서비스가 이 포트를 사용하는 경우 다음 방법 중 하나를 사용하여 충돌을 해결할 수 있습니다.
      - 다른 애플리케이션 또는 서비스가 다른 포트를 사용하도록 구성합니다(권장).
      - 다른 애플리케이션 또는 서비스를 제거합니다.
      - 다른 포트를 사용하도록 RDP를 구성한 다음, 원격 데스크톱 서비스를 다시 시작합니다(권장하지 않음).

#### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>방화벽이 RDP 포트를 차단하는지 확인

**psping** 도구를 사용하여 포트 3389를 통해 영향을 받는 컴퓨터에 연결할 수 있는지 테스트합니다.

1. 영향을 받는 컴퓨터가 아닌 다른 컴퓨터에서, <https://live.sysinternals.com/psping.exe>에서 **psping**을 다운로드합니다.
2. 관리자 권한으로 명령 프롬프트 창을 열고, **psping**을 설치한 디렉터리로 변경하고, 다음 명령을 입력합니다.  
   
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

## <a name="client-cannot-connect-class-not-registered"></a>클라이언트가 연결할 수 없음, "클래스가 등록되지 않았습니다"

Windows 10 버전 1709 이상을 실행하는 클라이언트를 사용하여 원격 컴퓨터에 연결하려고 시도할 때 클라이언트가 연결하지 않고 원격 데스크톱 세션 호스트 서버가 "클래스가 등록되지 않았습니다(0x80040154)" 오류 코드를 포함한 메시지를 표시할 수 있습니다.

연결하려는 사용자가 필수 사용자 프로필을 갖고 있는 경우에 이 이슈가 발생합니다. 이 이슈를 해결하려면 [2018년 7월 24일 - KB4338817(OS 빌드 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10 업데이트를 설치합니다.

## <a name="client-cannot-connect-no-licenses-available"></a>클라이언트가 연결할 수 없음, 사용 가능한 라이선스 없음

이 상황은 RDSH 서버 및 원격 데스크톱 라이선스 서버가 포함된 배포에 적용됩니다.

사용자가 어떤 동작을 목격하는지 확인합니다.

- 사용 가능한 라이선스 또는 라이선스 서버가 없어서 세션 연결이 끊어졌습니다.
- 보안 오류로 인해 액세스가 거부되었습니다.

도메인 관리자로 RD 세션 호스트에 로그인하여 RD 라이선스 진단 도구를 엽니다. 다음과 같은 메시지를 찾습니다.

  - 원격 데스크톱 세션 호스트 서버의 유예 기간이 만료되었지만, 라이선스 서버를 사용하여 RD 세션 호스트 서버가 구성되지 않았습니다. RD 세션 호스트 서버에 대한 라이선스 서버를 구성하지 않으면 RD 세션 호스트 서버에 대한 연결이 거부됩니다.
  - \<컴퓨터 이름\> 라이선스 서버를 사용할 수 없습니다. 네트워크 연결 문제로 인해 발생할 수 있습니다. 라이선스 서버에서 원격 데스크톱 라이선스 서비스가 중지되었거나 컴퓨터에 더 이상 RD 라이선스가 설치되어 있지 않습니다.

이러한 문제는 다음과 같은 사용자 메시지와 관련이 있는 경우가 많습니다.

  - 이 컴퓨터에 사용할 수 있는 원격 데스크톱 클라이언트 액세스 라이선스가 없어서 원격 세션이 끊겼습니다.
  - 라이선스를 제공하는 데 사용할 수 있는 원격 데스크톱 라이선스 서버가 없어서 원격 세션이 끊겼습니다.

이 경우 [RD 라이선스 서비스를 구성](#configure-the-rd-licensing-service)합니다.

RD 라이선스 진단 도구가 "RDP 프로토콜 구성 요소 X.224가 프로토콜 스트림에서 오류를 발견하여 클라이언트 연결을 끊겼습니다"와 비슷한 다른 문제를 나열하는 경우 라이선스 인증서에 영향을 주는 문제일 수 있습니다. 이와 같은 문제는 다음과 같은 사용자 메시지와 관련이 있는 경우가 많습니다.

보안 오류로 인해 클라이언트가 터미널 서버에 연결할 수 없습니다. 네트워크에 로그온되었는지 확인한 후 서버에 다시 연결해 보세요.

이 경우 [X509 인증서 레지스트리 키를 새로 고칩니다](#refresh-the-x509-certificate-registry-keys).

### <a name="configure-the-rd-licensing-service"></a>RD 라이선스 서비스 구성

다음 절차에서는 서버 관리자를 사용하여 구성을 변경합니다. 서버 관리자를 구성하고 사용하는 방법에 대한 내용은 [서버 관리자](https://docs.microsoft.com/windows-server/administration/server-manager/server-manager)를 참조하세요.

1. 서버 관리자를 열고 **원격 데스크톱 서비스**로 이동합니다.
2. **배포 개요**에서 **작업**을 선택한 다음, **배포 속성 편집**을 선택합니다.
3. **RD 라이선스**를 선택한 다음, 배포에 적합한 라이선스 모드(**디바이스 단위** 또는 **사용자 단위**)를 선택합니다.
4. RD 라이선스 서버의 FQDN(정규화된 도메인 이름)을 입력한 다음, **추가**를 선택합니다.
5. RD 라이선스 서버가 둘 이상인 경우 서버마다 4단계를 반복합니다. 
    ![서버 관리자의 RD 라이선스 서버 구성 옵션.](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

### <a name="refresh-the-x509-certificate-registry-keys"></a>X509 인증서 레지스트리 키 새로 고침

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)해 두세요.

이 문제를 해결하려면 X509 인증서 레지스트리 키를 백업한 후 제거하고, 컴퓨터를 다시 시작하고, RD 라이선스 서버를 다시 활성화합니다. 이를 위해 다음 단계를 수행합니다.

> [!NOTE]  
> 각 RDSH 서버에서 다음 절차를 수행합니다.

1. 레지스트리 편집기를 열고 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM**으로 이동합니다.
2. [레지스트리] 메뉴에서 **레지스트리 파일 내보내기**를 선택합니다.
3. **파일 이름** 상자에 **exported- Certificate**를 입력한 다음, **저장**을 선택합니다.
4. 다음 값을 각각 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택한 다음, **예**를 선택하여 삭제를 확인합니다.  
      - **인증서**
      - **X509 인증서**
      - **X509 인증서 ID**
      - **X509 인증서2**
5. 레지스트리 편집기를 종료한 다음, RDSH 서버를 다시 시작합니다.

## <a name="user-cannot-authenticate-or-must-authenticate-twice"></a>사용자가 인증할 수 없거나 두 번 인증해야 함

사용자 인증에 영향을 주는 문제를 일으킬 수 있는 여러 이슈가 있습니다. 이 섹션에서는 다음과 같은 사례를 해결합니다.

  - ["제한된 로그온 유형" 메시지와 함께 사용자 액세스가 거부됨](#access-denied-restricted-type-of-logon)
  - [이벤트 16965 "SAM 데이터베이스에 대한 원격 호출이 거부되었습니다" 메시지와 함께 사용자 또는 애플리케이션 액세스가 거부됨](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [사용자가 스마트 카드를 사용하여 로그인할 수 없음](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [원격 PC가 잠긴 경우 사용자가 암호를 두 번 입력해야 함](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [사용자가 로그인할 수 없고 "인증 오류" 및 "CredSSP 암호화 오라클 수정" 메시지가 수신됨](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [클라이언트 컴퓨터를 업데이트한 후 일부 사용자가 두 번 로그인해야 함](#after-you-update-client-computers-some-users-need-to-sign-in-twice)
  - [여러 RD 연결 브로커가 있는 RemoteGuard를 사용하는 배포에 대한 사용자 액세스가 거부됨](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### <a name="access-denied-restricted-type-of-logon"></a>액세스 거부됨, 제한된 로그온 유형

이 경우 Windows 10 또는 Windows Server 2016 컴퓨터에 연결하려고 시도하는 Windows 10 사용자는 다음 메시지와 함께 액세스가 거부됩니다.

> 원격 데스크톱 연결:  
> 시스템 관리자가 사용자가 사용할 수 있는 로그온 유형(네트워크 또는 대화형)을 제한했습니다. 도움이 필요한 경우 시스템 관리자 또는 기술 지원 팀에 문의하세요.

RDP 연결에 NLA(네트워크 수준 인증)가 필요하고 사용자가 **원격 데스크톱 사용자** 그룹의 구성원이 아닌 경우에 이 이슈가 발생합니다. **원격 데스크톱 사용자** 그룹이 **네트워크에서 이 컴퓨터 액세스** 사용자 권한에 할당되지 않은 경우에도 발생할 수 있습니다.

이 이슈를 해결하려면 다음 단계 중 하나를 수행합니다.

  - [사용자의 그룹 구성원 또는 사용자 권한 할당을 수정](#modify-the-users-group-membership-or-user-rights-assignment)합니다.
  - NLA를 끕니다(권장하지 않음).
  - Windows 10이 아닌 다른 원격 데스크톱 클라이언트를 사용합니다. 예를 들어 Windows 7 클라이언트에서는 이 이슈가 발생하지 않습니다.

#### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>사용자의 그룹 구성원 또는 사용자 권한 할당 수정

이 이슈가 사용자 한 명에게만 영향을 주는 경우 가장 간단한 해결 방법은 **원격 데스크톱 사용자** 그룹에 해당 사용자를 추가하는 것입니다.

해당 사용자가 이미 이 그룹의 구성원인 경우(또는 여러 그룹 구성원에게 동일한 문제가 있는 경우) 원격 Windows 10 또는 Windows Server 2016 컴퓨터의 사용자 권한 구성을 확인합니다.

1. GPE(그룹 정책 개체 편집기)를 열고 원격 컴퓨터의 로컬 정책에 연결합니다.
2. **컴퓨터 구성\\Windows 설정\\보안 설정\\로컬 정책\\사용자 권한 할당**으로 이동하여 **네트워크에서 이 컴퓨터 액세스**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.
3. **원격 데스크톱 사용자**(또는 부모 그룹)의 사용자 및 그룹 목록을 확인합니다.
4. 이 목록에 **원격 데스크톱 사용자**(또는 **모두** 같은 부모 그룹)가 없는 경우 목록에 추가해야 합니다(배포에 컴퓨터가 두 대 또는 세 대 이상 있는 경우 그룹 정책 개체를 사용).  
    예를 들어 **네트워크에서 이 컴퓨터 액세스**의 기본 구성원은 **모두**를 포함합니다. **모두**를 제거하기 위해 배포에서 그룹 정책 개체를 사용하는 경우 **원격 데스크톱 사용자**를 추가하도록 그룹 정책 개체를 업데이트하여 액세스를 복원해야 할 수도 있습니다.

### <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>액세스 거부됨, SAM 데이터베이스에 대한 원격 호출이 거부됨

이 동작은 도메인 컨트롤러가 Windows Server 2016 이상을 실행하고 사용자가 사용자 지정된 연결 앱을 사용하여 연결하려고 시도하는 경우에 발생할 가능성이 가장 높습니다. 특히, Active Directory에서 사용자의 프로필 정보에 액세스하는 애플리케이션은 액세스가 거부됩니다.

이 동작의 원인은 Windows 변경입니다. Windows Server 2012 R2 이하 버전에서 사용자가 원격 데스크톱에 로그온하면 RCM(원격 연결 관리자)은 DC(도메인 컨트롤러)에 연결하여 AD DS(Active Directory Domain Services)의 사용자 개체에 대한 원격 데스크과 관련된 구성을 쿼리합니다. 이 정보는 Active Directory 사용자 및 컴퓨터 MMC 스냅인에서 사용자 개체 속성의 원격 데스크톱 서비스 프로필 탭에 표시됩니다.

Windows Server 2016부터 RCM은 더 이상 AD DS의 사용자 개체를 쿼리하지 않습니다. 원격 데스크톱 서비스 특성을 사용 중이어서 RCM에 AD DS를 쿼리하도록 요구하는 경우 이전 RCM 동작을 수동으로 설정해야 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)해 두세요.

RD 세션 호스트 서버에서 레거시 RCM 동작을 사용하려면 다음 레지스트리 항목을 구성하고 **원격 데스크톱 서비스**를 다시 시작합니다.  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Services**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation name\>\\**  
      - 이름: **fQueryUserConfigFromDC**
      - 다음을 입력합니다. **Reg\_DWORD**
      - 값: **1**(10진수)

RD 세션 호스트 서버가 아닌 다른 서버에서 레거시 RCM 동작을 사용하려면 다음 레지스트리 항목 및 추가 레지스트리 항목을 구성하고 서비스를 다시 시작합니다.
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

이 동작에 대한 자세한 내용은 KB 3200967 [Windows Server에서 원격 연결 관리자 변경](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server)을 참조하세요.

### <a name="a-user-cannot-sign-in-by-using-a-smart-card"></a>사용자가 스마트 카드를 사용하여 로그인할 수 없음

이 문서에서는 사용자가 스마트 카드를 사용하여 원격 데스크톱에 로그인할 수 없는 세 가지 일반적인 상황을 해결합니다.  
  - [사용자가 RODC(읽기 전용 도메인 컨트롤러)를 사용하는 지사에 로그인할 수 없음](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [사용자가 최근에 업데이트된 Windows Server 2008 SP2 컴퓨터에 로그인할 수 없음](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [사용자가 최근에 업데이트된 Windows 컴퓨터에서 로그인 상태를 유지할 수 없고, 원격 데스크톱 서비스가 응답하지 않음(중지됨)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### <a name="cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc"></a>스마트 카드로 RODC를 사용하는 지사에 로그인할 수 없음

이 이슈는 RODC를 사용하는 지사 사이트에 RDSH 서버가 있는 배포에서 발생합니다. RDSH 서버는 루트 도메인에 호스트됩니다. 지사 사이트의 사용자는 자식 도메인에 속하며, 스마트 카드를 사용하여 인증합니다. RODC는 사용자 암호를 캐시하도록 구성됩니다(RODC는 **허용된 RODC 암호 복제 그룹** 소속). 사용자가 RDSH 서버의 세션에 로그인하려고 시도하면 "시도한 로그온이 잘못되었습니다. 사용자 이름이 잘못되었거나 인증 정보가 잘못되었기 때문입니다"라는 내용의 메시지가 수신됩니다.

이것은 루트 DC와 RODC가 사용자 자격 증명의 암호화를 관리하는 방식에서 이미 알려진 이슈입니다. 루트 DC는 암호화 키를 사용하여 자격 증명을 암호화하고, RODC는 클라이언트에 암호 해독 키를 제공합니다. 그러나 두 키가 일치하지 않습니다.

이 이슈를 해결하려면 RODC에서 암호 캐싱을 해제하거나 지사 사이트에 쓰기 가능한 DC를 배포하여 DC 토폴로지를 변경하는 방안을 고려해 보세요. 대안은 RDSH 서버를 사용자와 동일한 하위 도메인으로 이동하는 것입니다. 또 다른 대안은 사용자가 스마트 카드 없이 로그인하도록 허용하는 것입니다. 이러한 해결 방법을 사용하면 보안 성능 또는 수준이 저하될 수 있습니다.

#### <a name="cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer"></a>스마트 카드를 사용하여 Windows Server 2008 SP2 컴퓨터에 로그인 할 수 없음

사용자가 KB4093227(2018.4B)로 업데이트된 Windows Server 2008 SP2 컴퓨터에 로그인하려고 시도하면 이 이슈가 발생합니다. 사용자가 스마트 카드를 사용하여 로그인하려고 시도하면 “올바른 인증서가 없습니다. 카드를 꽉 맞도록 올바르게 삽입했는지 확인합니다”라는 내용의 메시지와 함께 액세스가 거부됩니다. 그와 동시에, Windows Server 컴퓨터는 "삽입한 스마트 카드에서 디지털 인증서를 검색하는 동안 오류가 발생했습니다. 서명이 잘못되었습니다"라는 애플리케이션 이벤트를 기록합니다.

이 이슈를 해결하려면 Windows Server 컴퓨터를 KB 4093227 [Windows Server 2008의 Windows RDP(원격 데스크톱 프로토콜) 서비스 거부 취약성에 대한 보안 업데이트 설명: 2018년 4월 10일](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)의 2018.06 B 재릴리스로 업데이트합니다.

#### <a name="cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>스마트 카드로 로그인 상태를 유지할 수 없으며 원격 데스크톱 서비스가 중지됨

사용자가 KB 4056446으로 업데이트된 Windows 또는 Windows Server 컴퓨터에 로그인하려고 시도하면 이 이슈가 발생합니다. 처음에는 사용자가 스마트 카드를 사용하여 시스템에 로그인할 수도 있지만, 그 후 “SCARD\_E\_NO\_SERVICE” 오류 메시지가 수신됩니다. 원격 컴퓨터가 응답하지 않을 수 있습니다.

이 이슈를 해결하려면 원격 컴퓨터를 다시 시작합니다.

이 이슈를 해결하려면 원격 컴퓨터를 적절한 픽스로 업데이트합니다.

  - Windows Server 2008 SP2: KB 4090928, [Windows의 lsm.exe 프로세스에서 핸들이 누수되어 스마트 카드 애플리케이션이 "SCARD\_E\_NO\_SERVICE" 오류를 표시할 수 있음](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2: KB 4103724, [2018년 5월 17일 - KB4103724(월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 및 Windows 10 버전 1607: KB 4103720, [2018년 5월 17일 - KB4103720(OS 빌드 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### <a name="if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice"></a>원격 PC가 잠긴 경우 사용자가 암호를 두 번 입력해야 함

RDP 연결 시 NLA가 필요 없는 배포에서 Windows 10 버전 1709를 실행하는 원격 데스크톱에 사용자가 연결을 시도할 때 이 이슈가 발생할 수 있습니다. 이러한 상황에서 원격 데스크톱이 잠긴 경우 사용자는 연결할 때 자격 증명을 두 번 입력해야 합니다.

이 이슈를 해결하려면 Windows 10 버전 1709 컴퓨터를 KB 4343893 [2018년 8월 30일 - KB4343893(OS 빌드 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893)으로 업데이트합니다.

### <a name="user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>사용자가 로그인할 수 없고 "인증 오류" 및 "CredSSP 암호화 오라클 수정" 메시지가 수신됨

사용자가 Windows Vista SP2 이상 또는 Windows Server 2008 SP2 이상 버전의 Windows를 사용하여 로그인하려고 시도하면 액세스가 거부되고 다음과 같은 메시지가 수신됩니다.

  - 인증 오류가 발생했습니다. 요청한 함수가 지원되지 않습니다.
  - CredSSP 암호화 오라클 수정이 원인일 수 있습니다.

"CredSSP 암호화 오라클 수정"은 2018년 3, 4, 5월에 출시된 보안 업데이트 세트를 말합니다. CredSSP는 다른 애플리케이션에 대한 인증 요청을 처리하는 인증 공급 기업입니다. 2018년 3월 13일 "3B" 및 후속 업데이트는 공격자가 사용자 자격 증명을 릴레이하여 대상 시스템에서 코드를 실행할 수 있는 악용을 해결합니다.

초기 업데이트에서는 다음과 같은 설정이 가능한 새 그룹 정책 개체 **암호화 오라클 수정**에 대한 지원이 추가되었습니다.

  - **취약**. CredSSP를 사용하는 클라이언트 애플리케이션을 안전하지 않은 버전으로 대체할 수 있지만, 이 동작은 원격 데스크톱을 공격에 노출합니다. CredSSP를 사용하는 서비스는 업데이트되지 않은 클라이언트를 수락합니다.
  - **완화됨**. CredSSP를 사용하는 클라이언트 애플리케이션을 안전하지 않은 버전으로 대체할 수 없지만, CredSSP를 사용하는 서비스는 업데이트되지 않은 클라이언트를 수락합니다.
  - **강제로 업데이트된 클라이언트**. CredSSP를 사용하는 클라이언트 애플리케이션을 안전하지 않은 버전으로 대체할 수 없으며, CredSSP를 사용하는 서비스는 패치되지 않은 클라이언트를 수락하지 않습니다. 
    참고: 모든 원격 호스트가 최신 버전을 지원하기 전에는 이 설정을 배포하면 안 됩니다.

2018년 5월 8일 업데이트에서는 기본 **암호화 오라클 수정** 설정이 **취약**에서 **완화됨**으로 변경되었습니다. 이 변경 내용이 적용되면서, 업데이트가 설치된 원격 데스크톱 클라이언트는 업데이트가 설치되지 않은 서버(또는 업데이트 후 다시 시작하지 않은 서버)에 연결할 수 없습니다. 업데이트의 효과 및 업데이트가 차단하는 통신 유형에 대한 자세한 내용은 KB 4093492 [CVE-2018-0886에 대한 CredSSP 업데이트](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)를 참조하세요.

이 이슈를 해결하려면 모든 시스템을 완전히 업데이트하고 다시 시작해야 합니다. 업데이트 전체 목록 및 취약성에 대한 자세한 내용은 [CVE-2018-0886 | CredSSP 원격 코드 실행 취약성](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886)을 참조하세요.

업데이트가 완료될 때까지 이 이슈를 해결하려면 KB 4093492에서 허용되는 연결 유형을 확인합니다. 가능한 대안이 없는 경우 다음 방법 중 하나를 고려해 볼 수 있습니다.

- 영향을 받는 클라이언트 컴퓨터에서 **암호화 오라클 수정** 정책을 다시 **취약**으로 설정합니다.
- **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\보안** 그룹 정책 폴더에서 다음 정책을 수정합니다.  
  - **원격(RDP) 연결에 특정 보안 계층 사용**: **사용**으로 설정하고 **RDP**를 선택합니다.
  - **네트워크 수준 인증을 사용하여 원격 연결에 대한 사용자 인증**: **사용 안 함**으로 설정합니다.
    > [!IMPORTANT]  
    > 이렇게 수정하면 배포의 보안이 약화됩니다. 사용하더라도 일시적으로만 사용해야 합니다.

그룹 정책 사용에 대한 자세한 내용은 [차단 GPO 수정](#modifying-a-blocking-gpo)을 참조하세요.

### <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>클라이언트 컴퓨터를 업데이트한 후 일부 사용자가 두 번 로그인해야 함

일부 Windows 7 또는 Windows 10 버전 1709에서 사용자가 원격 데스크톱 세션에 로그인하는 즉시 두 번째 로그인 화면이 표시됩니다. 이 이슈는 클라이언트 컴퓨터에서 다음 업데이트를 수신한 경우에 발생합니다.

  - Windows 7: KB 4103718, [2018년 5월 8일 - KB4103718(월별 롤업)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [2018년 5월 8일 - KB4103727(OS 빌드 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

이 이슈를 해결하려면 사용자가 연결하려는 컴퓨터(그리고 RDSH 또는 RDVI 서버)를 2018년 6월까지 완전히 업데이트해야 합니다. 여기에는 다음 업데이트가 포함됩니다.

  - Windows Server 2016: KB 4284880, [2018년 6월 12일 - KB4284880(OS 빌드 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [2018년 6월 12일 - KB4284815(월별 롤업)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855, [2018년 6월 12일 - KB4284855(월별 롤업)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [2018년 6월 12일 - KB4284826(월별 롤업)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Windows Server 2008, Windows Embedded POSReady 2009 및 Windows Embedded Standard 2009의 CredSSP 원격 코드 실행 취약성에 대한 보안 업데이트 설명: 2018년 3월 13일](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>여러 RD 연결 브로커가 있는 원격 Credential Guard를 사용하는 배포에 대한 사용자 액세스가 거부됨

Windows Defender 원격 Credential Guard를 사용하는 경우 두 개 이상의 원격 데스크톱 연결 브로커를 사용하는 고가용성 배포에서 이 이슈가 발생합니다. 사용자가 원격 데스크톱에 로그인할 수 없습니다.

이 이슈는 원격 Credential Guard에서 인증에 Kerberos를 사용하고 NTLM을 제한하기 때문에 발생합니다. 그러나 부하가 분산되는 고가용성 구성에서는 RD 연결 브로커가 Kerberos 작업을 지원할 수 없습니다.

RD 연결 브로커의 부하가 분산되는 고가용성 구성을 사용해야 하는 경우 원격 Credential Guard를 사용하지 않도록 설정하여 이 이슈를 해결할 수 있습니다. Windows Defender 원격 Credential Guard를 관리하는 방법에 대한 자세한 내용은 [Windows Defender 원격 Credential Guard를 사용하여 원격 데스크톱 자격 증명 보호](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)를 참조하세요.

## <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>사용자가 연결하면 "원격 데스크톱 서비스가 현재 사용 중입니다" 메시지가 수신됨

이 이슈를 해결하는 적절한 대응 방법을 찾으려면 다음 단계를 수행합니다.

1. 원격 데스크톱 서비스가 응답하지 않습니다(예: 시작 화면에서 원격 데스크톱 클라이언트가 "중지"된 것으로 표시됨).  
      - 서비스가 응답하지 않는 경우 [RDSH 서버 메모리 이슈](#rdsh-server-memory-issue)를 참조하세요.
      - 클라이언트가 정상적으로 서비스와 상호 작용하는 것으로 표시되면 다음 단계를 진행합니다.
2. 한 명 이상의 사용자가 원격 데스크톱 세션을 종료하는 경우 사용자가 다시 연결할 수 있나요?  
   - 세션을 종료하는 사용자가 몇 명이든 서비스에서 연결을 계속 거부하면 [RD 수신기 이슈](#rd-listener-issue)를 참조하세요.
   - 수많은 사용자가 세션을 종료한 후 서비스에서 다시 연결을 수락하는 경우 [연결 제한 정책을 확인](#check-the-connection-limit-policy)합니다.

### <a name="rdsh-server-memory-issue"></a>RDSH 서버 메모리 이슈

일부 Windows Server 2012 R2 RDSH 서버에서 메모리 누수가 발견되었습니다. 시간이 지나면서 이러한 서버가 다음과 같은 메시지와 함께 원격 데스크톱 연결 및 로컬 콘솔 로그인을 거부하기 시작합니다.

> 원격 데스크톱 서비스가 현재 사용 중이므로 수행하려는 작업을 완료할 수 없습니다. 몇 분 후에 다시 시도하세요. 다른 사용자는 여전히 로그인할 수 있어야 합니다.

또한 연결을 시도하는 원격 데스크톱 클라이언트가 응답하지 않습니다.

이 이슈를 해결하려면 RDSH 서버를 다시 시작합니다.

이 이슈를 해결하려면 KB 4093114, [2018년 4월 10일 - KB4093114(월별 롤업)](file:///C:/Users/v-jesits/AppData/Local/Microsoft/Windows/INetCache/Content.Outlook/FUB8OO45/April%2010,%202018—KB4093114%20(Monthly%20Rollup))을 RDSH 서버에 적용합니다.

### <a name="rd-listener-issue"></a>RD 수신기 이슈

Windows Server 2008 R2에서 Windows Server 2012 R2 또는 Windows Server 2016으로 바로 업그레이드된 일부 RDSH 서버에서 이슈가 발견되었습니다. 원격 데스크톱 클라이언트가 RDSH 서버에 연결할 때 RDSH 서버가 사용자 세션에 대한 RD 수신기를 만듭니다. 영향을 받는 서버는 사용자가 연결할 때 RD 수신기 수를 늘리기만 하고 줄이지는 않습니다.

이 이슈를 해결하려면 다음 방법을 사용합니다.

  - RDSH 서버를 다시 시작하여 RD 수신기 수를 초기화합니다.
  - 연결 제한을 매우 큰 값으로 설정하여 정책을 수정합니다. 연결 제한 정책 관리에 대한 자세한 내용은 [연결 제한 정책 확인](#check-the-connection-limit-policy)을 참조하세요.

이 이슈를 해결하려면 다음 업데이트를 RDSH 서버에 적용합니다.

  - Windows Server 2012 R2: KB 4343891, [2018년 8월 30일 - KB4343891(월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884, [2018년 8월 30일 - KB4343884(OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### <a name="check-the-connection-limit-policy"></a>연결 제한 정책 확인

개별 컴퓨터 수준에서 또는 GPO(그룹 정책 개체)를 구성하여 동시 원격 데스크톱 연결 수 제한을 설정할 수 있습니다. 기본적으로 제한은 설정되지 않습니다.

RDSH 서버의 현재 설정을 확인하고 기존 GPO를 파악하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력합니다.
  
```
gpresult /H c:\gpresult.html
```
   
이 명령이 완료되면 gpresult.html 파일을 열고, **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결**에서 **연결 수 제한** 정책을 찾습니다.

  - 이 정책을 **사용 안 함**으로 설정하면 그룹 정책이 RDP 연결을 제한하지 않습니다.
  - 이 정책이 **사용**으로 설정된 경우 **최우선 GPO**를 확인합니다. 연결 제한을 제거 또는 변경해야 하는 경우 이 GPO를 편집합니다.

정책 변경 내용을 적용하려면 영향을 받는 컴퓨터에서 명령 프롬프트 창을 열고 다음 명령을 입력합니다.
  
```
gpupdate /force
```
  
## <a name="rd-client-disconnects-and-cannot-reconnect-to-the-same-session"></a>RD 클라이언트의 연결이 끊어지고 동일한 세션에 다시 연결할 수 없음

원격 데스크톱 클라이언트와 원격 데스크톱의 연결이 끊어진 후 클라이언트가 즉시 다시 연결할 수 없습니다. 사용자가 다음과 같은 오류 메시지를 수신합니다.

  - 보안 오류로 인해 클라이언트가 터미널 서버에 연결할 수 없습니다. 네트워크에 로그온되었는지 확인한 후 서버에 다시 연결해 보세요.
  - 원격 데스크톱 연결이 끊어졌습니다. 보안 오류로 인해 클라이언트가 원격 컴퓨터에 연결할 수 없습니다. 네트워크에 로그온되어 있는지 확인하고 다시 연결하세요.

나중에 원격 데스크톱 클라이언트가 원격 데스크톱에 다시 연결합니다. 그러나 클라이언트를 원래 세션에 연결하는 대신, RDSH 서버가 클라이언트를 새 세션에 연결합니다. RDSH 서버를 확인해 보면 원래 세션이 연결 끊김 상태로 전환되지 않고 활성 상태를 유지하는 것을 알 수 있습니다.

이 이슈를 해결하려면 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\ 원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결** 그룹 정책 폴더에서 **Keep-alive 연결 간격 구성** 정책을 사용하도록 설정합니다. 이 정책을 사용하는 경우 keep-alive 간격을 입력해야 합니다. keep-alive 간격에 따라 서버가 세션 상태를 확인하는 빈도(분)가 결정됩니다.

인증 및 구성 설정을 잘못 구성하면 이 이슈가 발생할 수 있습니다. 서버 수준에서 또는 GPO를 사용하여 이러한 설정을 구성할 수 있습니다. 그룹 정책 설정은 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\보안** 그룹 정책 폴더에서 사용할 수 있습니다.

1. RD 세션 호스트 서버에서 권한이 상승된 명령 프롬프트 창을 엽니다.
2. **연결** 아래에서 연결 이름을 마우스 오른쪽 단추로 클릭한 다음, **속성**을 클릭합니다.
3. 연결에 대한 **속성** 대화 상자의 **일반** 탭, **보안** 레이어에서 보안 방법을 선택합니다.
4. **암호화 수준**에서 원하는 수준을 클릭합니다. **낮음**, **클라이언트 호환**, **높음** 또는 **FIPS 규격** 중에서 선택할 수 있습니다.

> [!NOTE]  
>  - 클라이언트와 RD 세션 호스트 서버 간의 통신에 최고 수준의 암호화가 필요하면 FIPS 규격 암호화를 사용합니다.
>  - 그룹 정책에서 구성하는 암호화 수준 설정은 원격 데스크톱 서비스 구성 도구를 사용하여 설정하는 구성을 재정의합니다. 또한 [시스템 암호화: 암호화, 해시, 서명에 FIPS 규격 알고리즘 사용](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) 정책을 사용하면 이 설정이 **클라이언트 연결 암호화 수준 설정** 정책을 재정의합니다. 시스템 암호화 정책은 **컴퓨터 구성\\Windows 설정\\보안 설정\\로컬 정책\\보안 옵션** 폴더에 있습니다.
>  - 암호화 수준을 변경하면 새로운 암호화 수준이 사용자가 다음에 로그온할 때 적용됩니다. 서버에 여러 암호화 수준이 필요한 경우 네트워크 어댑터를 여러 개 설치하고 각 어댑터를 별도로 구성합니다.
>  - 인증서에 상응하는 프라이빗 키가 있는지 확인하려면 원격 데스크톱 서비스 구성에서 인증서를 보려는 연결을 마우스 오른쪽 단추로 클릭하고, **일반**을 선택하고, **편집**을 선택하고, 보고 싶은 인증서를 선택하고, **인증서 보기**를 선택합니다. **일반** 탭 맨 아래에 "사용자가 이 인증서와 일치하는 프라이빗 키를 갖고 있습니다"라는 메시지가 표시되어야 합니다. 인증서 스냅인을 사용하여 이 정보를 볼 수도 있습니다.
>  - FIPS 규격 암호화(**시스템 암호화: 암호화, 해시, 서명에 FIPS 규격 알고리즘 사용** 정책 또는 원격 데스크톱 서버 구성의 **FIPS 규격** 설정)는 FIPS(Federal Information Processing Standard) 140-1 암호화 알고리즘에 따라 Microsoft 암호화 모듈을 사용하여 클라이언트에서 서버로 보낸 데이터와 서버에서 클라이언트로 보낸 데이터를 암호화 및 암호 해독합니다. 자세한 내용은 [FIPS 140 유효성 검사](https://docs.microsoft.com/windows/security/threat-protection/fips-140-validation)를 참조하세요.
>  - **높음** 설정은 클라이언트에서 서버로 보낸 데이터와 서버에서 클라이언트로 보낸 데이터를 강력한 128비트 암호화를 통해 암호화합니다.
>  - **클라이언트 호환** 설정은 클라이언트와 서버 간에 주고 받는 데이터를 클라이언트에서 지원하는 최대 키 강도로 암호화합니다.
>  - **낮음** 설정은 클라이언트에서 서버로 보낸 데이터를 56비트로 암호화합니다.

## <a name="remote-laptop-disconnects-from-wireless-network"></a>무선 네트워크에서 원격 노트북 연결 끊김

이 이슈는 원격 데스크톱 클라이언트가 802.1x 무선 네트워크를 사용하여 노트북 컴퓨터에 연결할 때 발생할 수 있습니다. 노트북의 무선 네트워크 연결이 끊어진 후 자동으로 다시 연결하지 않는 경우가 가끔 있습니다.

이는 무선 네트워크 연결에 대한 네트워크 인증 설정이 **사용자 인증**일 때 발생하는 알려진 이슈입니다.

이 이슈를 해결하려면 네트워크 인증 설정을 **사용자 또는 컴퓨터 인증** 또는 **컴퓨터 인증**으로 설정합니다.

 > [!NOTE]  
> 단일 컴퓨터에서 네트워크 인증 설정을 변경하려면 네트워크 및 공유 센터 제어판을 사용하여 새로운 설정으로 새 무선 연결을 만들어야 합니다.

GPO를 사용하여 무선 네트워크 설정을 구성하는 방법에 대한 전체 설명은 [무선 네트워크(IEEE 802.11) 정책 구성](https://docs.microsoft.com/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)을 참조하세요.

## <a name="user-experiences-poor-performance-or-application-problems"></a>사용자 환경의 성능이 저하되거나 애플리케이션에서 문제 발생

이 섹션에서는 사용자가 원격 데스크톱 기능을 사용할 때 발생할 수 있는 몇 가지 일반적인 이슈를 해결합니다.

  - [새 가상 머신 Microsoft Azure에 연결하는 사용자가 가끔 문제를 겪을 수 있습니다](#intermittent-problems-with-new-microsoft-azure-virtual-machines).
  - [Windows 10 버전 1709 원격 데스크톱에 연결하는 사용자가 비디오 재생 문제를 겪을 수 있습니다](#video-playback-issues-on-windows-10-version-1709).
  - [읽기 전용 사용자 프로필을 사용하여 Windows 10 원격 데스크톱에 연결하는 사용자는 데스크톱을 공유할 수 없습니다.](#desktop-sharing-issues-on-windows-10)
  - [이전 버전의 Windows 10에서 실행되는 클라이언트를 사용하여 Windows 10 원격 데스크톱에 연결하는 사용자는 NLA를 해제할 경우 성능 저하를 경험합니다.](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [사용자가 원격 데스크톱 세션에서 여러 애플리케이션을 실행하고 연결 해제 및 다시 연결을 자주 수행하면 다시 연결할 때 검은색 화면이 발생할 수 있습니다.](#black-screen-issue)

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>새 Microsoft Azure 가상 머신의 일시적인 문제

이 이슈는 최근에 프로비저닝된 가상 머신에 영향을 줍니다. 사용자가 가상 머신에 연결한 후 원격 데스크톱 세션에서 일부 사용자 설정을 올바르게 로드하지 않을 수 있습니다.

이 이슈를 해결하려면 가상 머신에서 연결을 끊고, 20분 이상 기다렸다가 다시 연결합니다.

이 이슈를 해결하려면 다음 업데이트를 가상 머신에 적절하게 적용합니다.

  - Windows 10 및 Windows Server 2016: KB 4343884, [2018년 8월 30일 - KB4343884(OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [2018년 8월 30일 - KB4343891(월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Windows 10 버전 1709의 비디오 재생 이슈

이 이슈는 사용자가 Windows 10 버전 1709를 실행하는 원격 컴퓨터에 연결할 때 발생합니다. 이러한 사용자가 VMR9(비디오 믹싱 렌더러 9) 코덱을 사용하여 비디오를 재생하면 검은색 창만 표시됩니다.

이는 Windows 10 버전 1709에서 알려진 이슈입니다. Windows 10 버전 1703에서는 이 이슈가 발생하지 않습니다.

### <a name="desktop-sharing-issues-on-windows-10"></a>Windows 10의 데스크톱 공유 이슈

이 이슈는 키오스크 시나리오처럼 사용자가 읽기 전용 사용자 프로필(및 관련된 레지스트리 하이브)을 갖고 있는 경우에 발생합니다. 이러한 사용자는 Windows 10 버전 1803을 실행하는 원격 컴퓨터에 연결할 때 데스크톱을 공유할 수 없습니다.

이 이슈를 해결하려면 Windows 10 업데이트 4340917, [2018년 7월 24일 - KB4340917(OS 빌드 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917)을 적용합니다.

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>NLA를 사용하지 않도록 설정하면 Windows 10 버전을 혼합할 때 성능 이슈 발생

NLA를 사용하지 않도록 설정하고, Windows 10을 실행하는 원격 데스크톱 클라이언트 컴퓨터가 다른 버전의 Windows 10을 실행하는 원격 데스크톱에 연결하는 경우 이 이슈가 발생합니다. Windows 10 버전 1709 이하를 실행하는 컴퓨터의 원격 데스크톱 클라이언트 사용자는 Windows 10 버전 1803 이상을 실행하는 원격 데스크톱에 연결할 때 성능 저하를 경험합니다.

NLA를 사용하지 않도록 설정하면 이전 클라이언트 컴퓨터가 Windows 10 버전 1803 이상에 연결할 때 속도가 느린 프로토콜을 사용하므로 이 문제가 발생합니다.

이 이슈를 해결하려면 KB 4340917, [2018년 7월 24일 - KB4340917(OS 빌드 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917)을 적용합니다.

### <a name="black-screen-issue"></a>검은색 화면 이슈

이 이슈는 Windows 8.0, Windows 8.1, Windows 10 RTM 및 Windows Server 2012 R2에서 발생합니다. 사용자는 원격 데스크톱에서 여러 애플리케이션을 시작한 다음, 세션 연결을 종료합니다. 사용자는 주기적으로 원격 데스크톱에 다시 연결하여 애플리케이션과 상호 작용한 다음, 다시 연결을 끊습니다. 어느 시점에 사용자가 다시 연결하면 원격 데스크톱 세션에서 검은색 화면만 표시합니다. 사용자는 원격 컴퓨터의 콘솔(또는 RDSH 서버 콘솔)에서 원격 데스크톱 세션을 종료해야 합니다. 이 작업은 애플리케이션을 중지합니다.

이 이슈를 해결하려면 다음 업데이트를 적절하게 적용합니다.

  - Windows 8 및 Windows Server 2012: KB4103719, [2018년 5월 17일 - KB4103719(월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 및 Windows Server 2012 R2: KB4103724, [2018년 5월 17일 - KB4103724(월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) 및 KB 4284863, [2018년 6월 21일 - KB4284863(월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10: KB4284860, [2018년 6월 12일 - KB4284860(OS 빌드 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)에서 수정됨
