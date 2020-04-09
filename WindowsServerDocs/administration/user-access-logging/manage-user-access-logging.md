---
title: 사용자 액세스 로깅 관리
description: 사용자 액세스 로깅을 관리 하는 방법을 설명 합니다.
ms.prod: windows-server
ms.technology: manage-user-access-logging
ms.topic: article
ms.assetid: 4f039017-4152-47eb-838e-bb6ef730b638
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ff33102a2197cc961a44290c5b7e4e3e40b0191
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851386"
---
# <a name="manage-user-access-logging"></a>사용자 액세스 로깅 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 UAL(사용자 액세스 로깅)을 관리하는 방법을 설명합니다.  
  
UAL은 서버 관리자가 로컬 서버에서 역할 및 서비스에 대한 고유한 클라이언트 요청 수를 수치화할 수 있도록 도와주는 기능입니다.  
  
UAL은 기본적으로 설치 및 사용되며, 거의 실시간으로 데이터를 수집합니다. UAL에는 몇 개의 구성 옵션이 있으며, 이 문서에서는 이러한 옵션 및 옵션의 용도에 대해 설명합니다.  
  
UAL의 이점에 대해 자세히 알아보려면 [사용자 액세스 로깅 시작](get-started-with-user-access-logging.md)을 참조 하세요.  
  
**이 문서의**  
  
이 문서에서 설명하는 구성 옵션은 다음과 같습니다.  
  
-   UAL 서비스 사용 안 함 및 사용  
  
-   데이터 수집 및 제거  
  
-   UAL에 의해 기록된 데이터 삭제  
  
-   많은 볼륨 환경에서 UAL 관리  
  
-   손상된 상태로부터 복구  
  
-   작업 폴더 사용 라이선스 추적 사용   
  
## <a name="disabling-and-enabling-the-ual-service"></a><a name="BKMK_Step1"></a>UAL 서비스 사용 안 함 및 사용  
UAL은 Windows Server 2012 이상을 실행 하는 컴퓨터가 설치 되 고 처음 시작 될 때 기본적으로 사용 하도록 설정 되 고 실행 됩니다. 관리자는 다른 운영 요구 사항이나 개인 정보 요구 사항을 준수하기 위해 UAL을 해제하거나 사용하지 않도록 설정할 수 있습니다. 서비스 콘솔을 사용 하거나 명령줄에서 또는 PowerShell cmdlet을 사용 하 여 UAL을 해제할 수 있습니다. 그러나 다음에 컴퓨터를 시작할 때 UAL이 다시 실행 되지 않도록 하려면 서비스를 사용 하지 않도록 설정 해야 합니다. 다음 절차에서는 UAL을 끄고 사용 하지 않도록 설정 하는 방법을 설명 합니다.  
  
> [!NOTE]  
> `Get-Service UALSVC` PowerShell cmdlet을 사용하여 UAL 서비스가 실행 중이거나 중지되었는지 여부 및 UAL 서비스가 사용하도록 설정되었거나 사용하지 않도록 설정되었는지 여부 등을 비롯하여 UAL 서비스에 대한 정보를 검색할 수 있습니다.  
  
#### <a name="to-stop-and-disable-the-ual-service-by-using-the-services-console"></a>서비스 콘솔을 사용하여 UAL 서비스를 중지하고 사용하지 않도록 설정하려면  
  
1.  로컬 관리자 권한이 있는 계정으로 서버에 로그인합니다.  
  
2.  서버 관리자에서 **도구**를 가리킨 다음 **서비스**를 클릭합니다.  
  
3.  아래로 스크롤하고 **User Access Logging Service**를 선택합니다. **서비스 중지**를 클릭합니다.  
  
4.  서비스 이름을 마우스 오른쪽 단추로 클릭 하\-하 고 **속성**을 선택 합니다. **일반** 탭에서 **시작 유형**을 **사용 안 함**으로 변경하고 **확인**을 클릭합니다.  
  
#### <a name="to-stop-and-disable-ual-from-the-command-line"></a>명령줄에서 UAL을 중지하고 사용하지 않도록 설정하려면  
  
1.  로컬 관리자 권한이 있는 계정으로 서버에 로그인합니다.  
  
