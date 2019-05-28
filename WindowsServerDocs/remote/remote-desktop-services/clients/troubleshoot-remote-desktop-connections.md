---
title: 원격 데스크톱 연결 문제 해결
description: 증상으로 정렬 하는 문제 해결 절차
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
ms.openlocfilehash: 4bbdd17f5e6e2b161e0dda0e172ea862a9107841
ms.sourcegitcommit: 564158d760f902ced7f18e6d63a9daafa2a92bd4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2019
ms.locfileid: "64988333"
---
# <a name="troubleshooting-remote-desktop-connections"></a>원격 데스크톱 연결 문제 해결
원격 데스크톱 서비스 (RDS) 문제의 가장 일반적인 몇 가지 간략 한 설명을 참조 하세요 [원격 데스크톱 클라이언트에 대 한 질문과 대답](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq)합니다. 이 문서에서는 연결 문제를 해결 하려면 몇 가지 고급 방법을 설명 합니다. 이러한 절차의 여러 다른 물리적 컴퓨터 또는 더 복잡 한 구성에 연결 하는 하나의 물리적 컴퓨터와 같은 간단한 구성을 통해 문제를 해결할 지 여부를 적용 합니다. 일부 절차는 보다 복잡 한 다중 사용자 시나리오에만 발생 하는 문제를 해결 합니다. 원격 데스크톱 구성 요소와 함께 작동 하는 방법에 대 한 자세한 내용은 참조 하세요. [원격 데스크톱 서비스 아키텍처](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture)합니다.

> [!NOTE]  
> 대부분의이 문서에 설명 된 절차를 필요한 여러 컴퓨터에 원격으로 액세스 해야 할 수 있습니다 중 일부에 액세스할 수 있습니다. 원격 관리 도구 및 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오 [원격 서버 관리 도구 (RSAT) Windows 운영 체제에 대 한](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)합니다.

다음 목록에서 사용자 (또는 사용자)에서 발생 하는 현상의 유형을 식별 합니다.

