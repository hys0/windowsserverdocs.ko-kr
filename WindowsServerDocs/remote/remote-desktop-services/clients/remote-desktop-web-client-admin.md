---
title: 사용자에 대한 원격 데스크톱 웹 클라이언트 설정
description: 관리자가 원격 데스크톱 웹 클라이언트를 설정하는 방법을 설명합니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: d6761c43eefe04430603a1a16e9e8d256176a736
ms.sourcegitcommit: 25376e261ebd5e85355c298cfd0bbd6b578a6a0c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2019
ms.locfileid: "68729535"
---
# <a name="set-up-the-remote-desktop-web-client-for-your-users"></a>사용자에 대한 원격 데스크톱 웹 클라이언트 설정

원격 데스크톱 웹 클라이언트를 사용하면 사용자가 호환되는 웹 브라우저를 통해 조직의 원격 데스크톱 인프라에 액세스할 수 있습니다. 어디에 있든 로컬 PC와 마찬가지로 원격 앱 또는 데스크톱과 상호 작용할 수 있습니다. 원격 데스크톱 웹 클라이언트를 설정하면 사용자가 시작하는 데 필요한 것은 단지 클라이언트, 자격 증명 및 지원되는 웹 브라우저에 액세스할 수 있는 URL뿐입니다.

>[!IMPORTANT]
>웹 클라이언트는 현재 Azure 애플리케이션 프록시 사용을 지원하지 않으며 웹 애플리케이션 프록시도 전혀 지원하지 않습니다. 자세한 내용은 [애플리케이션 프록시 서비스에서 RDS 사용](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services)을 참조하세요.

## <a name="what-youll-need-to-set-up-the-web-client"></a>웹 클라이언트를 설정하는 데 필요한 사항

시작하기 전에 다음 사항에 유의하세요.

* [원격 데스크톱 배포](../rds-deploy-infrastructure.md)에 Windows Server 2016 또는 2019에서 실행되는 RD 게이트웨이, RD 연결 브로커 및 RD 웹 액세스가 있는지 확인합니다.
* 배포가 장치 단위 라이선스 CAL(클라이언트 액세스 라이선스)이 아니라 [사용자 단위 CAL](../rds-client-access-license.md)로 구성되어 있는지 확인합니다. 그렇지 않으면 모든 라이선스가 사용됩니다.
* RD 게이트웨이에 [Windows 10 KB4025334 업데이트](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334)를 설치합니다. 이 KB(기술 자료)는 나중에 누적 업데이트에 이미 포함되어 있을 수 있습니다.
* 신뢰할 수 있는 공용 인증서가 RD 게이트웨이 및 RD 웹 액세스 역할로 구성되어 있는지 확인합니다.
* 사용자가 연결할 모든 컴퓨터에서 다음 OS 버전 중 하나를 실행하고 있는지 확인합니다.
  * Windows 10
  * Windows Server 2008R2 이상

Windows Server 2016(이상) 및 Windows 10(버전 1611 이상)에 연결하면 성능이 향상됩니다.

>[!IMPORTANT]
>미리 보기 기간 동안 웹 클라이언트를 사용하고 1.0.0 이전 버전을 설치한 경우 새 버전으로 이동하기 전에 먼저 이전 클라이언트를 제거해야 합니다. "웹 클라이언트가 이전 버전의 RDWebClientManagement를 사용하여 설치되었으며, 새 버전을 배포하기 전에 먼저 제거해야 합니다."라는 오류가 표시되면 다음 단계를 수행합니다.
>
>1. 관리자 권한 PowerShell 프롬프트를 엽니다.
>2. **Uninstall-Module RDWebClientManagement**를 실행하여 새 모듈을 제거합니다.
>3. 관리자 권한 PowerShell 프롬프트를 닫고 다시 엽니다.
>4. **Install-Module RDWebClientManagement -RequiredVersion \<이전 버전>을 실행하여 이전 모듈을 설치합니다.**
>5. **Uninstall-RDWebClient**를 실행하여 이전 웹 클라이언트를 제거합니다.
>6. **Uninstall-Module RDWebClientManagement**를 실행하여 이전 모듈을 제거합니다.
>7. 관리자 권한 PowerShell 프롬프트를 닫고 다시 엽니다.
>8. 다음과 같이 일반 설치 단계를 진행합니다.

## <a name="how-to-publish-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트를 게시하는 방법

웹 클라이언트를 처음 설치하려면 다음 단계를 수행합니다.