2.  Windows 로고 + R을 누른 다음 **cmd**를 입력하여 명령 프롬프트 창을 엽니다.  
  
    > [!IMPORTANT]  
    > **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
3.  **net stop ualsvc**를 입력한 다음 Enter 키를 누릅니다.  
  
4.  **netsh ualsvc set opmode mode=disable**을 입력한 다음 Enter 키를 누릅니다.  
   
다음 Windows PowerShell cmdlet은 이전 절차와 동일한 기능을 수행합니다. 서식 조건 때문에 각 cmdlet이 여러 줄로 자동 줄 바꿈되어 표시되더라도 한 줄에 입력합니다.  

Stop-service 및 Disable-Ual Windows PowerShell 명령을 사용하여 UAL을 중지하고 사용하지 않도록 설정할 수도 있습니다.  
  
```  
Stop-service ualsvc  
```  
  
```  
Disable-ual  
```  
  
나중에 UAL을 다시 시작 하 고 다시 사용 하도록 설정 하려는 경우 다음 절차를 수행 하 여 수행할 수 있습니다.  
  
#### <a name="to-start-and-enable-the-ual-service-by-using-the-services-console"></a>서비스 콘솔을 사용하여 UAL 서비스를 시작하고 사용하도록 설정하려면  
  
1.  로컬 관리자 권한이 있는 계정으로 서버에 로그인합니다.  
  
2.  서버 관리자에서 **도구**를 가리킨 다음 **서비스**를 클릭합니다.  
  
3.  아래로 스크롤하고 **User Access Logging Service**를 선택합니다. **서비스 시작**을 클릭합니다.  
  
4.  서비스 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다. **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
#### <a name="to-start-and-enable-ual-from-the-command-line"></a>명령줄에서 UAL을 시작하고 사용하도록 설정하려면  
  
1.  로컬 관리자 자격 증명으로 서버에 로그인합니다.  
  
2.  Windows 로고 + R을 누른 다음 **cmd**를 입력하여 명령 프롬프트 창을 엽니다.  
  
    > [!IMPORTANT]  
    > **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
3.  **net start ualsvc**를 입력한 다음 Enter 키를 누릅니다.  
  
4.  **netsh ualsvc set opmode mode=enable**을 입력한 다음 Enter 키를 누릅니다.  

다음 Windows PowerShell cmdlet은 이전 절차와 동일한 기능을 수행합니다. 서식 조건 때문에 각 cmdlet이 여러 줄로 자동 줄 바꿈되어 표시되더라도 한 줄에 입력합니다.
  
Start-service 및 Enable-Ual Windows PowerShell 명령을 사용하여 UAL을 시작하고 다시 사용하도록 설정할 수도 있습니다.  
  
```  
Enable-ual  
```  
  
```  
Start-service ualsvc  
```  
  
## <a name="collecting-ual-data"></a><a name="BKMK_Step2"></a>UAL 데이터 수집  
이전 섹션에서 설명한 PowerShell cmdlet 외에도, 12 개의 추가 cmdlet을 사용 하 여 UAL 데이터를 수집할 수 있습니다.  
  
-   **Get-UalOverview**: 설치된 제품 및 역할에 대한 UAL 관련 세부 정보 및 기록을 제공합니다.  
  
-   **Get-UalServerUser**: 로컬 또는 대상 서버의 클라이언트 사용자 액세스 데이터를 제공합니다.  
  
-   **Get-UalServerDevice**: 로컬 또는 대상 서버의 클라이언트 장치 액세스 데이터를 제공합니다.  
  
-   **Get-UalUserAccess**: 로컬 또는 대상 서버에 설치된 각 역할이나 제품의 클라이언트 사용자 액세스 데이터를 제공합니다.  
  
-   **Get-UalDeviceAccess**: 로컬 또는 대상 서버에 설치된 각 역할이나 제품의 클라이언트 장치 액세스 데이터를 제공합니다.  
  
-   **Get-UalDailyUserAccess**: 각 날짜의 클라이언트 사용자 액세스 데이터를 제공합니다.  
  
