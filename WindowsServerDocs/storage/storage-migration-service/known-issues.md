---
title: 저장소 마이그레이션 서비스의 알려진 문제
description: Microsoft 지원에 대 한 로그를 수집 하는 방법과 같은 저장소 마이그레이션 서비스에 대 한 알려진 문제 및 문제 해결 지원.
author: nedpyle
ms.author: nedpyle
manager: tiaascs
ms.date: 02/10/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: a9759f0ea8835c8e07bcd298b75024e3ee29c9ed
ms.sourcegitcommit: b5c12007b4c8fdad56076d4827790a79686596af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78856347"
---
# <a name="storage-migration-service-known-issues"></a>저장소 마이그레이션 서비스의 알려진 문제

이 항목에는 [저장소 마이그레이션 서비스](overview.md) 를 사용 하 여 서버를 마이그레이션할 때 알려진 문제에 대 한 답변이 포함 되어 있습니다.

Storage Migration Service는 Windows Server의 서비스와 Windows 관리 센터의 사용자 인터페이스의 두 부분으로 릴리스됩니다. 이 서비스는 windows server, 장기 서비스 채널 뿐만 아니라 Windows Server, 반기 채널에서 사용할 수 있습니다. Windows 관리 센터는 별도 다운로드로 사용할 수 있습니다. 또한 Windows 업데이트를 통해 출시 되는 Windows Server의 누적 업데이트에 대 한 변경 내용을 정기적으로 포함 합니다. 

예를 들어 Windows Server, 버전 1903에는 저장소 마이그레이션 서비스에 대 한 새로운 기능 및 수정이 포함 되어 있습니다 .이 서비스는 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)를 설치 하 여 windows server 2019 및 windows server 버전 1809 에서도 사용할 수 있습니다.

## <a name="collecting-logs"></a>Microsoft 지원 작업할 때 로그 파일을 수집 하는 방법

저장소 마이그레이션 서비스에는 Orchestrator 서비스와 프록시 서비스에 대 한 이벤트 로그가 포함 되어 있습니다. Orchestrator 서버는 항상 두 이벤트 로그를 모두 포함 하 고 프록시 서비스를 설치한 대상 서버는 프록시 로그를 포함 합니다. 이러한 로그는 다음 위치에 있습니다.

- 응용 프로그램 및 서비스 로그 \ Microsoft \ Windows \ StorageMigrationService
- 응용 프로그램 및 서비스 로그 \ Microsoft \ Windows \ StorageMigrationService-프록시

