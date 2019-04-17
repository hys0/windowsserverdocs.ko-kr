---
title: 사용자에 대한 원격 데스크톱 웹 클라이언트 설정
description: 관리자는 원격 데스크톱 웹 클라이언트를 설정할 수는 방법을 설명 합니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 2cb819a7f91646c61b84c3ee70550af6033ba340
ms.sourcegitcommit: 491c94b25501732c4a4abda533cc62b8bd278ed2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/22/2019
ms.locfileid: "9099186"
---
# 사용자에 대한 원격 데스크톱 웹 클라이언트 설정

원격 데스크톱 웹 클라이언트 호환 웹 브라우저를 통해 조직의 원격 데스크톱 인프라에 액세스할 수 있도록 합니다. 원격 앱 이나 데스크톱 현재 위치에 관계 없이 로컬 PC와 것 처럼 상호 작용할 수 있습니다. 원격 데스크톱 웹 클라이언트 설정 되 면 사용자가 시작 하기 위해 필요한 모든은 URL 클라이언트, 자격 증명 및 지원 되는 웹 브라우저 액세스할 수 있습니다.

>[!IMPORTANT]
>웹 클라이언트 Azure 응용 프로그램 프록시를 사용 하 여 현재 지원 하지 않으므로 및 웹 응용 프로그램 프록시를 전혀 지원 하지 않습니다. 자세한 내용은 [응용 프로그램 프록시 서비스를 사용 하 여 RDS](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services) 를 참조 하세요.

## 웹 클라이언트 설정 해야

시작 하기 전에 다음 사항을 염두에서에 유의 하십시오.

* [원격 데스크톱 배포](../rds-deploy-infrastructure.md) 에 RD 게이트웨이, RD 연결 브로커 및 RD 웹 액세스 2019 또는 Windows Server 2016에서 실행 되 고 있는지 확인 합니다.
* 장치별, 그렇지 않으면 모든 라이선스를 사용 하는 대신 [사용자 당 클라이언트 액세스 라이선스](../rds-client-access-license.md) (Cal)에 대 한 배포 구성 되어 있는지 확인 합니다.
* RD 게이트웨이에 [Windows 10 KB4025334 업데이트](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) 를 설치 합니다. 누적 업데이트 나중에 이미이 KB 포함 된 될 수 있습니다.
* RD 웹 액세스 및 RD 게이트웨이 역할에 대 한 공용 신뢰할 수 있는 인증서 구성 되어 있는지 확인 합니다.
* 사용자가 연결할 컴퓨터 다음 운영 체제 버전 중 하나를 실행 하 고 있는지 확인 합니다.
  * Windows 10
  * Windows Server 2008R2 이상

사용자에 게 더 나은 성능 연결 Windows Server 2016 (이상) 및 Windows 10 (버전 1611 이상)에 표시 됩니다.

>[!IMPORTANT]
>미리 보기 기간 동안 웹 클라이언트를 사용 하 고 버전 1.0.0 이전 설치 하는 경우에 새 버전으로 이동 하기 전에 먼저 이전 클라이언트를 제거 해야 합니다. "웹 클라이언트 RDWebClientManagement의 이전 버전을 사용 하 여 설치 된 및 새 버전을 배포 하기 전에 먼저 제거 해야 합니다." 라고 표시 되는 오류를 수신 하는 경우 다음이 단계를 따르세요.
>
>1. 관리자 권한 PowerShell 프롬프트를 엽니다.
>2. 새 모듈을 제거 하려면 **제거 모듈 RDWebClientManagement** 실행 합니다.
>3. 관리자 권한 PowerShell 프롬프트를 닫고 설정 합니다.
>4. 실행 **이전 모듈을 설치 하려면 설치 모듈 RDWebClientManagement-RequiredVersion \<old version>.**
>5. 이전 웹 client 제거 **RDWebClient 제거** 실행 합니다.
>6. 기존 모듈을 제거 하려면 **제거 모듈 RDWebClientManagement** 실행 합니다.
>7. 관리자 권한 PowerShell 프롬프트를 닫고 설정 합니다.
>8. 다음과 같이 일반 설치 단계를 진행 합니다.

## 원격 데스크톱 웹 클라이언트를 게시 하는 방법

처음으로 웹 클라이언트를 설치 하려면 다음이 단계를 따르세요.

