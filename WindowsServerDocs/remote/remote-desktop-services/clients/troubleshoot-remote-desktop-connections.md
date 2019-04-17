---
title: 원격 데스크톱 연결 문제 해결
description: 증상 별로 정렬 된 문제 해결 절차
ms.custom: na
ms.reviewer: rklemen;josh.bender
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: jobende
manager: ''
ms.author: v-tea;kaushika;rklemen;josh.bender
ms.date: 02/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8965df09fd57decf7f4a1b6b89861e5a67034a0a
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297402"
---
# 원격 데스크톱 연결 문제 해결
다양 한 원격 데스크톱 서비스 (RDS)는 가장 일반적인 문제에 간략하게 설명에 대 한 [질문과 대답 원격 데스크톱 클라이언트에 대 한](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq)참조 하세요. 이 문서에서는 연결 문제를 해결 하는 여러 가지 고급 방법을 설명 합니다. 이러한 절차의 여러 다른 물리적 컴퓨터 또는 더 복잡 한 구성에 연결 하는 하나의 물리적 컴퓨터와 같은 간단한 구성에서 문제를 해결 하려는 여부 적용 됩니다. 일부 절차는 더 복잡 한 다중 사용자 시나리오 에서만에서 발생 하는 문제를 해결 합니다. 원격 데스크톱 구성 요소와 함께 작동 방식에 대 한 자세한 내용은 [원격 데스크톱 서비스 아키텍처](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture)를 참조 하세요.

> [!NOTE]  
> 대부분의이 문서에서 설명 하는 절차에서는 여러 컴퓨터를 원격으로 액세스할 수 있을 수 있으며이 중 일부에 액세스 해야 합니다. 원격 관리 도구 및 구성 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구 (RSAT) Windows 운영 체제](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)를 참조 하세요.

다음 목록에서 사용자 (또는 사용자에 게)에서 발생 하는 증상 유형을 식별 합니다.