-   **Get-UalDailyDeviceAccess**: 각 날짜의 클라이언트 장치 액세스 데이터를 제공합니다.  
  
-   **Get-UalDailyAccess**: 각 날짜의 클라이언트 장치 액세스 데이터 및 사용자 액세스 데이터를 모두 제공합니다.  
  
-   **Get-UalHyperV**: 로컬 또는 대상 서버와 관련된 가상 컴퓨터 데이터를 제공합니다.  
  
-   **Get-UalDns**: 로컬 또는 대상 DNS 서버의 DNS 클라이언트 관련 데이터를 제공합니다.  
  
-   **Get-UalSystemId**: 로컬 또는 대상 서버를 고유하게 식별하는 시스템 관련 데이터를 제공합니다.  
  
`Get-UalSystemId`는 연결할 해당 서버의 다른 모든 데이터에 대한 서버의 고유 프로필을 제공합니다.  서버에서 `Get-UalSystemId`의 매개 변수 중 하나에 변경 내용이 발생 하는 경우 새 프로필이 만들어집니다.  `Get-UalOverview` 는 서버에서 설치되고 사용 중인 역할 목록을 관리자에게 제공합니다.  
  
> [!NOTE]  
> 인쇄 및 문서 서비스 및 파일 서비스의 기본 기능은 기본적으로 설치 됩니다. 따라서 관리자는 전체 역할이 설치된 것처럼 표시된 이 기능에 대한 정보를 항상 볼 수 있습니다. 이러한 서버 역할에 대해 UAL이 수집 하는 고유한 데이터로 인해 Hyper-v 및 DNS에 대 한 별도의 UAL cmdlet이 포함 됩니다.  
  
UAL cmdlet에 대한 일반적인 사용 사례 시나리오는 날짜 범위 동안 관리자가 고유한 클라이언트 액세스에 대한 UAL을 쿼리하는 것입니다. 이 작업은 다양 한 방법으로 수행할 수 있습니다. 다음은 날짜 범위 동안 고유한 장치 액세스를 쿼리 하는 데 권장 되는 방법입니다.  
  
```  
PS C:\Windows\system32>Gwmi -Namespace "root\AccessLogging" -query "SELECT * FROM MsftUal_DeviceAccess WHERE LastSeen >='1/01/2013' and LastSeen <='3/31/2013'"  
  
```  
  
이 방법은 해당 날짜 범위 동안 서버에 요청을 보낸 고유한 모든 클라이언트 디바이스에 대한 자세한 목록을 IP 주소별로 반환합니다.  
  
각 고유 클라이언트에 대 한 ' ActivityCount '는 하루 65535 개로 제한 됩니다. 또한 PowerShell에서 WMI를 호출 하는 것은 날짜별로 쿼리할 때만 필요 합니다.  다른 모든 UAL cmdlet 매개 변수는 다음 예제와 같이 예상 대로 PS 쿼리 내에서 사용할 수 있습니다.  
  
```  
PS C:\Windows\system32> Get-UalDeviceAccess -IPAddress "10.36.206.112"  
  
ActivityCount    : 1  
FirstSeen        : 6/23/2012 5:06:50 AM  
IPAddress        : 10.36.206.112  
LastSeen         : 6/23/2012 5:06:50 AM  
ProductName      : Windows Server 2012 Datacenter  
RoleGuid         : 10a9226f-50ee-49d8-a393-9a501d47ce04  
RoleName         : File Server  
TenantIdentifier : 00000000-0000-0000-0000-000000000000  
PSComputerName  
  
```  
  
UAL은 최대 2 년 분량의 기록을 보유 합니다. 관리자가 서비스를 실행 하는 동안 UAL 데이터를 검색 하도록 허용 하려면 UAL은 WMI 공급자의 사용을 위해 24 시간 마다 *GUID .mdb* 파일에 대해 활성 데이터베이스 파일 (현재 .mdb)의 복사본을 만듭니다.  
  
UAL은 한 해의 첫날에 새 *GUID.mdb*를 만듭니다. 이전 GUID는 공급자의 용도에 대 한 보관으로 보관 됩니다 *.*  2년이 지나면 원본 *GUID.mdb*를 덮어씁니다.  
  