1. RD 연결 브로커 서버에서 원격 데스크톱 연결에 사용 된 인증서를 가져와서.cer 파일로 내보냅니다. RD 연결 브로커에서 RD 웹 역할을 실행 하는 서버를.cer 파일을 복사 합니다.
2. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 엽니다.
3. Windows Server 2016에서 받은 편지함 버전 웹 클라이언트 관리 모듈을 설치를 지원 하지 않으므로 PowerShellGet 모듈을 업데이트 합니다. PowerShellGet을 업데이트 하려면 다음 cmdlet을 실행 합니다.
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >업데이트를 적용 하려면, 그렇지 않으면 모듈 작동 하지 않을 수 전에 PowerShell을 다시 시작 해야 합니다.

4. 이 cmdlet 사용 하 여 PowerShell 갤러리에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 설치 합니다.
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. 그런 다음 원격 데스크톱 웹 클라이언트의 최신 버전을 다운로드 하려면 다음 cmdlet을 실행 합니다.
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. 괄호로 값으로 대체 RD 브로커에서 복사한.cer 파일의 경로 사용 하 여이 cmdlet을 실행 합니다.
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. 마지막으로, 원격 데스크톱 웹 클라이언트를 게시 하려면이 cmdlet을 실행 합니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    형식으로, 서버 이름을 사용 하 여 웹 클라이언트 웹 클라이언트 URL에 액세스할 수 있도록 <https://server_FQDN/RDWeb/webclient/index.html>. URL (일반적으로 서버 FQDN)에 RD 웹 액세스 공용 인증서와 일치 하는 서버 이름을 사용을 고려해 야 합니다.

    >[!NOTE]
    >**게시 RDWebClientPackage** cmdlet을 실행할 때 볼 수 있습니다 장치별 Cal 이라는 경고 지원 되지 않으며, 사용자 당 Cal에 대 한 배포에 구성 된 경우에. 배포 사용자별 Cal을 사용 하는 경우이 경고를 무시할 수 있습니다. 구성 제한 인식 되도록 표시 됩니다.
8. 웹 클라이언트에 액세스 하는 사용자에 대 한 준비가 되 면 사람에 게 보냅니다 만든 웹 클라이언트 URL.

>[!NOTE]
>RDWebClientManagement 모듈에 대 한 지원 되는 모든 cmdlet의 목록을 보려면 PowerShell에서 다음 cmdlet을 실행 합니다.
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## 원격 데스크톱 웹 클라이언트를 업데이트 하는 방법

새 버전의 원격 데스크톱 웹 클라이언트를 사용할 수 있는 새 클라이언트를 사용 하 여 배포를 업데이트 하려면 다음이 단계를 따르세요.

1. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 열고 웹 클라이언트의 가능한 최신 버전을 다운로드 하려면 다음 cmdlet을 실행 합니다.
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. 필요에 따라이 cmdlet을 실행 하 여 공식 출시 하기 전에 테스트를 위해 클라이언트를 게시할 수 있습니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    클라이언트 웹 클라이언트 URL에 해당 하는 테스트 URL에 표시 되어야 합니다 (예를 들어 <https://server_FQDN/RDWeb/webclient-test/index.html>).
3. 다음 cmdlet을 실행 하 여 사용자에 대 한 클라이언트를 게시 합니다.
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    이렇게 하면 웹 페이지를 다시 때 모든 사용자에 대 한 클라이언트를 바뀝니다.

## 원격 데스크톱 웹 클라이언트를 제거 하는 방법

웹 클라이언트의 모든 추적 정보를 제거 하려면 다음이 단계를 따르세요.

1. RD 웹 액세스 서버에서 관리자 권한 PowerShell 프롬프트를 엽니다.
2. 테스트 및 프로덕션 클라이언트 게시 취소, 모든 로컬 패키지를 제거 하 고 웹 클라이언트 설정을 제거 합니다.

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 제거 합니다.

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## 인터넷 연결 없이 원격 데스크톱 웹 클라이언트를 설치 하는 방법

인터넷 연결이 없는 RD 웹 액세스 서버에 웹 클라이언트를 배포 하려면 다음이 단계를 따릅니다.

> [!NOTE]
> 인터넷 연결을 1.0.1 버전에서 이상 사용할 수 없는 설치 RDWebClientManagement PowerShell 모듈입니다.

> [!NOTE]
> 오프 라인 서버에 전송 하기 전에 필요한 파일을 다운로드 하려면 인터넷 액세스 권한이 있는 관리자 PC를 보내야 합니다.

> [!NOTE]
> 최종 사용자 PC 지금은 인터넷 연결이 필요합니다. 이 전체 오프 라인 시나리오를 제공 하는 클라이언트의 이후 릴리스에서 해결 될 것입니다.

### 인터넷 액세스를 사용 하 여 장치에서

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

5. RD 웹 액세스 서버에 "C:\WebClient\"의 콘텐츠를 복사 합니다.

### RD 웹 액세스 서버에서

[원격 데스크톱 웹 클라이언트를 게시 하는 방법](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client), 4, 5 단계를 다음으로 교체 지침을 따릅니다.

4. 로컬 폴더에서 원격 데스크톱 웹 클라이언트 관리 PowerShell 모듈을 가져옵니다.
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. 로컬 폴더 (적절 한 zip 파일을 사용 하 여 바꾸기)에서 원격 데스크톱 웹 클라이언트의 최신 버전을 배포 합니다.
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## Windows Server 2019에서에서 RD 게이트웨이 없이 RD 브로커에 연결
이 섹션에서는 Windows Server 2019에서 RD 게이트웨이 없이 RD 브로커는 웹 클라이언트 연결을 사용 하는 방법을 설명 합니다.

### RD 브로커 서버 설정

#### 인증서가 없기 RD 브로커 서버에 연결 하는 경우 다음이 단계를 수행 합니다.

1. **서버 관리자**를 열고 > **원격 데스크톱 서비스**.

2. **배포 개요** 섹션에서는 **작업** 드롭다운 메뉴를 선택 합니다.

3. 선택 **배포 속성 편집**, **배포 속성** 이라는 새 창이 열립니다.

4. **배포 속성** 창에서 왼쪽된 메뉴에서 **인증서** 를 선택 합니다.

5. 인증서 수준 목록에서 **사용 하도록 설정 Single Sign On RD 연결 브로커-** 를 선택 합니다. 두 가지 옵션이 있습니다: (1) 새 인증서 또는 만들 (2) 기존 인증서.

#### 이전에 바인딩된 RD 브로커 서버에 인증서가 하는 경우 다음이 단계를 수행 합니다.

1. Open 인증서 브로커 및 복사 **손도장** 값에 바인딩됩니다.

2. 이 인증서 보안 포트 3392 바인딩할 관리자 권한 PowerShell 창을 열고 **"< 지문 gt_"** 이전 단계에서 복사한 값으로 대체 하 고 다음 명령을 실행 합니다.

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 인증서가 올바르게 연결 하는 경우를 확인 하려면 다음 명령을 실행 합니다.
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 인증서 바인딩 목록에서 올바른 인증서를 포트 3392에 바인딩되어 있는지 확인 합니다.

3. Windows 레지스트리 (regedit) 및 nagivate를 열고 ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` **WebSocketURI**키를 찾습니다. 값으로 설정 되어 있어야 **https://+:3392/rdp/**.

### RD 세션 호스트 설정
RD 세션 호스트 서버는 RD 브로커 서버와에서 다른 경우 다음이 단계를 따르세요.

1. RD 세션 호스트 컴퓨터에 대 한 인증서를 만들고, 열고 **지문** 값을 복사 합니다.

2. 이 인증서 보안 포트 3392 바인딩할 관리자 권한 PowerShell 창을 열고 **"< 지문 gt_"** 이전 단계에서 복사한 값으로 대체 하 고 다음 명령을 실행 합니다.

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 인증서가 올바르게 연결 하는 경우를 확인 하려면 다음 명령을 실행 합니다.
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 인증서 바인딩 목록에서 올바른 인증서를 포트 3392에 바인딩되어 있는지 확인 합니다.

3. Windows 레지스트리 (regedit) 및 nagivate를 열고 ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` **WebSocketURI**키를 찾습니다. 값으로 설정 되어 있어야 **https://+:3392/rdp/**.

### 일반적인

* RD 세션 호스트와 RD 브로커 서버 Windows Server 2019 실행 되 고 있는지 확인 합니다.

* 해당 공용 RD 세션 호스트와 RD 브로커 서버에 대 한 인증서를 구성 하는 신뢰할 수 있는 확인 합니다.
    > [!NOTE]
    > RD 세션 호스트와 RD 브로커 서버 모두 동일한 컴퓨터를 공유 하는 경우 RD 브로커 서버 인증서를 설정 합니다. RD 세션 호스트 및 RD 브로커 서버 서로 다른 컴퓨터를 사용 하는 경우 둘 다 고유한 인증서를 사용 하 여 구성 해야 합니다.

* **주체 대체 이름 (SAN)** 각 인증서에 대 한 컴퓨터의 **정규화 된 도메인 이름 (FQDN)** 으로 설정 되어 있어야 합니다. **CN (일반 이름)** 에 각 인증서에 대 한 SAN 일치 해야 합니다.

## 문제 해결

웹 클라이언트를 처음 열 때 사용자는 다음 문제 중 하나로 보고, 하는 경우 다음 섹션에서는 알려 문제 해결에 수행할 작업입니다.

### 사용자의 브라우저 웹 클라이언트에 액세스 하려고 할 때 보안 경고를 표시 하는 경우 수행할 작업

RD 웹 액세스 역할 신뢰할 수 있는 인증서를 사용 하지 수도 있습니다. RD 웹 액세스 역할 공개적으로 신뢰할 수 있는 인증서로 구성 되어 있는지 확인 합니다.

작동 하지 않으면 웹에서 서버 이름을 클라이언트 URL 일치 하지 않을 RD 웹 인증서가 제공한 이름. RD 웹 역할을 호스팅하는 서버의 FQDN을 사용 하 여 URL 있는지 확인 합니다.

### 사용자가 연결할 수 없는 리소스에 웹 클라이언트를 사용 하 여 모든 리소스에서 항목을 볼 수 있지만 경우 수행할 작업

사용자 나열 된 리소스를 볼 수 있지만 웹 클라이언트와 연결할 수 없는 데이터를 보고 하는 경우 다음과 같은 작업을 확인 합니다.

* RD 게이트웨이 역할은 제대로 사용 하도록 구성 된 신뢰할 수 있는 공용 인증서?
* RD 게이트웨이 서버 필수 업데이트가 설치 되어 있습니까? 서버 [는 KB4025334 업데이트](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334) 설치에 있는지 확인 합니다.

사용자 가져옵니다 "예기치 않은 서버 인증 인증서를 수신 된" 오류 메시지는 인증서의 지문을 표시 한 다음에 연결 하 려 할 때 메시지입니다. RD 브로커 서버 인증서 관리자가 해당 지문을 사용 하 여 올바른 인증서를 찾을 수를 검색 합니다. 원격 데스크톱 배포 속성 페이지에서 RD 브로커 역할에 사용할 인증서 구성 되어 있는지 확인 합니다. 인증서 했는지 되지 않은 경우 만료 되 면.cer 파일 형식에 RD 웹 액세스 서버에 인증서를 복사 하 고 인증서의 파일 경로 교체 괄호로 값과 RD 웹 액세스 서버에서 다음 명령을 실행:

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### 콘솔 로그를 사용 하 여 문제를 진단

콘솔을 시청 하 여 문제의 원인을 직접를 진단 하려면 시도할 수 문제 해결이 문서의 다음 지침에 따라 문제를 해결할 수 없는 경우 브라우저에 로그인 합니다. 웹 클라이언트 웹 클라이언트 문제를 진단 하는 데 사용 하는 동안 브라우저 콘솔 로그 활동을 기록 하는 방법을 제공 합니다.

* 오른쪽 위 모서리에 있는 줄임표를 선택 하 고 드롭다운 메뉴에서 **에 대 한** 페이지로 이동 합니다.
* **캡처 지원 정보** 에서 **녹음/녹화 시작** 단추를 선택 합니다.
* 진단 하려는 문제를 생성 하는 웹 클라이언트의 줄여 작업을 수행 합니다.
* **에 대 한** 페이지를 찾아서 **기록 중지**를 선택 합니다.
* 브라우저 **RD 콘솔 Logs.txt**.txt 파일을 자동으로 다운로드 됩니다. 이 파일에는 대상 문제를 재현 하는 동안 발생 하는 전체 콘솔 로그 활동을 포함 됩니다.

콘솔은 브라우저를 통해 직접 액세스할 수도 있습니다. 콘솔은 일반적으로 개발자 도구 있습니다. **F12** 키를 눌러 또는 줄임표를 선택한 다음 **더 많은 도구**를 탐색 하 여 Microsoft Edge에서 로그에 액세스할 수는 예를 들어 > **개발자 도구**입니다.

## 웹 클라이언트 도움말 보기

이 문서의 정보 해결할 수 없는 되는 문제를 경험한, [전자 메일 보내기](mailto:rdwbclnt@microsoft.com) 를 보고할 수 있습니다. 요청 하거나 우리의 [제안 상자](https://aka.ms/rdwebfbk)에 새로운 기능에 대 한 응답 수도 있습니다.