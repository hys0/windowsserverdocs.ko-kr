---
title: 사용자에 대한 원격 데스크톱 웹 클라이언트 설정
description: 관리자 수 원격 데스크톱 웹 클라이언트에 설정 하는 방법을 설명 합니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: bf10f7f7444967247e51065bc6138fc0afd5ed1a
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976777"
---
# <a name="set-up-the-remote-desktop-web-client-for-your-users"></a>사용자에 대한 원격 데스크톱 웹 클라이언트 설정

원격 데스크톱 웹 클라이언트 호환 웹 브라우저를 통해 조직의 원격 데스크톱 인프라에 액세스할 수 있도록 합니다. 이러한 원격 앱 또는 위치에 관계 없이 로컬 PC와 함께 하 듯 데스크톱 상호 작용할 수 있습니다. 원격 데스크톱 웹 클라이언트를 설정한 후 사용자가 시작 하는 데 필요한 모든 url은 URL 클라이언트, 자격 증명 및 지원 되는 웹 브라우저를을 액세스할 수 있습니다.

>[!IMPORTANT]
>웹 클라이언트는 Azure 응용 프로그램 프록시를 사용 하 여 현재 지원 하지 않습니다 하 고 웹 응용 프로그램 프록시를 전혀 지원 하지 않습니다. 참조 [응용 프로그램 프록시 서비스를 사용 하 여 RDS를 사용 하 여](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services) 세부 정보에 대 한 합니다.

## <a name="what-youll-need-to-set-up-the-web-client"></a>웹 클라이언트를 설정 해야

시작 하기 전에 다음 사항에 유의 하십시오를 유지 합니다.

* 있는지 확인 하 [원격 데스크톱 배포](../rds-deploy-infrastructure.md) 에 RD 게이트웨이, RD 연결 브로커 및 RD 웹 액세스 2019 또는 Windows Server 2016에서 실행 합니다.
* 배포 구성가 있는지 확인 [사용자 단위 클라이언트 액세스 라이선스](../rds-client-access-license.md) (Cal) 장치 단위 대신이 고, 그렇지는 모든 라이선스에 의해 소비 됩니다.
* 설치 합니다 [Windows 10 KB4025334 업데이트](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) RD 게이트웨이에서 합니다. 나중에 누적 업데이트 될 수 있습니다이 기술 자료에 이미 있습니다.
* 신뢰할 수 있는 공용 인증서는 RD 게이트웨이 및 RD 웹 액세스 역할에 대해 구성 되어 있는지 확인 하십시오.
* 사용자가 연결할 컴퓨터 OS 버전 중 하나를 실행 중인 있는지 확인 합니다.
  * Windows 10
  * Windows Server 2008 r2 이상

더 나은 성능 연결에 Windows Server 2016 (이상) 및 Windows 10 (버전 1611 이상) 사용자에 게 표시 됩니다.

>[!IMPORTANT]
>미리 보기 기간 동안 웹 클라이언트를 사용 하 고 1.0.0 이전 버전을 설치 하는 경우에 새 버전으로 이동 하기 전에 먼저 이전 클라이언트를 제거 해야 합니다. "웹 클라이언트 RDWebClientManagement의 이전 버전을 사용 하 여 설치한 및 새 버전을 배포 하기 전에 먼저 제거 해야 합니다." 라는 오류가 표시를 하는 경우 다음이 단계를 수행 합니다.
>
>1. 관리자 권한 PowerShell 프롬프트를 엽니다.
>2. 실행할 **Uninstall-module RDWebClientManagement** 를 새로운 모듈을 제거 합니다.
>3. 관리자 권한 PowerShell 프롬프트를 닫고 다시 엽니다.
>4. 실행할 **Install-module RDWebClientManagement-RequiredVersion \<이전 버전 > 이전 모듈을 설치 합니다.**
>5. 실행할 **제거 RDWebClient** 이전 웹 클라이언트를 제거 합니다.
>6. 실행할 **Uninstall-module RDWebClientManagement** 이전 모듈을 제거 합니다.
>7. 관리자 권한 PowerShell 프롬프트를 닫고 다시 엽니다.
>8. 일반 설치 단계를 다음과 같이 진행 합니다.

## <a name="how-to-publish-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트를 게시 하는 방법

처음에 대 한 웹 클라이언트를 설치 하려면 다음이 단계를 수행 합니다.