> [!IMPORTANT]  
> 다음 절차는 고급 사용자만 수행할 수 있으며, 일반적으로 개발자가 UAL 애플리케이션 프로그래밍 인터페이스의 자체 계측을 테스트하기 위해 사용합니다...  
  
#### <a name="to-adjust-the-default-24-hour-interval-to-make-data-visible-to-the-wmi-provider"></a>WMI 공급자에 데이터를 표시하는 기본 24시간 간격을 조정하려면  
  
1.  로컬 관리자 권한이 있는 계정으로 서버에 로그인합니다.  
  
2.  Windows 로고 + R을 누른 다음 **cmd**를 입력하여 명령 프롬프트 창을 엽니다.  
  
3.  다음 레지스트리 값을 추가합니다.  **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\WMI\AutoLogger\Sum\PollingInterval (REG_DWORD)** .  
  
    > [!WARNING]  
    > 레지스트리를 잘못 편집하면 시스템이 크게 손상될 수 있습니다. 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 반드시 백업해야 합니다.  
  
    다음 예제는 2 분 간격 (장기 실행 상태로 권장 되지 않음)을 추가 하는 방법을 보여 줍니다. **REG add HKLM\System\CurrentControlSet\Control\WMI\\AutoLogger\Sum/V PollingInterval/T REG\_DWORD/d 12만/f**  
  
    시간 값은 밀리초 단위입니다. 최소값은 60초이고 최대 값은 7일이며 기본값은 24시간입니다.  
  
4.  서비스 콘솔을 사용하여 User Access Logging Service 중지하고 다시 시작합니다.  
  
## <a name="deleting-data-logged-by-ual"></a>UAL에 의해 기록된 데이터 삭제  
UAL은 업무에 필수적인 구성 요소로 고안된 구성 요소가 아닙니다. 높은 수준의 안정성을 유지하면서 로컬 시스템 운영에 미치는 영향을 최소화하기 위해 작성되었습니다. 이를 통해 관리자는 운영 요구 사항을 충족 하기 위해 UAL 데이터베이스 및 지원 파일 (\Windows\System32\LogFilesSUM\ 디렉터리의 모든 파일)을 수동으로 삭제할 수 있습니다.  
  
#### <a name="to-delete-data-logged-by-ual"></a>UAL에 의해 기록된 데이터를 삭제하려면  
  
1. User Access Logging Service 중지합니다.  
  
2. Windows 탐색기를 엽니다.  
  
3. **\Windows\System32\Logfiles\SUM\\** 로 이동 합니다.  
  
4. 폴더의 모든 파일을 삭제합니다.  
  
## <a name="managing-ual-in-high-volume-environments"></a>많은 볼륨 환경에서 UAL 관리  
이 섹션에서는 UAL이, 클라이언트 볼륨이 많은 서버에서 사용된 경우 관리자가 예상할 수 있는 항목에 대해 설명합니다.  
  
UAL에서 기록할 수 있는 최대 액세스 수는 하루에 65,535회입니다.  인터넷에 직접 연결 된 웹 서버와 같이 인터넷에 직접 연결 된 서버 또는 매우 높은 성능이 서버의 주요 기능 (예: HPC 워크 로드 환경) 인 경우에는 UAL을 사용 하지 않는 것이 좋습니다. UAL은 정기적으로 인터넷 연결 트래픽 볼륨을 제공 하는 많은 수의 배포 뿐만 아니라 많은 볼륨이 예상 되는 중소 규모의 엔터프라이즈 인트라넷 시나리오에 적합 합니다.  
  
**Ual 메모리**: UAL은 ESE (Extensible Storage Engine)를 사용 하므로 ual의 메모리 요구 사항은 시간이 지나면서 또는 클라이언트 요청 양에 따라 증가 합니다. 하지만 시스템 성능에 미치는 영향을 최소화해야 하므로 메모리는 무시됩니다.  
  
**Ual 디스크**: ual의 하드 디스크 요구 사항은 대략 다음과 같습니다.  
  
-   0개의 고유한 클라이언트 레코드: 22M  
  
-   50,000개의 고유한 클라이언트 레코드: 80M  
  
