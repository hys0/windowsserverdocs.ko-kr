---
title: 소프트웨어 인벤토리 로깅 집계
description: 소프트웨어 인벤토리 로깅 집계를 설치 하 고 관리 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4230a75-6bcd-47d9-ba92-a052a90a6abc
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81dbfb89d2e72af57c070db8473fd3b0e521906c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382943"
---
# <a name="software-inventory-logging-aggregator"></a>소프트웨어 인벤토리 로깅 집계

>적용 대상: Windows Server 2012 R2

## <a name="what-is-software-inventory-logging-aggregator"></a>소프트웨어 인벤토리 로깅 집계 란?
SILA(Software Inventory Logging Aggregator)는 데이터 센터의 Windows Server에 설치된 Microsoft 엔터프라이즈 소프트웨어의 개수와 유형에 대한 기본 보고서를 수신, 집계, 생성합니다.

SILA는 Windows Server에 설치하지만 Windows Server 설치에 포함되지 않는 소프트웨어입니다. 소프트웨어를 설치 하려면 먼저 Windows 다운로드 센터에서 무료로 다운로드 하세요. [Windows Server 용 소프트웨어 인벤토리 로깅 집계 1.0](https://www.microsoft.com/en-us/download/details.aspx?id=49046)

소프트웨어 인벤토리 로깅 프레임워크의 목적은 IT 환경 내의 많은 서버를 통해 배포되는 Microsoft 소프트웨어의 인벤토리 작성과 관련한 운영 비용을 절감하는 데 있습니다. 이 프레임 워크는이 SIL 집계 및 windows server 기능 (SIL (소프트웨어 인벤토리 로깅) 2012에 도입 된 Windows Server 기능)의 두 구성 요소로 구성 되어 있습니다. 이 Software Inventory Logging Aggregator 1.0은 단일 서버에 설치되며, SIL을 통해 데이터를 전달하도록 구성된 모든 Windows Server에서 인벤토리 데이터를 받습니다. 데이터 센터 관리자가 마스터 Windows Server 이미지의 SIL을 사용하여 환경에서 광범위하게 배포할 수 있도록 설계되었습니다.  이 소프트웨어 패키지는 대상 지점이며, 고객이 시간에 따른 쉬운 인벤토리 데이터 로깅을 위해 사내에 설치하도록 고안되었습니다. 또한 이 소프트웨어를 사용하면 Microsoft Excel에서 기본 인벤토리 보고서를 정기적으로 만들 수 있습니다. Software Inventory Logging Aggregator 1.0 보고서에는 Windows Server, System Center 및 SQL Server의 설치 수가 포함되어 있습니다.

> [!IMPORTANT]
> 이 소프트웨어를 사용하는 동안 데이터가 Microsoft로 전송되지 않습니다.

### <a name="data-sil-collects-over-time"></a>시간의 경과에 따라 SIL에서 수집하는 데이터
올바르게 배포한 경우 SIL Aggregator에서 다음과 같은 데이터를 확인할 수 있습니다.

-   데이터 센터의 고유한 Windows Server 설치

-   FQDN

-   GUID 식별

-   실제 프로세서 및 코어 수

-   가상 프로세서 수(VM인 경우)

-   실제 프로세서의 모델 및 유형

-   실제 프로세서에서 하이퍼 스레딩을 사용하는지 여부

-   섀시 일련 번호

-   각 호스트에서 동시에 실행 중인 Windows Server VM(호스트에서 하이퍼바이저를 실행 중인 경우)의 시간에 따른 최고 수위 표시 수 및 ID

-   동시에 실행 중인 관리 되는 \(System Center 에이전트의 최고 수 위 표시 수 및 호스트 이름, 시간에 따른 각 호스트에서 Windows Server vm 제공\)

-   관리 되는 상위\-워터 마크에서 계산 되는 vm에 설치 된 System Center 에이전트의 이름

-   라이선스를 필요로 하는 시간 \(전용 sku 및 버전에 따른 SQL Server 설치 수 및 위치\)

-   프로그램 추가\//제거에 설치 된 소프트웨어 목록

### <a name="who-will-use-sil"></a>SIL의 사용자는 누구인가요?

-   시간에 따라 중요 소프트웨어 인벤토리 데이터를 자동으로 수집하기 위한 경제적인 방법을 찾고 있는 **IT 전문가 또는 데이터 센터 관리자**

-   조직의 IT 배포에서 Microsoft 엔터프라이즈 소프트웨어의 사용량을 보고 해야 하는 **cio 및 재무 컨트롤러**

## <a name="getting-started"></a>시작하기
**필수 구성 요소**

VM 또는 실제 하드웨어의 하나 이상의 서버에 집계 및 보고를 위한 SIL Aggregator(Software Inventory Logging Aggregator) 설치:

-   **Windows Server 2012 R2**(Standard 또는 Datacenter Edition)

-   **IIS 서버 역할** 은 .Net Framework 4.5, WCF 서비스 및 HTTP 활성화와 함께 모두 **역할 및 기능 추가 마법사**의 동일한 선택 트리에 있습니다.

-   **SQL Server** 2012 SP2 Standard Edition 또는 SQL Server 2014 Standard Edition

-   **64비트 Microsoft Excel** 2013(설치 시 선택 사항이지만 보고서를 만드는 데 필요함)

-   선택 사항: **VMware PowerCLI 5.5.0.5836** (VMware 환경에 필요)

>[!Note]
>Windows Management Framework를 사용 하는 경우 SIL 집계 에서만 WMF 릴리스 5.1의 알려진 호환성 문제가 있습니다.  SIL 집계가 설치 된 서버에서 WMF 버전 4.0을 초과 하지 않아도 됩니다.

SIL (소프트웨어 인벤토리 로깅)은 다음 업데이트가 설치 된 Windows Server 버전에 있습니다.

-   **Windows Server 2016**이상

-   **Windows Server 2012 R2**(Standard 또는 Datacenter Edition)

    -   Windows Server 2012 R2 업데이트 **KB3000850**(2014년 11월)

    -   Windows Server 2012 R2 업데이트 **KB3060681**(2015년 6월)(Windows 업데이트에서 선택적 업데이트로 표시될 수 있음)

### <a name="security-and-account-types"></a>보안 및 계정 유형
**인증서 요구 사항**

SIL 및 SIL Aggregator에서 인증된 통신을 위해 SSL 인증서를 사용합니다. 이 일반 구성에서는 인벤토리 데이터를 받는 웹 서비스를 호스트하기 위해 하나의 인증서(서버 이름 및 인증서 이름 일치)로 SIL Aggregator를 설치합니다. 그런 다음 SIL 기능을 사용하여 인벤토리를 만들 Windows Server에서 다른 클라이언트 인증서를 사용하여 데이터를 SIL Aggregator에 푸시합니다. PowerShell cmdlet (Set-silaggregator, 아래 세부 정보)을 사용 하 여 집계에서 연결 된 데이터를 수락할 승인 된 인증서 목록에 인증서 지문을 추가 해야 합니다. SIL Aggregator에서는 인증서로 각 데이터 페이로드를 인증한 후 데이터베이스 처리 및 삽입을 계속합니다. 이 과정에 대한 자세한 내용은 **SIL Aggregator Cmdlet 세부 정보** 섹션을 참조하세요.

### <a name="polling-account-setup"></a>폴링 계정 설정
폴링 작업을 사용하기 위해 SIL Aggregator에 자격 증명을 추가할 경우 최소 권한 계정 접근 방식을 사용해야 합니다. 또한 보안 모범 사례에 따라 데이터 센터 또는 다른 IT 배포의 모든 호스트에 대해 동일한 자격 증명을 사용 하지 않아야 합니다.

SIL Aggregator에서 폴링을 위해 설정하려는 Windows Server 호스트에서 Administrators 그룹의 사용자를 사용하지 않으려면 다음 단계에 따라 사용자 계정에 해당 액세스 권한만 부여합니다.

##### <a name="to-setup-a-polling-account"></a>폴링 계정을 설정하려면

1.  SIL Aggregator에서 폴링하려는 Windows Server Hyper-V 호스트에서 Windows의 **컴퓨터 관리**를 사용하여 로컬 사용자 계정을 만듭니다. 이때 처음으로 로그인할 때 강제로 암호를 변경하도록 하는 상자의 선택을 취소해야 합니다.

2.  이 사용자를 **Remote Management Users** 그룹에 추가합니다.

3.  이 사용자를 **Hyper-V Administrators** 그룹에 추가합니다.

4.  관리자 권한으로 **시작** -> **실행**->**WMIMgmt.msc**.

5.  **작업** 섹션에서 **기타 작업** 을 클릭하고 **속성**을 선택합니다.

6.  **보안**을 클릭합니다.

7.  **네임스페이스** 트리 뷰에서 **cimv2 네임스페이스**를 선택합니다.

8.  **보안**(단추)을 클릭합니다.

9. **Remote Management Users** 그룹을 **machinename\group name** 형식으로 추가합니다.

10. **확인**을 클릭합니다.

11. **root\cimv2**에 대한 보안 창으로 돌아가서 **Remote Management Users**를 선택합니다.

12. 맨 아래에 있는 사용 권한 섹션에서 **원격 사용** 이 선택 되어 있는지 확인 합니다.

13. **적용**, **확인**을 차례로 클릭합니다.

14. **속성** 창에서 **확인** 을 클릭합니다.

### <a name="installing-sil-aggregator"></a>SIL Aggregator 설치
Windows Server에서 SIL Aggregator를 설치하기 전에 확인해야 할 몇 가지 사항이 있습니다.

-   이 소프트웨어의 웹 서비스를 호스트 하는 데 사용할 **유효한 SSL 인증서가 있습니다** .

    -   인증서가 **.pfx** 형식이어야 합니다.

    -   Windows Server 이름과 인증서 이름이 일치해야 합니다.

-   **SQL Server Standard Edition이 설치**되어 있거나, 이 소프트웨어와 함께 사용할 원격 서버에 설치되어 있어야 합니다.

    -   SIL Aggregator는 SQL Server 2012 SP2와 SQL Server 2014 모두에서 사용됩니다. SQL Server 설치 중에 선택할 때 필요한 특이 사항이 없습니다.

    -   설치 중에 데이터베이스를 만들려면 SIL Aggregator를 설치하는 데 사용되는 계정이 SQL에서 sysadmin 역할이어야 합니다.

    -   SIL Aggregator를 설치하기 전에 SIL Aggregator를 설치하는 데 사용되는 계정을 SQL Analysis Services에 관리자로 추가해야 합니다.

    -   설치되면 SQL Server 에이전트를 자동으로 실행하도록 구성해야 합니다.

-   **IIS 서버 역할**은 **역할 및 기능 추가 마법사**의 동일한 선택 트리에 .Net Framework 4.5, WCF 서비스 및 HTTP 활성화와 함께 추가됩니다.

-   서버에서 **관리 권한이 있는 계정으로 서버에 로그온됩니다** .

-   Windows 인증을 사용할 경우 **SQL Server에서 sysadmin 권한이 있는 계정으로 서버에 로그온됩니다**.

    또는

    SQL 인증을 사용할 경우 **SQL 관리 권한이 있는 계정에 대한 암호가 있어야 합니다**.

##### <a name="to-install-software-inventory-logging-aggregator"></a>Software Inventory Logging Aggregator를 설치하려면

1.  **Setup.exe** 를 두 번 클릭하여 설치를 시작합니다.

2.  [시작] 창에서 **다음** 을 클릭합니다.

3.  EULA에 동의하면 계약에 동의하는 상자를 선택하고 **다음**을 클릭합니다.

4.  **기능 선택**에서 **Software Inventory Logging Aggregator 및 보고 모듈 설치**를 선택하고 **다음**을 클릭합니다.

    보고 모듈만 설치하는 방법에 대한 자세한 내용은 **SIL Aggregator Cmdlet 세부 정보** 섹션에서 `Publish-SilReport`를 참조하세요.

5.  모든 필수 구성 요소를 확인한 후 **다음**을 클릭합니다.

6.  **계정 유형 선택**에서 기본 설정에 따라 **로컬 사용자** 또는 **gMSA**를 선택합니다.

    로컬 사용자 계정 옵션을 선택하면 자동 생성된 강력한 암호로 로컬 사용자를 만듭니다. 이 계정은 로컬 서버에서의 모든 SIL Aggregator 서비스 및 태스크 작업에 사용됩니다.  집계가 Active Directory 도메인의 일부인 경우 gMSA(그룹 관리 서비스 계정)를 사용하는 것이 좋습니다(Windows Server 2012 이상). GMSA에 대 한 자세한 내용은 다음을 참조 하세요. [그룹 관리 서비스 계정 개요](https://technet.microsoft.com/library/hh831782.aspx)

    -   SIL Aggregator에서 별도의 서버에 SQL Server 데이터베이스를 실행하려면 gMSA 계정 옵션을 사용해야 합니다.

    -   Active Directory에서 gMSA 사용 보안 그룹에 컴퓨터 계정을 추가한 후 서버를 다시 부팅 해야 합니다.

7.  **SQL Server 선택**에서 SQL Server(SQL 인스턴스를 설치할 경우) 또는 **localhost**(로컬 서버에 설치할 경우)를 입력합니다.

    SQL 인스턴스당 하나의 SIL Aggregator만 지원됩니다.

8.  인증 유형을 선택하고 **SQL 검증**을 클릭합니다.

9. **다음**을 클릭한 다음 **인터넷 정보 서비스 서버 정보**에서 포트 번호를 선택하거나 기본값을 유지합니다.

10. **.pfx** 파일 위치를 찾고 .pfx 파일에 대한 암호를 입력한 후 **다음**을 클릭합니다.

11. 마지막 화면에 설치 진행률이 표시됩니다. 성공적으로 완료되면 **마침**을 클릭합니다.

### <a name="uninstalling-sil-aggregator"></a>SIL Aggregator 제거

##### <a name="to-uninstall-software-inventory-logging-aggregator"></a>Software Inventory Logging Aggregator를 제거하려면

1.  관리자 권한으로 **PowerShell** 을 열고 `Stop-SilAggregator`를 입력합니다. 프롬프트가 반환되면 SIL Aggregator가 중지된 것입니다.

    기본적으로 SIL Aggregator에서는 20분이 경과하거나 100개의 파일을 받은 이후에 파일을 처리합니다.  대규모 환경에서는 이 시나리오가 발생되지 않지만, 소규모 환경에서는 집계가 중지되기 이전에 일부 파일이 계속 처리될 수 있습니다. 이러한 파일 및 데이터를 유지할 필요가 없는 경우 `–Force` 매개 변수를 사용하세요.

2.  **제어판**으로 이동한 다음 **프로그램 및 기능**, **프로그램 제거**, **Software Inventory Logging Aggregator**, **제거**를 차례로 클릭합니다.

    Software Inventory Logging Aggregator에서는 데이터베이스의 모든 데이터를 삭제할지 아니면 데이터베이스의 모든 데이터를 유지할지를 선택하라는 메시지가 표시된 창을 엽니다. 기본 선택은 모든 데이터를 유지하는 것입니다. 다시 설치하려면 기존 데이터베이스에 연결하여 집계가 종료된 위치를 선택할 수 있습니다.

3.  **유지** 또는 **삭제**를 선택하고 **다음**을 클릭합니다.

4.  진행률 표시줄이 완료되면 **마침**을 클릭합니다.

### <a name="start-using-sil-and-the-sil-aggregator"></a>SIL 및 SIL Aggregator 사용 시작

#### <a name="introduction-to-sil-aggregator-powershell-cmdlets"></a>SIL Aggregator PowerShell cmdlet 소개
다음 명령은 Windows PowerShell 콘솔에서 관리자 권한으로 실행할 수 있습니다.

|Windows PowerShell Cmdlet|함수|
|-----------------------------|------------|
|`Start-SilAggregator`|모든 Software Inventory Logging Aggregator 서비스 및 작업을 시작합니다. 집계 중에 SIL 로깅을 시작한 서버에서 HTTPS를 통해 데이터를 받으려면 이 명령을 실행해야 합니다.|
|`Stop-SilAggregator`|모든 Software Inventory Logging Aggregator 서비스 및 작업을 중지합니다. 작업 또는 서비스를 처리하는 동안 이 명령의 완료가 지연될 수 있습니다.|
|`Set-SilAggregator`|관리자가 Software Inventory Logging Aggregator에 대한 구성을 변경하도록 허용합니다.|
|`Add-SilVmHost`|정기적 간격 \(으로 폴링할 특정 호스트 이름 또는 호스트 이름 배열을 추가 하는 데 사용 되는 기본값은 1 시간 간격\)입니다.|
|`Remove-SilVmHost`|정기적으로 폴링할 특정 호스트 이름 또는 호스트 이름 배열을 제거하는 데 사용됩니다.|
|`Get-SilVMHost`|진행 중인 VM 실행 상태 데이터에 대해 Software Inventory Logging Aggregator를 폴링하도록 구성된 실제 호스트 목록을 검색하는 데 사용됩니다.|
|`Get-SILAggregatorData`|PowerShell 콘솔에서 데이터베이스의 데이터를 검색하는 데 사용됩니다.|
|`Publish-SilReport`|소프트웨어 인벤토리 로깅 데이터의 데이터베이스에서 보고서를 만드는 데 사용됩니다. **참고:** 집계에 대한 큐브 처리는 하루에 한 번 발생합니다. 따라서 집계에서 캡처되는 데이터는 다음 날까지 보고서에 표시되지 않습니다.|

#### <a name="suggested-order-to-start"></a>제안된 시작 순서
Software Inventory Logging Aggregator를 서버에 설치한 후 관리자 권한으로 PowerShell을 엽니다.

-   SIL Aggregator에서:

    -   `Start-SilAggregator`를 실행합니다.

        인벤토리를 만들도록 설정했거나 설정할 서버에서 HTTPS를 통해 전달되는 데이터를 집계 중에 적극적으로 받으려면 이 명령을 실행해야 합니다. 서버에서는 최대 30일 동안 데이터 페이로드를 로컬로 캐싱하므로, 이 집계에 먼저 전달하도록 서버를 설정한 경우에도 문제가 되지 않습니다. 집계에서 "targeturi"가 실행 되 면 모든 캐시 된 데이터가 집계에 한 번에 전달 되 고 모든 데이터가 처리 됩니다.

    -   `Add-SilVMHost`를 실행합니다.

        예: `add-silvmhost –vmhostname contoso1 –hostcredential get-credential`

        -   이 예에서 **contoso1**은 집계에서 시간에 따라 이 데이터를 추적하기 위해 실행 중인 VM을 위한 정기 업데이트에 대해 폴링할 실제 호스트 서버의 네트워크 이름 또는 IP 주소입니다. Get-Credential는 로그온한 사용자에게 해당 위치 다음부터 이 호스트를 폴링하는 데 사용할 계정을 입력하라는 메시지를 표시합니다. 동일한 호스트에서 동일한 명령을 실행하여 언제든지 사용되는 계정을 업데이트할 수 있습니다. 시간에 따른 계정 암호 변경 및 만료에 주의하세요. 자격 증명이 변경되거나 만료된 경우 호스트에 대한 폴링이 실패합니다.

        -   기본적으로 폴링은 `Start-SilAggregator` 가 실행되고 1시간 이후부터 또는 호스트가 폴링 목록에 새로 추가되고 1시간 이후부터 매시간 시작됩니다.  `Set-SilAggregator cmdlet`을 사용하여 폴링 간격을 변경할 수 있습니다.

        -   이 cmdlet은 미리 설정된 옵션 목록에서 자동으로 검색됩니다(**SIL Aggregator Cmdlet 세부 정보** 섹션 참조). 여기서 HostType 및 HyperVisorType은 추가 중인 호스트에 적합합니다. 이러한 항목을 인식할 수 없거나 제공된 자격 증명이 잘못된 경우 프롬프트가 표시됩니다. **Y**를 입력하여 수락하면 호스트가 추가되고 **알 수 없음**으로 나열되지만 폴링되지 않습니다.

    -   " `Set-SilAggregator –AddCertificateThumbprint` 사용자의 클라이언트 인증서의 지문" 실행

        SIL 로깅을 사용하도록 설정한 Windows Server에서 HTTPS를 통해 데이터를 받으려면 이 명령을 실행해야 합니다. 지문은 SIL Aggregator에서 데이터를 수락할 지문 목록에 추가됩니다. SIL Aggregator는 유효한 엔터프라이즈 클라이언트 인증 인증서를 수락하도록 설계되었습니다. 사용 되는 인증서는 데이터를 전달 하는 서버의  **\\localmachine\MY (로컬 컴퓨터-> 개인**) 저장소에 설치 해야 합니다.

-   인벤토리를 만들 Windows Server에서 관리자 권한으로 PowerShell을 열고 다음 명령을 실행합니다.

    -   `Set-SilLogging –TargetUri "https://contososilaggregator" –CertificateThumbprint "your client certificate's thumbprint"`를 실행합니다.

        -   이 명령은 Windows Server의 SIL에 인벤토리 데이터를 보낼 위치와 인증에 사용할 인증서를 알려줍니다.

            > [!IMPORTANT]
            > "Https://"가 TargetUri 값에 있는지 확인 합니다.

        -   이 지문을 포함하는 엔터프라이즈 클라이언트 인증서를 **\localmachine\MY**에 설치하거나 **certmgr.msc**를 사용하여 **로컬 컴퓨터 -> 개인** 저장소에 인증서를 설치해야 합니다.

            > [!IMPORTANT]
            > 이러한 값이 올바르지 않거나 인증서가 해당 저장소에 설치되어 있지 않거나 잘못된 경우 SIL 로깅이 시작될 때 대상으로 전달되지 않습니다. 데이터는 최대 30일 동안 로컬로 캐시됩니다.

    -   `Start-SilLogging`를 실행합니다.

        이 명령은 SIL 로깅을 시작합니다. 매시간 임의의 간격으로 SIL은 `–targeturi` 매개 변수에 지정된 집계에 인벤토리 데이터를 전달합니다. 처음에는 전체 데이터 집합을 전달합니다. 앞으로의 앞으로는 아무것도 변경 하지 않은 데이터를 식별 하는 "하트 비트"가 추가 될 예정입니다. 데이터 집합이 변경된 경우 다른 전체 데이터 집합이 전달됩니다.

    -   `Publish-SilData`를 실행합니다.

        -   로깅에 대해 SIL을 처음으로 사용할 경우 이 단계는 선택 사항입니다.

        -   여기서는 전체 데이터 집합을 수동으로 한 번 전달합니다.

        -   SIL 로깅을 시작한 후 오랜 시간이 경과하고 `Set-SilLogging`을 사용하여 새 SIL Aggregator를 지정한 경우 이 cmdlet을 한 번만 실행하여 전체 데이터 집합을 새 집계로 보내야 합니다.

다음 단계에 따라 가상 Windows Server 컴퓨터를 실행 중인 실제 호스트를 추가하고 해당 Windows Server 내에서 SIL 로깅(소프트웨어 인벤토리 로깅)을 사용하도록 설정한 경우 SIL Aggregator에서 언제든지 `Publish-SilReport –OpenReport` 를 실행할 수 있습니다(Excel 2013 필요). 하지만 SQL Server Analysis Services 큐브는 하루에 한 번 처리되므로 동일한 날짜에 보고서에서 데이터를 사용할 수 없습니다.

## <a name="architectural-overview"></a>아키텍처 개요
SIL는 밀어넣기 모드와 끌어오기 모드에서 모두 작동 하며 병렬로 작동 하는 두 구성 요소로 구성 됩니다. Windows Server의 SIL (소프트웨어 인벤토리 로깅) 기능 및 SILA (Software Inventory Logging)에서 다운로드 가능한 MSI를 다운로드 합니다. 인벤토리를 만들 서버에서는 SIL을 사용하여 HTTPS를 통해 소프트웨어 인벤토리 데이터를 SIL Aggregator에 푸시합니다(1시간마다 각 시간 내의 임의의 시점에). 집계에서는 실제 하이퍼바이저 호스트를 차례로 폴링하거나 쿼리하여 1시간마다 하드웨어 인벤토리 데이터를 끌어옵니다. SIL의 전체 기능을 사용하려면 푸시와 끌어오기 모두를 적절히 구성해야 합니다. 푸시와 끌어오기를 순서에 관계없이 구성할 수 있습니다. 하지만 집계에서 큐브 처리는 하루에 한 번만 발생하므로, 집계에서 푸시 또는 끌어보기를 통해 캡처되는 데이터는 다음 날까지 보고서에 표시되지 않습니다.

![](../media/software-inventory-logging/SILA_Architecture.png)

> [!IMPORTANT]
> 이 소프트웨어를 사용하는 동안 데이터가 Microsoft로 전송되지 않습니다.

## <a name="enable-sil-on-multiple-servers"></a>여러 서버에서 SIL 사용
가상 머신의 프라이빗 클라우드와 같은 분산된 서버 인프라에서 SIL을 사용하도록 설정하는 몇 가지 방법이 있습니다.  다음은 네트워크에서 처음으로 시작할 때 인벤토리 데이터를 SIL Aggregator로 자동으로 보내도록 Windows Server 이미지를 설정하는 방법을 보여주는 한 가지 예입니다.

Windows Server가 설치된 각 실행 중인 VM 또는 실제 컴퓨터/장치의 PowerShell 콘솔에서 다음 cmdlet을 관리자 권한으로 실행합니다( **필수 구성 요소** 섹션 참조).

이러한 단계를 사용하려면 .pfx 형식의 유효한 클라이언트 SSL 인증서가 필요합니다.  `Set-SILAggregator –AddCertificateThumbprint` cmdlet을 사용하여 이 인증서의 지문을 SIL Aggregator에 추가해야 합니다. 이 클라이언트 인증서가 SIL Aggregator의 이름과 일치할 필요는 없습니다.

-   `$secpasswd = ConvertTo-SecureString "`**<password for the account with permissions to the network location holding your client pfx file>**`" -AsPlainText –Force`

-   `$mycreds = New-Object System.Management.Automation.PSCredential ("`**<user account with permissions to the network location holding your client  pfx file>**`", $secpasswd)`

-   `$driveLetters = ([int][char]'C')..([int][char]'Z') | % {[char]$_}`

-   `$occupiedDriveLetters = Get-Volume | % DriveLetter`

-   `$availableDriveLetters = $driveLetters | ? {$occupiedDriveLetters -notcontains $_}`

-   `$firstAvailableDriveLetter = $availableDriveLetters[0]`

-   `New-PSDrive -Name $firstAvailableDriveLetter -PSProvider filesystem -root`**server\path pfx 인증서 파일을 보관 하는 파일 > < \\** `-credential $mycreds`

-   `Copy-Item ${firstAvailableDriveLetter}:\`**새 드라이브의 디렉터리에 certificatename .pfx 파일을 < > c:\<선택한 위치 >**

-   `Remove-PSDrive –Name $firstAvailableDriveLetter`

-   `$mypwd = ConvertTo-SecureString -String "`**<password for the certificate pfx file>**`" -Force –AsPlainText`

-   `Import-PfxCertificate -FilePath c:\` **<location\\certificatename.pfx>** `cert:\localMachine\my -Password $mypwd`

-   `Set-sillogging –targeturi "https://` **<machinename of your SIL Aggregator>** `–certificatethumbprint`

> [!NOTE] 
> 클라이언트 pfx 파일의 인증서 지문을 사용 하 고 **set-silaggregator '-AddCertificateThumbprint** cmdlet을 사용 하 여 SIL 집계에 추가 합니다.

-   `Start-sillogging`

SIL Aggregator에 연결할 수 없는 경우 SIL 인벤토리 데이터는 최대 30일 동안 Windows Server에 로컬로 캐시됩니다. 집계에 푸시되면 모든 캐시된 데이터가 전달됩니다.

이전 집계에 푸시한 후 SIL 데이터를 새 SIL Aggregator에 푸시할 경우 위 목록에 `Publish-SilData` 를 추가합니다. 그러면 SIL 데이터의 전체 보수가 전송되므로 이 컴퓨터에 대해 새 집계가 필요합니다.

## <a name="software-inventory-logging-aggregator-reports"></a>Software Inventory Logging Aggregator 보고서
![](../media/software-inventory-logging/SILA_Report.png)

### <a name="cube-processing"></a>큐브 처리
Software Inventory Logging Aggregator에서 SQL Server Analysis Services 큐브는 매일 오전 3:00:00(로컬 시스템 시간)에 한 번 처리됩니다. 보고서에는 해당 시간까지 캡처된 모든 데이터가 반영되지만, 같은 날짜의 해당 시간 이후에 캡처된 데이터는 반영되지 않습니다.

### <a name="high-water-mark"></a>최고 수위 표시
소프트웨어 인벤토리 로깅 집계 보고서의 기본 측면은 일반적으로 동시에 실행 중인 Windows Server의 "최고 수 위 표시" 라고 하는 것입니다. 이는 이러한 보고서의 Windows Server 및 System Center 수에 적용됩니다. Windows Server의 경우 각 실제 호스트에는 OS 유형에 상관없이 1개월의 과정 동안 대부분의 Windows Server VM이 동시에 실행 중인 시점이 있습니다. 이를 해당 월에 대한 최고 수위 표시라고 합니다. System Center의 경우 매월 각 실제 호스트에서 대부분의 관리되는 Windows Server가 동시에 실행 중인 시점이 있습니다. 관리되는 서버는 하나 이상의 System Center 에이전트가 있을 때 식별됩니다. 보고서에는 실제 호스트에 대한 최신 최고 수위 표시만 표시됩니다. 최고 수위 표시 이후의 데이터는 표시되지 않습니다. 해당 시점 이후에는 Windows Server VM(WS 탭) 또는 관리되는 Windows Server VM(SC 탭)의 수가 최고 수위 표시 아래로 떨어진 것으로 간주될 수 있습니다. 이 사용량 추적 및 표시 방법은 이러한 제품에 대한 라이선스 모델을 지원하고 용량 계획을 돕기 위한 것입니다.

보고서의 SQL 관련 탭에서는 SQL Server 설치가 누적 되어 계산 됩니다. 안 함. 합계는 실행 중인 SQL Server 설치 수입니다.

> [!NOTE]
> 소프트웨어 인벤토리 로깅을 사용하는 것이 해당 사용 조건에 따라 Microsoft 소프트웨어 사용을 정확히 보고해야 하는 의무를 대체하지는 않습니다.

### <a name="poll-date-time"></a>폴링 날짜/시간
Software Inventory Logging Aggregator를 사용할 경우 최고 수위 표시 수는 폴링을 기반으로 집계됨을 알고 있어야 합니다. 즉, 최고 수위 표시는 기본 실제 호스트의 폴링을 통해서만 캡처할 수 있습니다. 따라서 최고 수 위 표시 수는 해당 "폴링 날짜/시간"과 직접 연결 됩니다. 폴링 간격을 조정할 수 있지만, 높은 간격 값을 사용할 경우 캡처되는 최고 수위 표시의 충실도에 영향을 줍니다. 간격이 높을수록 데이터가 실제 사용을 대표하는 정도가 낮아집니다.

### <a name="reports-are-month-by-month"></a>월별 보고서
연간 보고서를 비롯한 모든 보고서는 월별 보고서로 표시됩니다. 최고 수위 표시, 합계 및 컴퓨터 데이터는 매달 월초에 다시 설정됩니다.

새로운 달로 바뀔 때 영향을 받는 보고서 데이터는 다음과 같습니다.

-   모든 호스트에 대한 모든 최고 수위 표시는 새로운 달을 시작할 때 다시 설정됩니다.

-   집계 중에 VM에서 HTTPS를 통해 하나 이상의 전체 페이로드를 수신하지만 하트비트 수신이 중지될 경우, 해당 달의 모든 기본 호스트 폴링에서는 호스트, VM, VM 데이터 간에 연관성이 있으므로 해당 달에 해당 VM이 계속 실행 중이었거나 중지된 것으로 간주합니다. 새로운 달이 시작되면 해당 VM으로부터 전체 페이로드 또는 하트비트를 받을 때까지 이 연결이 지워집니다.

### <a name="additional-notes-on-report-behavior"></a>보고서 동작에 대한 추가 메모

-   [요약] 탭은 인벤토리의 빠른 참조 목록으로 제공됩니다. 호스트와 VM은 동일한 열에 나열됩니다.

-   회색 또는 흐리게 표시되는 모든 값을 무시합니다. 이러한 값은 SSAS 큐브로부터 보고서를 작성하는 아티팩트입니다.

-   VM이 "알 수 없는 OS"로 나열 되는 경우 집계는 HTTPS를 통해 SIL를 통해 해당 VM에서 전체 데이터 페이로드를 수신 하지 않았음을 의미 합니다.

-   "알 수 없는 호스트" 아래에 나열 된 Vm은 Windows Server Vm이 HTTPS를 통해 인벤토리 데이터를 집계에 성공적으로 전달 하지만 집계가 해당 VM에 대 한 기본 호스트를 적극적 또는 성공적으로 폴링하고 있지 않습니다. 기본 호스트를 알 수 없으므로 이러한 항목의 수는 항상 0입니다. `Add-SilVMHost` cmdlet을 사용하고 올바른 자격 증명을 제공하여 폴링을 위해 호스트 또는 모든 호스트를 SIL Aggregator에 추가합니다. 폴링된 이후에는 보고서에서 VM 데이터와 호스트 데이터가 연결됩니다.

-   모든 날짜와 시간은 SIL Aggregator 시스템 시간 및 로캘에 로컬입니다. 여기에는 SIL 사용 시스템에서 HTTPS를 통해 받은 인벤토리 데이터가 포함됩니다. 이러한 파일이 수신 후 20분 이내에 처리되면 데이터는 데이터베이스에 로컬 시스템 시간으로 삽입됩니다.

-   "SIL 집계"는 소프트웨어 인벤토리 로깅 집계가 설치 된 모든 서버 컴퓨터에 표시 됩니다.

-   실제 호스트에서 프로세서 수 또는 실제 메모리 양이 변경되면 보고서에 이전 행과 함께 새 행이 나타납니다. 새로 추가한 호스트인 것처럼 폴링 업데이트가 이전 행에서는 중단되고 새 행에서는 계속됩니다.

-   **요약** 및 **세부 정보** 탭에서 동시에 실행 중인 Windows Server 또는 관리되는 Windows Server에 대한 열이 나열되는 합계는 아래의 모든 호스트에 대한 모든 최고 수위 표시의 합계를 나타냅니다. 여기에는 하이퍼바이저 호스트가 아니고 실행 중인 vm이 없는 Windows Server 뿐만 아니라, 실행 중인 vm이 있지만 "알 수 없음"으로, HTTPS를 통해 SIL에서 VM 내에 데이터가 수신 되지 않으므로 "알 수 없음"이 발생 합니다. 이러한 항목은 편의상 합계로 계산됩니다.

-   **대시보드** 탭의 **SQL Server** 섹션에서 총 SQL Server 설치 수는 대시보드에 있는 모든 버전 합계를 요약한 것입니다.  단일 서버에 여러 버전의 SQL이 설치되어 있는 경우 **SQL 세부 정보** 탭에 표시된 합계와 일치하지 않을 수 있습니다.  대시보드에서는 각 서버에서 이러한 값을 개별적으로 계산하지만 **세부 정보** 탭에서는 그렇지 않습니다.  여러 SQL 버전이 하나의 Windows Server에 설치되어 있는 경우 해당 버전은 항상 사용 조건당 하나로 계산됩니다.

-   **대시보드** 탭의 **Windows Server** 섹션에서 **기타 하이퍼바이저 호스트** 및 **총 하이퍼바이저 호스트** 행에는 Hyper-V를 실행 중이거나 실행 중이 아닌 실제 Windows Server 호스트 수가 포함되어 있습니다.

### <a name="column-descriptions"></a>열 설명
다음은 SIL Aggregator에서 만드는 Excel 기반 보고서의 **Windows 서버 세부 정보** 탭에 있는 각 열에 대한 설명입니다. 다른 데이터 탭은 동일하거나 이러한 열의 하위 집합입니다. 한 가지 예외는 SQL Server 탭에 있는 "설치 수"입니다 (최고 수 위 **표시** 섹션 참조).

|열 머리글|설명|
|-----------------|---------------|
|월|보고서의 데이터는 월별로 최신 순으로 그룹화됩니다. 같은 달의 데이터는 특정 순서로 나열되지 않습니다.|
|호스트 이름|SIL Aggregator에서 폴링하고 있는 실제 호스트의 네트워크 이름 또는 FQDN입니다.<br /><br />Get-SilVMHost cmdlet을 사용하여 추가되었지만 폴링되지 않았거나 더 이상 폴링되지 않는 호스트를 찾습니다. 마지막으로 성공한 폴링이 표시됩니다.|
|호스트 유형|실제 호스트의 운영 체제 제조업체입니다.|
|하이퍼바이저 유형|실제 호스트의 하이퍼바이저 제조업체입니다.|
|프로세서 제조업체|실제 호스트의 프로세서 제조업체입니다.|
|프로세서 모델|실제 호스트의 프로세서 모델입니다.|
|하이퍼 스레딩을 사용하나요?|실제 호스트의 프로세서에서 하이퍼 스레딩을 사용하도록 설정했는지 여부에 따라 True 또는 False로 표시합니다.|
|VM 이름|Windows Server 가상 컴퓨터의 네트워크 이름 또는 FQDN입니다. 집계 중에 이 컴퓨터에서 HTTPS를 통해 데이터를 받지 않는 경우 하이퍼바이저의 VM 이름이 나열됩니다.|
|호스트별로 동시에 실행 중인 Windows Server VM|호스트에서 동시에 실행 중인 Windows Server VM의 수입니다. 해당 호스트에 대해 해당 달의 가장 높은 수는 해당 시점에 나열 및 캡처된 최고 수위 표시입니다.<br /><br />이 설명서의 **최고 수위 표시** 섹션을 참조하세요.<br /><br />Windows Server를 설치한 실제 호스트 또는 Windows Server를 설치했지만 알려진 Windows Server VM이 실행되고 있지 않은 실제 호스트는 항상 하나로 계산됩니다. 호스트에서 하나 이상의 알려진 Windows Server VM이 실행되고 있고 Windows Server가 자체 호스트에서 실행 중인 경우 호스트 OS는 계산에 포함되지 않습니다.|
|실제 프로세서 수|실제 호스트에 설치된 실제 프로세서 수입니다.|
|실제 코어 수|실제 호스트에 설치된 실제 프로세서 코어의 수입니다.|
|가상 프로세서 수|Windows에서 VM 내에서 인식하는 가상 프로세서의 수입니다. 이 값은 Windows Server에서 SIL을 사용하여 HTTPS를 통해 전달되는 데이터에서만 가져옵니다.|
|폴링 날짜/시간|실제 호스트에서 동시에 실행 중인 Windows Server VM의 최신 최고 수위 표시 지점의 날짜 및 시간입니다.<br /><br />이 설명서의 **폴링 날짜/시간** 섹션을 참조하세요.|
|VM에 마지막 표시된 날짜/시간|집계 중에 이 Windows Server VM에서 HTTPS를 통해 마지막으로 데이터 인벤토리를 받은 날짜 및 시간입니다.|
|호스트에 마지막 표시된 날짜/시간|집계 중에 이 Windows Server 실제 호스트에서 HTTPS를 통해 마지막으로 데이터 인벤토리를 받은 날짜 및 시간입니다.<br /><br />Windows Server 및 HyperV를 실행 중인 실제 호스트에서 SIL을 사용하고 HTTPS를 통해 인벤토리 데이터를 SIL Aggregator로 전달할 수 있습니다.|

## <a name="sil-aggregator-cmdlets-detail"></a>SIL Aggregator Cmdlet 세부 정보
다음은 SIL Aggregator cmdlet에 대한 세부 정보입니다. 전체 cmdlet 설명서는 다음을 참조 하세요. [SIL 집계 PowerShell cmdlet](https://technet.microsoft.com/library/mt548455.aspx)

### <a name="publish-silreport"></a>Publish-SilReport

-   이 cmdlet은 그대로 사용 되며, 소프트웨어 인벤토리 로깅 보고서를 만들어 로그인 한 사용자의 Documents 디렉터리에 저장 합니다. cmdlet이 실행 되는 컴퓨터에는 Excel 2013이 필요 합니다.

-   `–OpenReport` 매개 변수와 함께 사용되어 보고서를 만든 후 보기 위해 Excel에서 엽니다.

-   SIL Aggregator를 설치할 때 보고 모듈만 설치할 수 있습니다. 보고 모듈을 Windows 클라이언트 운영 체제(Windows 8.1, Windows 10 등)에 설치할 수 있습니다. 그러면 씬 클라이언트(노트북, 태블릿 등)에서 SIL Aggregator 데이터베이스 서버에 연결하여 SIL 보고서를 직접 게시할 수 있습니다.

    -   다음 예에서는 SILContoso라는 SIL Aggregator 데이터베이스 서버를 사용 및 연결하고 로컬 컴퓨터에서 SIL 보고서를 만들어서 여는 데 사용할 자격 증명을 묻는 메시지를 표시합니다.

        `Publish-SilReport -DBServerName "SILContoso" -DBServerCredential Get-Credential –OpenReport`

    -   대부분의 경우 처음으로 연결하기 전에 SIL Aggregator 데이터베이스 서버에서 방화벽의 포트를 열어서 연결을 허용해야 합니다. IT 전문가는 이 설정을 미리 수행하여 재무 관리자 또는 다른 인벤토리 관리자가 자체 보고서를 만들 수 있도록 액세스 권한을 부여하고자 합니다. 이 작업을 수행하는 단계는 아래 링크를 참조하세요. 일반적으로 SQL Server Analysis Services의 기본 포트는 2383입니다.

### <a name="add-silvmhost"></a>Add-SilVMHost
다음은 `Add-SilVMHost` cmdlet을 사용할 때 지원되는 호스트 유형 및 하이퍼바이저 버전입니다. 이러한 항목을 지정할 필요는 없습니다. `Add-SilVMHost` cmdlet에서는 지원되는 조합을 자동으로 검색합니다. 검색할 수 없거나 제공된 자격 증명이 잘못된 경우 프롬프트가 표시됩니다. 사용자가 "Y" 항목을 사용 하 여 수락 하면 호스트가 추가 되지만 폴링 되지 않습니다. "알 수 없음"으로 추가 됩니다.

|하이퍼바이저 버전|SIL Aggregator         HostType 값|SIL Aggregator HypervisorType 값|
|----------------------|-----------------------------------------|---------------------------------------|
|Windows Server, 2012 R2|Windows|HyperV|
|VMware 5.5|VMware|Esxi|
|Xen 4.x|Ubuntu, OpenSuse 또는 CentOS|Xen|
|XenServer 6.2|Citrix|XenServer|
|KVM|Ubuntu, OpenSuse 또는 CentOS|KVM|

이러한 하이퍼바이저 플랫폼 및 유형의 다른 버전도 작동할 수 있습니다.  SIL Aggregator는 아래 sshnet 버전과 함께 제공됩니다.  Linux 기반 가상화 플랫폼과 통신하는 데 사용됩니다.

<pre>sshnet 2014.4.6-beta1
https://sshnet.codeplex.com/releases/view/120504
Copyright (c) 2010, RENCI</pre>

### <a name="get-silaggregator"></a>Get-SilAggregator
`Get-SilAggregator`에서는 Software Inventory Logging Aggregator 응용 프로그램에 대한 구성 정보를 제공합니다. 다음과 같은 예제 출력이 표시됩니다.

-   응용 프로그램이 실행 중입니다.

-   폴링 간격은 1시간입니다(시간 단위 증분 변경 가능).

-   폴링 시작 시간

-   다른 컴퓨터에서 이 집계에 데이터를 전달하기 위해 설정해야 하는 대상 URI

-   이 집계에서 SIL 데이터를 수락하는 데 사용되는 인증서 지문

-   설치 시 지정된 계정 유형

    `PS C:\Windows\system32> Get-SilAggregator`

    ``

    `State          : Running HostPollIntervalInHours : Every 1 Hour(s)`

    `PollStartTime      : 8/24/2015 5:07:33 AM`

    `TargetURI        : https://SilContoso`

    `CertificateThumbprint  : 3efc6b8ce7d5eefba5107ede9d1caca550417452, 2dc4ea8bfb64b1246a8c1ffa1b701cd1042a3412`

    `UserProfile       : Local`

### <a name="set-silaggregator"></a>Set-SilAggregator
`Set-SilAggregator` cmdlet을 사용하여 다음을 수행할 수 있습니다.

-   폴링이 발생할 시간 간격 변경

-   폴링을 지정된 간격으로 시작할 시작 날짜 및 시간 변경

-   SIL Aggregator에서 데이터를 수락하거나 연결된 인증서 지문 추가 또는 제거

### <a name="get-aggregatordata"></a>Get-AggregatorData

-   이 cmdlet을 단독으로 사용하면 SIL Aggregator Excel 보고서의 [Windows Server 세부 정보] 탭의 내용이 표시됩니다.

-   이 cmdlet을 매개 변수와 함께 사용하여 데이터베이스에서 데이터를 직접 검색함으로써 SIL 전체 솔루션에 대한 사용자 지정 사용을 지원할 수 있습니다.

-   `–StartTime` 및 `–Endtime` 매개 변수는 시작 날짜 월의 1일부터 종료 날짜 월의 말일까지의 보고서 데이터를 표시합니다.

![](../media/software-inventory-logging/SILA_Get-SILAggregator.png)

### <a name="get-silvmhost"></a>Get-SilVMHost

-   이 cmdlet은 SIL Aggregator에서 폴링하도록 구성된 실제 호스트, 최근에 성공한 폴링 날짜 및 시간, HostType(또는 OS 제조업체) 및 HypervisorType(하이퍼바이저 제조업체)의 목록을 출력합니다. HostType 및 HypervisorType에 대한 자세한 내용은 Add-SilVMHost 세부 정보를 참조하세요.

    호스트에 폴링 날짜 및 시간이 없지만 지원되는 HostType 및 HypervisorType이 있는 경우 폴링이 아직 시작되거나 성공하지 않은 것입니다.

-   또한 이 cmdlet은 VM에서 가져온 데이터(VM에서 사용 가능한 경우)를 통해 추가된 호스트 이름을 나열합니다. 이러한 이름은 목록에 나타나지만 HostType 또는 HypervisorType이 없습니다. 이 데이터를 사용하면 폴링하도록 설정되지 않은 VM과 호스트를 일치시킬 수 있습니다.

-   `–StartTime` 및`–EndTime` 매개 변수를 사용하면 언제 호스트가 처음으로 추가되고 마지막으로 폴링되었는지를 쉽게 알 수 있습니다.

### <a name="remove-silvmhost"></a>Remove-SilVMHost

-   이 cmdlet은 폴링할 호스트 목록에서 호스트를 제거합니다. 호스트가 제거된 경우 호스트의 VM에서 호스트를 목록에 다시 추가할 수 있지만 `Add-SilVMHost` cmdlet을 사용하여 올바른 자격 증명을 지정해도 호스트가 폴링되지 않습니다.

-   호스트가 제거된 경우 해당 호스트는 폴링에서 제거되지만 보고서에서는 제거되지 않습니다. 폴링이 중단되므로 호스트는 다음 달의 보고서에 표시되지 않습니다.

-   `–StartTime` 및`–EndTime` 매개 변수를 개별적으로 사용하여 특정 날짜까지 폴링되거나 특정 날짜부터 폴링된 호스트 그룹을 제거할 수 있습니다.

## <a name="avoid-these-errors-and-issues-with-sil-and-sil-aggregator-troubleshooting-guide"></a>SIL 및 SIL Aggregator와 관련한 다음 오류 및 문제 방지(문제 해결 가이드)

-   `SilLogging` 또는 `Publish-Sildata` cmdlet 실패 또는 오류 시 확인해야 할 사항:

    -   **targeturi** 입력에 **https://** 가 있는지를 확인합니다.

    -   Windows Server에 대한 모든 필요한 업데이트가 설치되어 있는지 확인합니다(SIL에 대한 필수 구성 요소 참조).  이를 확인 하는 빠른 방법은 다음 cmdlet을 사용 하 여 확인 하는 것입니다.`Get-SilWindowsUpdate *3060*, *3000*`

    -   집계를 인증하는 데 사용 중인 인증서가 SilLogging을 사용하여 인벤토리를 만들 로컬 서버의 해당 저장소에 설치되어 있는지 확인합니다(시작 섹션 참조).

    -   SIL Aggregator에서 집계를 인증하는 데 사용 중인 인증서의 인증서 지문이 `Set-SilAggregator –AddCertificateThumbprint` cmdlet을 사용하여 목록에 추가되는지 확인합니다(시작 섹션 참조).

    -   엔터프라이즈 인증서를 사용 중인 경우 SIL을 사용하도록 설정된 서버가 인증서를 만든 도메인에 가입되어 있거나 루트 인증 기관을 통해 인증 가능한지를 확인합니다. 데이터를 집계로 전달/푸시하려는 로컬 컴퓨터의 인증서를 신뢰할 수 없는 경우 이 작업이 실패하고 오류가 발생합니다.

    -   위의 모든 항목이 선택되어 있는 경우 SIL Aggregator를 설치하는 데 사용되는 인증서가 정상 상태이고 SIL Aggregator 서버의 이름과 일치하는지를 확인할 수 있습니다. 다른 컴퓨터에서 동일한 SIL Aggregator에 전달되는 경우에는 이 단계를 수행할 필요가 없습니다.

    -   \Windows\System32\\Logfiles\\SIL를 전달/푸시하는 서버에서 캐시 된 SIL 파일에 대 한 다음 위치를 확인할 수 있습니다. `SilLogging`이 시작되고 1시간 이상 실행 중이거나 `Publish-SilData`를 최근에 실행했지만 이 디렉터리에 파일이 없는 경우 집계에 대한 로깅이 성공한 것입니다.

-   로그인한 사용자에게 SQL 데이터베이스 및 Analysis Services 액세스 권한이 있는지를 확인합니다.

    -   이 작업은 SIL Aggregator를 설치할 때 수행해야 합니다.

    -   PowerShell을 원격으로 사용 하 여 SIL 집계를 관리할 때 필요 합니다.

-   클라이언트 데스크톱 OS에서 SIL Aggregator 보고서를 게시합니다.

    -   Windows 클라이언트(8.1/10)에서 보고 모듈만 설치하려면 이 옵션을 사용합니다.

    -   powershell을 원격으로 사용하여 보고서를 만들 때 문제가 발생할 경우 연결하려는 SIL Aggregator에서 방화벽 포트를 열어야 할 수 있습니다(SIL Aggregator Cmdlet 세부 정보 섹션의 `Publish-SilReport` Cmdlet 참조).

-   gMSA 옵션을 사용할 경우:

    -   Active Directory의 gMSA 사용 컴퓨터 그룹에 조인한 후 서버를 다시 부팅 해야 합니다.

    -   설치 프로세스에서 domain\user를 입력할 때 정규화 된 도메인을 사용 하지 않습니다. 예를 들어 **mydomain\gmsaaccount**를 사용 합니다. **Mydomain을 입력 하지<i> </i> 않습니다. \gmsaaccount**

-   사용자 환경에서 Windows Management Framework를 사용 하는 경우:

    -   SILA가 설치 된 서버에 WMF 5.1가 설치 되어 있지 않아야 합니다.  DLL **' mpunits. d s s '** 와 관련 된 이벤트 로그에서 오류를 발생 시킬 수 있습니다.  이렇게 하면 제대로 작동 하지 않습니다.  SILA에는 WMF 4.0만 필요 합니다.

## <a name="managing-sil-over-time"></a>시간에 따른 SIL 관리

### <a name="uninstallreinstall-sil-aggregator"></a>SIL Aggregator 제거/다시 설치
SIL Aggregator를 제거했다가 다시 설치해야 하는 경우 기존 및 기록 인벤토리 데이터의 손실 없이 작업을 수행할 수 있습니다. 이 설명서에 제공된 단계에 따라 제거하고 소프트웨어 인벤토리 로깅 데이터베이스 유지 옵션을 선택하면 됩니다. 그런 다음 이 설명서에 제공된 단계에 따라 SIL Aggregator를 다시 설치하고 기존 데이터베이스에 연결하는 옵션을 선택합니다.

이 작업을 수행한 후 SIL Aggregator에서 이전에 폴링한 모든 호스트에서 `Add-SilVMHost` cmdlet을 사용하여 자격 증명을 업데이트해야 합니다. 이때 해당 호스트에서 데이터 수집을 계속한다고 가정합니다. 또한 보고서에서 동일한 호스트에 대한 중복 입력을 방지하려면 원래 추가한 것과 동일한 네트워크 주소를 사용하여 폴링하도록 호스트를 다시 추가해야 합니다. 다음은 `Add-SilVMHost` cmdlet을 사용하여 호스트를 추가하는 데 사용할 수 있는 세 가지 지원되는 vmhostname 유형입니다.

-   IP 주소

-   FQDN(정규화된 도메인 이름)

-   NetBIOS 이름

### <a name="changing-sil-aggregators"></a>SIL Aggregator 변경
다른 SIL Aggregator가 있는 환경에서 서버 인벤토리 만들기를 시작하려면 해당 서버에서 SIL cmdlet을 사용하여 인증서 지문(필요한 경우) 및 targeturi(`Set-SilLogging –TargetUri`)를 변경하면 됩니다. 이 작업을 수행한 후 `Publish-SilData` cmdlet을 한 번 이상 사용하여 새로 지정된 SIL Aggregator에 전체 인벤토리를 전달해야 합니다.

### <a name="changing-or-updating-certificates"></a>인증서 변경 또는 업데이트
**데이터 손실을 방지 하는 중요 한 단계:** 서버에서 SIL 집계에 데이터를 전달 하는 데 사용 하는 인증서를 변경 해야 하지만 대상 집계는 동일 하 게 유지 되는 경우 다음 단계를 사용 하 여 집계로의 전송에서 잠재적 데이터 손실을 방지 합니다.

-   SIL Aggregator에서 `Set-SilAggregator –AddCertificateThumbprint` cmdlet을 사용하여 새 지문을 SIL Aggregator에 추가합니다.

-   데이터를 전달하는 모든 서버에서 기본 방법을 사용하여 **\LOCALMACHINE\MY**에 사용할 새 인증서를 설치합니다.

-   데이터를 전달하는 모든 서버에서 `Set-SilLogging –CertificateThumbprint` cmdlet을 사용하여 새 인증서의 지문을 업데이트합니다.

-   **업무용 데이터를 전달 하는 모든 서버를 업데이트 한 후에만 cmdlet** 을 사용 하 여 `Set-SilAggregator –RemoveCertificateThumbprint` SIL 집계에서 이전 지문을 제거 합니다. 서버에서 SIL Aggregator에서 제거된 이전 인증서를 사용하여 데이터를 전달하는 경우 **데이터가 손실되고** 집계 중에 데이터베이스에 삽입되지 않습니다. 이는 서버가 이전에 SIL 집계에 데이터를 전달한 경우에만 영향을 주며,이 인증서는 SIL 집계의 지문 목록에서 데이터를 수락 하기 위해 제거 됩니다.

## <a name="release-notes"></a>릴리스 정보

-   SIL Aggregator가 SQL Server Standard Edition 설치의 존재 여부를 처리하지 않고 이에 대해 보고하지 않는 알려진 문제가 있습니다.  이 문제를 해결하는 단계는 다음과 같습니다.

    1.  SIL Aggregator에서 SQL Server Management Studio를 엽니다.

    2.  데이터베이스 엔진에 연결합니다.

    3.  선택 트리에서 SoftwareInventoryLogging 데이터베이스를 확장한 다음 테이블을 확장합니다.

    4.  Dbo를 마우스 오른쪽 단추로 클릭 **합니다. Dbo.sqlserveredition**를 선택한 다음 '**상위 200 행 편집**'을 선택 합니다.

    5.  "Standard Edition" 옆의 PropertyNumValue를 **2760240536** (-1534726760)로 변경 합니다.

    6.  쿼리를 닫아 변경 내용을 저장합니다.

    7.  SIL을 실행 중이며 이미 이 집계에 데이터를 기록한 모든 서버의 경우 SQL Server Standard Edition의 존재 여부를 올바르게 처리하려면 집계에 대해 `Publish-SilData` Cmdlet을 한 번 실행해야 할 수 있습니다.

-   실제 서버에서 하이퍼 스레딩을 사용하도록 설정한 경우 SIL에서 생성한 보고서의 모든 프로세서 코어 수에 스레드 수가 포함됩니다.  하이퍼 스레딩을 사용하도록 설정한 서버에서 실제 코어 수를 가져오려면 이러한 수를 절반으로 줄여야 합니다.

-   Windows Server와 System Center 모두에 대해 레이블이 "**동시에 실행 중**..." 인 행 ( **대시보드** 탭) 및 열 ( **요약 및 세부 정보** 탭)의 합계가 두 위치 간에 정확히 일치 하지 않습니다. **대시보드** 탭에서 "**Windows Server 장치 (알려진 vm 없음**)" 값을 "**동시에 실행 중**..."으로 추가 해야 합니다. **요약 및 세부 정보** 탭에서이 숫자와 동일한 값입니다.

-   이 설명서의 **시간에 따른 SIL 관리** 섹션에서 인증서를 변경하거나 업데이트할 경우 **데이터 손실 방지를 위한 중요 단계** 를 참조하세요.

-   Windows Server 2008 R2 및 Windows Server 2012 호스트를 폴링 호스트 목록에 추가할 수 있지만, 이 버전(1.0)의 SIL Aggregator에서는 Windows/Hyper-V 기반 호스트에서 모든 기능을 사용하도록 Windows Server 2012 R2 폴링만 지원합니다.  특히 Windows Server 2008 R2 호스트를 폴링할 경우 가상 컴퓨터와 호스트를 SIL Aggregator 보고서에서 일치시킬 수 없습니다.

## <a name="see-also"></a>관련 항목
[Windows Server 용 소프트웨어 인벤토리 로깅 집계 1.0](https://www.microsoft.com/en-us/download/details.aspx?id=49046)<br>
[SIL 집계 PowerShell cmdlet](https://technet.microsoft.com/library/mt548455.aspx)<br>
[SIL PowerShell cmdlet](https://technet.microsoft.com/library/dn283390.aspx)<br>
[SIL 개요](https://technet.microsoft.com/library/dn268301.aspx)<br>
[SIL 관리](https://technet.microsoft.com/library/dn383584.aspx)