1. RD 연결 브로커 서버에서 원격 데스크톱 연결에 사용 되는 인증서를 가져와야 하 고.cer 파일로 내보냅니다. RD 웹 역할을 실행 하는 서버에 RD 연결 브로커에서.cer 파일을 복사 합니다.
2. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 엽니다.
3. Windows Server 2016에서 받은 편지함 버전 웹 클라이언트 management 모듈 설치를 지원 하지 않으므로 PowerShellGet 모듈을 업데이트 합니다. PowerShellGet을 업데이트 하려면 다음 cmdlet을 실행 합니다.
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >적용 하려면 먼저 업데이트, 그렇지 않으면 모듈 작동 하지 않을 수 PowerShell을 다시 시작 해야 합니다.

4. 이 cmdlet 사용 하 여 PowerShell 갤러리에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 설치 합니다.
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. 그 후 원격 데스크톱 웹 클라이언트의 최신 버전을 다운로드 하려면 다음 cmdlet을 실행 합니다.
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. 다음으로 RD 브로커에서 복사 된.cer 파일의 경로 사용 하 여 대체 대괄호로 묶은 값을 사용 하 여이 cmdlet을 실행 합니다.
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. 마지막으로, 원격 데스크톱 웹 클라이언트를 게시 하려면이 cmdlet을 실행 합니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    형식으로 서버 이름을 사용 하 여 웹 클라이언트 URL에 웹 클라이언트를 액세스할 수 있도록 <https://server_FQDN/RDWeb/webclient/index.html>입니다. RD 웹 액세스 공용 URL (일반적으로 서버 FQDN) 인증서와 일치 하는 서버 이름을 사용 하는 것이 반드시 합니다.

    >[!NOTE]
    >실행 하는 경우는 **게시 RDWebClientPackage** cmdlet 표시 될 수 있습니다 장치 단위 Cal을 알리는 경고가 지원 되지 않으며, 사용자 단위 Cal에 대 한 배포 구성 된 경우에 합니다. 배포 사용자 단위 Cal을 사용 하는 경우이 경고를 무시할 수 있습니다. 구성 제한 사항을 알고 있는지 확인 하도록 표시 합니다.
8. 웹 클라이언트에 액세스 하려면 사용자에 대 한 준비가 사람에 게 보냅니다 만든 웹 클라이언트 URL입니다.

>[!NOTE]
>RDWebClientManagement 모듈에 대 한 모든 지원 되는 cmdlet의 목록을 보려면 PowerShell에서 다음 cmdlet을 실행 합니다.
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## <a name="how-to-update-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트를 업데이트 하는 방법

원격 데스크톱 웹 클라이언트의 새 버전이 제공 된 경우 새 클라이언트를 사용 하 여 배포를 업데이트 하려면 다음이 단계를 수행 하십시오.

1. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 열고 웹 클라이언트의 사용 가능한 최신 버전을 다운로드 하려면 다음 cmdlet을 실행 합니다.
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. 필요에 따라 공식 릴리스 전에이 cmdlet을 실행 하 여 테스트에 대 한 클라이언트를 게시할 수 있습니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    클라이언트 웹 클라이언트 URL에 해당 하는 테스트 URL에 표시 됩니다 (예를 들어 <https://server_FQDN/RDWeb/webclient-test/index.html>).
3. 다음 cmdlet을 실행 하 여 사용자에 대 한 클라이언트를 게시 합니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    이렇게 하면 해당 웹 페이지를 다시 시작 하는 경우 모든 사용자 용 클라이언트를 바뀝니다.

## <a name="how-to-uninstall-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트를 제거 하는 방법

웹 클라이언트의 모든 흔적을 제거 하려면 다음이 단계를 수행 합니다.

1. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 엽니다.
2. 테스트 및 프로덕션 클라이언트를 게시 취소 하 고, 모든 로컬 패키지를 제거 하 고 및 웹 클라이언트 설정을 제거:

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 제거 합니다.

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## <a name="how-to-install-the-remote-desktop-web-client-without-an-internet-connection"></a>인터넷 연결 없이 원격 데스크톱 웹 클라이언트를 설치 하는 방법

인터넷에 연결 되지 않은 RD 웹 액세스 서버에 웹 클라이언트를 배포 하려면 다음이 단계를 따릅니다.

> [!NOTE]
> 인터넷 연결이 버전 1.0.1 이상 사용할 수 없는 설치 RDWebClientManagement PowerShell 모듈입니다.

> [!NOTE]
> 오프 라인 서버에이 전송 하기 전에 필요한 파일을 다운로드 하려면 인터넷에 연결 된 PC를 관리를 해야 합니다.

> [!NOTE]
> 최종 사용자 PC는 이제 인터넷에 연결을 해야합니다. 이 전체 오프 라인 시나리오를 제공 하기 위해 클라이언트의 이후 릴리스에서 해결 될 예정입니다.

### <a name="from-a-device-with-internet-access"></a>인터넷에 연결 된 장치에서

1. PowerShell 프롬프트를 엽니다.

2. PowerShell 갤러리에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 가져옵니다.
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. 다른 장치에서 설치에 대 한 원격 데스크톱 웹 클라이언트의 최신 버전을 다운로드 합니다.
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. RDWebClientManagement PowerShell 모듈의 최신 버전을 다운로드 합니다.
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. 콘텐츠 복사 "C:\WebClient\" RD 웹 액세스 서버입니다.

### <a name="from-the-rd-web-access-server"></a>RD 웹 액세스 서버에서

지침을 따릅니다 [원격 데스크톱 웹 클라이언트를 게시 하는 방법](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client), 4, 5 단계 다음으로 바꿉니다.

4. 로컬 폴더에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 가져옵니다.
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. 로컬 폴더 (적절 한 zip 파일을 사용 하 여 대체)에서 원격 데스크톱 웹 클라이언트의 최신 버전을 배포 합니다.
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## <a name="connecting-to-rd-broker-without-rd-gateway-in-windows-server-2019"></a>Windows Server 2019에서에서 RD 게이트웨이 없이 RD Broker에 연결
이 섹션에서는 Windows Server 2019에 RD 게이트웨이 없이 RD Broker에 웹 클라이언트 연결을 사용 하는 방법을 설명 합니다.

### <a name="setting-up-the-rd-broker-server"></a>RD 브로커 서버 설정

#### <a name="follow-these-steps-if-there-is-no-certificate-bound-to-the-rd-broker-server"></a>인증서가 없는 RD 브로커 서버에 연결 하는 경우 다음이 단계를 수행 합니다.

1. 오픈 **서버 관리자** > **원격 데스크톱 서비스**합니다.

2. **배포 개요** 섹션을 선택 합니다 **작업** 드롭다운 메뉴입니다.

3. 선택 **배포 속성 편집**, 라는 새 창을 **배포 속성** 열립니다.

4. 에 **배포 속성** 창에서 **인증서** 왼쪽된 메뉴에서.

5. 인증서 수준 목록에서 선택 **RD 연결 브로커-사용 Single Sign On**합니다. 두 가지가 있습니다. (1) 만들거나 새 인증서 (2) 기존 인증서.

#### <a name="follow-these-steps-if-there-is-a-certificate-previously-bound-to-the-rd-broker-server"></a>RD 브로커 서버를 이전에 바인딩된 인증서를 있으면 다음이 단계를 수행 합니다.

1. 열기 인증서 바인딩된 Broker에 복사 합니다 **지문** 값입니다.

2. 보안 포트 3392에이 인증서를 바인딩할 관리자 권한 PowerShell 창을 열고 다음을 실행 명령을 바꾸는 **"< 지문 >"** 이전 단계에서 복사한 값을 사용 하 여:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 인증서가 올바르게 바인딩된 경우를 확인 하려면 다음 명령을 실행 합니다.
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 인증서 바인딩 목록에서 올바른 인증서 3392 포트에 바인딩되어 있는지 확인 합니다.

3. Windows 레지스트리 (regedit)를 열고에 nagivate ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` 키를 찾아서 **WebSocketURI**합니다. 값으로 설정 되어 있어야 **https://+:3392/rdp/** 합니다.

### <a name="setting-up-the-rd-session-host"></a>RD 세션 호스트 설정
RD 세션 호스트 서버는 RD 브로커 서버와 다른 경우 다음이 단계를 따르세요.

1. RD 세션 호스트 컴퓨터에 대 한 인증서를 만들고 연를 복사 합니다 **지문을** 값입니다.

2. 보안 포트 3392에이 인증서를 바인딩할 관리자 권한 PowerShell 창을 열고 다음을 실행 명령을 바꾸는 **"< 지문 >"** 이전 단계에서 복사한 값을 사용 하 여:

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 인증서가 올바르게 바인딩된 경우를 확인 하려면 다음 명령을 실행 합니다.
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 인증서 바인딩 목록에서 올바른 인증서 3392 포트에 바인딩되어 있는지 확인 합니다.

3. Windows 레지스트리 (regedit)를 열고에 nagivate ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` 키를 찾아서 **WebSocketURI**합니다. 값으로 설정 되어 있어야 **https://+:3392/rdp/** 합니다.

### <a name="general-observations"></a>일반 관찰

* RD 세션 호스트 및 RD 브로커 서버가 Windows Server 2019 실행 되 고 있는지 확인 합니다.

* 해당 공용 RD 브로커 및 RD 세션 호스트 서버에 대 한 인증서를 구성 하는 신뢰할 수 있는 것을 확인 합니다.
    > [!NOTE]
    > RD 세션 호스트 및 RD 브로커 서버를 둘 다 동일한 컴퓨터를 공유 하는 경우 RD 브로커 서버 인증서를 설정 합니다. RD 세션 호스트 및 RD 브로커 서버가 다른 컴퓨터를 사용 하는 경우 둘 다 고유한 인증서를 사용 하 여 구성 해야 합니다.

* 합니다 **주체 대체 이름 (SAN)** 컴퓨터의 각 인증서를 설정 해야에 대 한 **정규화 된 도메인 이름 (FQDN)** 합니다. 합니다 **CN (일반 이름)** 각 인증서에 대 한 SAN과 일치 해야 합니다.

## <a name="how-to-pre-configure-settings-for-remote-desktop-web-client-users"></a>원격 데스크톱 웹 클라이언트 사용자에 대 한 설정을 미리 구성 하는 방법
이 섹션에서는 PowerShell을 사용 하 여 원격 데스크톱 웹 클라이언트 배포에 대 한 설정을 구성 하는 방법을 알려줍니다. 이러한 PowerShell cmdlet 컨트롤 사용자 설정을 변경 하려면 조직의 보안 고려 사항에 따라 또는 워크플로 위한 것입니다. 다음 설정을 모두에 있는 합니다 **설정을** 웹 클라이언트의 사이드 패널입니다. 

### <a name="suppress-telemetry"></a>원격 분석 표시 안 함
기본적으로 사용자를 Microsoft로 전송 되는 원격 분석 데이터의 컬렉션을 사용할지 선택할 수 있습니다. Microsoft가 수집 원격 분석 데이터에 대 한 내용은에서 링크를 통해이 개인정보취급방침 참조 하십시오 합니다 **에 대 한** 측면 패널입니다.

관리자 권한으로 다음 PowerShell cmdlet을 사용 하 여 배포에 대 한 원격 분석 수집 하지 않으려면 선택할 수 있습니다.

   ```PowerShell
    Set-RDWebClientDeploymentSetting -SuppressTelemetry $true
   ```

기본적으로 사용자는 원격 분석을 사용할지 여부를 선택할 수 있습니다. 부울 값을 **$false** 클라이언트의 기본 동작이 일치 합니다. 부울 값을 **$true** 원격 분석을 사용 하지 않도록 설정 하 고 원격 분석 설정에서 사용자를 제한 합니다.

### <a name="remote-resource-launch-method"></a>원격 리소스 launch 메서드
기본적으로 사용자가 브라우저에서 (1) 또는 (2) 해당 컴퓨터에 설치 하는 다른 클라이언트를 사용 하 여 처리 하는.rdp 파일을 다운로드 하 여 원격 리소스를 시작할 수 있습니다. 관리자 권한으로 다음 Powershell 명령 사용 하 여 배포에 원격 리소스 시작 메서드를 제한 하려면 선택할 수 있습니다.

   ```PowerShell
    Set-RDWebClientDeploymentSetting -LaunchResourceInBrowser ($true|$false)
   ```
 기본적으로 사용자 시작 방법 중 하나를 선택할 수 있습니다. 부울 값을 **$true** 브라우저에서 리소스를 시작 하려면 사용자에 게 강제 됩니다. 부울 값을 **$false** .rdp 파일을 로컬에 설치 된 RDP 클라이언트를 사용 하 여 처리를 다운로드 하 여 리소스를 시작 하려면 사용자에 게 강제 됩니다.

### <a name="reset-rdwebclientdeploymentsetting-configurations-to-default"></a>RDWebClientDeploymentSetting 구성을 기본값으로 다시 설정
모든 배포 수준 웹 클라이언트 설정을 기본 구성으로 다시 설정 하려면 다음 PowerShell cmdlet을 실행 합니다.

   ```PowerShell
    Reset-RDWebClientDeploymentSetting 
   ```

## <a name="troubleshooting"></a>문제 해결

웹 클라이언트를 처음 열 때 사용자는 다음 문제 중 하나로 보고서를 하는 경우 다음 섹션에서는 알려줍니다 해결 하려면 어떻게 해야 합니다.

### <a name="what-to-do-if-the-users-browser-shows-a-security-warning-when-they-try-to-access-the-web-client"></a>사용자의 브라우저 웹 클라이언트에 액세스 하려고 할 때 보안 경고를 표시 하는 경우 수행할 작업

RD 웹 액세스 역할을 신뢰할 수 있는 인증서를 사용 하지 않을 수 있습니다. RD 웹 액세스 역할을 공개적으로 신뢰할 수 있는 인증서로 구성 되어 있는지 확인 하십시오.

작동 하지 않는 경우 웹에서 서버 이름을 클라이언트 URL 수 이름과 일치 하지 RD 웹 인증서를 제공한 합니다. URL RD 웹 역할을 호스팅하는 서버의 FQDN을 사용 해야 합니다.

### <a name="what-to-do-if-the-user-cant-connect-to-a-resource-with-the-web-client-even-though-they-can-see-the-items-under-all-resources"></a>사용자에 연결할 수 없으면 리소스를 웹 클라이언트를 사용 하 여 모든 리소스 아래에 있는 항목을 볼 수 있습니다 하는 경우에 수행할 작업

사용자는 나열 된 리소스를 볼 수 있습니다 하는 경우에 웹 클라이언트를 사용 하 여 연결할 수 없습니다는 보고를 하는 경우 다음 작업을 확인 합니다.

* RD 게이트웨이 역할은 제대로 구성 되어 신뢰할 수 있는 공용 인증서를 사용 하도록 있습니까?
* RD 게이트웨이 서버 필수 업데이트가 설치 되어 있습니까? 서버에 있는지 [KB4025334 업데이트](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) 설치 합니다.

사용자가 "예기치 않은 서버 인증 인증서를 받았습니다" 오류가 발생 하는 경우 메시지는 인증서의 지문이 표시 됩니다에 연결 하 려 할 때 메시지입니다. 올바른 인증서를 찾으려면 해당 지문을 사용 하 여 RD 브로커 서버의 인증서 관리자를 검색 합니다. 원격 데스크톱 배포 속성 페이지에서 RD 브로커 역할에 사용할 인증서 구성 되어 있는지 확인 합니다. 있도록 인증서 만료 되지 않았으면, RD 웹 액세스 서버에 인증서를.cer 파일 형식으로 복사 후 인증서의 파일 경로로 대체 대괄호로 묶은 값을 사용 하 여 RD 웹 액세스 서버에서 다음 명령을 실행 합니다.

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### <a name="diagnose-issues-with-the-console-log"></a>콘솔 로그를 사용 하 여 문제 진단

이 문서의 문제 해결 지침에 따라 문제를 해결할 수 없는 경우 콘솔을 시청 하 여 직접 문제의 소스를 진단 하려고 수 브라우저에 로그인 합니다. 웹 클라이언트 문제를 진단 하기 위해 웹 클라이언트를 사용 하는 동안 브라우저 콘솔 로그 작업을 기록 하는 방법을 제공 합니다.

* 오른쪽 위 모서리에서 줄임표를 선택 하 고 이동 합니다 **에 대 한** 드롭다운 메뉴에서 페이지입니다.
* 아래 **지원 정보를 캡처** 선택 합니다 **기록을 시작** 단추.
* 진단 하려는 문제가 생성 되는 웹 클라이언트에서 작업을 수행 합니다.
* 로 이동 합니다 **에 대 한** 선택한 페이지 **녹음 중지**합니다.
* 브라우저 라는.txt 파일을 자동으로 다운로드 됩니다 **RD 콘솔 Logs.txt**합니다. 이 파일에는 대상 문제를 재현 하는 동안 생성 된 전체 콘솔 로그 작업이 포함 됩니다.

콘솔은 브라우저를 통해 직접 액세스할 수도 있습니다. 개발자 도구 콘솔을 일반적으로 있습니다. 예를 들어, Microsoft Edge에 대 한 로그인 키를 눌러 액세스할 수 있습니다 합니다 **F12** 키 또는 줄임표를 선택 하 여로 이동한 후 **도구 더 보기** > **개발자도구**.

## <a name="get-help-with-the-web-client"></a>웹 클라이언트를 사용 하 여 도움말을 보려면

이 문서의 정보를 해결할 수 없는 문제가 발생 한 경우 [전자 메일을 보내거나](mailto:rdwbclnt@microsoft.com) 보고 하도록 합니다. 또한 요청 하거나 새 기능에 투표 하세요 [활짝](https://aka.ms/rdwebfbk)합니다.
