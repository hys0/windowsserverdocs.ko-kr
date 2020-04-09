---
title: 소프트웨어 인벤토리 로깅 관리
description: 소프트웨어 인벤토리 로깅을 관리 하는 방법을 설명 합니다.
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.topic: article
ms.assetid: 812173d1-2904-42f4-a9e2-de19effec201
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2176793bd0b7103f69c57476034342a0617329e8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851426"
---
# <a name="manage-software-inventory-logging"></a>소프트웨어 인벤토리 로깅 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

이 문서에서는 데이터 센터 관리자가 시간에 따른 배포에 대 한 Microsoft 소프트웨어 자산 관리 데이터를 쉽게 기록할 수 있도록 하는 소프트웨어 인벤토리 로깅을 관리 하는 방법을 설명 합니다. 이 문서에서는 소프트웨어 인벤토리 로깅을 관리하는 방법에 대해 설명합니다. Windows Server 2012 r 2에서 소프트웨어 인벤토리 로깅을 사용 하기 전에 인벤토리를 만들어야 하는 각 시스템에 Windows 업데이트 [kb 3000850](https://support.microsoft.com/kb/3000850) 및 [kb 3060681](https://support.microsoft.com/kb/3060681) 이 설치 되어 있는지 확인 합니다. Windows Server 2016에는 특별 Dows 업데이트가 필요 하지 않습니다. 이 기능은 인벤토리를 만들 각 서버에서 로컬로 실행됩니다. 원격 서버에서 데이터를 수집하지 않습니다.  

또한 Windows Server 2012 R2 이전의 두 가지 Windows Server 버전에도 소프트웨어 인벤토리 로깅 기능을 추가할 수 있습니다. 다음 업데이트를 설치 하 여 Windows Server 2012 및 Windows Server 2008 R2 s p 1에 소프트웨어 인벤토리 로깅 기능을 추가할 수 있습니다.

- **Windows Server 2012 (Standard 또는 Datacenter Edition)** 

> [!NOTE] 
> 아래의 업데이트 패키지를 적용하기 전에 [WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855)이 설치되어 있는지 확인하세요.

-  Windows Server 2012용 WMF 4.0 업데이트 패키지: [KB 3119938](https://support.microsoft.com/kb/3119938)

- **Windows Server 2008 R2 SP1**

> [!NOTE] 
> 아래의 업데이트 패키지를 적용하기 전에 [WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855)이 설치되어 있는지 확인하세요.


- [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)필요


- Windows Server 2008 R2용 WMF 4.0 업데이트 패키지: [KB 3109118](https://support.microsoft.com/kb/3109118)


이 기능을 사용하여 인벤토리를 만드는 방법에는 기본적으로 두 가지가 있습니다.  
  
1.  매시간 SIL 데이터 원본에서 수집하고 네트워크를 통해 지정된 대상(URI)으로 페이로드를 전달하려면 SIL 로깅 기능을 시작합니다.  
  
2.  임의의 간격으로 SIL 데이터를 수동으로 쿼리하려면 PowerShell 또는 WMI를 사용합니다.  
  
SIL 로깅을 시작하려면 몇 가지 계획 및 예측이 필요하지만 수동으로 데이터를 쿼리하는 것에 비해 상당한 이점이 있습니다. SIL 로깅을 사용하는 경우 데이터 센터 관리자에게 다음과 같은 세 가지 이점이 있습니다.  
  
-   지속적으로 시간별로 기록(로그)을 수집하여 단일 원본에 대해 유연하고 포괄적인 보고서를 얻을 수 있습니다.  
  
-   컴퓨터 검색 시 발생하는 여러 가지 일반적인 인벤토리 도구 문제를 해결할 수 있습니다.  
  
-   데이터가 HTTPS와 SSL을 통해 암호화되므로 보안 수준을 유지하는 동시에 신뢰 경계 문제와 많은 일반 인벤토리 도구에 필요한 관리자 권한 문제를 해결할 수 있습니다.  
  
소프트웨어 인벤토리 로깅은 기본적으로 설치되지만 로깅이 기본적으로 시작되지는 않았습니다. 소프트웨어 인벤토리 로깅의 모든 구성은 PowerShell cmdlet을 통해 수행됩니다. 소프트웨어 인벤토리 로깅에 대한 구성 옵션은 매우 적습니다. 이 문서에서는 이러한 옵션과 원래의 용도 및 데이터 수집에 사용되는 cmdlet에 대해 설명합니다(위의 두 번째 방법을 사용하는 경우).  
  
**이 문서의**  
  
이 문서에서 설명하는 구성 옵션은 다음과 같습니다.  
  
-   [소프트웨어 인벤토리 로깅 시작 및 중지](manage-software-inventory-logging.md#BKMK_Step1)  
  
-   [시간별 소프트웨어 인벤토리 로깅](manage-software-inventory-logging.md#BKMK_Step2)  
  
-   [소프트웨어 인벤토리 로깅 데이터 표시](manage-software-inventory-logging.md#BKMK_Step3)  
  
-   [소프트웨어 인벤토리 로깅에 의해 기록 된 데이터 삭제](manage-software-inventory-logging.md#BKMK_Step4)  
  
-   [소프트웨어 인벤토리 로깅에 의해 기록 된 데이터 백업 및 복원] 관리-소프트웨어-인벤토리-로깅. md # BKMK_Step5)  
  
-   [소프트웨어 인벤토리 로깅에 의해 기록 및 게시 된 데이터 읽기](manage-software-inventory-logging.md#BKMK_Step6)  
  
-   [소프트웨어 인벤토리 로깅 보안](manage-software-inventory-logging.md#BKMK_Step7)  
  
-   [Windows Server 소프트웨어 인벤토리 로깅의 날짜 및 시간 설정 작업](manage-software-inventory-logging.md#BKMK_Step8)  
  
-   [탑재 된 가상 하드 디스크에서 소프트웨어 인벤토리 로깅 사용 및 구성](manage-software-inventory-logging.md#BKMK_Step10)  
  
-   [KB 3000850 없이 Windows Server 2012 r 2에서 소프트웨어 인벤토리 로깅 사용 개요](manage-software-inventory-logging.md#BKMK_Step11)  
  
-   [KB 3000850 없이 Windows Server 2012 R2 Hyper-v 환경에서 소프트웨어 인벤토리 로깅 사용](manage-software-inventory-logging.md#BKMK_Step12)  
  
> [!NOTE]  
> 이 항목에는 설명된 일부 절차를 자동화하는 데 사용할 수 있는 예제 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 Cmdlet 사용을 참조하십시오.

  
## <a name="starting-and-stopping-software-inventory-logging"></a><a name="BKMK_Step1"></a>소프트웨어 인벤토리 로깅 시작 및 중지  
소프트웨어 인벤토리를 기록 하려면 Windows Server 2012 r 2를 실행 하는 컴퓨터에서 소프트웨어 인벤토리 로깅 일별 수집 및 네트워크를 통한 전달이 사용 하도록 설정 되어 있어야 합니다.  
  
> [!NOTE]  
> **[Get-SilLogging](https://technet.microsoft.com/library/dn283396.aspx)** PowerShell cmdlet을 사용하여 실행 또는 중지 여부 등 소프트웨어 인벤토리 로깅 서비스에 대한 정보를 검색할 수 있습니다.  
  
#### <a name="to-start-software-inventory-logging"></a>소프트웨어 인벤토리 로깅을 시작하려면  
  
1.  로컬 관리자 권한이 있는 계정으로 서버에 로그인합니다.  
  
2.  관리자 권한으로 PowerShell을 엽니다.  
  
3.  PowerShell 프롬프트에서 **[Start-SilLogging](https://technet.microsoft.com/library/dn283391.aspx)**  
  
> [!NOTE]  
> 인증서 지문을 설정하지 않고 대상을 설정할 수는 있지만 이 경우 전달이 실패하여 데이터가 최대 30일(기본값) 동안 로컬에 저장됩니다(이후 삭제됨). 유효한 인증서 해시가 대상에 대해 설정되고 해당하는 유효한 인증서가 LocalMachine/개인 저장소에 설치되어 있으면 대상이 이 인증서를 사용하여 이 데이터를 허용하도록 구성된 경우 로컬에 저장된 데이터가 대상에 전달됩니다(자세한 내용은 [Software Inventory Logging Aggregator](Software-Inventory-Logging-Aggregator.md) 참조).  
  
#### <a name="to-stop-software-inventory-logging"></a>소프트웨어 인벤토리 로깅을 중지하려면  
  
1.  로컬 관리자 권한이 있는 계정으로 서버에 로그인합니다.  
  
2.  관리자 권한으로 PowerShell을 엽니다.  
  
3.  PowerShell 프롬프트에서 **[Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)**  
  
## <a name="configuring-software-inventory-logging"></a>소프트웨어 인벤토리 로깅 구성  
시간에 따라 집계 서버로 데이터를 전달하도록 소프트웨어 인벤토리 로깅을 구성하는 단계는 다음과 같이 세 가지입니다.  
  
1.  **Set-sillogging – TargetUri** 를 사용 하 여 집계 서버의 웹 주소 ("https://"로 시작 해야 함)를 지정 합니다.  
  
2.  **Set-SilLogging –CertificateThumbprint** 를 사용하여 집계 서버로의 데이터 전송을 인증하는 데 사용할 유효한 SSL 인증서의 지문 해시를 지정합니다(해시를 허용하도록 집계 서버를 구성해야 함).  
  
3.  네트워크의 유효한 SSL 인증서를 전달되는 데이터가 있는 로컬 서버의 **로컬 컴퓨터/개인 저장소** (또는 **/LocalMachine/MY**)에 설치합니다.  
  
**Start-SilLogging**을 사용하기 전에 이러한 단계를 완료하는 것이 좋습니다.  **Start-SilLogging**을 사용한 후에 사용하려면 SIL을 중지했다가 다시 시작하면 됩니다.  또는 Publish-SilData Cmdlet을 사용하여 집계 서버에 이 서버의 전체 데이터가 있는지 확인할 수 있습니다.  
  
SIL 프레임워크 설정 전반에 대한 포괄적인 가이드는 [Software Inventory Logging Aggregator](software-inventory-logging-aggregator.md)를 참조하세요.  특히 **Publish-SilData** 에서 오류가 발생하거나 다른 이유로 SIL 로깅이 실패하는 경우 문제 해결 섹션을 참조하세요.  
  
## <a name="software-inventory-logging-over-time"></a><a name="BKMK_Step2"></a>시간별 소프트웨어 인벤토리 로깅  
관리자가 소프트웨어 인벤토리 로깅을 시작하면 시간별로 데이터 수집 및 집계 서버(대상 URI)로의 전달이 시작됩니다. 처음에는 특정 시점에 [Get-SilData](https://technet.microsoft.com/library/dn283388.aspx) 가 검색하여 콘솔에 표시한 것과 동일한 전체 데이터 집합이 전달됩니다. 그런 다음 SIL은 각 간격에 따라 데이터를 검사하고 마지막 수집 이후 변경된 데이터가 없으면 작은 식별 응답만 대상 집계 서버로 전달합니다. 값이 변경된 경우 SIL은 전체 데이터 집합을 다시 전송합니다.  
  
> [!IMPORTANT]  
> 임의의 간격에 어떤 이유로든 대상 URI에 연결할 수 없거나 네트워크를 통한 데이터 전송에 실패한 경우 수집된 데이터가 최대 30일(기본값) 동안 로컬에 저장됩니다(이후 삭제됨). 다음에 대상 집계 서버로의 데이터 전달이 성공하면 로컬에 저장된 모든 데이터가 전달되고 로컬에 캐시된 데이터는 삭제됩니다.  
  
## <a name="displaying-software-inventory-logging-data"></a><a name="BKMK_Step3"></a>소프트웨어 인벤토리 로깅 데이터 표시  
이전 섹션에서 설명한 PowerShell cmdlet 외에도 6가지 추가 cmdlet을 사용하여 소프트웨어 인벤토리 로깅 데이터를 수집할 수 있습니다.  
  
-   **[Get-silcomputer](https://technet.microsoft.com/library/dn283392.aspx)** : 사용 가능한 경우 물리적 호스트의 FQDN 또는 호스트 이름 뿐만 아니라 특정 서버 및 운영 체제 관련 데이터에 대 한 특정 시점 값을 표시 합니다.  
  
-   **[Get-silcomputeridentity (KB 3000850)](https://technet.microsoft.com/library/dn858074.aspx)** : 개별 서버에 대해 SIL에서 사용 하는 식별자를 표시 합니다.  
  
-   **[Get-sildata](https://technet.microsoft.com/library/dn283388.aspx)** : 모든 소프트웨어 인벤토리 로깅 데이터의 특정 시점 컬렉션을 표시 합니다.  
  
-   **[Get-silsoftware](https://technet.microsoft.com/library/dn283397.aspx)** : 컴퓨터에 설치 된 모든 소프트웨어의 지정 시간 id를 표시 합니다.  
  
-   **[Get-silualaccess](https://technet.microsoft.com/library/dn283389.aspx)** : 지난 2 일간 서버에 대 한 클라이언트 사용자 요청과 총 고유 클라이언트 장치 요청 수를 표시 합니다.  
  
-   **[Get-silwindowsupdate](https://technet.microsoft.com/library/dn283393.aspx)** : 컴퓨터에 설치 된 모든 Windows 업데이트의 특정 시점 목록을 표시 합니다.  
  
소프트웨어 인벤토리 로깅 cmdlet의 일반적인 사용 사례 시나리오는 관리자가 [Get-SilSoftware](https://technet.microsoft.com/library/dn283397.aspx)를 통해 소프트웨어 인벤토리 로깅을 쿼리하여 모든 소프트웨어 인벤토리 로깅 데이터의 특정 시점 컬렉션을 얻는 것입니다.  
  
**출력 예제**  
  
```  
PS C:\> Get-SilData   
  
ID                 : 961FF8A1-8549-4BEC-8DF6-3B3E32C26FFA  
UUID               : B49ACB4C-7D9C-4806-9917-AE750BB3DA84  
VMGUID             : E84CCCBD-0D0F-486B-A424-9780C7CF92E4  
Name               : Server01Guest.Test.Contoso.com  
HypervisorHostName : Server01.Test.Contoso.com  
  
ID          : {F0C3E5D1-1ADE-321E-8167-68EF0DE699A5}  
Name        : Microsoft Visual C++ 2010  x86 Redistributable - 10.0.40219  
InstallDate : 12/5/2013  
Publisher   : Microsoft Corporation  
Version     : 10.0.40219  
  
ID          : {89F4137D-6C26-4A84-BDB8-2E5A4BB71E00}  
Name        : Microsoft Silverlight  
InstallDate : 3/20/2014  
Publisher   : Microsoft Corporation  
Version     : 5.1.30214.0  
  
ChassisSerialNumber       : 4452-0564-0284-2290-0113-6804-05  
CollectedDateTime         : 10/27/2014 4:01:33 PM  
Model                     : Virtual Machine  
Name                      : Server01Guest.Test.Contoso.com  
NumberOfCores             : 1  
NumberOfLogicalProcessors : 1  
NumberOfProcessors        : 1  
OSName                    : Microsoft Windows Server 2012 R2 Datacenter  
OSSku                     : 8  
OSSuite                   : 400  
OSSuiteMask               : 400  
OSVersion                 : 6.3.9600  
ProcessorFamily           : 179  
ProcessorManufacturer     : GenuineIntel  
ProcessorName             : Intel(R) Xeon(R) CPU           E5440  @ 2.83GHz  
SystemManufacturer        : Microsoft Corporation  
  
```  
  
> [!NOTE]  
> 이 cmdlet의 출력은 이 기능을 위해 함께 사용되는 다른 모든 **Get-Sil** cmdlet과 동일하지만 비동기적으로 콘솔에 제공되어 개체 순서가 항상 같지 않을 수 있습니다.  
>   
> **Get-Sil** cmdlet을 사용하기 위해 소프트웨어 인벤토리 로깅을 시작할 필요는 없습니다.  
  
## <a name="deleting-data-logged-by-software-inventory-logging"></a><a name="BKMK_Step4"></a>소프트웨어 인벤토리 로깅에 의해 기록 된 데이터 삭제  
소프트웨어 인벤토리 로깅은 업무에 필수적인 구성 요소로 고안된 것이 아닙니다. 높은 수준의 안정성을 유지하면서 로컬 시스템 운영에 미치는 영향을 최소화하기 위해 작성되었습니다. 이를 통해 관리자는 소프트웨어 인벤토리 로깅 데이터베이스 및 지원 파일 (\Windows\System32\LogFiles\SIL 디렉터리의 모든 파일)을 수동으로 삭제 하 여 운영 요구 사항을 충족할 수 있습니다.  
  
#### <a name="to-delete-data-logged-by-software-inventory-logging"></a>소프트웨어 인벤토리 로깅에 의해 기록된 데이터를 삭제하려면  
  
1. PowerShell에서 **[Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)** 명령을 사용하여 소프트웨어 인벤토리 로깅을 중지합니다.  
  
2. Windows 탐색기를 엽니다.  
  
3. \Windows\System32\Logfiles\SIL로 이동 **\\**  
  
4. 폴더의 모든 파일을 삭제합니다.  
  
## <a name="backing-up-and-restoring-data-logged-by-software-inventory-logging"></a><a name="BKMK_Step5"></a>소프트웨어 인벤토리 로깅에 의해 기록 된 데이터 백업 및 복원  
네트워크를 통한 전달이 실패한 경우 소프트웨어 인벤토리 로깅은 데이터의 시간별 컬렉션을 일시적으로 저장합니다. 로그 파일은 \Windows\System32\LogFiles\SIL\ 디렉터리에 저장됩니다. 이 소프트웨어 인벤토리 로깅 데이터의 백업은 정기적 서버 백업 일정에 따라 수행할 수 있습니다.  
  
> [!IMPORTANT]  
> 어떤 이유로든 설치 복구 또는 운영 체제의 업그레이드가 필요한 경우 로컬에 저장된 로그 파일이 모두 손실됩니다.  이 데이터가 운영에 중요 한 경우 새 운영 체제를 설치 하기 전에 백업 하는 것이 좋습니다. 복구하거나 업그레이드한 후 동일한 위치에 복원합니다.  
  
> [!NOTE]  
> SIL에 의해 로컬로 기록 되는 데이터의 보존 기간을 관리 하는 이유가 중요할 경우 여기에서 레지스트리 값을 변경 하 여 구성할 수 있습니다. \ HKEY_LOCAL_MACHINE\\SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging. 기본값은 30 일 동안 ' 30 '입니다.  
  
## <a name="reading-data-logged-and-published-by-software-inventory-logging"></a><a name="BKMK_Step6"></a>소프트웨어 인벤토리 로깅에 의해 기록 및 게시 된 데이터 읽기  
SIL에 의해 기록 되었지만 로컬에 저장 되거나 (대상 URI로의 전달이 실패 한 경우) 대상 집계 서버로 성공적으로 전달 된 데이터는 이진 파일 (각 날짜의 데이터)에 저장 됩니다. PowerShell에서 이 데이터를 표시하려면 [Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx) cmdlet을 사용합니다.  
  
## <a name="software-inventory-logging-security"></a><a name="BKMK_Step7"></a>소프트웨어 인벤토리 로깅 보안  
소프트웨어 인벤토리 로깅 WMI 및 PowerShell API에서 데이터를 성공적으로 검색하려면 로컬 서버에 대한 관리자 권한이 필요합니다.  
  
시간별로 계속 집계 지점으로 데이터를 전달하는 소프트웨어 인벤토리 로깅 기능의 전체 기능을 활용하려면 관리자가 클라이언트 인증서를 사용하여 HTTPS를 통한 데이터 전송을 위해 보안 SSL 세션이 되도록 해야 합니다. HTTPS 인증의 기본적인 개요는 [HTTPS 인증](https://technet.microsoft.com/library/cc736680(v=WS.10).aspx)에서 확인할 수 있습니다.  
  
Windows Server에 로컬로 저장된 데이터(기능이 시작되었지만 어떤 이유로든 대상에 연결할 수 없는 경우)는 로컬 서버의 관리자 권한으로만 액세스할 수 있습니다.  
  
## <a name="working-with-date-and-time-settings-in-windows-server-2012-r2-software-inventory-logging"></a><a name="BKMK_Step8"></a>Windows Server 2012 R2 소프트웨어 인벤토리 로깅의 날짜 및 시간 설정 작업  
  
-   [Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TimeOfDay를 사용하여 SIL 로깅이 실행되는 시간을 설정하려면 날짜 및 시간을 지정해야 합니다. 날짜에 도달할 때까지 달력 날짜가 설정 되 고 로컬 시스템 시간에 로깅이 발생 하지 않습니다.  
  
-   [Get-silsoftware](https://technet.microsoft.com/library/dn283397.aspx)또는 [get-silwindowsupdate](https://technet.microsoft.com/library/dn283393.aspx)를 사용 하는 경우 "InstallDate"은 항상 의미 없는 값인 12:00:00am을 표시 합니다.  
  
-   [Get-silualaccess](https://technet.microsoft.com/library/dn283389.aspx)를 사용 하는 경우 "SampleDate"는 항상 의미 없는 값으로 11:59:00pm을 표시 합니다.  날짜는 이러한 cmdlet 쿼리와 관련 된 데이터입니다.  
  
## <a name="enabling-and-configuring-software-inventory-logging-in-a-mounted-virtual-hard-disk"></a><a name="BKMK_Step10"></a>탑재 된 가상 하드 디스크에서 소프트웨어 인벤토리 로깅 사용 및 구성  
소프트웨어 인벤토리 로깅은 오프라인 가상 컴퓨터에서의 구성 및 사용도 지원합니다. 이에 대 한 실용적인 용도는 데이터 센터 전체 배포를 위한 ' 골드 이미지 ' 설치 뿐만 아니라 온-프레미스에서 클라우드 배포로의 최종 사용자 이미지 구성에 사용 하기 위한 것입니다.  
  
이러한 용도를 지원하기 위해 소프트웨어 인벤토리 로깅에는 구성 가능한 각 옵션과 관련된 레지스트리 항목이 있습니다.  이러한 레지스트리 값은 \ HKEY_LOCAL_MACHINE\\SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging.에서 찾을 수 있습니다.  
  
|||||  
|-|-|-|-|  
|**기능**|**값 이름**|**데이터**|**해당 Cmdlet (실행 중인 OS 에서만 사용 가능)**|  
|시작/중지 기능|CollectionState|1 또는 0|[Start-SilLogging](https://technet.microsoft.com/library/dn283391.aspx), [Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)|  
|네트워크의 대상 집계 지점을 지정합니다.|TargetUri|string|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TargetURI|  
|대상 웹 서버에 대한 SSL 인증에 사용되는 인증서 지문 또는 인증서 해시를 지정합니다.|CertificateThumbprint|string|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -CertificateThumbprint|  
|기능을 시작해야 하는 날짜 및 시간을 지정합니다(로컬 시스템 시간을 기준으로 설정된 값이 미래인 경우).|CollectionTime|기본값: 2000-01-01T03:00:00|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TimeOfDay|  
  
오프라인 VHD(실행 중이 아닌 VM OS)에서 이러한 값을 수정하려면 VHD를 먼저 탑재하고 다음 명령을 사용하여 변경해야 합니다.  
  
-   [Reg load](https://technet.microsoft.com/library/cc742053.aspx)  
  
-   [Reg delete](https://technet.microsoft.com/library/cc742145.aspx)  
  
-   [Reg add](https://technet.microsoft.com/library/cc742162.aspx)  
  
-   [Reg unload](https://technet.microsoft.com/library/cc742043.aspx)  
  
OS가 시작되면 소프트웨어 인벤토리 로깅이 이러한 값을 검사하고 적절하게 실행합니다.  
  
## <a name="overview-of-using-software-inventory-logging-in-windows-server-2012-r2-without-kb-3000850"></a><a name="BKMK_Step11"></a>KB 3000850 없이 Windows Server 2012 r 2에서 소프트웨어 인벤토리 로깅 사용 개요  
[KB 3000850](https://support.microsoft.com/kb/3000850)에서는 소프트웨어 인벤토리 로깅 기능 및 기본 설정이 다음과 같이 변경되었습니다.  
  
-   SIL 로깅이 시작될 때 컬렉션 및 네트워크를 통한 전달의 기본 간격이 매일에서 매시간(각 시간 내의 임의 시점)으로 변경되었습니다.  
  
-   Get-SilComputer, Get-SilComputerIdentity 및 Get-SilSoftware의 개체만 포함하도록 기본 데이터 페이로드가 축소되었습니다.  
  
-   Hyper-V 환경에서 채널 통신을 호스트하는 게스트가 제거되었습니다.  
  
## <a name="using-software-inventory-logging-in-a-windows-server-2012-r2-hyper-v-environment-without-kb-3000850"></a><a name="BKMK_Step12"></a>KB 3000850 없이 Windows Server 2012 R2 Hyper-v 환경에서 소프트웨어 인벤토리 로깅 사용  
  
> [!NOTE]  
> [KB 3000850](https://support.microsoft.com/kb/3000850) 업데이트 설치 시 이 기능은 제거됩니다.  
  
Windows Server 2012 R2 Hyper-v 호스트에서 소프트웨어 인벤토리 로깅을 사용 하는 경우 게스트에서 SIL 로깅이 시작 된 경우 로컬에서 실행 되는 Windows Server 2012 R2 게스트에서 SIL 데이터를 검색할 수 있습니다. 그러나 Get-sildata 및 Get-sildata Powershell cmdlet을 사용 하 고 호스트와 게스트 모두에서 WIndows Server 2012 r 2를 사용 하는 경우에만 가능 합니다.  이 기능의 목적은 게스트 Vm을 테 넌 트에 제공 하는 데이터 센터 관리자 또는 대기업의 다른 엔터티를 사용 하 여 하이퍼바이저 호스트에서 소프트웨어 인벤토리 데이터를 캡처한 다음이 모든 데이터를 집계 (또는 대상 URI)로 전달 하는 것입니다.  
  
다음은 SIL 로깅이 시작 된 Windows Server 2012 R2 게스트 VM 하나를 실행 하는 Windows Server 2012 R2 Hyper-v 호스트에서 PowerShell 콘솔의 출력이 표시 되는 것과 같은 두 가지 예입니다.  Get-sildata만 사용 하는 첫 번째 예제에서는 호스트의 모든 데이터가 예상 대로 출력 됩니다.  또한 게스트의 모든 SIL 데이터가 축소 된 형식으로 포함 됩니다.  게스트에서이 데이터를 확장 하 고 보려면 아래의 두 번째 예제에 사용 된 코드 조각을 잘라내어 붙여 넣습니다.  게스트의 SIL 데이터 개체는 항상 개체 내에 연결 된 VM GUID를 갖습니다.  
  
> [!NOTE]  
> SIL 데이터는 콘솔의 출력이므로 Get-SilData cmdlet을 사용하는 경우 데이터 스트림에서 개체가 항상 예측 순서대로 출력되지는 않습니다.  아래의 두 예제에서 텍스트는이 문서에 대 한 설명 도구로만 컬러 코딩 (실제 호스트 데이터의 경우 파란색, 가상 게스트 데이터의 경우 녹색) 되었습니다.  
  
**출력 예 1**  
  
![](../media/software-inventory-logging/SILHyper-VExample1.png)  
  
**출력 예 2** (w/Expand-get-sildata 함수)  
  
![](../media/software-inventory-logging/SILHyper-VExample2.png)  
  
## <a name="see-also"></a>관련 항목  
[소프트웨어 인벤토리 로깅 시작](get-started-with-software-inventory-logging.md)  
[소프트웨어 인벤토리 로깅 집계](software-inventory-logging-aggregator.md)  
[Windows PowerShell의 소프트웨어 인벤토리 로깅 Cmdlet](https://technet.microsoft.com/library/dn283390.aspx)  
[하려면 import-binarymilog](https://technet.microsoft.com/library/dn262592.aspx)  
[내보내기-하려면 import-binarymilog](https://technet.microsoft.com/library/dn262591.aspx)  
  