-   500,000개의 고유한 클라이언트 레코드: 384M  
  
-   1,000,000개의 고유한 클라이언트 레코드: 729M  
  
## <a name="recovering-from-a-corrupt-state"></a>손상된 상태로부터 복구  
이 섹션에서는 높은 수준에서 UAL의 ESE (Extensible Storage Engine) 사용 및 UAL 데이터가 손상 되거나 복구 불능 상태일 경우 관리자가 수행할 수 있는 작업에 대해 설명 합니다.  
  
UAL은 ESE를 사용하여 시스템 리소스 사용 및 손상에 대한 저항을 최적화합니다.  ESE 이점에 대한 자세한 내용은 MSDN에서 [Extensible Storage Engine](https://msdn.microsoft.com/library/windows/desktop/gg269259(v=exchg.10).aspx) (영문)을 참조하세요.  
  
UAL 서비스가 시작될 때마다 ESE에서 소프트 복구를 수행합니다. 자세한 내용은 MSDN에서 [Extensible Storage Engine 파일](https://msdn.microsoft.com/library/windows/desktop/gg294069(v=exchg.10).aspx) (영문)을 참조하세요.  
  
소프트웨어 복구에 문제가 있으면 ESE가 크래시 복구를 수행합니다. 자세한 내용은 MSDN에서의 [JetInit 함수](https://msdn.microsoft.com/library/windows/desktop/gg294068(v=exchg.10).aspx) (영문)를 참조하세요.  
  
UAL이 계속해서 기존의 ESE 파일 집합을 사용하여 시작할 수 없는 경우 UAL은 \Windows\System32\LogFiles\SUM\ 디렉터리에서 모든 파일을 삭제합니다. 이 파일이 삭제되면 User Access Logging Service 다시 시작되고 새 파일이 만들어집니다. 그러면 새로 설치된 컴퓨터에서처럼 UAL 서비스가 다시 시작됩니다.  
  
> [!IMPORTANT]  
> UAL 데이터베이스 디렉터리의 파일은 이동하거나 수정하면 안 됩니다. 이 파일을 이동하거나 수정할 경우 이 섹션에 설명된 정리 루틴을 비롯한 복구 단계가 시작됩니다. \Windows\System32\LogFiles\SUM\ 디렉터리를 백업해야 할 경우 이 디렉터리의 모든 파일을 같이 백업해야 복원 작업이 제대로 수행됩니다.  
  
## <a name="enable-work-folders-usage-license-tracking"></a>작업 폴더 사용 라이선스 추적 사용  
작업 폴더 서버는 UAL을 사용하여 클라이언트 사용 현황을 보고할 수 있습니다. UAL과 달리 작업 폴더 로깅은 기본적으로 켜져 있지 않습니다. 다음과 같이 레지스트리 키를 변경하여 사용하도록 설정할 수 있습니다.  
  
```  
Reg add HKLM\Software\Microsoft\Windows\CurrentVersion\SyncShareSrv /v EnableWorkFoldersUAL /t REG_DWORD /d 1  
```  
  
로깅을 사용하도록 설정하려면 레지스트리 키를 추가한 후 서버에서 SyncShareSvc 서비스를 다시 시작해야 합니다.  
  
로깅 기능을 사용하도록 설정하면 클라이언트가 서버에 연결할 때마다 Windows 로그\응용 프로그램 채널에 2 정보 이벤트가 기록됩니다. 작업 폴더의 경우 각 사용자에게 서버에 연결하고 10분마다 데이터 업데이트를 확인하는 하나 이상의 클라이언트 디바이스가 있을 수 있습니다. 서버에서 1000명의 사용자가 발생하고 각 사용자에게 2개의 디바이스가 있는 경우 70분마다 응용 프로그램 로그를 덮어쓰므로 관련되지 않은 문제 해결이 어려워집니다. 이를 방지 하기 위해 사용자 액세스 로깅 서비스를 일시적으로 사용 하지 않도록 설정 하거나 서버의 Windows Logs\Application 채널 크기를 늘릴 수 있습니다.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목  

- [사용자 액세스 로깅 시작](get-started-with-user-access-logging.md)
  