1. RD 연결 브로커 서버에서 원격 데스크톱 연결에 사용되는 인증서를 가져와서 .cer 파일로 내보냅니다. .cer 파일을 RD 연결 브로커에서 RD 웹 역할을 실행하는 서버로 복사합니다.
2. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 엽니다.
3. Windows Server 2016에서는 받은 편지함 버전이 웹 클라이언트 관리 모듈 설치를 지원하지 않으므로 PowerShellGet 모듈을 업데이트합니다. PowerShellGet을 업데이트하려면 다음 cmdlet을 실행합니다.
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >업데이트가 적용되기 전에 먼저 PowerShell을 다시 시작해야 합니다. 그렇지 않으면 모듈이 작동하지 않을 수 있습니다.

4. 다음 cmdlet을 사용하여 PowerShell 갤러리에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 설치합니다.
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. 그런 다음, 다음 cmdlet을 실행하여 최신 버전의 원격 데스크톱 웹 클라이언트를 다운로드합니다.
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. 다음으로, 아래의 cmdlet에서 괄호로 묶은 값을 RD 브로커에서 복사한 .cer 파일의 경로로 바꾼 후에 해당 cmdlet을 실행합니다.
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. 마지막으로, 다음 cmdlet을 실행하여 원격 데스크톱 웹 클라이언트를 게시합니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    <https://server_FQDN/RDWeb/webclient/index.html> 형식의 서버 이름을 사용하여 웹 클라이언트 URL에서 웹 클라이언트에 액세스할 수 있는지 확인합니다. URL(일반적으로 서버 FQDN)에서 RD 웹 액세스 공용 인증서와 일치하는 서버 이름을 사용하는 것이 중요합니다.

    >[!NOTE]
    >**Publish-RDWebClientPackage** cmdlet을 실행하면 배포가 사용자 단위 CAL로 구성된 경우에도 장치 단위 CAL이 지원되지 않는다는 경고가 표시될 수 있습니다. 배포에서 사용자 단위 CAL을 사용하는 경우 이 경고는 무시할 수 있습니다. 이는 구성 제한 사항을 알고 있는지 확인하기 위해 표시됩니다.
8. 사용자가 웹 클라이언트에 액세스할 준비가 되면 사용자에게 만든 웹 클라이언트 URL을 보내기만 하면 됩니다.

>[!NOTE]
>RDWebClientManagement 모듈에 지원되는 모든 cmdlet의 목록을 보려면 PowerShell에서 다음 cmdlet을 실행하세요.
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## <a name="how-to-update-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트를 업데이트하는 방법

새 버전의 원격 데스크톱 웹 클라이언트를 사용할 수 있으면 다음 단계에 따라 새 클라이언트를 사용하여 배포를 업데이트합니다.

1. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 열고, 다음 cmdlet을 실행하여 사용 가능한 최신 버전의 웹 클라이언트를 다운로드합니다.
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. 필요에 따라 다음 cmdlet을 실행하여 공식 릴리스 전에 테스트할 클라이언트를 게시할 수 있습니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    클라이언트가 웹 클라이언트 URL에 해당하는 테스트 URL(예: <https://server_FQDN/RDWeb/webclient-test/index.html>)에 표시됩니다.
3. 다음 cmdlet을 실행하여 사용자에 대한 클라이언트를 게시합니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    이 경우 웹 페이지를 다시 시작하면 모든 사용자에 대한 클라이언트가 바뀝니다.

## <a name="how-to-uninstall-the-remote-desktop-web-client"></a>원격 데스크톱 웹 클라이언트를 제거하는 방법

웹 클라이언트의 모든 흔적을 제거하려면 다음 단계를 수행합니다.

1. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 엽니다.
2. 테스트 및 프로덕션 클라이언트의 게시를 취소하고, 모든 로컬 패키지를 제거하고, 웹 클라이언트 설정을 제거합니다.

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 제거합니다.

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## <a name="how-to-install-the-remote-desktop-web-client-without-an-internet-connection"></a>인터넷 연결이 없는 원격 데스크톱 웹 클라이언트를 설치하는 방법

다음 단계에 따라 웹 클라이언트를 인터넷에 연결되지 않는 RD 웹 액세스 서버에 배포합니다.

> [!NOTE]
> 인터넷 연결이 없는 설치는 RDWebClientManagement PowerShell 모듈의 버전 1.0.1 이상에서 사용할 수 있습니다.

> [!NOTE]
> 필요한 파일을 오프라인 서버에 전송하기 전에 해당 파일을 다운로드하려면 여전히 인터넷에 액세스할 수 있는 관리 PC가 필요합니다.

> [!NOTE]
> 최종 사용자 PC에는 당분간 인터넷 연결이 필요합니다. 이 문제는 완전한 오프라인 시나리오를 제공하는 클라이언트의 향후 릴리스에서 해결될 예정입니다.

### <a name="from-a-device-with-internet-access"></a>인터넷에 액세스할 수 있는 디바이스에서

1. PowerShell 프롬프트를 엽니다.

2. PowerShell 갤러리에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 가져옵니다.
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. 다른 디바이스에 설치할 최신 버전의 원격 데스크톱 웹 클라이언트를 다운로드합니다.
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. 최신 버전의 RDWebClientManagement PowerShell 모듈을 다운로드합니다.
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. "C:\WebClient\"의 콘텐츠를 RD 웹 액세스 서버에 복사합니다.

### <a name="from-the-rd-web-access-server"></a>RD 웹 액세스 서버에서

[원격 데스크톱 웹 클라이언트를 게시하는 방법](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client)의 지침에 따라 4단계와 5단계를 다음 단계로 바꿉니다.

4. 로컬 폴더에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 가져옵니다.
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. 로컬 폴더에서 최신 버전의 원격 데스크톱 웹 클라이언트를 배포합니다(해당 zip 파일로 바꿈).
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## <a name="connecting-to-rd-broker-without-rd-gateway-in-windows-server-2019"></a>Windows Server 2019에서 RD 게이트웨이가 없는 RD 브로커에 연결
이 섹션에서는 Windows Server 2019에서 RD 게이트웨이가 없는 RD 브로커에 대한 웹 클라이언트 연결을 설정하는 방법에 대해 설명합니다.

### <a name="setting-up-the-rd-broker-server"></a>RD 브로커 서버 설정

#### <a name="follow-these-steps-if-there-is-no-certificate-bound-to-the-rd-broker-server"></a>RD 브로커 서버에 바인딩된 인증서가 없는 경우 다음 단계를 수행합니다.

1. **서버 관리자** > **원격 데스크톱 서비스**를 엽니다.

2. **배포 개요** 섹션에서 **작업** 드롭다운 메뉴를 선택합니다.

3. **배포 속성 편집**을 선택합니다. **배포 속성**이라는 새 창이 열립니다.

4. **배포 속성** 창의 왼쪽 메뉴에서 **인증서**를 선택합니다.

5. [인증서 수준] 목록에서 **RD 연결 브로커 - Single Sign On 사용**을 선택합니다. 두 가지 옵션으로 (1) 새 인증서 만들기 또는 (2) 기존 인증서가 있습니다.

#### <a name="follow-these-steps-if-there-is-a-certificate-previously-bound-to-the-rd-broker-server"></a>이전에 RD 브로커 서버에 바인딩된 인증서가 있는 경우 다음 단계를 수행합니다.

1. 브로커에 바인딩된 인증서를 열고, **지문** 값을 복사합니다.

2. 이 인증서를 3392 보안 포트에 바인딩하려면 관리자 권한 PowerShell 창을 열고, 다음 명령을 실행하여 **"< thumbprint >"** 를 이전 단계에서 복사한 값으로 바꿉니다.

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 인증서가 올바르게 바인딩되었는지 확인하려면 다음 명령을 실행하세요.
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 인증서 바인딩 목록에서 올바른 인증서가 3392 포트에 바인딩되어 있는지 확인합니다.

3. Windows 레지스트리(regedit)를 열고, ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp```로 이동하고, **WebSocketURI** 키를 찾습니다. 값은 <strong>https://+:3392/rdp/</strong>로 설정해야 합니다.

### <a name="setting-up-the-rd-session-host"></a>RD 세션 호스트 설정
RD 세션 호스트 서버가 RD 브로커 서버와 다른 경우 다음 단계를 수행합니다.

1. RD 세션 호스트 머신에 대한 인증서를 만들고, 이를 열고, **지문** 값을 복사합니다.

2. 이 인증서를 3392 보안 포트에 바인딩하려면 관리자 권한 PowerShell 창을 열고, 다음 명령을 실행하여 **"< thumbprint >"** 를 이전 단계에서 복사한 값으로 바꿉니다.

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 인증서가 올바르게 바인딩되었는지 확인하려면 다음 명령을 실행하세요.
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 인증서 바인딩 목록에서 올바른 인증서가 3392 포트에 바인딩되어 있는지 확인합니다.

3. Windows 레지스트리(regedit)를 열고, ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp```로 이동하고, **WebSocketURI** 키를 찾습니다. 값은 <https://+:3392/rdp/>로 설정해야 합니다.

### <a name="general-observations"></a>일반 관찰

* RD 세션 호스트와 RD 브로커 서버에서 모두 Windows Server 2019를 실행하고 있는지 확인합니다.

* 해당 신뢰할 수 있는 공용 인증서가 RD 세션 호스트 및 RD 브로커 서버 모두로 구성되어 있는지 확인합니다.
    > [!NOTE]
    > RD 세션 호스트와 RD 브로커 서버에서 모두 동일한 머신을 공유하는 경우 RD 브로커 서버 인증서만 설정합니다. RD 세션 호스트와 RD 브로커 서버가 서로 다른 머신을 사용하는 경우 두 가지 모두 고유한 인증서로 구성해야 합니다.

* 각 인증서에 대한 **SAN(주체 대체 이름)** 은 머신의 **FQDN(정규화된 도메인 이름)** 으로 설정해야 합니다. **CN(일반 이름)** 은 각 인증서의 SAN과 일치해야 합니다.

## <a name="how-to-pre-configure-settings-for-remote-desktop-web-client-users"></a>원격 데스크톱 웹 클라이언트 사용자에 대한 설정을 미리 구성하는 방법
이 섹션에서는 PowerShell을 사용하여 원격 데스크톱 웹 클라이언트 배포에 대한 설정을 구성하는 방법에 대해 설명합니다. 이러한 PowerShell cmdlet은 조직의 보안 고려 사항 또는 의도된 워크플로에 따라 설정을 변경하는 사용자의 기능을 제어합니다. 웹 클라이언트의 **설정** 사이드 패널에 있는 모든 설정은 다음과 같습니다.

### <a name="suppress-telemetry"></a>원격 분석 표시 안 함
기본적으로 사용자는 Microsoft에 보내는 원격 분석 데이터 수집을 사용하거나 사용하지 않도록 선택할 수 있습니다. Microsoft에서 수집하는 원격 분석 데이터에 대한 자세한 내용은 **정보** 사이드 패널의 링크를 통해 개인정보처리방침을 참조하세요.

관리자는 다음 PowerShell cmdlet을 사용하여 배포에 대한 원격 분석 수집을 표시하지 않도록 선택할 수 있습니다.

   ```PowerShell
    Set-RDWebClientDeploymentSetting -Name "SuppressTelemetry" $true
   ```

기본적으로 사용자는 원격 분석을 사용하거나 사용하지 않도록 선택할 수 있습니다. **$false** 부울 값은 기본 클라이언트 동작과 일치합니다. **$true** 부울 값은 원격 분석을 사용하지 않도록 설정하고 사용자가 원격 분석 사용을 설정하도록 제한합니다.

### <a name="remote-resource-launch-method"></a>원격 리소스 시작 방법
기본적으로 사용자는 (1) 브라우저에서 원격 리소스를 시작하거나 (2) 머신에 설치된 다른 클라이언트에서 처리할 .rdp 파일을 다운로드하여 원격 리소스를 시작하도록 선택할 수 있습니다. 관리자는 다음 Powershell 명령을 사용하여 배포에 대한 원격 리소스 시작 방법을 제한하도록 선택할 수 있습니다.

   ```PowerShell
    Set-RDWebClientDeploymentSetting -Name "LaunchResourceInBrowser" ($true|$false)
   ```
 기본적으로 사용자는 두 가지 시작 방법 중 하나를 선택할 수 있습니다. **$true** 부울 값은 사용자가 브라우저에서 리소스를 시작하도록 합니다. **$false** 부울 값은 사용자가 로컬로 설치된 RDP 클라이언트에서 처리할 .rdp 파일을 다운로드하여 리소스를 시작하도록 강제 적용합니다.

### <a name="reset-rdwebclientdeploymentsetting-configurations-to-default"></a>RDWebClientDeploymentSetting 구성을 기본값으로 다시 설정
배포 수준 웹 클라이언트 설정을 기본 구성으로 다시 설정하려면 다음 PowerShell cmdlet을 실행하고, --Name 매개 변수를 사용하여 재설정할 설정을 지정합니다.
  
  ```PowerShell
    Reset-RDWebClientDeploymentSetting -Name "LaunchResourceInBrowser"
    Reset-RDWebClientDeploymentSetting -Name "SuppressTelemetry"
   ```

## <a name="troubleshooting"></a>문제 해결

다음 섹션에서는 사용자가 웹 클라이언트를 처음 열 때 다음 문제 중 하나가 보고되는 경우 해당 문제를 해결하기 위해 수행해야 하는 작업을 알려줍니다.

### <a name="what-to-do-if-the-users-browser-shows-a-security-warning-when-they-try-to-access-the-web-client"></a>웹 클라이언트에 액세스하려고 할 때 사용자의 브라우저에 보안 경고가 표시되는 경우 수행해야 하는 작업

RD 웹 액세스 역할에서 신뢰할 수 있는 인증서를 사용하고 있지 않을 수 있습니다. RD 웹 액세스 역할이 공개적으로 신뢰할 수 있는 인증서로 구성되어 있는지 확인합니다.

그래도 작동하지 않으면 웹 클라이언트 URL의 서버 이름이 RD 웹 인증서에서 제공된 이름과 일치하지 않을 수 있습니다. URL이 RD 웹 역할을 호스팅하는 서버의 FQDN을 사용하는지 확인합니다.

### <a name="what-to-do-if-the-user-cant-connect-to-a-resource-with-the-web-client-even-though-they-can-see-the-items-under-all-resources"></a>[모든 리소스] 아래에서 항목을 볼 수 있지만 사용자가 웹 클라이언트를 통해 리소스에 연결할 수 없는 경우 수행해야 하는 작업

사용자가 나열된 리소스를 볼 수 있지만 웹 클라이언트에 연결할 수 없다고 보고하는 경우 다음 사항을 확인합니다.

* RD 게이트웨이 역할이 신뢰할 수 있는 공용 인증서를 사용하도록 제대로 구성되어 있나요?
* RD 게이트웨이 서버에 필요한 업데이트가 설치되어 있나요? 서버에는 [KB4025334 업데이트](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334)가 설치되어 있어야 합니다.

사용자가 연결하려고 할 때 "예기치 않은 서버 인증 인증서를 받았습니다" 오류 메시지가 표시되면 이 메시지에서 인증서의 지문을 표시합니다. 올바른 인증서를 찾기 위해 해당 지문을 사용하여 RD 브로커 서버의 인증서 관리자를 검색합니다. 인증서를 원격 데스크톱 배포 속성 페이지의 RD 브로커 역할에 사용하도록 구성되어 있는지 확인합니다. 인증서가 만료되지 않았는지 확인한 후, .cer 파일 형식의 인증서를 RD 웹 액세스 서버에 복사하고, 다음 명령에서 괄호로 묶은 값을 인증서의 파일 경로로 바꾼 후에 해당 명령을 RD 웹 액세스 서버에서 실행합니다.

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### <a name="diagnose-issues-with-the-console-log"></a>콘솔 로그를 사용하여 문제 진단

이 문서의 문제 해결 지침에 따라 문제를 해결할 수 없는 경우 브라우저에서 콘솔 로그를 확인하여 문제의 원인을 직접 진단할 수 있습니다. 웹 클라이언트는 웹 클라이언트를 사용하면서 문제를 진단하는 데 도움이 되는 브라우저 콘솔 로그 활동을 기록하는 방법을 제공합니다.

* 오른쪽 위 모서리에서 줄임표를 선택하고, 드롭다운 메뉴의 **정보** 페이지로 이동합니다.
* **지원 정보 캡처** 아래에서 **기록 시작** 단추를 선택합니다.
* 진단하려는 문제를 생성한 웹 클라이언트에서 작업을 수행합니다.
* **정보** 페이지로 이동하고, **기록 중지**를 선택합니다.
* 브라우저에서 **RD Console Logs.txt**라는 .txt 파일을 자동으로 다운로드합니다. 이 파일에는 대상 문제를 재현하는 동안 생성된 콘솔 로그 활동이 모두 포함됩니다.

또한 콘솔은 브라우저를 통해 직접 액세스할 수도 있습니다. 콘솔은 일반적으로 개발자 도구 아래에 있습니다. 예를 들어 **F12** 키를 누르거나 줄임표를 선택한 다음, **기타 도구** > **개발자 도구**로 이동하여 Microsoft Edge의 로그에 액세스할 수 있습니다.

## <a name="get-help-with-the-web-client"></a>웹 클라이언트에 대한 도움 받기

이 문서의 정보로 해결할 수 없는 이슈가 발생하면 [기술 커뮤니티](https://aka.ms/wvdtc)에서 이슈를 보고할 수 있습니다. 또한 [제안 상자](https://remotedesktop.uservoice.com/forums/911494-remote-desktop-web-client)에서 새로운 기능을 요청하거나 투표할 수 있습니다.