- [원격 데스크톱 클라이언트, 원격 데스크톱에 연결할 수 없는 하지만 특정 증상 나 메시지 (일반 문제 해결 단계)](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [원격 데스크톱 클라이언트, 원격 데스크톱에 연결할 수 없는 및 "클래스가 등록 되지 않았습니다." 메시지가](#client-cannot-connect-class-not-registered)
- [원격 데스크톱 클라이언트, 원격 데스크톱에 연결할 수 없는 및 수신는 "없이 사용할 수 있는 라이선스" 또는 "보안 오류" 메시지](#client-cannot-connect-no-licenses-available)
- [사용자가 "액세스 거부" 메시지가 수신 하거나 두 번 자격 증명을 제공 해야 합니다.](#user-cannot-authenticate-or-must-authenticate-twice)
- [연결에 "원격 데스크톱 서비스는 현재 작업 중" 메시지가](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [원격 데스크톱 클라이언트 연결을 끊고 동일한 세션에 다시 연결할 수 없습니다.](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [사용자 무선 네트워크를 통해 원격 랩톱에 연결 하 고 네트워크에서 노트북을 분리 하는 다음](#remote-laptop-disconnects-from-wireless-network)합니다.
- [원격 응용 프로그램 성능이 저하 되거나 사용자 경험](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> RDP 연결 끊기 코드 목록이 현재 [ExtendedDisconnectReasonCode 열거형](https://docs.microsoft.com/en-us/windows/desktop/TermServ/extendeddisconnectreasoncode)을 참조 하세요. 

## 특정 증상 없거나 메시지 (일반 문제 해결 단계)

다음이 단계를 사용 하 여 원격 데스크톱 클라이언트 원격 데스크톱에 연결할 수 없는 하지만 메시지 또는 데 도움을 주는 다른 증상 원인을 파악 하는 것을 제공 하지 않습니다. 이러한 종류의 문제의 가장 일반적인 이유 중 상당수를 해결 하려면 다음 메서드를 사용 합니다.

- [RDP 프로토콜의 상태를 확인](#check-the-status-of-the-rdp-protocol)
- [RDP 서비스의 상태를 확인](#check-the-status-of-the-rdp-services)
- [RDP 수신기가 작동 하는지 확인 합니다.](#check-that-the-rdp-listener-is-functioning)
- [RDP 수신기 포트를 확인 합니다.](#check-the-rdp-listener-port)

### RDP 프로토콜의 상태를 확인

#### 로컬 컴퓨터에 RDP 프로토콜의 상태를 확인

확인 하 고 로컬 컴퓨터에 RDP 프로토콜의 상태를 변경 하려면 [원격 데스크톱을 사용 하는 방법을](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)참조 하세요.

> [!NOTE]  
> 원격 데스크톱 옵션을 사용할 수 없는 경우에 [그룹 정책 개체를 RDP를 차단 하 고 있는지 여부를 확인](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)참조 하세요.

#### 원격 컴퓨터에 RDP 프로토콜의 상태를 확인

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 수행 합니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 하기 전에 수정 [복원에 대 한 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 하 고 문제가 발생 하는 경우.

확인 하 고 원격 컴퓨터에 RDP 프로토콜의 상태를 변경 하려면 네트워크 레지스트리 연결을 사용 합니다.

1. **시작**, **실행**을 선택한 다음 **regedt32**를 입력 합니다.
2. 레지스트리 편집기에서 **파일**을 선택 하 고 **네트워크 레지스트리 연결**을 선택 합니다.
3. **컴퓨터 선택** 대화 상자에서 원격 컴퓨터의 이름을 입력 **이름 확인**을 선택한 다음 **확인**을 선택 합니다.
4. **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal 서버**로 이동 합니다.  
   ![레지스트리 편집기를 fDenyTSConnections 항목 표시](..\media\troubleshoot-remote-desktop-connections\RegEntry_fDenyTSConnections.png)
   - **FDenyTSConnections** 키 값이 **0**인 경우 RDP 사용은
   - **FDenyTSConnections** 키 값이 **1**이면 다음 RDP은 사용할 수 없습니다.
5. RDP를 사용 하려면 **1** 에서 **fDenyTSConnections** 의 값을 **0**으로 변경 합니다.

#### 로컬 컴퓨터에서 그룹 정책 개체 (GPO)는 RDP를 차단 여부 확인

사용자 인터페이스에서 RDP 설정할 수 없으며, 변경한 후 **fDenyTSConnections** 의 값을 **1** 로 되돌아갑니다 컴퓨터 수준 설정을 GPO 재정의 될 수 있습니다.

로컬 컴퓨터에서 그룹 정책 구성을 확인 하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력 합니다.
```
gpresult /H c:\gpresult.html
```
이 명령은 완료 되 면 gpresult.html를 엽니다. **컴퓨터 구성 요소 \ \ Components\\Remote 데스크톱 Services\\Remote 데스크톱 세션 Host\\Connections** **사용자가 원격 데스크톱 서비스를 사용 하 여 원격으로 연결 하도록 허용** 정책을 찾습니다.

- 이 정책에 대 한 설정으로 **** 인 경우 그룹 정책은 RDP 연결을 차단 하지 않습니다.
- 이 정책 설정을 **사용 하지 않는**경우, **영업 GPO**를 확인 합니다. 이것은 RDP 연결을 차단 하는 GPO 합니다.
![gpresult.html 예제 세그먼트는 도메인 수준 GPO * * 블록 RDP * *는 RDP를 비활성화 합니다.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_GP.png)
   
  ![예제 세그먼트는는 gpresult.html * * 로컬 그룹 정책 * *는 RDP를 비활성화 합니다.](..\media\troubleshoot-remote-desktop-connections\GPResult_RDSH_Connections_LGP.png)

#### GPO는 원격 컴퓨터에 RDP 차단 여부 확인

원격 컴퓨터에서 그룹 정책 구성을 확인 하려면 명령은 로컬 컴퓨터와 거의 동일 합니다.
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
이 명령을 생성 하는 파일 (**gpresult-\<computer name\>.html**)는 로컬 컴퓨터 버전 (**gpresult.html**)에서 동일한 정보 형식을 사용 합니다.

#### 차단 GPO 수정

그룹 정책 개체 편집기 (GPE) 및 그룹 정책 관리 콘솔 (GPM)에서 이러한 설정을 수정할 수 있습니다. 그룹 정책을 사용 하는 방법에 대 한 자세한 내용은 [고급 그룹 정책 관리](https://docs.microsoft.com/en-us/microsoft-desktop-optimization-pack/agpm/)를 참조 하세요.

차단 정책을 수정 하려면 다음 방법 중 하나를 사용 합니다.

- GPE에서 (예: 로컬 또는 도메인), 적절 한 수준의 GPO에 액세스 하 고 **컴퓨터 구성 요소 \ \ Components\\Remote 데스크톱 Services\\Remote 데스크톱 세션 Host\\Connections**로 이동\\허용** 사용자가 원격 데스크톱 서비스를 사용 하 여 원격으로 연결할**합니다.  
   1. **사용** 또는 **구성 되지 않은**정책을 설정 합니다.
   2. 영향을 받는 컴퓨터에서 관리자 권한으로 명령 프롬프트 창을 열고 **gpupdate /force** 명령을 실행 합니다.
- GPM, 차단 정책이 영향을 받는 컴퓨터에 적용 되는 OU로 이동 하 고 OU에서 정책을 삭제 합니다.

### RDP 서비스의 상태를 확인

(클라이언트) 로컬 컴퓨터와 원격 (대상) 컴퓨터에서 다음과 같은 서비스를 실행 해야 합니다.

- 원격 데스크톱 서비스 (: term Service)
- 원격 데스크톱 서비스 사용자 모드 포트 리디렉터 (UmRdpService)

로컬 또는 원격으로 서비스를 관리 서비스 MMC 스냅인을 사용할 수 있습니다. 로컬 또는 원격으로 PowerShell를 사용할 수도 있습니다 (원격 컴퓨터는 수락 하도록 구성 원격 PowerShell 명령).

![서비스 MMC 스냅인에서 원격 데스크톱 서비스를 지원 합니다. 기본 서비스 설정을 수정 하지 마십시오.](..\media\troubleshoot-remote-desktop-connections\RDSServiceStatus.png)

두 컴퓨터 모두에서 하나 또는 둘 다 서비스를 실행 하 고 있지 하기 시작 합니다.

> [!NOTE]  
> 원격 데스크톱 서비스를 시작 하면 **예** 를 클릭 자동으로 원격 데스크톱 서비스 사용자 모드 포트 리디렉터 서비스를 다시 시작 합니다.

### RDP 수신기가 작동 하는지 확인 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 수행 합니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 하기 전에 수정 [복원에 대 한 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 하 고 문제가 발생 하는 경우.

#### RDP 수신기의 상태를 확인

이 절차에 대 한 관리자 권한이 있는 PowerShell 인스턴스를 사용 합니다. 로컬 컴퓨터에 대 한 관리자 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 그러나이 절차는 로컬 및 원격으로 둘 다 동일한 명령이 작동 하기 때문에 PowerShell을 사용 합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결할 **Enter-pssession-ComputerName \<computer name\>** 를 입력 합니다.
2. **Qwinsta**를 입력 합니다. 
    ![Qwinsta 명령 컴퓨터의 포트에서 수신 대기 하는 프로세스를 나열 합니다.](..\media\troubleshoot-remote-desktop-connections\WPS_qwinsta.png)
3. 목록에 있는 경우 **수신 대기**상태로 **rdp tcp** , RDP 수신기 작동 합니다. [RDP 수신기 포트 확인](#check-the-rdp-listener-port)로 이동 합니다. 그렇지 않으면 4 단계에서 계속 합니다.
4. 작업 중인 컴퓨터에서 RDP 수신기 구성을 내보냅니다.
    1. 영향을 받는 컴퓨터에 동일한 운영 체제 버전에는 컴퓨터에 로그인 하 고 해당 컴퓨터의 레지스트리 (예를 들어 사용 하 여 액세스할 레지스트리 편집기).
    2. 다음 레지스트리 항목으로 이동 합니다.  
        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP Tcp**
    3. 항목을.reg 파일을 내보냅니다. 예를 들어, 레지스트리 편집기에서 항목을 마우스 오른쪽 단추로 클릭 **내보내기**고 내보낸된 설정에 대 한 파일 이름을 입력 합니다.
    4. 영향을 받는 컴퓨터를 내보낸된.reg 파일을 복사 합니다.
5. RDP 수신기 구성, 영향을 받는 컴퓨터에 대 한 관리자 권한이 있는 PowerShell 창을 열고 (또는 PowerShell 창을 열고 가져오고 영향을 받는 컴퓨터에 원격으로 연결).
   1. 기존 레지스트리 항목에 백업 하려면 다음 명령을 입력 합니다.  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 기존 레지스트리 항목을 제거 하려면 다음 명령을 입력 합니다.  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 새 레지스트리 항목을 가져오고 다음 서비스를 다시 시작을 하려면 다음 명령을 입력 합니다.  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      여기서 \<filename\> 내보낸된.reg 파일의 이름입니다.
6. 원격 데스크톱 연결을 다시 시도 하 여 구성을 테스트 합니다. 여전히 연결할 수 없는 경우 영향을 받는 컴퓨터를 다시 시작 합니다.
7. 여전히 연결할 [RDP 자체 서명 된 인증서의 상태를 확인할](#check-the-status-of-the-rdp-self-signed-certificate)수 없습니다.

#### RDP 자체 서명 된 인증서의 상태를 확인

1. 여전히 연결할 수 없는 경우 인증서 MMC 스냅인을 엽니다. **컴퓨터 계정**, 관리 하는 인증서 저장소를 선택 하 라는 메시지가 표시 되 고 영향을 받는 컴퓨터를 선택 합니다.
2. **원격 데스크톱**에서 **인증서** 폴더에서 RDP 자체 서명 된 인증서를 삭제 합니다. 
    ![인증서 MMC 스냅인에서 원격 데스크톱 인증서입니다.](..\media\troubleshoot-remote-desktop-connections\MMCCert_Delete.png)
3. 영향을 받는 컴퓨터에서 원격 데스크톱 서비스 서비스를 다시 시작 합니다.
4. 인증서 스냅인 새로 고칩니다.
5. RDP 자체 서명 된 인증서를 다시 작성 되어 있지 않으면 [MachineKeys 폴더의 사용 권한을 확인](#check-the-permissions-of-the-machinekeys-folder)합니다.

#### MachineKeys 폴더의 사용 권한을 확인합니다

1. 영향을 받는 컴퓨터에서 탐색기를 열고 **C:\\ProgramData\\Microsoft\\Crypto\\RSA\\**이동 합니다.
2. **MachineKeys**를 마우스 오른쪽 단추로 클릭, **속성**, **보안**을 선택한 다음 **고급**을 선택 합니다.
3. 다음 사용 권한을 구성 되어 있는지 확인 합니다.
      - Builtin\\Administrators: 모든 권한
      - 모두: 읽기, 쓰기

### RDP 수신기 포트를 확인 합니다.

로컬 (클라이언트) 컴퓨터와 원격 (대상) 컴퓨터에서 RDP 수신기 포트 3389에서 수신 대기 해야 합니다. 다른 응용 프로그램이이 포트를 사용 해야 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 수행 합니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 하기 전에 수정 [복원에 대 한 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 하 고 문제가 발생 하는 경우.

을 선택 하거나 RDP 포트를 변경 하려면 레지스트리 편집기를 사용 합니다.

1. 시작, **실행**을 선택한 다음 **regedt32**를 입력 합니다.
      - 원격 컴퓨터에 연결 하 고 **파일**을 선택한 다음 **네트워크 레지스트리 연결**을 선택 합니다.
      - **컴퓨터 선택** 대화 상자에서 원격 컴퓨터의 이름을 입력 **이름 확인**을 선택한 다음 **확인**을 선택 합니다.
2. 레지스트리를 열고 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** 로 이동 합니다. 
    ![RDP 프로토콜에 대 한 향하는 하위 키입니다.](..\media\troubleshoot-remote-desktop-connections\RegEntry_PortNumber.png)
3. **향하** **는 3389**이외의 값이 있으면 **3389**으로 변경 합니다. 
   > [!IMPORTANT]  
    > 다른 포트를 사용 하 여 원격 데스크톱 서비스를 호스트할 수 있습니다. 하지만 이렇게 하지 않는 것이 좋습니다. 이러한 구성을 문제 해결이 문서의 범위를 벗어납니다.
4. 포트 번호를 변경한 후 원격 데스크톱 서비스를 다시 시작 합니다.

#### 다른 응용 프로그램에 동일한 포트를 사용 하려는 아닌지 확인 합니다.

이 절차에 대 한 관리자 권한이 있는 PowerShell 인스턴스를 사용 합니다. 로컬 컴퓨터에 대 한 관리자 권한이 있는 명령 프롬프트를 사용할 수도 있습니다. 하지만이 절차는 로컬 및 원격으로 동일한 명령이 작동 하기 때문에 PowerShell을 사용 합니다.

1. PowerShell 창을 엽니다. 원격 컴퓨터에 연결할 **Enter-pssession-ComputerName \<computer name\>** 를 입력 합니다.
2. 다음 명령을 입력합니다.  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Netstat 명령을 수신 하 게 서비스와 포트의 목록을 만듭니다.](..\media\troubleshoot-remote-desktop-connections\WPS_netstat.png)
1. **듣는 중**상태와 함께 TCP 포트 3389에 대 한 항목 (또는 할당 된 RDP 포트) 찾습니다. 
    > [!NOTE]  
   > 프로세스 또는 포트를 사용 하 여 서비스의 PID (프로세스 Id) PID 열 아래에 나타납니다.
1. 포트 3389 (또는 할당 된 RDP 포트) 응용 프로그램을 사용 하 여을 확인 하려면 다음 명령을 입력 합니다.  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Tasklist 명령 특정 프로세스의 세부 정보를 보고합니다.](..\media\troubleshoot-remote-desktop-connections\WPS_tasklist.png)
1. ( **Netstat** 출력)에서 포트와 연결 된 PID 번호에 대 한 항목을 찾습니다. 서비스 또는 해당 PID와 관련 된 프로세스를 오른쪽에 표시 됩니다.
1. 응용 프로그램이 나 서비스 원격 데스크톱 서비스 (TermServ.exe) 이외의 포트를 사용 하는 경우 다음 방법 중 하나를 사용 하 여 충돌을 해결할 수 있습니다.
      - 다른 응용 프로그램이 나 서비스 (권장) 다른 포트를 사용 하 여 구성 합니다.
      - 다른 응용 프로그램 또는 서비스를 제거 합니다.
      - 다른 포트를 사용 하 여 RDP를 구성 하 고 (권장 하지 않음) 원격 데스크톱 서비스 서비스를 다시 시작 합니다.

#### 방화벽 RDP 포트를 차단 하 고 있는지 여부 확인

**Psping** 도구를 사용 하 여 포트 3389를 사용 하 여 영향을 받는 컴퓨터를 연결할 수 있는지 여부를 테스트 합니다.

1. 영향을 받는 컴퓨터에서 다른 컴퓨터에서 **psping** 에서 다운로드 <https://live.sysinternals.com/psping.exe>.
2. 관리자 권한으로 명령 프롬프트 창을 열고, **psping**설치한 디렉터리로 이동한 후 다음 명령을 입력 합니다.  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. 다음과 같은 결과 위해 **psping** 명령의 출력을 확인 합니다.  
      - **연결을 \<computer IP\>**: 원격 컴퓨터에 연결할 수 있습니다.
      - **(0% 손실)**: 연결 하려는 모든 시도가 성공 합니다.
      - **원격 컴퓨터의 네트워크 연결을 거부**: 원격 컴퓨터에 연결할 수 없습니다.
      - **(100% 손실)**: 연결 하려는 모든 시도가 실패 합니다.
1. **Psping** 영향을 받는 컴퓨터에 연결 하는 기능을 테스트 하는 여러 컴퓨터에서 실행 합니다.
1. Note 영향을 받는 컴퓨터 다른 모든 컴퓨터, 다른 컴퓨터 또는 다른 하나의 컴퓨터에서 연결을 차단 여부.
1. 다음 단계를 권장 합니다.
      - 네트워크에 영향을 받는 컴퓨터에 RDP 트래픽을 허용 하는지 확인 하려면 네트워크 관리자에 게 참여 합니다.
      - 방화벽이 RDP 포트를 차단 하 고 있는지 여부를 결정 하는 원본 컴퓨터 (영향을 받는 컴퓨터에서 Windows 방화벽을 포함) 영향을 받는 컴퓨터 사이의 방화벽 구성을 조사 합니다.

## 클라이언트를 연결할 수 없는 "클래스가 등록 되지 않았습니다."

나중에 클라이언트는 연결할 수 없습니다 원격 데스크톱 세션 호스트 서버는 메시지를 보고 하는 동안 또는 Windows 10, 버전 1709 실행 하는 클라이언트를 사용 하 여 원격 컴퓨터에 연결 하려고 하면 포함 된 "등록된 되지 않았습니다 (0x80040154) 클래스" 오류 코드입니다.

이 문제는 연결을 시도 하는 사용자가 필수 사용자 프로필을 하는 경우 발생 합니다. 이 문제를 해결 하려면 설치 합니다 [2018 년 7 월 24 일-KB4338817 (OS 빌드 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10 업데이트 합니다.

## 클라이언트를 연결할 수 없는 라이선스를 사용할 수 없음

이 경우 RDSH 서버와 원격 데스크톱 라이선싱 서버를 포함 하는 배포에 적용 됩니다.

어떤 종류의 사용자에 게 표시 되는 동작을 식별 합니다.

- 세션 연결이 끊어졌습니다 라이선스 없음 사용할 수 있거나 없는 라이선스 서버를 사용할 수
- 보안 오류로 인해 액세스가 거부 됨

RD 세션 호스트 도메인 관리자로 로그인 하 고 RD 라이선스 진단 기를 엽니다. 다음과 같은 메시지를 찾습니다.

  - 유예 기간에 대 한 원격 데스크톱 세션 호스트 서버 만료 되 면 하지만 모든 라이선스 서버를 사용 하 여 RD 세션 호스트 서버 구성 되지 않았습니다. RD 세션 호스트 서버에 대 한 라이선스 서버를 구성 하지 않으면 RD 세션 호스트 서버에 대 한 연결을 거부 됩니다.
  - 라이선스 서버 \<computer name\> 수는 없습니다. 이 네트워크 연결 문제 때문일 수, 라이선스 서버에서 원격 데스크톱 라이선싱 서비스가 중지 또는 RD 라이선싱가 컴퓨터에 설치 되지 않은 합니다.

이러한 문제 다음 사용자 메시지와 연결 하는 경향이 있습니다.

  - 이 컴퓨터에 사용할 수 없는 원격 데스크톱 클라이언트 액세스 라이선스는 원격 세션 연결이 끊어졌습니다.
  - 원격 데스크톱 라이선스 서버가 없는 라이선스를 제공 하기 위해 사용할 수 있는 원격 세션 연결이 끊어졌습니다.

이 경우 [RD 라이선스 서비스를 구성](#configure-the-rd-licensing-service)합니다.

RD 라이선스 진단 기 "RDP 프로토콜 구성 요소 X.224 프로토콜 스트림의 오류를 감지 및 클라이언트의 연결이 끊어졌습니다" 있을 같은 기타 문제를 나열 하는 경우 라이선스 인증서에 영향을 주는 문제일 수 있습니다. 이러한 문제는 다음과 같은 사용자 메시지와 관련 된 경향이 있습니다.

보안 오류로 인해 클라이언트 터미널 서버에 연결할 수 없습니다. 네트워크에 로그온 있는지에 확인 한 후 다시 서버에 연결을 시도 합니다.

이 경우 [새로 고침의 X509 인증서 레지스트리 키](#refresh-the-x509-certificate-registry-keys).

### RD 라이선스 서비스 구성

다음 절차는 구성을 변경 하기 위해 서버 관리자를 사용 합니다. 구성 하 고 서버 관리자를 사용 하는 방법에 대 한 정보를 [서버 관리자](https://docs.microsoft.com/en-us/windows-server/administration/server-manager/server-manager)를 참조 하세요.

1. 서버 관리자를 열고 **원격 데스크톱 서비스**를 탐색 합니다.
2. **배포 개요** **작업**을 선택 하 고 **배포 속성 편집**을 선택 합니다.
3. **RD 라이선스**를 선택 하 고 배포 (**장치** 또는 **사용자 단위**)에 대 한 적절 한 라이선스 모드를 선택 합니다.
4. RD 라이선스 서버의 정규화 된 도메인 이름 (FQDN)를 입력 한 다음 **추가**선택 합니다.
5. RD 라이선스 서버를 여러 개 있는 경우 각 서버에 대해 4 단계를 반복 합니다. 
    ![RD 라이선스 서버 구성 옵션 서버 관리자에서입니다.](..\media\troubleshoot-remote-desktop-connections\RDLicensing_Configure.png)

### 새로 고침의 X509 인증서 레지스트리 키

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 수행 합니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 하기 전에 수정 [복원에 대 한 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 하 고 문제가 발생 하는 경우.

이 문제를 해결 하려면 백업 및 제거의 X509 인증서 레지스트리 키를 그 다음으로 컴퓨터를 활성화 RD 라이선스 서버를 다시 시작 합니다. 이렇게 하려면 다음이 단계를 따르세요.

> [!NOTE]  
> 각 RDSH 서버에서 다음 절차를 수행 합니다.

1. 레지스트리 편집기를 열고 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM**이동 합니다.
2. 레지스트리 메뉴에서 **레지스트리 파일 내보내기**를 선택 합니다.
3. **파일 이름** 상자에서 **내보낸 인증서** 를 입력 한 다음 **저장**을 선택 합니다.
4. 다음 값 중 각각을 마우스 오른쪽 단추로 클릭, **삭제**를 선택 하 고 **예** 를 삭제 확인를 선택 합니다.  
      - **Certificate**
      - **X509 인증서**
      - **X509 인증서 ID**
      - **X509 Certificate2**
5. 레지스트리 편집기를 종료 한 다음 RDSH 서버를 다시 시작 합니다.

## 사용자를 인증할 수 없는 또는 두 번 인증 해야 합니다.

사용자 인증에 영향을 주는 문제를 일으킬 수 있는 몇 가지 문제가 있습니다. 이 섹션에서는 다음과 같은 경우를 다룹니다.

  - [사용자가 "로그온 유형 제한" 메시지와 함께 액세스 거부](#access-denied-restricted-type-of-logon)
  - [사용자 또는 응용 프로그램 16965 이벤트를 사용 하 여 액세스 거부 되었습니다 "SAM 데이터베이스에 대 한 원격 호출이 거부 되었습니다"](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [스마트 카드를 사용 하 여 사용자가 로그인 할 수 없습니다.](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [사용자 암호를 두 번 입력 해야 하는 원격 PC 잠긴 경우](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [사용자가 로그인 할 수 없습니다 및 "인증 오류" 및 "CredSSP 암호화 oracle 수정" 메시지를 수신 합니다.](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [일부 사용자를 두 번 로그인 해야 클라이언트 컴퓨터를 업데이트](#after-you-update-client-computers-some-users-need-to-sign-in-twice)합니다.
  - [사용자의 경우에 여러 RD 연결 브로커를 사용 하 여 RemoteGuard를 사용 하는 배포에 대 한 액세스 거부 됨](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### 액세스 거부, 제한 된 로그온 유형

이 경우 Windows 10 또는 Windows Server 2016 컴퓨터에 연결 하려고 하는 Windows 10 사용자는 액세스할 수와 같은 메시지가:

> 원격 데스크톱 연결:  
> 시스템 관리자가 로그온 유형을 제한 (네트워크 또는 대화형)를 사용할 수 있습니다. 도움이 필요 하면 시스템 관리자 또는 기술 지원에 문의 합니다.

네트워크 수준 인증 (NLA) RDP 연결에 대 한 필수 이며 사용자가 **원격 데스크톱 사용자** 그룹의 구성원이 아닙니다.이 문제가 발생 합니다. **원격 데스크톱 사용자** 그룹 **네트워크에서이 컴퓨터 액세스** 사용자 권한을 할당 되지 않은 경우에 발생할 수 있습니다.

이 문제를 해결 하려면 다음이 단계 중 하나를 따릅니다.

  - [사용자의 그룹 구성원 또는 사용자 권한 할당을 수정](#modify-the-users-group-membership-or-user-rights-assignment)합니다.
  - NLA (권장 하지 않음)을 끕니다.
  - Windows 10 이외의 원격 데스크톱 클라이언트를 사용 합니다. 예를 들어 Windows 7 클라이언트에는이 문제가 없습니다.

#### 사용자의 그룹 구성원 또는 사용자 권한 할당을 수정 합니다.

이 문제는 단일 사용자에 영향을 가장 간단한이 문제를 해결 하려면이 **원격 데스크톱 사용자** 그룹에 사용자를 추가 하는 것입니다.

사용자가 이미이 그룹의 구성원 (또는 여러 그룹 구성원이 같은 문제가 있는 경우), 원격 Windows 10 또는 Windows Server 2016 컴퓨터에서 사용자 권한 구성을 확인 합니다.

1. 그룹 정책 개체 (GPE) 편집기를 열고 원격 컴퓨터의 로컬 정책에 연결 합니다.
2. **컴퓨터 Configuration\\Windows Settings\\Security Settings\\Local Policies\\User 권한 할당**를 찾아서 **네트워크에서이 컴퓨터 액세스**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.
3. **원격 데스크톱 사용자** (또는 부모 그룹)에 대 한 사용자 및 그룹의 목록을 확인 합니다.
4. 목록 **원격 데스크톱 사용자** (또는 **모든 사용자**와 같은 부모 그룹) 포함 하지 않을 경우 목록에 추가 해야 (배포에서를 두 개 이상 또는 두 컴퓨터가 있는 경우 그룹 정책 개체를 사용 함).  
    예를 들어 **네트워크에서이 컴퓨터 액세스** 에 대 한 기본 멤버십에 **모두**포함 됩니다. 그룹 정책 개체를 사용 하 여 **모두**제거 하는 배포, **원격 데스크톱 사용자**를 추가 하려면 그룹 정책 개체를 업데이트 하 여 액세스를 복원 해야 합니다.

### 액세스 거부, SAM 데이터베이스에 대 한 원격 호출이 거부 되었습니다.

이 동작은 도메인 컨트롤러에 Windows Server 2016 이상을 실행 하 고 사용자가 사용자 지정 된 연결 앱을 사용 하 여 연결을 시도 하는 경우 발생할 가능성이 가장 높습니다. 특히, Active Directory에서 사용자의 프로필 정보에 액세스 하는 응용 프로그램 액세스를 거부 됩니다.

이 동작을 변경 함으로써에서 Windows 높습니다. Windows Server 2012 R2 및 이전 버전에서는 사용자가 로그온 하는 원격 데스크톱, 원격 연결 관리자 (RCM) 연락처 도메인 컨트롤러를 Active Directory 도메인에서 사용자 개체에 원격 데스크톱에만 적용 되는 구성을 쿼리할 (DC) 서비스 (AD DS)입니다. 이 정보는 Active Directory 사용자 및 컴퓨터 MMC 스냅인에서 사용자의 개체 속성의 원격 데스크톱 서비스 프로필 탭에 표시 됩니다.

RCM은 Windows Server 2016 부터는 AD DS에서 사용자가 개체를 쿼리하여 더 이상. 원격 데스크톱 서비스 특성을 사용 하는 때문에 AD DS를 쿼리에 필요한 경우 이전 RCM 동작을 수동으로 설정 해야 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중 하 게 수행 합니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 하기 전에 수정 [복원에 대 한 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22) 하 고 문제가 발생 하는 경우.

RD 세션 호스트 서버에 레거시 RCM 동작을 사용 하려면 다음 레지스트리 항목을 구성 하 고 **원격 데스크톱** 서비스를 다시 시작 합니다.  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal 서비스**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation name\>\\**  
      - 이름: **fQueryUserConfigFromDC**
      - 유형: **Reg\_DWORD**
      - 값: **1** (십진수)

RD 세션 호스트 서버 이외의 다른 서버에서 레거시 RCM 동작을 사용 하려면 다음과 같은 추가 레지스트리 항목 및 이러한 레지스트리 항목을 구성 하 고 서비스를 다시 시작.
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal 서버**

이 문제에 대 한 자세한 내용은 KB 3200967 [변경 Windows Server의 원격 연결 관리자를](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server)참조 하세요.

### 스마트 카드를 사용 하 여 사용자가 로그인 할 수 없습니다.

이 문서는 사용자가 로그인 할 수 없습니다 원격 데스크톱에 스마트 카드를 사용 하 여 세 가지 일반적인 상황을 해결 합니다.  
  - [사용자는 읽기 전용 도메인 컨트롤러 (RODC)를 사용 하는 지점에 로그인 할 수 없습니다.](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [사용자가 최근에 업데이트 된 Windows Server 2008 SP2 컴퓨터에 로그인 할 수 없습니다.](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [사용자가 로그인 최근에 업데이트 된 Windows 컴퓨터에 유지 되지 않을 수 해지고 원격 데스크톱 서비스 응답 하지 않는 (일시 중단)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### 스마트 카드는 RODC 사용 하 여 지점에 로그인 할 수 없습니다.

이 문제는 RODC를 사용 하는 지점 사이트에는 RDSH 서버를 포함 하는 배포에서 발생 합니다. RDSH 서버 루트 도메인에 호스트 됩니다. 지점 사이트에 사용자가 자식 도메인에 속하며 인증용 스마트 카드를 사용 합니다. RODC 캐시 사용자 암호 (RODC **허용 RODC 암호 복제 그룹**에 속한)으로 구성 됩니다. "시도한 로그온 올바르지 않습니다 같은 메시지를 받은 사용자를 RDSH 서버에서 세션에 로그인 하려고 하는 경우. 이것이 사용자 이름 또는 인증 정보를 잘못 되었기 때문입니다. "

이것은 방식으로 알려진된 문제는 루트 DC 및 RODC 사용자 자격 증명의 암호화를 관리 합니다. 루트 DC는 암호화 키를 사용 하 여 자격 증명을 암호화 하 고 RODC 클라이언트 암호 해독 키를 제공 합니다. 그러나 두 개의 키 일치 하지 않습니다.

이 문제를 해결 하려면 암호 RODC에 캐싱 꺼서 또는 쓰기 가능 DC 지점 사이트를 배포 하 여 DC 토폴로지를 변경 하는 것이 좋습니다. 하는 다른 방법은 사용자와 동일한 자식 도메인 RDSH 서버를 이동 하는 것입니다. 또 다른 방법은 사용자가 스마트 카드 없이 로그인 하도록 허용 하는 것입니다. 이러한 솔루션의 성능이 나 보안 수준을 절충안 필요할 수 있습니다.

#### Windows Server 2008 SP2 컴퓨터에 스마트 카드를 사용 하 여 로그인 수 없습니다.

사용자가 KB4093227를 사용 하 여 업데이트 된 Windows Server 2008 SP2 컴퓨터에 로그인 하면이 문제가 발생 (2018.4B). 사용자가 스마트 카드를 사용 하 여 로그인 하려고 하면 "올바른 인증서가 없습니다과 같은 메시지를 사용 하 여 액세스가 거부 됩니다. 카드 올바르게 삽입 되 고 딱 확인 합니다. " 동시에, Windows Server 컴퓨터 이벤트를 기록 응용 프로그램 "삽입 된 스마트 카드에서 디지털 인증서를 검색 하는 동안 오류가 발생 합니다. 잘못 된 서명 합니다. "

이 문제를 해결 하려면 Windows Server 컴퓨터는 2018.06Bre로 업데이트-KB 4093227 릴리스의 [Windows 원격 데스크톱 프로토콜 (RDP) 거부 Windows Server 2008의 서비스 취약점에 대 한 보안 업데이트의 설명: 2018 년 4 월 10 일](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)합니다.

#### 스마트 카드 및 원격 데스크톱 서비스 서비스 중단을 사용 하 여 서명 된 상태로 유지할 수 없습니다.

사용자가 KB 4056446를 사용 하 여 업데이트 된 Windows 또는 Windows Server 컴퓨터에 로그인 하면이 문제가 발생 합니다. 처음에 사용자는 스마트 카드를 사용 하 여 시스템에 로그인 할 수 있지만 "SCARD\_E\_NO\_SERVICE" 오류 메시지를 받습니다. 원격 컴퓨터 응답 하지 않을 수 있습니다.

이 문제를 해결 하려면 원격 컴퓨터를 다시 시작 합니다.

이 문제를 해결 하려면 적절 한 해결으로 원격 컴퓨터를 업데이트 합니다.

  - Windows Server 2008 s p 2: KB 4090928, [Windows 누수 lsm.exe 프로세스에서 처리 하 고 스마트 카드 응용 프로그램 "SCARD\_E\_NO\_SERVICE" 오류가 표시 될 수 있습니다](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2: KB, 4103724 [2018 년 5 월 17-KB4103724 (월별 롤업의 미리 보기)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 및 Windows 10 버전 1607: KB 4103720 [2018 년 5 월 17-KB4103720 (OS 빌드 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### 사용자 암호를 두 번 입력 해야 하는 원격 PC 잠긴 경우

이 문제는 사용자가 RDP 연결 NLA 필요 하지 않은 배포에서 Windows 10 버전 1709 실행 하는 원격 데스크톱에 연결 하려고 할 때 발생할 수 있습니다. 이러한 조건에서 원격 데스크톱을 잠근 경우 사용자를 연결할 때 두 번 자신의 자격 증명을 입력 해야 합니다.

이 문제를 해결 하려면 Windows 10 버전 1709 컴퓨터 KB 4343893 업데이트로 [2018 년 8 월 30 일-KB4343893 (OS 빌드 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893).

### 사용자가 로그인 할 수 없습니다 및 "인증 오류" 및 "CredSSP 암호화 oracle 수정" 메시지를 수신 합니다.

사용자가 모든 버전의 Windows Vista SP2 및 이후 버전 또는 Windows Server 2008 s p 2에서 Windows 및 이후 버전을 사용 하 여 로그인 하려고 하면 액세스할 수 있으며 다음과 같은 메시지가:

  - 인증 오류가 발생 했습니다. 요청한 함수가 지원 되지 않습니다.
  - CredSSP 암호화 oracle 시정 때문일 수 있습니다.

"CredSSP 암호화 oracle 수정" 3 월, 4 월 및 2018 년 5 월에 출시 되는 보안 업데이트의 집합을 나타냅니다. CredSSP는 다른 응용 프로그램에 대 한 인증 요청을 처리 하는 인증 공급자입니다. 13 2018 년 3 월, "3B" 및 후속 업데이트는 공격자가 대상 시스템에서 코드를 실행할 사용자 자격 증명을 릴레이는 악용 해결 방법입니다.

초기 업데이트 **암호화 Oracle 수정**, 다음 가능한 설정이 있는 새 그룹 정책 개체에 대 한 지원이 추가 되었습니다.

  - **취약**합니다. CredSSP를 사용 하는 클라이언트 응용 프로그램을 보안 되지 않은 버전 대체 수 있지만이 동작을 공격 하는 원격 데스크톱 노출 합니다. CredSSP를 사용 하는 서비스 업데이트 되지 않은 클라이언트를 수락 합니다.
  - **완화**합니다. CredSSP를 사용 하는 클라이언트 응용 프로그램 안전 하지 않은 버전으로 다시 떨어질 수 있지만 CredSSP를 사용 하는 서비스 업데이트 되지 않은 클라이언트는 허용.
  - **힘 클라이언트를 업데이트**합니다. CredSSP를 사용 하는 클라이언트 응용 프로그램 안전 하지 않은 버전으로 다시 떨어질 수 및 CredSSP를 사용 하는 서비스 패치가 적용 되지 않은 클라이언트를 허용 하지 않습니다. 
    참고: 모든 원격 호스트 최신 버전을 지원 될 때까지이 설정을 배포 하지 말아야 합니다.

기본 **암호화 Oracle 시정** 설정은 **Vulnerable** 에서 **완화**로 변경 하는 2018 년 5 월 8 일 업데이트 합니다. 이러한 변경으로 업데이트가 원격 데스크톱 클라이언트 없는 (또는 다시 시작 하지 않은 서버 업데이트)는 서버에 연결할 수 없습니다. 업데이트 및 통신은 차단 하는 유형 효과 대 한 자세한 내용은 KB 4093492, [c v E-2018-0886에 대 한 업데이트 CredSSP](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)참조 하세요.

이 문제를 해결 하려면 모든 시스템은 완전히 업데이트 및 다시 시작을 확인 합니다. 업데이트 및 보안 문제에 대 한 자세한 내용은의 전체 목록, c v E-2018-0886 [를 참조 하세요. | CredSSP 원격 코드 취약점이](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886)합니다.

업데이트가 완료 될 때까지이 문제를 해결 하려면 KB 4093492 허용 된 유형의 연결을 확인 합니다. 불가능 대 한 대안이 없는 경우 다음 방법 중 하나를 고려할 수 있습니다.

  - 영향을 받는 클라이언트 컴퓨터에 대 한 **암호화 Oracle 시정** 정책을 **Vulnerable**로 다시 설정 합니다.
  - **컴퓨터 구성 요소 \ \ Components\\Remote 데스크톱 Services\\Remote 데스크톱 세션 Host\\Security** 그룹 정책 폴더의 다음 정책 수정 합니다.  
      - **(RDP)에 대 한 원격 연결에 대 한 특정 보안 계층을 사용 해야**: **사용** 으로 설정 하 고 **RDP**를 선택 합니다.
      - **네트워크 수준 인증을 사용 하 여 원격 연결에 대 한 사용자 인증**: **사용 안 함**으로 설정 합니다.
      > [!IMPORTANT]  
      > 이러한 수정 배포의 보안을 줄입니다. 만 전혀 사용 하는 경우에 임시 되어야 합니다.

그룹 정책 사용에 대 한 자세한 내용은 [수정 차단 GPO를](#modifying-a-blocking-gpo)참조 하세요.

### 일부 사용자를 두 번 로그인 해야 클라이언트 컴퓨터를 업데이트 한 후

일부 Windows 7 또는 Windows 10 버전 1709에서 사용자가 원격 데스크톱 세션에 로그인 하 고 즉시 두 번째 로그인 화면을 표시 합니다. 이 문제는 클라이언트 컴퓨터에서 다음 업데이트를 수신 하는 경우 발생 합니다.

  - Windows 7: KB, 4103718 [2018 년 5 월 8 일-KB4103718 (월별 롤업)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB, 4103727 [2018 년 5 월 8 일-KB4103727 (OS 빌드 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

이 문제를 해결 하려면 컴퓨터 (뿐만 아니라 RDSH 또는 RDVI 서버)에 연결 하는 사용자가 원하는 2018 년 6 월 통해 완전히 업데이트 되었는지 확인 합니다. 다음과 같은 업데이트가 포함 됩니다.

  - Windows Server 2016: KB, 4284880 [2018 년 6 월 12 일-KB4284880 (OS 빌드 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB, 4284815 [2018 년 6 월 12 일-KB4284815 (월별 롤업)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB, 4284855 [2018 년 6 월 12 일-KB4284855 (월별 롤업)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB, 4284826 [2018 년 6 월 12 일-KB4284826 (월별 롤업)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 s p 2: KB4056564 [Windows Server 2008, Windows Embedded POSReady 2009, 및 Windows Embedded 표준 2009 CredSSP 원격 코드 실행 취약점에 대 한 보안 업데이트의 설명: 2018 년 3 월 13 일](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### 사용자의 경우에 여러 RD 연결 브로커를 사용 하 여 원격 Credential Guard를 사용 하는 배포에 대 한 액세스 거부 됨

Windows Defender 원격 Credential Guard 사용 중인 경우 두 개 이상의 원격 데스크톱 연결 브로커를 사용 하 여 고가용성 배포에 이러한 문제가 발생 합니다. 사용자가 원격 데스크톱에 로그인 할 수 없습니다.

이 문제는 원격 Credential Guard Kerberos 인증을 사용 하 여 및 NTLM 제한 때문에 발생 합니다. 그러나 부하 분산 된 고가용성 구성에서 RD 연결 브로커 Kerberos 작업을 지원 하지 않습니다.

RD 연결 브로커 부하 분산을 사용 하 여 고가용성 구성을 사용 해야 할 경우 원격 Credential Guard를 사용 하지 않도록 설정 하 여이 문제를 해결할 수 있습니다. Windows Defender 원격 Credential Guard를 관리 하는 방법에 대 한 자세한 내용은 [Windows Defender 원격 Credential Guard로 보호 원격 데스크톱 자격 증명](https://docs.microsoft.com/en-us/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)을 참조 하세요.

## 연결을 사용자에 게 "원격 데스크톱 서비스는 현재 작업 중" 메시지가

이 문제에 대 한 적절 한 응답을 확인 하려면 다음 단계를 사용 합니다.

1. 원격 데스크톱 서비스 서비스 응답 하지 않는 됩니다. (예를 들어 원격 데스크톱 클라이언트 멈춘 것 처럼 "" 시작 화면에서).  
      - 서비스 응답 하지 않는 되더라도 [RDSH 서버 메모리 문제](#rdsh-server-memory-issue)를 참조 하세요.
      - 일반적으로 서비스와 상호 작용을 클라이언트에 표시 되 면 다음 단계를 계속 합니다.
2. 하나 이상의 사용자가 원격 데스크톱 세션 연결을 해제 하는 경우 사용자가 다시 연결할 수 있습니다.  
   - 얼마나 많은 사용자가 자신의 세션 연결 끊기에 관계 없이 연결을 거부 하는 서비스 계속 되 면 [RD 수신기 문제](#rd-listener-issue)를 참조 하세요.
   - 서비스 시작을 수락 하는 경우 사용자가 다양 한 후 다시 연결 [연결 제한 정책을 확인](#check-the-connection-limit-policy)가 세션 연결이 끊어져 합니다.

### RDSH 서버 메모리 문제

일부 Windows Server 2012 R2 RDSH 서버에서 메모리 누수를 발견 되었습니다. 시간이 지남에 따라 이러한 서버는 원격 데스크톱 연결와 같은 메시지를 사용 하 여 로컬 콘솔 사이 니 지 기능 거부 하도록 시작 합니다.

> 원격 데스크톱 서비스 현재 사용 중 이므로 작업을 수행 하려는 작업을 완료할 수 없습니다. 몇 분 후에 다시 시도 하세요. 다른 사용자가 로그인 할 수 해야 합니다.

원격 데스크톱 클라이언트에도 연결을 시도 응답 하지 않는 됩니다.

이 문제를 해결 하려면 RDSH 서버를 다시 시작 합니다.

이 문제를 해결 하려면 KB 4093114 적용 [2018 년 4 월 10 일-KB4093114 (월별 롤업)] (file:///C:\\Users\\v-jesits\\AppData\\Local\\Microsoft\\Windows\\INetCache\\Content.Outlook\\FUB8OO45\\April%2010,%202018—KB4093114%20\(Monthly% 20Rollup\)), RDSH 서버.

### RD 수신기 문제

Windows Server 2012 r 2로 Windows Server 2008 r 2에서 직접 업그레이드 하는 일부 RDSH 서버 또는 Windows Server 2016에서 설명한는 문제를 해결 합니다. 원격 데스크톱 클라이언트 RDSH 서버에 연결할 때 RDSH 서버 사용자 세션에 대 한 RD 수신기를 만듭니다. 영향을 받는 서버 유지 RD 수신기는 사용자가 연결 증가 하지만 되지 감소의 수입니다.

이 문제를 해결 하려면 다음 메서드를 사용할 수 있습니다.

  - RD 수신기의 수를 재설정 하 RDSH 서버를 다시 시작
  - 매우 큰 값으로 설정 하 고 연결 제한 정책을 수정 합니다. 연결 제한 정책을 관리 하는 방법에 대 한 자세한 내용은 [연결 제한 정책을 확인](#check-the-connection-limit-policy)을 참조 하세요.

이 문제를 해결 하려면 다음 업데이트 RDSH 서버에 적용 됩니다.

  - Windows Server 2012 R2: KB, 4343891 [2018 년 8 월 30 일-KB4343891 (월별 롤업의 미리 보기)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB, 4343884 [2018 년 8 월 30 일-KB4343884 (OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### 연결 제한 정책을 확인합니다

개별 컴퓨터 수준 또는 그룹 정책 개체 (GPO)를 구성 하 여 동시 원격 데스크톱 연결 수에 제한을 설정할 수 있습니다. 기본적으로 제한이 설정 되지 않았습니다.

현재 설정을 확인 하 고 RDSH 서버에서 기존 Gpo를 식별 하려면 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 입력 합니다.
  
```
gpresult /H c:\gpresult.html
```
   
이 명령은 완료 되 면 gpresult.html를 열고 **컴퓨터 구성 요소 \ \ Components\\Remote 데스크톱 Services\\Remote 데스크톱 세션 Host\\Connections**찾은 **연결 수가 제한** 정책입니다.

  - 이 정책 설정을 **사용 하지 않는**경우, 그룹 정책에는 RDP 연결 하지 제한 됩니다.
  - 이 정책 설정을 **사용**이면 **영업 GPO**를 확인 합니다. 제거 또는 연결 제한을 변경 해야 할 경우이 GPO를 편집 합니다.

정책 변경 내용을 적용할 영향을 받는 컴퓨터에서 명령 프롬프트 창을 열고 다음 명령을 입력 합니다.
  
```
gpupdate /force
```
  
## RD 클라이언트 연결을 끊고 동일한 세션에 다시 연결할 수 없습니다.

원격 데스크톱 클라이언트 원격 데스크톱에 대 한 연결을 잃으면 후 클라이언트 즉시 다시 연결할 수 없습니다. 사용자는 다음과 같은 오류 메시지를 받습니다.

  - 보안 오류로 인해 클라이언트 터미널 서버에 연결할 수 없습니다. 네트워크에 로그온 있는지에 확인 한 후 다시 서버에 연결을 시도 합니다.
  - 원격 데스크톱 연결 끊김 합니다. 보안 오류로 인해 클라이언트에서 원격 컴퓨터에 연결할 수 없습니다. 네트워크에 로그온 하 고 다시 연결을 확인 합니다.

나중에 원격 데스크톱 클라이언트 원격 데스크톱에 다시 연결 합니다. 그러나 원래 세션에 클라이언트를 연결 하는 대신 RDSH 서버 클라이언트를 연결 새 세션을 합니다. RDSH 서버 확인 연결이 끊긴된 상태를 입력 하지 하지만 대신 활성 상태로 유지 되는 원래 세션을 보여 줍니다.

이 문제를 해결 하려면 컴퓨터 구성 요소 \ \ Components\\Remote 데스크톱 Services\\Remote 데스크톱 세션 Host\\Connections **에서 **구성 유지 연결 간격** 정책을 사용할 수 있습니다. **그룹 정책 폴더. 이 정책을 사용 하면 연결 유지 간격을 입력 해야 합니다. 연결 유지 간격 빈도, 세션 상태를 확인할 서버 시간 (분)을 결정 합니다.

이 문제는 인증 및 구성 설정의 잘못 된 구성은 때문일 수 있습니다. 서버 수준 또는 Gpo를 사용 하 여 이러한 설정을 구성할 수 있습니다. 그룹 정책 설정은 **컴퓨터 구성 요소 \ \ Components\\Remote 데스크톱 Services\\Remote 데스크톱 세션 Host\\Security** 그룹 정책 폴더에서 제공 됩니다.

1. RD 세션 호스트 서버에서 원격 데스크톱 세션 호스트 구성을 엽니다.
2. **연결**연결의 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.
3. **보안** 계층의 **일반** 탭에는 연결에 대 한 **속성** 대화 상자에서 보안 방법을 선택 합니다.
4. **암호화 수준**원하는 수준을 클릭 합니다. **낮음**, **클라이언트 호환**, **높음**또는 **FIPS 규격**선택할 수 있습니다.

> [!NOTE]  
>  - 가장 높은 수준의 암호화를 필요로 하는 클라이언트와 RD 세션 호스트 서버 간 통신을 할 때 FIPS 규격 암호화를 사용 합니다.
>  - 그룹 정책에서 구성 하는 암호화 수준 설정은 원격 데스크톱 서비스 구성 도구를 사용 하 여 설정한 구성 보다 우선 합니다. 또한 사용 하면 합니다 [시스템 암호화: 암호화, 해시 및 서명을 사용 하 여 FIPS 규격 알고리즘](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) 정책에이 설정을 **클라이언트 연결 암호화 수준** 정책 보다 우선 합니다. 시스템 암호화 정책은 **컴퓨터 Configuration\\Windows Settings\\Security Settings\\Local Policies\\Security 옵션** 폴더에서입니다.
>  - 암호화 수준을 변경 하면 새 암호화 수준은 사용자가 로그온 다음에 적용이 됩니다. 여러 수준의 하나의 서버에서 암호화를 필요로 하는 경우 여러 네트워크 어댑터를 설치 하 고 각 어댑터를 개별적으로 구성 합니다.
>  - 원격 데스크톱 서비스 구성에서 해당 인증서에 해당 개인 키를 확인 하려면 인증서 보기, **일반**선택, **편집**을 선택 하 려는 인증서 연결을 마우스 오른쪽 단추로 클릭 보고, 하 고 **인증서 보기를**선택 합니다. 이때 "개인 키가이 인증서에 해당 하 는" **일반** 탭의 맨 아래에 표시 되어야 합니다. 인증서 스냅인 사용 하 여이 정보를 볼 수도 있습니다.
>  - FIPS 규격 암호화 (합니다 **시스템 암호화: 암호화, 해시 및 서명을 사용 하 여 FIPS 규격 알고리즘** 원격 데스크톱 서버 구성에서 **FIPS 규격** 설정 또는 정책)를 암호화 하 고에서 전송 된 데이터의 암호를 해독 합니다 서버 및 클라이언트에, 정보 처리 표준 FIPS (Federal) 140-1 암호화 알고리즘을 사용 하 여 Microsoft 암호화 모듈을 사용 하 여 서버에서 클라이언트입니다. 자세한 내용은 [FIPS 140 유효성 검사](https://docs.microsoft.com/en-us/windows/security/threat-protection/fips-140-validation)를 참조 하세요.
>  - **높음** 설정 강력한 128 비트 암호화를 사용 하 여 서버를 클라이언트 및 서버 클라이언트를에서 전송 되는 데이터를 암호화 합니다.
>  - 클라이언트와 클라이언트에서 지 원하는 최대 키 강도로 서버 간에 전송 되는 데이터를 암호화 하는 **클라이언트와 호환 가능한** 설정 합니다.
>  - **낮음** 설정은 요청 암호화를 사용 하 여 서버를 클라이언트에서 전송 되는 데이터를 암호화 합니다.

## 무선 네트워크에서 연결을 끊습니다 원격 노트북

원격 데스크톱 클라이언트 802.1 x 무선 네트워크를 사용 하 여 노트북 컴퓨터에 연결할 때이 문제가 발생할 수 있습니다. 일시적으로, 노트북 무선 네트워크에서 연결을 끊고 자동으로 다시 연결 되지 않습니다.

무선 네트워크 연결에 대 한 네트워크 인증 설정을 **사용자 인증**때 발생 하는 알려진된 문제입니다.

이 문제를 해결 하려면 **사용자 또는 컴퓨터 인증** 또는 **컴퓨터 인증**네트워크 인증 설정을 설정 합니다.

 > [!NOTE]  
> 단일 컴퓨터에서 네트워크 인증 설정을 변경 하려면 제어판의 네트워크 및 공유 센터를 사용 하 여 새 설정을 사용 하 여 새 무선 연결을 만듭니다.

Gpo를 사용 하 여 무선 네트워크 설정을 구성 하는 방법에 대 한 전체 설명을, [구성 무선 네트워크 (IEEE 802.11) 정책](https://docs.microsoft.com/en-us/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)을 참조 하세요.

## 사용자 환경을 성능이 저하 되거나 응용 프로그램 문제

이 섹션에서는 사용자가 원격 데스크톱 기능을 사용할 때 발생할 수 있는 몇 가지 일반적인 문제를 해결 합니다.

  - [사용자가 Microsoft Azure를 일시적으로 새 가상 컴퓨터에 연결 하는 문제가 발생](#intermittent-problems-with-new-microsoft-azure-virtual-machines)합니다.
  - [Windows 10 버전 1709 원격 데스크톱에 연결 하는 사용자가 비디오를 재생 하는 문제가 있을 수 있습니다](#video-playback-issues-on-windows-10-version-1709).
  - [Windows 10 원격 데스크톱에 연결 하는 읽기 전용 사용자 프로필을 사용 하 여 사용자에 게 데스크톱을 공유할 수 없습니다.](#desktop-sharing-issues-on-windows-10)
  - [이전 버전의 Windows 10에서 실행 하는 클라이언트를 사용 하 여 Windows 10 원격 데스크톱에 연결 된 사용자 환경을 성능이 저하 NLA 사용 불가능](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [원격 데스크톱 세션에서 여러 응용 프로그램을 실행 하 고 분리 하 고 자주 다시 연결을 다시 연결 하는 검은색 화면을 발생할 수 있습니다.](#black-screen-issue)

### 새로운 Microsoft Azure 가상 컴퓨터의 일시적인 문제

이 문제는 최근에 프로 비전 하는 가상 컴퓨터에 영향을 줍니다. 원격 데스크톱 세션 사용자의 모든 설정 하면 가상 컴퓨터에 연결한 후 로드 되지 않는 올바르게 합니다.

이 문제를 해결 하려면 가상 컴퓨터에서 분리, 20 분 이상 기다린 후 다시 연결 합니다.

이 문제를 해결 하려면 다음 업데이트를 적절 하 게 가상 컴퓨터에 적용 됩니다.

  - Windows 10 및 Windows Server 2016: 4343884, KB [2018 년 8 월 30 일-KB4343884 (OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB, 4343891 [2018 년 8 월 30 일-KB4343891 (월별 롤업의 미리 보기)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### Windows 10 버전 1709에서 비디오 재생 문제

이 문제는 사용자가 Windows 10, 버전 1709 실행 하는 원격 컴퓨터에 연결할 때 발생 합니다. 이러한 사용자는 v m r 9를 사용 하 여 비디오 재생 때 (비디오 MixingRenderer9) 코덱 플레이어는 검은색 창이 보여 줍니다.

Windows 10, 버전 1709의에서 알려진된 문제입니다. Windows 10 버전 1703에서에서 문제가 발생 하지 않습니다.

### Windows 10에서 문제를 공유 하는 데스크톱

이 문제는 사용자에 게 읽기 전용 사용자 프로필 (및 관련된 레지스트리 하이브)와 같은 키오스크 시나리오에서 발생 합니다. 이러한 사용자가 Windows 10, 버전 1803 실행 하는 원격 컴퓨터에 연결 하는 경우 데스크톱을 공유할 수 없습니다.

이 문제를 해결 하려면 Windows 10 업데이트 4340917, 적용 [2018 년 7 월 24 일-KB4340917 (OS 빌드 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917).

### 성능 문제 NLA 사용 되지 않는 경우 Windows 10의 버전을 혼합 하는 경우

NLA은 사용 되지 않으며 Windows 10을 실행 하는 원격 데스크톱 클라이언트 컴퓨터는 다른 버전의 Windows 10을 실행 하는 원격 데스크톱에 연결 하는 경우이 문제가 발생 합니다. Windows 10, 버전 1709 또는 이전 버전을 실행 하는 컴퓨터에서 원격 데스크톱 클라이언트의 사용자에 게 Windows 10, 버전 1803 또는 이후 버전을 실행 하는 원격 데스크톱에 연결 될 때 성능이 저하 발생 합니다.

NLA 비활성화 되 면 이전 클라이언트 컴퓨터를 Windows 10, 버전 1803 또는 이후 버전에 연결할 때 더 느린 프로토콜을 사용 하는 때문에 발생 합니다.

이 문제를 해결 하려면 적용 KB 4340917 [2018 년 7 월 24 일-KB4340917 (OS 빌드 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917).

### 빈 화면이 문제

Windows 8.0, Windows 8.1, Windows 10 RTM 및 Windows Server 2012 r 2에 이러한 문제가 발생 합니다. 사용자는 원격 데스크톱에서 여러 응용 프로그램을 실행 한 다음 세션에서 연결을 끊습니다. 주기적으로 원격 데스크톱 응용 프로그램을 상호 작용 하 고 다시 연결 끊기-사용자가 다시 연결 합니다. 사용자가 다시 연결 되 면 어느 시점에서는 원격 데스크톱 세션 방금 검은색 화면을 표시 합니다. 사용자는 원격 컴퓨터의 콘솔 (또는 RDSH 서버 콘솔)에서 원격 데스크톱 세션을 끝내 야 합니다. 이 작업은 응용 프로그램을 중지합니다.

이 문제를 해결 하려면 다음 업데이트를 적절 하 게 적용 됩니다.

  - Windows 8 및 Windows Server 2012: KB4103719, [2018 년 5 월 17-KB4103719 (월별 롤업의 미리 보기)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 및 Windows Server 2012 r 2: KB4103724, [2018 년 5 월 17-KB4103724 (월별 롤업의 미리 보기)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) 및 4284863, KB [2018 년 6 월 21-KB4284863 (월별 롤업의 미리 보기)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10: KB4284860에서 수정 [2018 년 6 월 12 일-KB4284860 (OS 빌드 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)