- [원격 데스크톱 클라이언트, 원격 데스크톱에 연결할 수 없습니다. 있지만 특정 증상 또는 메시지 (일반 문제 해결 단계)에 없습니다.](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [원격 데스크톱 클라이언트, 원격 데스크톱에 연결할 수 없습니다 및 "클래스가 등록 되지 않았습니다." 메시지를 수신 합니다.](#client-cannot-connect-class-not-registered)
- [원격 데스크톱 클라이언트는 원격 데스크톱에 연결할 수 없습니다 받고는 "사용 가능한 라이선스가" 또는 "보안 오류" 메시지](#client-cannot-connect-no-licenses-available)
- [사용자 "액세스 거부" 메시지를 수신 하거나 자격 증명을 두 번 제공 해야 합니다.](#user-cannot-authenticate-or-must-authenticate-twice)
- [연결에 "원격 데스크톱 서비스는 현재 사용 중" 메시지가](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [원격 데스크톱 클라이언트 연결을 끊고 동일한 세션에 다시 연결할 수 없습니다.](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [무선 네트워크를 통해 원격 모드 상태의 랩톱 사용자가 연결 하 고 다음 네트워크에서 연결이 끊깁니다 랩톱](#remote-laptop-disconnects-from-wireless-network)합니다.
- [사용자 환경을 성능이 저하 되거나 원격 응용 프로그램 문제](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> RDP 연결 끊기 코드의 현재 목록에 대해서 [ExtendedDisconnectReasonCode 열거형](https://docs.microsoft.com/en-us/windows/desktop/TermServ/extendeddisconnectreasoncode)합니다. 

## <a name="no-specific-symptoms-or-messages-general-troubleshooting-steps"></a>특정 증상 없거나 메시지 (일반 문제 해결 단계)

원격 데스크톱 클라이언트를 원격 데스크톱에 연결할 수 없습니다 하지만 메시지 또는 다른 증상 도움이 되는 원인을 식별 하는 것을 제공 하지 않습니다 하는 경우 다음이 단계를 사용 합니다. 이러한 문제의 가장 일반적인 원인은 많은 문제를 해결 하려면 다음 메서드를 사용 합니다.

- [RDP 프로토콜의 상태를 확인 합니다.](#check-the-status-of-the-rdp-protocol)
- [RDP 서비스의 상태를 확인 합니다.](#check-the-status-of-the-rdp-services)
- [RDP 수신기가 작동 하는지 확인 합니다.](#check-that-the-rdp-listener-is-functioning)
- [RDP 수신기 포트를 확인 합니다.](#check-the-rdp-listener-port)

### <a name="check-the-status-of-the-rdp-protocol"></a>RDP 프로토콜의 상태를 확인 합니다.

#### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>로컬 컴퓨터에서 RDP 프로토콜의 상태를 확인 합니다.

확인 하 고 로컬 컴퓨터에서 RDP 프로토콜의 상태를 변경 하려면 참조 [원격 데스크톱을 사용 하도록 설정 하는 방법을](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)합니다.

> [!NOTE]  
> 원격 데스크톱 옵션을 사용할 수 없는 경우 [그룹 정책 개체를 RDP를 차단 하 고 있는지 여부를 확인](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)합니다.

#### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>원격 컴퓨터에서 RDP 프로토콜의 상태를 확인 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정 하기 전에 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 문제가 발생할 경우.

확인 하 고 원격 컴퓨터에서 RDP 프로토콜의 상태를 변경 하려면 네트워크 레지스트리 연결을 사용 합니다.

1. 선택 **시작**를 선택 **실행**를 입력 한 다음 **regedt32**합니다.
2. 레지스트리 편집기에서 선택 **파일**를 선택한 후 **네트워크 레지스트리 연결**합니다.
3. 에 **컴퓨터 선택** 대화 상자, 원격 컴퓨터의 이름을 입력 한 다음 선택 **이름 확인**를 선택한 후 **확인**합니다.
4. 이동할 **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\컨트롤\\터미널 서버**합니다.  
   ![레지스트리 편집기를 fDenyTSConnections 항목 표시](..\media\troubleshoot-remote-desktop-connections\RegEntry_fDenyTSConnections.png)
   - 하는 경우의 값을 **fDenyTSConnections** 키는 **0**, RDP 사용 됩니다
   - 하는 경우의 값을 **fDenyTSConnections** 키는 **1**, RDP를 사용 하지 않도록 설정 하는 다음
5. RDP를 사용 하려면 값을 변경 **fDenyTSConnections** 에서 **1** 하 **0**합니다.

#### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>그룹 정책 개체 (GPO)는 로컬 컴퓨터에서 RDP를 차단 여부를 확인 합니다.

사용자 인터페이스의 RDP를 설정할 수 없습니다 아니면 값 **fDenyTSConnections** 되돌아갑니다 **1** GPO를 해당 작업을 변경한 후 컴퓨터 수준 설정을 보다 우선할 수 있습니다.

로컬 컴퓨터에서 그룹 정책 구성을 확인 하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력 합니다.
```
gpresult /H c:\gpresult.html
```
이 명령은 완료 되 면 gpresult.html를 엽니다. **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결**, 찾을 합니다 **원격 데스크톱 서비스를 사용 하 여 원격으로 연결할 수 있도록** 정책입니다.

- 이 정책에 대 한 설정이 **사용**, 그룹 정책 RDP 연결을 차단 하지.
- 이 정책에 대 한 설정이 **사용 안 함**, 체크 **최우선 GPO**합니다. RDP 연결을 차단 하는 GPO입니다.
![예제 세그먼트를 나타나는 gpresult.html 도메인 수준 GPO * * 블록 RDP * *은 RDP를 비활성화 합니다.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_GP.png)
   
  ![gpresult.html의 예에서는 세그먼트를 * * 로컬 그룹 정책 * *은 RDP를 비활성화 합니다.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_LGP.png)

#### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>GPO는 원격 컴퓨터에서 RDP를 차단 여부를 확인 합니다.

원격 컴퓨터에서 그룹 정책 구성을 확인 하려면 명령이입니다 로컬 컴퓨터와 거의 동일 합니다.
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
이 명령은 생성 된 파일 (**gpresult-\<컴퓨터 이름\>.html**) 로컬 컴퓨터 버전으로 동일한 정보 형식을 사용 (**gpresult.html**) 사용 합니다.

#### <a name="modifying-a-blocking-gpo"></a>차단 GPO를 수정합니다.

그룹 정책 개체 편집기 (GPE) 및 그룹 정책 관리 콘솔 (GPM)에서 이러한 설정을 수정할 수 있습니다. 그룹 정책을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [고급 그룹 정책 관리](https://docs.microsoft.com/en-us/microsoft-desktop-optimization-pack/agpm/)합니다.

차단 정책을 수정 하려면 다음 방법 중 하나를 사용 합니다.

- 로 이동한 GPE 합니다 (예: 로컬 또는 도메인)에 적절 한 수준의 GPO에 액세스할 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\Remote Desktop Services\\ 원격 데스크톱 세션 호스트\\연결**\\**Remote Desktop Services를 사용 하 여 원격으로 연결할 수 있도록**입니다.  
   1. 정책을 설정 **Enabled** 또는 **구성 되지 않은**합니다.
   2. 영향을 받는 컴퓨터에서 관리자로 명령 프롬프트 창을 열고 실행 합니다 **gpupdate /force** 명령입니다.
- GPM에서 차단 정책 영향을 받는 컴퓨터에 적용 되는 OU에 이동 하 고 OU에서 정책을 삭제 합니다.

### <a name="check-the-status-of-the-rdp-services"></a>RDP 서비스의 상태를 확인 합니다.

로컬 클라이언트 컴퓨터와 원격 (대상) 컴퓨터에서 다음 서비스가 실행 해야 합니다.

- 원격 데스크톱 서비스 (TermService)
- 원격 데스크톱 서비스 UserMode 포트 리디렉터 (UmRdpService)

로컬 또는 원격으로 서비스를 관리 하려면 서비스 MMC 스냅인을 사용할 수 있습니다. 로컬 또는 원격으로 PowerShell 사용할 수도 있습니다 (경우 원격 컴퓨터 허용 하도록 구성 된 원격 PowerShell 명령).

![서비스 MMC 스냅인에서 원격 데스크톱 서비스. 기본 서비스 설정을 수정 하지 마십시오.](..\media\troubleshoot-remote-desktop-connections\RDSServiceStatus.png)

어느 쪽 컴퓨터 든, 하나 또는 두 서비스를 실행 하지 않는 경우 해당 시작 합니다.

> [!NOTE]  
> 원격 데스크톱 서비스를 시작 하는 경우 클릭 **예** 자동으로 원격 데스크톱 서비스 UserMode 포트 리디렉터 서비스 다시 시작 합니다.

### <a name="check-that-the-rdp-listener-is-functioning"></a>RDP 수신기가 작동 하는지 확인 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정 하기 전에 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 문제가 발생할 경우.

#### <a name="check-the-status-of-the-rdp-listener"></a>RDP 수신기의 상태를 확인 합니다.

이 절차에 대 한 관리 권한이 있는 PowerShell 인스턴스를 사용 합니다. 로컬 컴퓨터에 대 한 관리 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 그러나이 절차는 로컬 및 원격 모두 동일한 명령을 작동 하기 때문에 PowerShell를 사용 합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결 하려면 입력 **Enter-pssession-ComputerName \<컴퓨터 이름\>** 합니다.
2. 입력 **qwinsta**합니다. 
    ![Qwinsta 명령은 컴퓨터의 포트에서 수신 하는 프로세스를 나열 합니다.](..\media\troubleshoot-remote-desktop-connections\WPS_qwinsta.png)
3. 목록에 포함 된 경우 **: rdp-tcp** 상태의 **수신**, RDP 수신기가 작동 합니다. 진행 [RDP 수신기 포트 확인](#check-the-rdp-listener-port)합니다. 그렇지 않은 경우 4 단계에서 계속 합니다.
4. 작동 중인 컴퓨터에서 RDP 수신기 구성을 내보냅니다.
    1. 영향을 받는 컴퓨터에 동일한 운영 체제 버전에 있는 컴퓨터에 로그인 하 고 (예를 들어 레지스트리 편집기를 사용)가 해당 컴퓨터의 레지스트리에 액세스 합니다.
    2. 다음 레지스트리 항목으로 이동 합니다.  
        **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\제어\\터미널 서버\\WinStations\\Rdp-tcp**
    3. .Reg 파일에 항목을 내보냅니다. 예를 들어 레지스트리 편집기에서 항목을 마우스 오른쪽 단추로 클릭 하 여 선택 합니다 **내보내기**를 선택한 다음 내보낸된 설정 파일 이름을 입력 합니다.
    4. 영향을 받는 컴퓨터에 내보낸된.reg 파일을 복사 합니다.
5. RDP 수신기 구성, 영향을 받는 컴퓨터에 대 한 관리 권한이 있는 PowerShell 창을 엽니다 (또는 PowerShell 창을 열고 가져오고 영향을 받는 컴퓨터에 원격으로 연결할).
   1. 기존 레지스트리 항목을 백업 하려면 다음 명령을 입력 합니다.  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 기존 레지스트리 항목을 제거 하려면 다음 명령을 입력 합니다.  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 새 레지스트리 항목을 가져오고 서비스를 다시 시작 후, 다음 명령을 입력 합니다.  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      여기서 \<filename\> 내보낸된.reg 파일의 이름입니다.
6. 원격 데스크톱 연결을 다시 시도 하 여 구성을 테스트 합니다. 여전히 연결할 수 없는 경우에 영향을 받는 컴퓨터 다시 시작 합니다.
7. 여전히 연결할 수 없는 경우 [RDP 자체 서명 된 인증서의 상태를 확인할](#check-the-status-of-the-rdp-self-signed-certificate)합니다.

#### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>RDP 자체 서명 된 인증서의 상태를 확인 합니다.

1. 여전히 연결할 수 없는 경우에 인증서 MMC 스냅인을 엽니다. 경우 관리를 인증서 저장소를 선택 하 라는 메시지가 표시 **컴퓨터 계정**, 영향을 받는 컴퓨터를 선택 합니다.
2. 에 **인증서** 아래에 폴더 **원격 데스크톱**, RDP 자체 서명 된 인증서를 삭제 합니다. 
    ![MMC 인증서 스냅인에서 원격 데스크톱 인증서입니다.](..\media\troubleshoot-remote-desktop-connections\MMCCert_Delete.png)
3. 영향을 받는 컴퓨터에서 원격 데스크톱 서비스를 다시 시작 합니다.
4. 인증서 스냅인을 새로 고칩니다.
5. RDP 자체 서명 된 인증서를 다시 생성 되지 않았으면 [MachineKeys 폴더의 사용 권한을 확인](#check-the-permissions-of-the-machinekeys-folder)합니다.

#### <a name="check-the-permissions-of-the-machinekeys-folder"></a>MachineKeys 폴더의 사용 권한을 확인합니다

1. 영향을 받는 컴퓨터에서 탐색기를 열고 다음 이동할 **c:\\ProgramData\\Microsoft\\Crypto\\RSA\\** 합니다.
2. 마우스 오른쪽 단추로 클릭 **MachineKeys**를 선택 **속성**를 선택 **보안**를 선택한 후 **고급**합니다.
3. 다음 사용 권한이 구성 되어 있는지 확인 합니다.
      - 기본 제공\\관리자: 모든 권한
      - 모든 사용자: 읽기, 쓰기

### <a name="check-the-rdp-listener-port"></a>RDP 수신기 포트를 확인 합니다.

로컬 클라이언트 컴퓨터와 원격 (대상) 컴퓨터에서 RDP 수신기 포트 3389에서 수신 대기 해야 합니다. 다른 응용 프로그램이이 포트를 사용 해야 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정 하기 전에 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 문제가 발생할 경우.

을 확인 하거나 RDP 포트를 변경 하려면 레지스트리 편집기를 사용 합니다.

1. 시작을 선택 **실행**, 누릅니다 **regedt32**합니다.
      - 원격 컴퓨터에 연결 하려면 선택 **파일**를 선택한 후 **네트워크 레지스트리 연결**합니다.
      - 에 **컴퓨터 선택** 대화 상자, 원격 컴퓨터의 이름을 입력 한 다음 선택 **이름 확인**를 선택한 후 **확인**합니다.
2. 레지스트리를 열고 이동할 **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\컨트롤\\터미널 서버\\WinStations\\ \<수신기\>** 합니다. 
    ![PortNumber 하위 키를 RDP 프로토콜에 대 한 합니다.](..\media\troubleshoot-remote-desktop-connections\RegEntry_PortNumber.png)
3. 하는 경우 **PortNumber** 이외의 값이 **3389**을로 변경 **3389**합니다. 
   > [!IMPORTANT]  
    > 다른 포트를 사용 하 여 원격 데스크톱 서비스를 작동할 수 있습니다. 그러나이 수행 하지 않는 것이 좋습니다. 이러한 구성 문제 해결이 문서의 범위를 벗어납니다.
4. 포트 번호를 변경한 후 원격 데스크톱 서비스를 다시 시작 합니다.

#### <a name="check-that-another-application-is-not-trying-to-use-the-same-port"></a>다른 응용 프로그램에 동일한 포트를 사용 하려는 아닌지 확인 합니다.

이 절차에 대 한 관리 권한이 있는 PowerShell 인스턴스를 사용 합니다. 로컬 컴퓨터에 대 한 관리 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 그러나이 절차는 동일한 명령을 로컬 및 원격으로 작업 하기 때문에 PowerShell를 사용 합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결 하려면 입력 **Enter-pssession-ComputerName \<컴퓨터 이름\>** 합니다.
2. 다음 명령을 입력합니다.  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Netstat 명령에는 포트 및 수신 대기 하는 서비스의 목록을 생성 합니다.](..\media\troubleshoot-remote-desktop-connections\WPS_netstat.png)
1. 상태가 **Listening**인 TCP 포트 3389 또는 할당된 RDP 포트의 항목을 찾습니다. 
    > [!NOTE]  
   > 해당 포트를 사용하는 서비스나 프로세스의 PID(프로세스 식별자)가 PID 열 아래에 나타납니다.
1. 포트 3389 (또는 할당 된 RDP 포트)는 응용 프로그램 사용을 확인 하려면 다음 명령을 입력 합니다.  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Tasklist 명령을 특정 프로세스의 세부 정보를 보고합니다.](..\media\troubleshoot-remote-desktop-connections\WPS_tasklist.png)
1. 포트와 연결 된 PID 번호에 대 한 항목을 찾습니다 (에서 합니다 **netstat** 출력). 서비스 또는 해당 PID와 연결 된 프로세스를 오른쪽에 표시 됩니다.
1. 응용 프로그램 또는 서비스 원격 데스크톱 서비스 (TermServ.exe) 이외의 포트를 사용 중인 경우에 다음 방법 중 하나를 사용 하 여 충돌을 해결할 수 있습니다.
      - 다른 응용 프로그램 또는 서비스 (권장) 다른 포트를 사용 하도록 구성 합니다.
      - 다른 응용 프로그램 또는 서비스를 제거 합니다.
      - 다른 포트를 사용 하는 RDP를 구성 하 고 (권장 하지 않음) 원격 데스크톱 서비스 서비스를 다시 시작 합니다.

#### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>방화벽 RDP 포트를 차단 하 고 있는지 여부를 확인 합니다.

사용 된 **psping** 포트 3389를 사용 하 여 영향을 받는 컴퓨터를 연결할 수 있는지 여부를 테스트 도구입니다.

1. 영향을 받는 컴퓨터에서 다른 컴퓨터에 다운로드 **psping** 에서 <https://live.sysinternals.com/psping.exe>합니다.
2. 관리자 권한으로 명령 프롬프트 창을 열고, 설치 된 디렉터리로 변경 **psping**, 다음 명령을 입력 합니다.  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. 출력을 확인 합니다 **psping** 다음과 같이 결과 대 한 명령:  
      - **연결할 \<컴퓨터 IP\>** : 원격 컴퓨터에 연결할 수 있습니다.
      - **(0% 손실)** : 연결 하려는 모든 시도 성공 했습니다.
      - **원격 컴퓨터에서 네트워크 연결을 거부**: 원격 컴퓨터에 연결할 수 없습니다.
      - **(100% 손실)** : 연결 하려는 모든 시도가 실패 합니다.
1. 실행할 **psping** 영향을 받는 컴퓨터에 연결 하는 기능을 테스트 하려면 여러 컴퓨터에서.
1. 영향을 받는 컴퓨터에서 다른 모든 컴퓨터, 다른 컴퓨터 또는 다른 컴퓨터는 하나의 연결을 차단 하는지 여부를 note 합니다.
1. 다음 단계를 권장 합니다.
      - 네트워크에 영향을 받는 컴퓨터에 RDP 트래픽을 허용 하는지 확인 하려면 네트워크 관리자를 참여 합니다.
      - 방화벽 RDP 포트를 차단 하 고 있는지 여부를 확인 하려면 원본 컴퓨터와 영향을 받는 컴퓨터 (영향을 받는 컴퓨터의 Windows 방화벽을 포함) 간의 모든 방화벽의 구성을 조사 합니다.

## <a name="client-cannot-connect-class-not-registered"></a>클라이언트가 연결할 수 없습니다 "클래스가 등록 되지 않았습니다"

Windows 10 버전 1709 실행 하는 클라이언트를 사용 하 여 원격 컴퓨터에 연결 하려고 하면 때나 나중에 클라이언트 수를 연결할 원격 데스크톱 세션 호스트 서버에 메시지를 보고 하는 동안 "클래스 등록된 되지 않은 (0x80040154)" 오류 코드를 포함 하는 합니다.

연결 하려는 사용자가 필수 사용자 프로필을 하는 경우이 문제가 발생 합니다. 이 문제를 해결 하려면 설치 합니다 [2018 년 7 월 24 일-KB4338817 (OS 빌드 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10 업데이트 합니다.

## <a name="client-cannot-connect-no-licenses-available"></a>클라이언트가 연결할 수 없는 경우 사용 가능한 라이선스가 없습니다.

이 상황을 RDSH 서버 및 원격 데스크톱 라이선스 서버를 포함 하는 배포에 적용 됩니다.

사용자가 표시 되는 동작의 종류를 식별 합니다.

- 사용할 수 없는 라이선스 또는 라이선스 서버가 없는 때문에 세션 연결이 끊어진
- 보안 오류로 인해 액세스가 거부 되었습니다.

도메인 관리자로 RD 세션 호스트에 로그인 하 고 RD 라이선스 진단 도구를 엽니다. 다음과 같은 메시지를 찾습니다.

  - 유예 기간을 원격 데스크톱 세션 호스트 서버 만료 되었지만 RD 세션 호스트 서버 라이선스 서버를 사용 하 여 구성 되지 않았습니다. RD 세션 호스트 서버와 연결 하는 RD 세션 호스트 서버에 대 한 라이선스 서버를 구성 하지 않으면 거부 됩니다.
  - 라이선스 서버 \<컴퓨터 이름\> 를 사용할 수 없습니다. 네트워크 연결 문제로 인해 발생할 수 없습니다, 원격 데스크톱 라이선스 서비스가 라이선스 서버에서 중지 된 또는 컴퓨터에서 RD 라이선싱가 설치 되지 않은 합니다.

이러한 문제 다음 사용자 메시지를 사용 하 여 연결 되어야 하는 경향이 있습니다.

  - 이 컴퓨터에 대 한 사용 가능한 원격 데스크톱 클라이언트 액세스 라이선스가 없습니다 없으므로 원격 세션이 끊겼습니다 수 있습니다.
  - 라이선스를 제공할 수 있는 원격 데스크톱 라이선스 서버가 없으므로 원격 세션이 끊겼습니다 수 있습니다.

이 예에서 [RD 라이선싱 서비스 구성](#configure-the-rd-licensing-service)합니다.

RD 라이선스 진단 도구 "RDP 프로토콜 X.224 구성 요소에서 프로토콜 스트림의 오류를 검색 및 클라이언트 연결이 끊겼습니다." 있을 같은 다른 문제를 나열 하는 경우 라이선스 인증서에 영향을 주는 문제일 수 있습니다. 이러한 문제는 다음과 같은 사용자 메시지를 사용 하 여 연결 되어야 하는 경향이 있습니다.

클라이언트 보안 오류로 인해 터미널 서버에 연결 하지 못했습니다. 네트워크에 로그온 되었는지, 후 서버에 다시 연결을 시도 합니다.

이 예에서 [새로 고침 X509 인증서 레지스트리 키](#refresh-the-x509-certificate-registry-keys)합니다.

### <a name="configure-the-rd-licensing-service"></a>RD 라이선싱 서비스 구성

다음 절차는 서버 관리자를 사용 하 여 구성을 변경 합니다. 구성 서버 관리자를 사용 하는 방법에 대 한 정보를 참조 하세요 [서버 관리자](https://docs.microsoft.com/en-us/windows-server/administration/server-manager/server-manager)합니다.

1. 서버 관리자를 열고 다음 이동할 **원격 데스크톱 서비스**합니다.
2. **배포 개요**를 선택 **태스크**를 선택한 후 **배포 속성 편집**합니다.
3. 선택 **RD 라이선싱**를 선택한 다음 배포에 대 한 적절 한 라이선스 모드 (**장치별** 또는 **사용자별**).
4. RD 라이선스 서버의 정규화 된 도메인 이름 (FQDN)을 입력 하 고 선택한 **추가**합니다.
5. RD 라이선스 서버가 둘 이상인 경우 각 서버에 대해 4 단계를 반복 합니다. 
    ![RD 라이선스 서버 구성 옵션의 서버 관리자입니다.](..\media\troubleshoot-remote-desktop-connections\RDLicensing_Configure.png)

### <a name="refresh-the-x509-certificate-registry-keys"></a>새로 고침 X509 인증서 레지스트리 키

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정 하기 전에 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 문제가 발생할 경우.

이 문제를 해결 하려면 백업 및 다음 제거 X509 인증서 레지스트리 키를 그 다음으로 컴퓨터를 다시 활성화 RD 라이선스 서버 다시 시작 합니다. 이를 위해 다음 단계를 수행합니다.

> [!NOTE]  
> 각 RDSH 서버에서 다음 절차를 수행 합니다.

1. 레지스트리 편집기를 열고 이동할 **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\컨트롤\\터미널 서버\\RCM**.
2. 레지스트리 메뉴에서 선택 **레지스트리 파일 내보내기**합니다.
3. 형식 **내보낸 인증서** 에 **파일 이름** 상자를 선택한 후 **저장**합니다.
4. 다음 값을 선택의 각를 마우스 오른쪽 단추로 클릭 **삭제할**를 선택한 후 **예** 삭제를 확인 하려면:  
      - **인증서**
      - **X509 인증서**
      - **X509 인증서 ID**
      - **X509 Certificate2**
5. 레지스트리 편집기를 종료 하 고 RDSH 서버 다시 시작 합니다.

## <a name="user-cannot-authenticate-or-must-authenticate-twice"></a>사용자를 인증할 수 없습니다 또는 두 번 인증 해야 합니다.

사용자 인증에 영향을 주는 문제가 발생할 수 있는 몇 가지 문제가 있습니다. 이 섹션에서는 다음과 같은 경우:

  - [사용자는 "로그온 유형 제한" 메시지를 사용 하 여 액세스를 거부](#access-denied-restricted-type-of-logon)
  - [사용자 또는 응용 프로그램을 16965 이벤트를 사용 하 여 액세스 거부 "SAM 데이터베이스에 원격 호출을 거부 되었습니다"](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [사용자가 스마트 카드를 사용 하 여 로그인 할 수 없습니다.](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [원격 PC에서 차단 된 경우 사용자가 암호를 두 번 입력 해야](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [사용자는 로그인 할 수 없습니다 하 고 "인증 오류" 및 "CredSSP 암호화 oracle 수정" 메시지를 수신 합니다.](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [일부 사용자를 두 번 로그인 해야 클라이언트 컴퓨터를 업데이트 한 후](#after-you-update-client-computers-some-users-need-to-sign-in-twice)합니다.
  - [사용자가 여러 RD 연결 브로커를 사용 하 여 RemoteGuard를 사용 하는 배포에 대 한 액세스를 거부 됩니다.](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### <a name="access-denied-restricted-type-of-logon"></a>액세스가 거부 되어 로그온의 제한 된 형식

이 경우 Windows 10 또는 Windows Server 2016 컴퓨터에 연결 하려고 하는 Windows 10 사용자 다음 메시지를 사용 하 여 액세스를 거부 됩니다.

> 원격 데스크톱 연결:  
> 시스템 관리자가 로그온 유형의 제한 (네트워크 또는 대화형)는 사용할 수 있습니다. 지원이 필요한 경우 시스템 관리자나 기술 지원에 문의 합니다.

네트워크 수준 인증 NLA () RDP 연결에 대 한 필수 항목이 며 사용자가 멤버인 되지 경우이 문제가 발생 합니다 **Remote Desktop Users** 그룹입니다. 경우 발생할 수 있습니다 합니다 **Remote Desktop Users** 그룹에 할당 되지 않았습니다 합니다 **네트워크에서이 컴퓨터 액세스** 사용자 권한.

이 문제를 해결 하려면 다음이 단계 중 하나를 수행 합니다.

  - [사용자의 그룹 구성원 또는 사용자 권한 할당 수정](#modify-the-users-group-membership-or-user-rights-assignment)합니다.
  - NLA (권장 하지 않음)를 해제 합니다.
  - Windows 10 이외의 다른 원격 데스크톱 클라이언트를 사용 합니다. 예를 들어, Windows 7 클라이언트에는이 문제가 없습니다.

#### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>사용자의 그룹 구성원 또는 사용자 권한 할당 수정

가장 간단한이 문제를 해결 하려면이 사용자를 추가 하는 것이 문제를 단일 사용자에 영향을 주는 경우 합니다 **Remote Desktop Users** 그룹입니다.

사용자가 이미이 그룹의 구성원 (또는 여러 그룹 멤버에 동일한 문제가 있는 경우), 원격 컴퓨터의 Windows 10 또는 Windows Server 2016 사용자 권한 구성을 확인 합니다.

1. 그룹 정책 개체 편집기 (GPE)를 열고 원격 컴퓨터의 로컬 정책에 연결 합니다.
2. 이동할 **컴퓨터 구성\\Windows 설정\\보안 설정을\\로컬 정책\\사용자 권한 할당**를 마우스 오른쪽 단추로 클릭 **이 액세스 네트워크에서 컴퓨터**를 선택한 후 **속성**합니다.
3. 사용자 및 그룹 목록을 확인 하세요 **Remote Desktop Users** (또는 부모 그룹).
4. 목록에 포함 되어 있지 않으면 **Remote Desktop Users** (또는 부모와 같은 그룹 **Everyone**) 목록에 추가 해야 (개 또는 두 컴퓨터 배포에 있는 경우 그룹 정책 개체를 사용 함) .  
    예를 들어의 기본 멤버 자격 **네트워크에서이 컴퓨터 액세스** 포함 **Everyone**합니다. 배포에서 제거 하려면 그룹 정책 개체를 사용 하는 경우 **Everyone**를 추가 하려면 그룹 정책 개체를 업데이트 하 여 액세스를 복원 해야 할 수 있습니다 **Remote Desktop Users**합니다.

### <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>액세스 거부, SAM 데이터베이스에 원격 호출을 거부 되었습니다.

이 동작은 도메인 컨트롤러가 Windows Server 2016 이상을 실행 하 고 사용자가 사용자 지정된 연결 앱을 사용 하 여 연결 하려고 하는 경우 발생할 가능성이 가장 높습니다. 특히, Active Directory에서 사용자의 프로필 정보에 액세스 하는 응용 프로그램 액세스가 거부 됩니다.

이 동작은 Windows 변경의 결과입니다. Windows Server 2012 R2 및 이전 버전의 경우 사용자 로그온 원격 데스크톱, 원격 연결 관리자 (RCM) 연락처에 도메인 컨트롤러 (DC) Active Directory 도메인의 사용자 개체에 특정 한 원격 데스크톱 구성을 쿼리할 수 서비스 (AD DS)입니다. 이 정보는 Active Directory 사용자 및 컴퓨터 MMC 스냅인에서 사용자의 개체 속성의 원격 데스크톱 서비스 프로필 탭에 표시 됩니다.

RCM은 Windows Server 2016부터, AD DS에 사용자 개체를 쿼리하여 더 이상. 원격 데스크톱 서비스 특성을 사용 하 고 있으므로 AD DS를 쿼리 하는 RCM에 필요한 경우 이전 RCM 동작을 수동으로 설정 해야 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정 하기 전에 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 문제가 발생할 경우.

RD 세션 호스트 서버에서 레거시 RCM 동작을 사용 하려면 다음 레지스트리 항목을 구성 하 고 다시 시작 합니다 **원격 데스크톱 서비스** 서비스:  
  - **HKEY\_로컬\_MACHINE\\소프트웨어\\정책\\Microsoft\\Windows NT\\터미널 서비스**
  - **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\제어\\터미널 서버\\WinStations\\\<Winstation 이름\>\\**  
      - Name: **fQueryUserConfigFromDC**
      - 형식: **Reg\_DWORD**
      - 값: **1** (10 진수)

RD 세션 호스트 서버 이외의 서버에서 레거시 RCM 동작을 사용 하려면 이러한 레지스트리 항목 및 다음 추가 레지스트리 항목 구성 (및 서비스를 다시 시작 후):
  - **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\컨트롤\\터미널 서버**

이 동작에 대 한 자세한 내용은 참조 KB 3200967 [Windows Server의 원격 연결 관리자를 변경](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server)합니다.

### <a name="a-user-cannot-sign-in-by-using-a-smart-card"></a>사용자가 스마트 카드를 사용 하 여 로그인 할 수 없습니다.

이 문서는 사용자 로그인 원격 데스크톱 스마트 카드를 사용 하 여 세 가지 일반적인 상황을 해결 합니다.  
  - [사용자가 읽기 전용 도메인 컨트롤러 (RODC)를 사용 하는 지점에 로그인 할 수 없습니다.](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [사용자가 최근에 업데이트 된 Windows Server 2008 SP2 컴퓨터에 로그인 할 수 없습니다.](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [사용자 수 없습니다. 최근에 업데이트 된 Windows 컴퓨터에 로그인 상태 유지 되며 원격 데스크톱 서비스 응답 (일시 중단)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### <a name="cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc"></a>RODC는 지사에서 스마트 카드 로그인 할 수 없습니다.

RODC를 사용 하는 분기 사이트에 RDSH 서버를 포함 하는 배포에서이 문제가 발생 합니다. RDSH 서버 루트 도메인에서 호스트 됩니다. 분기 사이트에서 사용자가 자식 도메인에 속하며 인증에 대 한 스마트 카드를 사용 합니다. RODC는 사용자 암호를 캐시 하도록 구성 된 (RODC가 속한 합니다 **허용 된 RODC Password Replication Group**). "시도한 로그온 올바르지 않습니다 같은 메시지를 받은 사용자를 RDSH 서버에서 세션에 로그인 하려고 하는 경우. 이 값은 잘못 된 사용자 이름 또는 인증 정보로 인해. "

이것은 방식으로 알려진된 문제는 루트 DC와 RODC 관리 사용자 자격 증명을 암호화 합니다. 자격 증명을 암호화 하려면 암호화 키를 사용 하는 루트 DC 및 RODC 클라이언트에 대 한 암호 해독 키를 제공 합니다. 그러나 두 키 일치 하지 않습니다.

이 문제를 해결 하려면 DC 또는 RODC에서 암호 캐싱이 해제 하 여 분기 사이트에 쓰기 가능한 DC를 배포 하 여 토폴로지를 변경 하는 것이 좋습니다. 대체 방법 RDSH 서버는 사용자와 같은 하위 도메인으로 옮기는 것입니다. 다른 방법은 사용자가 스마트 카드 없이 로그인 할 수 있도록 하는 것입니다. 이러한 솔루션 중 원하는 성능 또는 보안 수준을 절충 해야 합니다.

#### <a name="cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer"></a>Windows Server 2008 SP2 컴퓨터에 스마트 카드 로그인 할 수 없습니다.

사용자가 KB4093227를 사용 하 여 업데이트 된 Windows Server 2008 SP2 컴퓨터에 로그인 하는 경우이 문제가 발생 (2018.4B). 사용자가 스마트 카드를 사용 하 여 로그인 할 때 "올바른 인증서가 없습니다 같은 메시지를 사용 하 여 액세스를 거부 됩니다. 카드 올바르게 삽입와 긴밀 하 게 적합 한 있는지 확인 합니다. " 동시에, Windows Server 컴퓨터는 응용 프로그램 이벤트 기록 "삽입된 된 스마트 카드에서 디지털 인증서를 검색 하는 동안 오류가 발생 했습니다. 시그니처가 잘못 되었습니다. "

이 문제를 해결 하려면 Windows Server 컴퓨터를 업데이트 합니다 2018.06 B의 재릴리스에 KB 4093227 [설명은 Windows Server 2008 서비스 취약점으로 인 한 Windows 원격 데스크톱 프로토콜 (RDP) 거부 용 보안 업데이트: 2018 년 4 월 10 일](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)합니다.

#### <a name="cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>스마트 카드 및 원격 데스크톱 서비스 서비스 중지를 사용 하 여 서명 된 상태로 유지할 수 없습니다.

사용자가 KB 4056446를 사용 하 여 업데이트 된 Windows 또는 Windows Server 컴퓨터에 로그인 하는 경우이 문제가 발생 합니다. 처음에 사용자 스마트 카드를 사용 하 여 시스템에 로그인 할 수 있지만 다음 수신를 "SCARD\_E\_NO\_서비스" 오류 메시지입니다. 원격 컴퓨터가 응답 하지 않을 수 있습니다.

이 문제를 해결 하려면 원격 컴퓨터를 다시 시작 합니다.

이 문제를 해결 하려면 적절 한 해결을 사용 하 여 원격 컴퓨터를 업데이트 합니다.

  - Windows Server 2008 SP2: KB, 4090928 [Windows lsm.exe 프로세스 핸들 누수 및 스마트 카드 응용 프로그램 표시 될 수 있습니다 "SCARD\_E\_NO\_서비스" 오류](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2: KB 4103724, [2018 년 5 월 17 일-KB4103724 (월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 및 Windows 10 버전 1607: KB 4103720, [2018 년 5 월 17 일-KB4103720 (OS 빌드 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### <a name="if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice"></a>원격 PC에서 차단 된 경우 사용자가 암호를 두 번 입력 해야

이 문제는 사용자는 RDP 연결 하지 않아도 NLA 배포에서 Windows 10 버전 1709 실행 하는 원격 데스크톱에 연결 하려고 할 때 발생할 수 있습니다. 이러한 상황에서 원격 데스크톱에서 차단 된 경우 사용자를 연결 하는 경우에 두 번 자신의 자격 증명을 입력 해야 합니다.

이 문제를 해결 하려면 Windows 10 버전 1709 컴퓨터를 업데이트 합니다 (kb) 4343893 [2018 년 8 월 30 일-KB4343893 (OS 빌드 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893)합니다.

### <a name="user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>사용자 로그인 할 수 없습니다 하 고 "인증 오류" 및 "CredSSP 암호화 oracle 수정" 메시지를 수신 합니다.

사용자가 Windows Vista SP2 및 이후 버전 또는 Windows Server 2008 SP2에서 Windows의 모든 버전 및 이후 버전을 사용 하 여 로그인을 시도 하는 경우 액세스가 거부 됩니다 하며 다음과 같은 메시지를 수신 합니다.

  - 인증 오류가 발생 했습니다. 요청한 함수가 지원 되지 않습니다.
  - CredSSP 암호화 oracle 재구성 때문일 수 있습니다.

"CredSSP 암호화 oracle 수정"은 2018 년 5 월 3 월, 4 월에 출시 된 보안 업데이트의 집합을 가리킵니다. CredSSP는 다른 응용 프로그램에 대 한 인증 요청을 처리 하는 인증 공급자입니다. 13 2018 년 3 월 "3B" 및 후속 업데이트 공격자 코드를 실행할 대상 시스템에 사용자 자격 증명을 릴레이는 악용을 해결 합니다.

초기 업데이트에는 새 그룹 정책 개체에 대 한 지원이 추가 되었습니다 **암호화 Oracle 재구성**, 다음 가능한 설정이 포함 된:

  - **취약 한**합니다. CredSSP를 사용 하는 클라이언트 응용 프로그램 안전 하지 않은 버전으로 대체할 수 있습니다 하지만이 동작은 공격 하는 원격 데스크톱을 표시 합니다. CredSSP를 사용 하는 서비스는 업데이트 되지 않은 클라이언트를 수락 합니다.
  - **완화**합니다. CredSSP를 사용 하는 클라이언트 응용 프로그램은 안전 하지 않은 버전으로 다시 이동할 수 없습니다. 하지만 CredSSP를 사용 하는 서비스는 업데이트 되지 않은 클라이언트를 허용 합니다.
  - **강제 클라이언트 업데이트**합니다. 안전 하지 않은 버전으로 다시 이동할 수 없습니다. CredSSP를 사용 하는 클라이언트 응용 프로그램 및 CredSSP를 사용 하는 서비스 패치가 적용 되지 않은 클라이언트를 허용 하지 않습니다. 
    참고: 최신 버전을 지원 하는 모든 원격 호스트 될 때까지이 설정은 배포 되어야 합니다.

2018 년 5 월 8 일 업데이트 기본값을 변경 **암호화 Oracle 재구성** 에서 설정 **Vulnerable** 하 **완화 됨**합니다. 진행에서이 변경으로 원격 데스크톱 클라이언트 업데이트를 설치 하는 서버 없는 (또는 서버를 다시 시작 하지 않은 업데이트)에 연결할 수 없습니다. 업데이트 및 차단 하는 통신 유형에 미치는 영향에 대 한 자세한 내용은 참조 KB 4093492 [CredSSP CVE-2018-0886 업데이트](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)합니다.

이 문제를 해결 하려면 모든 시스템 완벽 하 게 업데이트를 다시 시작을 확인 합니다. 업데이트 및 취약성에 대 한 자세한 내용은의 전체 목록을 참조 하세요. [CVE-2018-0886 | CredSSP 원격 코드 실행 취약점으로 인 한](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886)합니다.

업데이트가 완료 될 때까지이 문제를 해결 하려면 연결의 허용 되는 형식에 대 한 KB 4093492를 확인 합니다. 가능한 대안이 없습니다 경우에 다음 방법 중 하나를 고려해볼 수 있습니다.

  - 영향을 받는 클라이언트 컴퓨터에 대 한 설정 합니다 **암호화 Oracle 재구성** 정책을 다시 **Vulnerable**합니다.
  - 다음 정책을 수정 합니다 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\Remote Desktop Services\\원격 데스크톱 세션 호스트\\ 보안** 그룹 정책 폴더:  
      - **원격 (RDP) 연결에 대 한 특정 보안 계층의 사용을 필요로**:로 **Enabled** 선택한 **RDP**합니다.
      - **네트워크 수준 인증을 사용 하 여 원격 연결에 대 한 사용자 인증을 요구**:로 **비활성**합니다.
      > [!IMPORTANT]  
      > 배포의 보안이 약화 하는 이러한 수정 합니다. 만 전혀 사용 하는 경우에 임시 여야 합니다.

그룹 정책 사용 하 여 작업에 대 한 자세한 내용은 참조 하세요. [차단 GPO 수정](#modifying-a-blocking-gpo)합니다.

### <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>일부 사용자를 두 번 로그인 해야 클라이언트 컴퓨터를 업데이트 한 후

일부 Windows 7 또는 Windows 10 버전 1709에서 사용자 원격 데스크톱 세션에 로그인 하 고 즉시 두 번째 로그인 화면을 참조 하세요. 이 문제는 클라이언트 컴퓨터에서 다음 업데이트를 수신 하는 경우 발생 합니다.

  - Windows 7: KB 4103718, [2018 년 5 월 8 일-KB4103718 (월별 롤업)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [2018 년 5 월 8 일-KB4103727 (OS 빌드 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

이 문제를 해결 하려면 사용자가 (뿐만 아니라 RDSH 또는 RDVI 서버)에 연결 하려면 컴퓨터를 2018 년 6 월을 통해 완전히 업데이트를 확인 합니다. 다음과 같은 업데이트가 포함 됩니다.

  - Windows Server 2016: KB 4284880, [2018 년 6 월 12 일-KB4284880 (OS 빌드 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [2018 년 6 월 12 일-KB4284815 (월별 롤업)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855, [2018 년 6 월 12 일-KB4284855 (월별 롤업)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [2018 년 6 월 12 일-KB4284826 (월별 롤업)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [설명은 Windows Server 2008, Windows Embedded POSReady 2009, Windows Embedded Standard 2009에 CredSSP 원격 코드 실행 취약점에 대 한 보안 업데이트: 2018 년 3 월 13 일](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>사용자가 여러 RD 연결 브로커를 사용 하 여 원격 Credential Guard 사용 하는 배포에 대 한 액세스를 거부 됩니다.

Windows Defender 원격 Credential Guard 사용 하는 경우 두 개 이상의 원격 데스크톱 연결 브로커를 사용 하는 고가용성 배포에 이러한 문제가 발생 합니다. 사용자는 원격 데스크톱 로그인 수 없습니다.

이 문제는 원격 Credential Guard 인증에 Kerberos를 사용 하 고 NTLM을 제한 하기 때문에 발생 합니다. 그러나 부하 분산 된 고가용성 구성에서 RD 연결 브로커 Kerberos 작업을 지원할 수 없습니다.

부하 분산 된 RD 연결 브로커 고가용성 구성을 사용 해야 할 경우 원격 Credential Guard 사용 하지 않도록 설정 하 여이 문제를 해결할 수 있습니다. Windows Defender 원격 Credential Guard 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows Defender 원격 Credential Guard 사용 하 여 보호 하는 원격 데스크톱 자격 증명](https://docs.microsoft.com/en-us/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)합니다.

## <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>연결에서 사용자에 게 "원격 데스크톱 서비스는 현재 사용 중" 메시지가

이 문제에 대 한 적절 한 응답을 확인 하려면 다음 단계를 사용 합니다.

1. 원격 데스크톱 서비스가 응답 하지 않습니다 (예: 원격 데스크톱 클라이언트 시작 화면에서 "중단" 표시 됩니다).  
      - 서비스 응답 하지 않는 경우, 참조 [RDSH 서버 메모리 문제](#rdsh-server-memory-issue)합니다.
      - 클라이언트에 일반적으로 서비스와 상호 작용할 수 있으면 다음 단계로 이동 합니다.
2. 하나 이상의 사용자가 원격 데스크톱 세션 연결을 해제 하는 경우 사용자가 연결할 수 다시?  
   - 사용자 수에 관계 없이 연결을 거부 하는 서비스가 계속 되 면 해당 세션 연결 끊기, 참조 [RD 수신기 문제](#rd-listener-issue)합니다.
   - 서비스를 수락 하는 경우 사용자 수가 후에 다시 연결의 세션 연결이 끊어질 [연결 제한 정책을 확인](#check-the-connection-limit-policy)합니다.

### <a name="rdsh-server-memory-issue"></a>RDSH 서버 메모리 문제

일부 Windows Server 2012 R2 RDSH 서버에서 메모리 누수가 발견 되었습니다. 시간이 지남에 따라 이러한 서버는 다음과 같은 메시지를 사용 하 여 로컬 콘솔 로그인 및 원격 데스크톱 연결을 거부 하려면:

> 원격 데스크톱 서비스를 현재 사용 중 이므로 수행 하려는 작업을 완료할 수 없습니다. 몇 분 후에 다시 시도 하세요. 다른 사용자가 로그인 할 수 해야 합니다.

또한 연결을 시도 하는 원격 데스크톱 클라이언트 응답 하지 않게 합니다.

이 문제를 해결 하기 위해 RDSH 서버 다시 시작 합니다.

이 문제를 해결 하려면 KB 4093114 적용 [2018 년 4 월 10 일-KB4093114 (월별 롤업)] (file:// /c\\사용자\\v jesits\\AppData\\현지\\Microsoft\\Windows\\INetCache\\Content.Outlook\\FUB8OO45\\%202018 2010 년 4 월 %-KB4093114 %20\(월간 %20Rollup\)), RDSH 서버.

### <a name="rd-listener-issue"></a>RD 수신기 문제

Windows Server 2012 R2로 Windows Server 2008 R2에서 직접 업그레이드 된 일부 RDSH 서버 또는 Windows Server 2016에서 설명한 문제. 원격 데스크톱 클라이언트 RDSH 서버에 연결할 때 RDSH 서버 사용자 세션에 대 한 RD 수신기를 만듭니다. 영향을 받는 서버는 사용자 연결을 증가 하는 RD 수신기 하지만 감소 되지 개수를 유지 합니다.

이 문제를 해결 하려면 다음 메서드를 사용할 수 있습니다.

  - RD 수신기 수가 다시 설정 하려면 RDSH 서버를 다시 시작
  - 매우 큰 값으로 설정 하는 연결 제한 정책을 수정 합니다. 연결 제한 정책 관리에 대 한 자세한 내용은 참조 하세요. [연결 제한 정책을 확인](#check-the-connection-limit-policy)합니다.

이 문제를 해결 하려면 다음 업데이트가 RDSH 서버에 적용 됩니다.

  - Windows Server 2012 R2: KB 4343891, [2018 년 8 월 30 일-KB4343891 (월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884, [2018 년 8 월 30 일-KB4343884 (OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### <a name="check-the-connection-limit-policy"></a>연결 제한 정책 확인

개별 컴퓨터 수준에서 또는 그룹 정책 개체 (GPO)를 구성 하 여 동시 원격 데스크톱 연결 수가 한도 설정할 수 있습니다. 기본적으로 설정 되지 됩니다.

현재 설정을 확인 하 고 RDSH 서버에서 모든 기존 Gpo를 식별 하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력 합니다.
  
```
gpresult /H c:\gpresult.html
```
   
이 명령이 완료 되 면 열려 gpresult.html 후에 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\Remote Desktop Services\\원격 데스크톱 세션 호스트 \\연결**를 찾을 합니다 **연결 수 제한** 정책입니다.

  - 이 정책에 대 한 설정이 **사용 안 함**를 다음 그룹 정책 RDP 연결을 제한 하지 않습니다.
  - 이 정책에 대 한 설정이 **Enabled**를 확인 한 다음 **최우선 GPO**합니다. 제거 하거나 연결 제한을 변경 해야 할 경우이 GPO를 편집 합니다.

정책 변경 내용을 적용할 영향을 받는 컴퓨터에서 명령 프롬프트 창을 열고 다음 명령을 입력 합니다.
  
```
gpupdate /force
```
  
## <a name="rd-client-disconnects-and-cannot-reconnect-to-the-same-session"></a>RD 클라이언트 연결을 끊고 동일한 세션에 다시 연결할 수 없습니다.

원격 데스크톱 클라이언트와 원격 데스크톱 연결, 클라이언트 즉시 다시 연결할 수 없습니다. 사용자는 다음과 같은 오류 메시지를 받습니다.

  - 클라이언트 보안 오류로 인해 터미널 서버에 연결 하지 못했습니다. 네트워크에 로그온 되었는지, 후 서버에 다시 연결을 시도 합니다.
  - 원격 데스크톱 연결이 끊어졌습니다. 클라이언트 보안 오류로 인해 원격 컴퓨터에 연결 하지 못했습니다. 네트워크에 로그온 하 고 다시 연결을 확인 합니다.

나중에 원격 데스크톱 클라이언트는 원격 데스크톱에 다시 연결 합니다. 그러나 클라이언트가 원래 세션에 연결 하는 대신 RDSH 서버에 클라이언트를 연결 새 세션입니다. 연결이 끊어진된 상태를 입력 하지 않은 하지만 대신 활성 상태로 유지 되는 원래 세션 RDSH 서버를 확인 하는 중 알 수 있습니다.

설정할 수 있습니다.이 문제를 해결 하려면 합니다 **구성 연결 유지 연결 간격** 정책에는 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\ 원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\연결** 그룹 정책 폴더입니다. 이 정책을 사용 하는 경우 keep-alive 간격을 입력 해야 합니다. 연결 유지 간격 빈도, 세션 상태 확인 서버 (분)을 결정 합니다.

인증 및 구성 설정 잘못 구성 하 여이 문제를 발생할 수 있습니다. 서버 수준 또는 Gpo를 사용 하 여 이러한 설정을 구성할 수 있습니다. 그룹 정책 설정에서 사용할 수는 **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\Remote Desktop Services\\원격 데스크톱 세션 호스트\\ 보안** 그룹 정책 폴더입니다.

1. RD 세션 호스트 서버에서 권한이 상승된 명령 프롬프트 창을 엽니다.
2. 아래 **연결**연결의 이름을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다.
3. 에 **속성** 연결을 위한 대화 상자에는 **일반** 탭의 **보안** 계층, 보안 방법 선택 합니다.
4. **암호화 수준**, 원하는 수준을 클릭 합니다. 선택할 수 있습니다 **낮은**, **클라이언트 호환**합니다 **높은**, 또는 **FIPS 규격**합니다.

> [!NOTE]  
>  - 최고 수준의 암호화를 요구 하는 클라이언트와 RD 세션 호스트 서버 간의 통신 FIPS 규격 암호화를 사용 합니다.
>  - 그룹 정책에서 구성 하는 모든 암호화 수준의 설정을 원격 데스크톱 서비스 구성 도구를 사용 하 여 설정할 수 있는 구성을 재정의 합니다. 또한 사용 하는 경우는 [시스템 암호화: 암호화, 해시, 서명에 FIPS 호환 알고리즘 사용](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) 정책에이 설정을 재정의 합니다 **클라이언트 연결 암호화 수준 설정** 정책입니다. 시스템 암호화 정책에는 **컴퓨터 구성\\Windows 설정\\보안 설정을\\로컬 정책\\보안 옵션** 폴더입니다.
>  - 암호화 수준을 변경하면 새로운 암호화 수준이 사용자가 다음에 로그온할 때 적용됩니다. 여러 수준의 하나 이상의 서버에서 암호화를 필요로 하는 경우 여러 네트워크 어댑터를 설치 하 고 각 어댑터를 별도로 구성 합니다.
>  - 원격 데스크톱 서비스 구성에 해당 개인 키에 해당 인증서를 확인 하려면 인증서를 보려면 원하는 연결을 마우스 오른쪽 단추로 **일반적인**, 선택 **편집**를 선택 하 고 보려는 원하는 인증서를 선택 **인증서 보기**합니다. 맨 아래에 **일반** 탭, 문, "개인 키가이 인증서에 해당 하 는" 나타납니다. 또한 인증서 스냅인을 사용 하 여이 정보를 볼 수 있습니다.
>  - FIPS 규격 암호화 (의 **시스템 암호화: 암호화, 해시 및 서명에 사용 하 여 FIPS 호환 알고리즘** 정책 또는 **FIPS 규격** 원격 데스크톱 서버 구성에서 설정) 암호화 하 고 서버와 클라이언트에서 전송 된 데이터를 해독 합니다. 처리 표준 FIPS (Federal Information) 140-1 암호화 알고리즘을 사용 하 여 클라이언트에 서버는 Microsoft 암호화 모듈을 사용합니다. 자세한 내용은 [FIPS 140 유효성 검사](https://docs.microsoft.com/en-us/windows/security/threat-protection/fips-140-validation)합니다.
>  - 합니다 **높은** 설정 강력한 128 비트 암호화를 사용 하 여 서버에 클라이언트에서 서버를 클라이언트로 전송 된 데이터를 암호화 합니다.
>  - 합니다 **클라이언트 호환** 설정은 클라이언트에서 지원 되는 최대 키 강도로 서버와 클라이언트 간에 전송 된 데이터를 암호화 합니다.
>  - 합니다 **낮은** 56 비트 암호화를 사용 하 여 서버에 클라이언트에서 보낸 데이터를 암호화 하는 설정입니다.

## <a name="remote-laptop-disconnects-from-wireless-network"></a>원격 랩톱에서 무선 네트워크 연결을 끊습니다.

이 문제는 원격 데스크톱 클라이언트는 802.1x 무선 네트워크를 사용 하 여 랩톱 컴퓨터를 연결할 때 발생할 수 있습니다. 가끔씩 랩톱에서 무선 네트워크 연결을 끊습니다 및 자동으로 다시 연결 하지 않습니다.

이 무선 네트워크 연결에 대 한 네트워크 인증 설정 되 면 발생 하는 알려진된 문제 **사용자 인증**합니다.

이 문제를 해결 하려면로 네트워크 인증 설정 **사용자 또는 컴퓨터 인증** 하거나 **컴퓨터 인증**합니다.

 > [!NOTE]  
> 단일 컴퓨터에서 네트워크 인증 설정을 변경 하려면 새 설정을 사용 하 여 새 무선 연결을 만들려면 네트워크 및 공유 센터 제어판을 사용 해야 합니다.

Gpo를 사용 하 여 무선 네트워크 설정을 구성 하는 방법에 대 한 전체 설명과 대해서 [구성 무선 네트워크 (IEEE 802.11) 정책](https://docs.microsoft.com/en-us/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)합니다.

## <a name="user-experiences-poor-performance-or-application-problems"></a>사용자 환경을 성능이 저하 되거나 응용 프로그램 문제

이 섹션에서는 사용자가 원격 데스크톱 기능을 사용할 때 발생할 수 있는 몇 가지 일반적인 문제를 해결 합니다.

  - [문제가 일시적으로 새 가상 머신을 Microsoft Azure에 연결 하는 사용자](#intermittent-problems-with-new-microsoft-azure-virtual-machines)합니다.
  - [Windows 10 버전 1709에 대 한 원격 데스크톱에 연결 하는 사용자는 비디오를 재생 하는 문제가 있을 수 있습니다](#video-playback-issues-on-windows-10-version-1709)합니다.
  - [Windows 10 원격 데스크톱에 연결 하는 읽기 전용 사용자 프로필을 사용 하 여 사용자 데스크톱을 공유할 수 없습니다.](#desktop-sharing-issues-on-windows-10)
  - [이전 버전의 Windows 10에서 실행 되는 클라이언트를 사용 하 여 Windows 10 원격 데스크톱에 연결 된 사용자 NLA를 사용 하지 않도록 설정 하는 경우 성능 저하를 경험합니다](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [원격 데스크톱 세션에서 여러 응용 프로그램을 실행 하 고 분리 하 고 자주 다시 연결을 다시 연결할 때 검은 화면을 발생할 수 있습니다.](#black-screen-issue)

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>새 Microsoft Azure virtual machines를 사용 하 여 일시적인 문제

이 문제가 최근에 프로 비전 된 가상 머신입니다. 원격 데스크톱 세션을 사용자가 가상 컴퓨터에 연결 하면 모든 사용자 설정을 로드할 수 있습니다 정확 합니다.

이 문제를 해결 하려면 가상 컴퓨터에서 연결 끊기, 20 분 이상 기다린 후 다시 연결.

이 문제를 해결 하려면 다음 업데이트를 적절 하 게 가상 컴퓨터에 적용 됩니다.

  - Windows 10 및 Windows Server 2016의 경우: KB 4343884, [2018 년 8 월 30 일-KB4343884 (OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [2018 년 8 월 30 일-KB4343891 (월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Windows 10 버전 1709에서 비디오 재생 문제

사용자가 Windows 10 버전 1709 실행 하는 원격 컴퓨터에 연결 하는 경우이 문제가 발생 합니다. 이러한 사용자는 v m r 9를 사용 하 여 비디오 재생 하면 (비디오 혼합 렌더러 9) 코덱, 플레이어 black 창을 보여 줍니다.

Windows 10 버전 1709에서에서 알려진된 문제입니다. Windows 10 버전 1703에서에서 문제가 발생 하지 않습니다.

### <a name="desktop-sharing-issues-on-windows-10"></a>Windows 10에서 문제를 공유 하는 데스크톱

이 문제는 사용자에 게 읽기 전용 사용자 프로필 (및 관련된 레지스트리 hive)와 같은 키오스크 시나리오에서 발생 합니다. 이러한 사용자가 Windows 10, 버전 1803에서를 실행 하는 원격 컴퓨터에 연결할 때 데스크톱을 공유할 수 없습니다.

이 문제를 해결 하려면 4340917, Windows 10 업데이트를 적용 [2018 년 7 월 24 일-KB4340917 (OS 빌드 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917)합니다.

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>NLA를 사용 하지 않도록 설정 하는 경우 Windows 10의 버전을 혼합 하는 경우 성능 문제

NLA를 사용 하지 않도록 설정 하 고 Windows 10을 실행 하는 원격 데스크톱 클라이언트 컴퓨터는 서로 다른 버전의 Windows 10을 실행 하는 원격 데스크톱에 연결 하는 경우이 문제가 발생 합니다. Windows 10 버전 1709 또는 이전 버전을 실행 하는 컴퓨터에서 원격 데스크톱 클라이언트의 사용자가 Windows 10, 버전 1803 이상이 실행 되는 원격 데스크톱에 연결할 때 성능 저하를 경험 합니다.

NLA를 사용 하지 않도록 설정 하는 경우 이전 클라이언트 컴퓨터에서 Windows 10, 버전 1803 또는 이후 버전에 연결할 때 속도가 느린 프로토콜을 사용 하는이 발생 합니다.

이 문제를 해결 하려면 KB 4340917 적용 [2018 년 7 월 24 일-KB4340917 (OS 빌드 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917)합니다.

### <a name="black-screen-issue"></a>검은색 화면이 문제

Windows 8.0, Windows 8.1, Windows 10 RTM 및 Windows Server 2012 R2에서이 문제가 발생합니다. 사용자는 원격 데스크톱에서 여러 응용 프로그램을 시작 후 세션에서 연결을 끊습니다. 정기적으로 사용자가 원격 데스크톱 응용 프로그램 상호 작용 하 고 다시 연결을 끊습니다. 어느 시점에서 사용자 다시 연결 되 면 원격 데스크톱 세션을 방금 black 화면을 보여 줍니다. 사용자는 원격 컴퓨터의 콘솔 (또는 RDSH 서버 콘솔)에서 원격 데스크톱 세션을 종료 해야 합니다. 이 작업은 응용 프로그램을 중지합니다.

이 문제를 해결 하려면 적절 하 게 다음 업데이트를 적용 합니다.

  - Windows 8 and Windows Server 2012: KB4103719, [2018 년 5 월 17 일-KB4103719 (월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 및 Windows Server 2012 R2: KB4103724 [2018 년 5 월 17 일-KB4103724 (월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) 및 KB 4284863, [2018 년 6 월 21 일-KB4284863 (월별 롤업 미리 보기)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10: KB4284860, 고정 [2018 년 6 월 12 일-KB4284860 (OS 빌드 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)