오프 라인으로 보거나 Microsoft 지원에 보내기 위해 이러한 로그를 수집 해야 하는 경우 GitHub에서 사용할 수 있는 오픈 소스 PowerShell 스크립트가 있습니다.

 [저장소 마이그레이션 서비스 도우미](https://aka.ms/smslogs) 

사용에 대 한 추가 정보를 검토 합니다.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Windows Server 2019를 관리 하지 않는 경우 Windows 관리 센터에 저장소 마이그레이션 서비스가 표시 되지 않음

Windows 관리 센터 1809 버전을 사용 하 여 Windows Server 2019 orchestrator를 관리 하는 경우 Storage Migration Service에 대 한 도구 옵션이 표시 되지 않습니다. 

Windows 관리 센터 저장소 마이그레이션 서비스 확장은 Windows Server 2019 버전 1809 이상 운영 체제만 관리 하기 위해 버전에 바인딩되어 있습니다. 이전 Windows Server 운영 체제 또는 insider preview를 관리 하는 데 사용 하는 경우 도구는 표시 되지 않습니다. 이 동작은 의도된 것입니다. 

문제를 해결 하려면 Windows Server 2019 빌드 1809 이상 버전을 사용 하거나 업그레이드 합니다.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>"대상 컴퓨터에서 토큰 필터 정책에 대 한 액세스가 거부 되었습니다." 오류로 인해 저장소 마이그레이션 서비스에서 유효성 검사가 실패 함

유효성 검사를 반복할 때 "실패: 대상 컴퓨터에서 토큰 필터 정책에 대 한 액세스가 거부 되었습니다." 오류가 표시 됩니다. 원본 및 대상 컴퓨터에 대 한 올바른 로컬 관리자 자격 증명을 제공한 경우에도이 문제가 발생 합니다.

이 문제는 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 업데이트에서 해결 되었습니다. 

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage Migration Service는 Windows Server 2019 Evaluation 또는 Windows Server 2019 Essentials edition에 포함 되어 있지 않습니다.

Windows 관리 센터를 사용 하 여 [Windows server 2019 Evaluation 릴리스](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 또는 windows Server 2019 Essentials 버전에 연결 하는 경우 저장소 마이그레이션 서비스를 관리할 수 있는 옵션이 없습니다. Storage Migration Service는 역할 및 기능에도 포함 되어 있지 않습니다.

이 문제는 Windows Server 2019 및 Windows Server 2019 Essentials의 평가용 미디어에서 서비스 문제로 인해 발생 합니다. 

평가를 위해이 문제를 해결 하려면 Windows Server 2019의 정품, MSDN, OEM 또는 볼륨 라이선스 버전을 설치 하 고 활성화 하지 마십시오. 정품 인증을 사용 하지 않으면 모든 버전의 Windows Server가 180 일간 평가 모드로 작동 합니다. 

이후 버전의 Windows Server에서는이 문제가 해결 되었습니다.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>저장소 마이그레이션 서비스에서 전송 오류 CSV 다운로드 시간 초과

Windows 관리 센터 또는 PowerShell을 사용 하 여 전송 작업에 대 한 자세한 오류 전용 CSV 로그를 다운로드 하는 경우 오류 메시지가 표시 됩니다.

 >   전송 로그-방화벽에서 파일 공유를 사용할 수 있는지 확인 하세요. :이 요청 작업이 net.tcp:/localhost: 28940/sms/service/1/transfer에서 구성 된 시간 제한 (00:01:00) 내에 회신을 받지 못했습니다. 이 작업에 할당된 시간이 보다 긴 시간 제한의 일부일 수 있습니다. 서비스가 아직 작업을 처리 중이거나 서비스가 회신 메시지를 보낼 수 없었기 때문일 수 있습니다. 채널/프록시를 IContextChannel로 캐스팅 하 고 OperationTimeout 속성을 설정 하 여 작업 시간 제한을 늘리고 서비스가 클라이언트에 연결할 수 있는지 확인 하세요.

이 문제는 저장소 마이그레이션 서비스에서 허용 하는 기본 1 분 제한 시간 내에 필터링 할 수 없는 너무 많은 전송 된 파일에 의해 발생 합니다. 

이 문제를 해결하려면

1. Orchestrator 컴퓨터에서 Notepad.exe를 사용 하 여 *%SYSTEMROOT%\SMS\Microsoft.StorageMigration.Service.exe.config* 파일을 편집 하 여 "sendTimeout"를 1 분 기본값에서 10 분으로 변경 합니다.

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Orchestrator 컴퓨터에서 "Storage Migration Service" 서비스를 다시 시작 합니다. 
3. Orchestrator 컴퓨터에서 Regedit.exe를 시작 합니다.
4. 다음 레지스트리 하위 키를 찾아 클릭합니다. 

   `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. 편집 메뉴에서 새로 만들기를 가리키고 DWORD 값을 클릭합니다. 
6. DWORD 이름에 "WcfOperationTimeoutInMinutes"를 입력 한 다음 ENTER 키를 누릅니다.
7. "WcfOperationTimeoutInMinutes"을 마우스 오른쪽 단추로 클릭 한 다음 수정을 클릭 합니다. 
8. 기본 데이터 상자에서 "10 진수"를 클릭 합니다.
9. 값 데이터 상자에 "10"을 입력 한 다음 확인을 클릭 합니다.
10. 레지스트리 편집기를 종료 합니다.
11. 오류 전용 CSV 파일 다운로드를 다시 시도 합니다. 

이후 버전의 Windows Server 2019에서이 동작을 변경 하려고 합니다.  

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>대상 프록시 및 자격 증명 관리 권한에 대 한 유효성 검사 경고

전송 작업의 유효성을 검사할 때 다음과 같은 경고가 표시 됩니다.

 > **자격 증명에는 관리 권한이 있습니다.**
 > 경고: 원격으로 작업을 사용할 수 없습니다.
 > **대상 프록시가 등록 되었습니다.**
 > 경고: 대상 프록시를 찾을 수 없습니다.

Windows Server 2019 대상 컴퓨터에 저장소 마이그레이션 서비스 프록시 서비스를 설치 하지 않았거나 대상 컴퓨터가 Windows Server 2016 또는 Windows Server 2012 r 2 인 경우이 동작은 의도적으로 설계 된 것입니다. 전송 성능을 크게 개선 하기 위해 프록시가 설치 된 Windows Server 2019 컴퓨터로 마이그레이션하는 것이 좋습니다.  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>특정 파일은 인벤토리 또는 전송 하지 않으며 오류 5 "액세스가 거부 되었습니다."

원본 컴퓨터에서 대상 컴퓨터로 파일을 인벤토리 또는 전송 하는 경우 사용자가 관리자 그룹 권한을 제거 하는 파일은 마이그레이션하지 못합니다. 저장소 마이그레이션 서비스 검사-프록시 디버그는 다음을 보여 줍니다.

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          2/26/2019 9:00:04 AM
    Event ID:      10000
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      srv1.contoso.com
    Description:

    02/26/2019-09:00:04.860 [Error] Transfer error for \\srv1.contoso.com\public\indy.png: (5) Access is denied.
    Stack Trace:
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile(String fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes)
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(String path)
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(FileInfo file)
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo()
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer()
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer()   

이 문제는 저장소 마이그레이션 서비스에서 백업 권한이 호출 되지 않은 코드 오류로 인해 발생 합니다. 

이 문제를 해결 하려면 오 케 스트레이 터 컴퓨터에 [KB4490481 (OS 빌드 17763.404)를 Windows 업데이트](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) 설치 하 고 프록시 서비스가 설치 된 경우 대상 컴퓨터에 설치 합니다. 원본 마이그레이션 사용자 계정이 원본 컴퓨터 및 저장소 마이그레이션 서비스 orchestrator의 로컬 관리자 인지 확인 합니다. 대상 마이그레이션 사용자 계정이 대상 컴퓨터 및 저장소 마이그레이션 서비스 orchestrator의 로컬 관리자 인지 확인 합니다. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>저장소 마이그레이션 서비스를 사용 하 여 데이터를 사전 시드 하는 경우 DFSR 해시가 일치 하지 않음

저장소 마이그레이션 서비스를 사용 하 여 파일을 새 대상으로 전송 하는 경우, 미리 시드 된 복제 또는 DFSR 데이터베이스 복제를 통해 기존 DFSR 서버와 해당 데이터를 복제 하도록 DFSR (DFS 복제)을 구성 하면 모든 파일에서 해시가 발생 합니다. 불일치 및가 다시 복제 됩니다. SMS를 사용 하 여 전송 하 고 나면 데이터 스트림, 보안 스트림, 크기 및 특성이 모두 정확히 일치 하는 것으로 나타납니다. ICACLS 또는 DFSR 데이터베이스 복제 디버그 로그를 사용 하 여 파일을 검사 하면 다음과 같은 결과가 나타납니다.

원본 파일:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png/save D:AI (A;; FA;;; BA) (A;; 0) x1200a9;;D D) (A;; 0) x1301bf;;D U) (A; ID; FA;;;) BA) (A; ID; FA;;;) SY) (A; ID; 0x1200a9;;;) BU

대상 파일:

  icacls d:\test\thatcher.png/save D:AI (A;; FA;;; BA) (A;; 0) x1301bf;;D U) (A;; 0) x1200a9;;D D) (A; ID; FA;;;) BA) (A; ID; FA;;;) SY) (A; ID; 0x1200a9;;;) BU)**S: PAINO_ACCESS_CONTROL**

DFSR 디버그 로그:

    20190308 10:18:53.116 3948 DBCL  4045 [WARN] DBClone::IDTableImportUpdate Mismatch record was found. 

    Local ACL hash:1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 
    LastWriteTime:20190308 18:09:44.876 
    FileSizeLow:1131654 
    FileSizeHigh:0 
    Attributes:32 

    Clone ACL hash:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** 
    LastWriteTime:20190308 18:09:44.876 
    FileSizeLow:1131654 
    FileSizeHigh:0 
    Attributes:32 

이 문제는 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 업데이트에 의해 해결 됩니다.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Windows Server 2008 r 2에서 전송할 때 "모든 끝점에서 저장소를 전송할 수 없음" 오류

Windows Server 2008 R2 원본 컴퓨터에서 데이터를 전송 하려고 할 때 데이터를 전송 하지 않고 오류를 수신 합니다.  

    Couldn't transfer storage on any of the endpoints.
    0x9044

이 오류는 Windows Server 2008 R2 컴퓨터가 Windows 업데이트의 모든 중요 및 중요 업데이트를 사용 하 여 완전히 패치 되지 않은 경우에 발생 합니다. 저장소 마이그레이션 서비스와 관계 없이, 운영 체제에 최신 버전의 Windows Server에 대 한 보안 향상 기능이 포함 되어 있지 않기 때문에 보안을 위해 Windows Server 2008 R2 컴퓨터에 패치를 적용 하는 것이 좋습니다.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>"끝점에서 저장소를 전송 하지 못했습니다." 및 "원본 장치가 온라인 상태 인지 확인-액세스할 수 없습니다." 라는 오류가 발생 합니다.

원본 컴퓨터에서 데이터를 전송 하려고 하면 일부 또는 모든 공유가 전송 되지 않고 요약 오류가 발생 합니다.

    Couldn't transfer storage on any of the endpoints.
    0x9044

SMB 전송 세부 정보를 검사 하면 오류가 표시 됩니다.

    Check if the source device is online - we couldn't access it.

StorageMigrationService/Admin 이벤트 로그를 검사 하면 다음이 표시 됩니다.

    Couldn't transfer storage.

    Job: Job1
    ID:  
    State: Failed
    Error: 36931
    Error Message: 

   지침: 자세한 오류를 확인 하 고 전송 요구 사항이 충족 되는지 확인 합니다. 전송 작업에서 원본 및 대상 컴퓨터를 전송할 수 없습니다. 이는 방화벽 규칙 또는 권한 누락으로 인해 오 케 스트레이 터 컴퓨터가 원본 또는 대상 컴퓨터에 연결할 수 없기 때문일 수 있습니다.

StorageMigrationService-프록시/디버그 로그를 검사 하면 다음이 표시 됩니다.

    07/02/2019-13:35:57.231 [Error] Transfer validation failed. ErrorCode: 40961, Source endpoint is not reachable, or doesn't exist, or source credentials are invalid, or authenticated user doesn't have sufficient permissions to access it.
    at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferOperation.Validate()
    at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferRequestHandler.ProcessRequest(FileTransferRequest fileTransferRequest, Guid operationId)    

이는 마이그레이션 계정에 SMB 공유에 대 한 최소한의 읽기 권한이 없는 경우에 매니페스트 되는 코드 오류 였습니다. 이 문제는 누적 업데이트 [4520062](https://support.microsoft.com/help/4520062/windows-10-update-kb4520062)에서 처음으로 수정 되었습니다. 

## <a name="error-0x80005000-when-running-inventory"></a>인벤토리를 실행 하는 경우 오류 0x80005000

[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 를 설치 하 고 인벤토리 실행을 시도한 후 인벤토리가 실패 하 고 오류가 발생 합니다.

    EXCEPTION FROM HRESULT: 0x80005000
  
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          9/9/2019 5:21:42 PM
    Event ID:      2503
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      FS02.TailwindTraders.net
    Description:
    Couldn't inventory the computers.
    Job: foo2
    ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b
    State: Failed
    Error: 36934
    Error Message: Inventory failed for all devices
    Guidance: Check the detailed error and make sure the inventory requirements are met. The job couldn't inventory any of the specified source computers. This could be because the orchestrator computer couldn't reach it over the network, possibly due to a firewall rule or missing permissions.
  
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          9/9/2019 5:21:42 PM
    Event ID:      2509
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      FS02.TailwindTraders.net
    Description:
    Couldn't inventory a computer.
    Job: foo2
    Computer: FS01.TailwindTraders.net
    State: Failed
    Error: -2147463168
    Error Message: 
    Guidance: Check the detailed error and make sure the inventory requirements are met. The inventory couldn't determine any aspects of the specified source computer. This could be because of missing permissions or privileges on the source or a blocked firewall port.
  
    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          2/14/2020 1:18:21 PM
    Event ID:      10000
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      2019-rtm-orc.ned.contoso.com
    Description:
    02/14/2020-13:18:21.097 [Erro] Failed device discovery stage SystemInfo with error: (0x80005000) Unknown error (0x80005000)   
  
이 오류는 'meghan@contoso.com'와 같은 UPN (사용자 계정 이름) 형식으로 마이그레이션 자격 증명을 제공 하는 경우 저장소 마이그레이션 서비스의 코드 오류로 인해 발생 합니다. 저장소 마이그레이션 서비스 오 케 스트레이 터 서비스에서이 형식을 올바르게 구문 분석 하지 못했습니다. 그러면 KB4512534 및 19H1의 클러스터 마이그레이션 지원에 추가 된 도메인 조회에 실패 하 게 됩니다.

이 문제를 해결 하려면 ' Contoso\Meghan '과 같은 도메인 \ 사용자 형식으로 자격 증명을 제공 하십시오.

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>"ServiceError0x9006" 또는 "프록시를 현재 사용할 수 없습니다." 오류가 발생 합니다. Windows Server 장애 조치 (failover) 클러스터로 마이그레이션하는 경우

클러스터 된 파일 서버에 대해 데이터를 전송 하려고 하면 다음과 같은 오류가 표시 됩니다. 

    Make sure the proxy service is installed and running, and then try again. The proxy isn't currently available.
    0x9006
    ServiceError0x9006,Microsoft.StorageMigration.Commands.UnregisterSmsProxyCommand

파일 서버 리소스가 원래 Windows Server 2019 클러스터 소유자 노드에서 새 노드로 이동 하 고 저장소 마이그레이션 서비스 프록시 기능이 해당 노드에 설치 되지 않은 경우이 오류가 발생 합니다.

한 가지 해결 방법으로, 전송 쌍을 처음 구성할 때 사용 중인 원래 소유자 클러스터 노드로 대상 파일 서버 리소스를 다시 이동 합니다.

대안으로 다음을 수행 합니다.

1. 클러스터의 모든 노드에 저장소 마이그레이션 서비스 프록시 기능을 설치 합니다.
2. Orchestrator 컴퓨터에서 다음 Storage Migration Service PowerShell 명령을 실행 합니다. 

   ```PowerShell
   Register-SMSProxy -ComputerName *destination server* -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>클러스터 노드에서 인벤토리를 실행 하는 동안 "Dll을 찾을 수 없습니다" 오류가 발생 함

저장소 마이그레이션 서비스를 사용 하 여 인벤토리를 실행 하 고 Windows Server 장애 조치 (failover) 클러스터를 대상으로 지정 하는 경우 파일 서버 원본을 일반적으로 사용 하는 경우 다음 오류가 표시 됩니다.

    DLL not found
    [Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)   

이 문제를 해결 하려면 Storage Migration Service orchestrator를 실행 하는 서버에 "장애 조치 (Failover) 클러스터 관리 도구" (RSAT-클러스터링-Mgmt)를 설치 합니다. 

## <a name="error-there-are-no-more-endpoints-available-from-the-endpoint-mapper-when-running-inventory-against-a-windows-server-2003-source-computer"></a>Windows Server 2003 원본 컴퓨터에 대해 인벤토리를 실행 하는 경우 "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다." 오류가 발생 합니다.

Windows Server 2003 원본 컴퓨터에 대해 저장소 마이그레이션 서비스 orchestrator를 사용 하 여 인벤토리를 실행 하려고 할 때 다음과 같은 오류가 표시 됩니다.

    There are no more endpoints available from the endpoint mapper  

이 문제는 [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) 업데이트에서 해결 됩니다.

## <a name="uninstalling-a-cumulutative-update-prevents-storage-migration-service-from-starting"></a>Cumulutative 업데이트를 제거 하면 저장소 마이그레이션 서비스를 시작할 수 없습니다.

Windows Server 누적 업데이트를 제거 하면 저장소 마이그레이션 서비스가 시작 되지 않을 수 있습니다. 이 문제를 해결 하기 위해 Storage Migration Service 데이터베이스를 백업 및 삭제할 수 있습니다.

1.  관리자가 저장소 마이그레이션 서비스 orchestrator 서버에서 관리자의 구성원 인 관리자 권한 cmd 프롬프트를 열고 다음을 실행 합니다.

     ```
     TAKEOWN /d y /a /r /f c:\ProgramData\Microsoft\StorageMigrationService
     
     MD c:\ProgramData\Microsoft\StorageMigrationService\backup

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService\* /grant Administrators:(GA)

     XCOPY c:\ProgramData\Microsoft\StorageMigrationService\* .\backup\*

     DEL c:\ProgramData\Microsoft\StorageMigrationService\* /q

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService  /GRANT networkservice:F /T /C

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService /GRANT networkservice:(GA) /T /C
     ```
   
2.  저장소 마이그레이션 서비스 서비스를 시작 합니다. 그러면 새 데이터베이스가 생성 됩니다.

## <a name="error-clusctl_resource_netname_repair_vco-failed-against-netname-resource-and-windows-server-2008-r2-cluster-cutover-fails"></a>"NetName RESOURCE에 대해 실패 한 CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO" 및 Windows Server 2008 R2 클러스터를 장애 조치 (failover) 하는 동안 오류 발생

Windows Server 2008 R2 클러스터 원본에서 잘라내기를 실행 하려고 하면 "원본 컴퓨터 이름 바꾸기 ..." 단계에서 중단 됩니다. 다음과 같은 오류가 표시 됩니다.

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          10/17/2019 6:44:48 PM
    Event ID:      10000
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      WIN-RNS0D0PMPJH.contoso.com
    Description:
    10/17/2019-18:44:48.727 [Erro] Exception error: 0x1. Message: Control code CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO failed against netName resource 2008r2FS., stackTrace:    at Microsoft.FailoverClusters.Framework.ClusterUtils.NetnameRepairVCO(SafeClusterResourceHandle netNameResourceHandle, String netName)
       at Microsoft.FailoverClusters.Framework.ClusterUtils.RenameFSNetName(SafeClusterHandle ClusterHandle, String clusterName, String FsResourceId, String NetNameResourceId, String newDnsName, CancellationToken ct)
       at Microsoft.StorageMigration.Proxy.Cutover.CutoverUtils.RenameFSNetName(NetworkCredential networkCredential, Boolean isLocal, String clusterName, String fsResourceId, String nnResourceId, String newDnsName, CancellationToken ct)    [d:\os\src\base\dms\proxy\cutover\cutoverproxy\CutoverUtils.cs::RenameFSNetName::1510]

이 문제는 이전 버전의 Windows Server에서 API 누락으로 인해 발생 합니다. 현재 Windows Server 2008 및 Windows Server 2003 클러스터를 마이그레이션할 수 있는 방법은 없습니다. 인벤토리를 수행 하 고 Windows Server 2008 R2 클러스터에서 문제 없이 전송 한 다음 수동으로 클러스터의 원본 파일 서버 리소스 (netname 및 IP 주소)를 변경 하 고 대상 클러스터 netname 및 IP를 변경 하 여 수동으로 조치를 수행할 수 있습니다. 원본 원본과 일치 하는 주소입니다. 

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer-when-using-dhcp"></a>"38% 매핑 네트워크 인터페이스를 원본 컴퓨터에서 중단" 하는 방법 " DHCP를 사용 하는 경우 

원본 컴퓨터의 전환을 실행 하려고 할 때 하나 이상의 네트워크 인터페이스에서 새 정적 (DHCP 아님) IP 주소를 사용 하도록 원본 컴퓨터를 설정 하 고, 이동이 중단 되는 것은 "38% 원본에서 네트워크 인터페이스 매핑 ..." 단계에서 중단 됩니다. SMS 이벤트 로그에 다음과 같은 오류가 표시 됩니다.

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          11/13/2019 3:47:06 PM
    Event ID:      20494
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      orc2019-rtm.corp.contoso.com
    Description:
    Couldn't set the IP address on the network adapter.

    Computer: fs12.corp.contoso.com
    Adapter: microsoft hyper-v network adapter
    IP address: 10.0.0.99
    Network mask: 16
    Error: 40970
    Error Message: Unknown error (0xa00a)

    Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.

원본 컴퓨터를 검사 하면 원래 IP 주소를 변경할 수 없다는 것을 볼 수 있습니다. 

새 고정 IP 주소, 서브넷 및 게이트웨이를 지정 하는 경우에만 Windows 관리 센터 "구성에서 구성" 화면에서 "DHCP 사용"을 선택한 경우에는이 문제가 발생 하지 않습니다. 

이 문제는 [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) 업데이트에서 해결 됩니다.

## <a name="slower-than-expected-re-transfer-performance"></a>예상 되는 다시 전송 성능 보다 느림

전송을 완료 한 후 동일한 데이터를 다시 전송 하는 것을 실행 하면 원본 서버에서 데이터가 거의 변경 되지 않은 경우에도 전송 시간이 크게 향상 되지 않을 수 있습니다.

이는 매우 많은 수의 파일과 중첩 된 폴더를 전송할 때 예상 되는 동작입니다. 데이터의 크기는 관련이 없습니다. 먼저 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 에서이 동작을 개선 하 고 전송 성능을 최적화 합니다. 성능을 더 조정 하려면 [인벤토리 최적화 및 전송 성능](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq#optimizing-inventory-and-transfer-performance)을 검토 하세요.

## <a name="data-does-not-transfer-user-renamed-when-migrating-to-or-from-a-domain-controller"></a>데이터가 전송 되지 않고 도메인 컨트롤러에서 또는 도메인 컨트롤러에서 마이그레이션할 때 사용자 이름이 바뀜

도메인 컨트롤러로의 전송을 시작한 후 다음을 수행 합니다.

 1. 데이터가 마이그레이션되지 않으며 대상에 공유가 생성 되지 않습니다.
 2. Windows 관리 센터에 오류 메시지가 표시 되지 않은 빨간색 오류 기호가 표시 됩니다.
 3. 하나 이상의 AD 사용자 및 도메인 로컬 그룹의 이름 및/또는 Windows 2000 이전 로그온 특성이 변경 되었습니다.
 4. SMS orchestrator에서 이벤트 3509이 표시 됩니다.
 
        Log Name:      Microsoft-Windows-StorageMigrationService/Admin
        Source:        Microsoft-Windows-StorageMigrationService
        Date:          1/10/2020 2:53:48 PM
        Event ID:      3509
        Task Category: None
        Level:         Error
        Keywords:      
        User:          NETWORK SERVICE
        Computer:      orc2019-rtm.corp.contoso.com
        Description:
        Couldn't transfer storage for a computer.

        Job: dctest3
        Computer: dc02-2019.corp.contoso.com
        Destination Computer: dc03-2019.corp.contoso.com
        State: Failed
        Error: 53251
        Error Message: Local accounts migration failed with error System.Exception: -2147467259
           at Microsoft.StorageMigration.Service.DeviceHelper.MigrateSecurity(IDeviceRecord sourceDeviceRecord, IDeviceRecord destinationDeviceRecord, TransferConfiguration config, Guid proxyId, CancellationToken cancelToken)

이는 저장소 마이그레이션 서비스를 사용 하 여 도메인 컨트롤러에서 마이그레이션하려는 경우와 "사용자 및 그룹 마이그레이션" 옵션을 사용 하 여 계정의 이름을 바꾸거나 계정을 다시 사용 하는 경우에 예상 되는 동작입니다. "사용자 및 그룹을 전송 하지 않음"을 선택 하는 대신 [저장소 마이그레이션 서비스에서는 DC 마이그레이션이 지원 되지 않습니다](faq.md). DC에는 로컬 사용자 및 그룹이 포함 되지 않기 때문에 저장소 마이그레이션 서비스는 두 구성원 서버 간에 마이그레이션하는 경우 처럼 이러한 보안 주체를 처리 하 고, 오류 및 손상 되거나 복사 된 계정에 따라 Acl을 조정 하려고 시도 합니다. 

이미 전송을 한 번 더 실행 한 경우:

 1. DC에 대해 다음 AD PowerShell 명령을 사용 하 여 수정 된 모든 사용자 또는 그룹을 찾습니다 (도메인 dinstringuished 이름에 맞게 SearchBase 변경). 

    ```PowerShell
    Get-ADObject -Filter 'Description -like "*storage migration service renamed*"' -SearchBase 'DC=<domain>,DC=<TLD>' | ft name,distinguishedname
    ```
   
 2. 원래 이름으로 반환 되는 모든 사용자에 대해 "사용자 로그온 이름 (Windows 이전 2000)"을 편집 하 여이 내용가 로그온 할 수 있도록 저장소 마이그레이션 서비스에서 추가 된 임의 문자 접미사를 제거 합니다.
 3. 원래 이름으로 반환 되는 모든 그룹에 대해 "그룹 이름 (Windows 이전 2000)"을 편집 하 여 저장소 마이그레이션 서비스에 의해 추가 된 임의 문자 접미사를 제거 합니다.
 4. 저장소 마이그레이션 서비스에서 추가 된 접미사를 포함 하는 사용 하지 않도록 설정 된 사용자 또는 그룹의 경우 이러한 계정을 삭제할 수 있습니다. 사용자 계정에는 도메인 사용자 그룹만 포함 되 고 저장소 마이그레이션 서비스 전송 시작 시간과 일치 하는 날짜/시간이 만들어지므로 사용자 계정이 나중에 추가 되었는지 확인할 수 있습니다.
 
 전송 목적으로 도메인 컨트롤러에서 저장소 마이그레이션 서비스를 사용 하려는 경우 Windows 관리 센터의 전송 설정 페이지에서 항상 "사용자 및 그룹을 전송 하지 않음"을 선택 해야 합니다.
 
 ## <a name="error-53-failed-to-inventory-all-specified-devices-when-running-inventory"></a>인벤토리를 실행 하는 경우 오류 53, "지정 된 모든 장치를 인벤토리 하지 못했습니다." 

인벤토리를 실행 하려고 할 때 다음을 수신 합니다.

    Failed to inventory all specified devices 
    
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          1/16/2020 8:31:17 AM
    Event ID:      2516
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      ned.corp.contoso.com
    Description:
    Couldn't inventory files on the specified endpoint.
    Job: ned1
    Computer: ned.corp.contoso.com
    Endpoint: hithere
    State: Failed
    File Count: 0
    File Size in KB: 0
    Error: 53
    Error Message: Endpoint scan failed
    Guidance: Check the detailed error and make sure the inventory requirements are met. This could be because of missing permissions on the source computer.

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          1/16/2020 8:31:17 AM
    Event ID:      10004
    Task Category: None
    Level:         Critical
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      ned.corp.contoso.com
    Description:
    01/16/2020-08:31:17.031 [Crit] Consumer Task failed with error:The network path was not found.
    . StackTrace=   at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
       at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)
       at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetEnvironmentPathFolders(String ServerName, Boolean IsServerLocal)
       at Microsoft.StorageMigration.Proxy.Service.Discovery.ScanUtils.<ScanSMBEndpoint>d__3.MoveNext()
       at Microsoft.StorageMigration.Proxy.EndpointScanOperation.Run()
       at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(EndpointScanRequest scanRequest, Guid operationId)
       at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(Object request)
       at Microsoft.StorageMigration.Proxy.Common.ProducerConsumerManager`3.Consume(CancellationToken token)    
       
    01/16/2020-08:31:10.015 [Erro] Endpoint Scan failed. Error: (53) The network path was not found.
    Stack trace:
       at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
       at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)

이 단계에서 저장소 마이그레이션 서비스 오 케 스트레이 터가 원격 레지스트리 읽기를 시도 하 여 원본 컴퓨터 구성을 확인 하 고 있지만 레지스트리 경로가 존재 하지 않는다는 것을 원본 서버에서 거부 하 고 있습니다. 다음과 같은 문제가 원인일 수 있습니다.

 - 원본 컴퓨터에서 원격 레지스트리 서비스가 실행 되 고 있지 않습니다.
 - 방화벽에서 Orchestrator의 원본 서버에 대 한 원격 레지스트리 연결을 허용 하지 않습니다.
 - 원본 컴퓨터에 연결할 수 있는 원격 레지스트리 권한이 원본 마이그레이션 계정에 없습니다.
 - 원본 컴퓨터의 레지스트리 내에서 "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\CurrentVersion" 또는 "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\에 있는 원본 마이그레이션 계정에 읽기 권한이 없습니다. LanmanServer
 
 ## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer"></a>"38% 매핑 네트워크 인터페이스를 원본 컴퓨터에서 중단" 하는 방법 " 

원본 컴퓨터에 대 한 잘라내기를 실행 하려고 할 때 잘라내기는 "38% 원본에서의 네트워크 인터페이스 매핑 ..." 단계에서 중단 됩니다. SMS 이벤트 로그에 다음과 같은 오류가 표시 됩니다.

    Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
    Source:        Microsoft-Windows-StorageMigrationService-Proxy
    Date:          1/11/2020 8:51:14 AM
    Event ID:      20505
    Task Category: None
    Level:         Error
    Keywords:      
    User:          NETWORK SERVICE
    Computer:      nedwardo.contosocom
    Description:
    Couldn't establish a CIM session with the computer.

    Computer: 172.16.10.37
    User Name: nedwardo\MsftSmsStorMigratSvc
    Error: 40970
    Error Message: Unknown error (0xa00a)

    Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.

이 문제는 원본 컴퓨터에서 다음 레지스트리 값을 설정 하는 그룹 정책에 의해 발생 합니다.

 "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System LocalAccountTokenFilterPolicy = 0"
 
이 설정은 표준 그룹 정책의 일부가 아니므로 [Microsoft Security 준수 도구 키트](https://www.microsoft.com/download/details.aspx?id=55319)를 사용 하 여 구성 된 추가 기능입니다.
 
 - Windows Server 2012 R2: "컴퓨터 구성 \ Templates\SCM: 네트워크 로그온 시 로컬 계정에 해시 Mitigations\Apply UAC 제한 사항 전달"
 - Widows Server 2016: "Computer Templates\MS Security Guide\Apply network 로그온의 로컬 계정에 대 한 UAC 제한 사항"
 
사용자 지정 레지스트리 설정을 사용 하 여 그룹 정책 기본 설정을 사용 하 여 설정할 수도 있습니다. GPRESULT 도구를 사용 하 여이 설정을 원본 컴퓨터에 적용 하는 정책을 확인할 수 있습니다.

Storage Migration Service는 중지 프로세스의 일부로 일시적으로 [LocalAccountTokenFilterPolicy](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows) 를 사용 하도록 설정 하 고 완료 되 면 제거 합니다. 그룹 정책 충돌 하는 GPO (그룹 정책 개체)를 적용 하면 저장소 마이그레이션 서비스를 재정의 하 여 이동 하지 않습니다.

이 문제를 해결 하려면 다음 옵션 중 하나를 사용 합니다.

1. 이 충돌 하는 GPO를 적용 하는 Active Directory OU에서 원본 컴퓨터를 임시로 이동 합니다. 
2. 이 충돌 정책을 적용 하는 GPO를 일시적으로 사용 하지 않도록 설정 합니다.
3. 이 설정을 사용 안 함으로 설정 하 고 원본 서버의 특정 OU에 적용 되는 새 GPO를 일시적으로 만들어 다른 Gpo 보다 우선 순위가 높습니다.

## <a name="see-also"></a>참고 항목

- [Storage Migration Service 개요](overview.md)
