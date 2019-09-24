---
title: 저장소 마이그레이션 서비스의 알려진 문제
description: Microsoft 지원에 대 한 로그를 수집 하는 방법과 같은 저장소 마이그레이션 서비스에 대 한 알려진 문제 및 문제 해결 지원.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 07/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: d8437e0e33a370ab698d25f25b43fbbcbae97792
ms.sourcegitcommit: 45415ba58907d650cfda45f4c57f6ddf1255dcbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71206916"
---
# <a name="storage-migration-service-known-issues"></a>저장소 마이그레이션 서비스의 알려진 문제

이 항목에는 [저장소 마이그레이션 서비스](overview.md) 를 사용 하 여 서버를 마이그레이션할 때 알려진 문제에 대 한 답변이 포함 되어 있습니다.

Storage Migration Service는 Windows Server의 서비스와 Windows 관리 센터의 사용자 인터페이스의 두 부분으로 릴리스됩니다. 이 서비스는 windows server, 장기 서비스 채널 뿐만 아니라 Windows Server, 반기 채널에서 사용할 수 있습니다. Windows 관리 센터는 별도 다운로드로 사용할 수 있습니다. 또한 Windows 업데이트를 통해 출시 되는 Windows Server의 누적 업데이트에 대 한 변경 내용을 정기적으로 포함 합니다. 

예를 들어 Windows Server, 버전 1903에는 저장소 마이그레이션 서비스에 대 한 새로운 기능 및 수정이 포함 되어 있습니다 .이 서비스는 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)를 설치 하 여 windows server 2019 및 windows server 버전 1809 에서도 사용할 수 있습니다.

## <a name="collecting-logs"></a>Microsoft 지원 작업할 때 로그 파일을 수집 하는 방법

저장소 마이그레이션 서비스에는 Orchestrator 서비스와 프록시 서비스에 대 한 이벤트 로그가 포함 되어 있습니다. Urchestrator 서버는 항상 두 이벤트 로그를 모두 포함 하 고 프록시 서비스를 설치한 대상 서버는 프록시 로그를 포함 합니다. 이러한 로그는 다음 위치에 있습니다.

- 응용 프로그램 및 서비스 로그 \ Microsoft \ Windows \ StorageMigrationService
- 응용 프로그램 및 서비스 로그 \ Microsoft \ Windows \ StorageMigrationService-프록시

오프 라인으로 보거나 Microsoft 지원에 보내기 위해 이러한 로그를 수집 해야 하는 경우 GitHub에서 사용할 수 있는 오픈 소스 PowerShell 스크립트가 있습니다.

 [저장소 마이그레이션 서비스 도우미](https://aka.ms/smslogs) 

사용에 대 한 추가 정보를 검토 합니다.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Windows Server 2019를 관리 하지 않는 경우 Windows 관리 센터에 저장소 마이그레이션 서비스가 표시 되지 않음

Windows 관리 센터 1809 버전을 사용 하 여 Windows Server 2019 orchestrator를 관리 하는 경우 Storage Migration Service에 대 한 도구 옵션이 표시 되지 않습니다. 

Windows 관리 센터 저장소 마이그레이션 서비스 확장은 Windows Server 2019 버전 1809 이상 운영 체제만 관리 하기 위해 버전에 바인딩되어 있습니다. 이전 Windows Server 운영 체제 또는 insider preview를 관리 하는 데 사용 하는 경우 도구는 표시 되지 않습니다. 이 동작은 의도된 것입니다. 

문제를 해결 하려면 Windows Server 2019 빌드 1809 이상 버전을 사용 하거나 업그레이드 합니다.

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>저장소 마이그레이션 서비스를 사용 하는 경우에는 가공선에서 고정 IP를 선택할 수 없습니다.

Windows 관리 센터에서 0.57 버전의 Storage Migration Service 확장을 사용 하 고 있으며,이 경우에는 주소에 대 한 고정 IP를 선택할 수 없습니다. 강제로 DHCP를 사용 합니다.

이 문제를 해결 하려면 Windows 관리 센터의 **설정** > **확장** 에서 업데이트 된 버전 저장소 마이그레이션 서비스 0.57.2를 설치할 수 있음을 나타내는 경고를 확인 합니다. Windows 관리 센터에 대 한 브라우저 탭을 다시 시작 해야 할 수 있습니다.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>"대상 컴퓨터에서 토큰 필터 정책에 대 한 액세스가 거부 되었습니다." 오류로 인해 저장소 마이그레이션 서비스에서 유효성 검사가 실패 함

유효성 검사를 통해 가공선을 실행 하면 오류 "실패: 대상 컴퓨터의 토큰 필터 정책에 대 한 액세스가 거부 되었습니다. " 원본 및 대상 컴퓨터에 대 한 올바른 로컬 관리자 자격 증명을 제공한 경우에도이 문제가 발생 합니다.

이 문제는 Windows Server 2019의 코드 오류로 인해 발생 합니다. 이 문제는 대상 컴퓨터를 Storage Migration Service Orchestrator로 사용할 때 발생 합니다.

이 문제를 해결 하려면 계획 된 마이그레이션 대상이 아닌 Windows Server 2019 컴퓨터에 Storage Migration Service를 설치한 다음 Windows 관리 센터를 사용 하 여 해당 서버에 연결 하 고 마이그레이션을 수행 합니다.

이후 버전의 Windows Server에서는이 문제를 해결 했습니다. 이 수정 프로그램의 백 포트를 요청 하려면 [Microsoft 지원](https://support.microsoft.com) 을 통해 지원 사례를 여세요.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage Migration Service는 Windows Server 2019 Evaluation 또는 Windows Server 2019 Essentials edition에 포함 되어 있지 않습니다.

Windows 관리 센터를 사용 하 여 [Windows server 2019 Evaluation 릴리스](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 또는 windows Server 2019 Essentials 버전에 연결 하는 경우 저장소 마이그레이션 서비스를 관리할 수 있는 옵션이 없습니다. Storage Migration Service는 역할 및 기능에도 포함 되어 있지 않습니다.

이 문제는 Windows Server 2019 및 Windows Server 2019 Essentials의 평가용 미디어에서 서비스 문제로 인해 발생 합니다. 

평가를 위해이 문제를 해결 하려면 Windows Server 2019의 정품, MSDN, OEM 또는 볼륨 라이선스 버전을 설치 하 고 활성화 하지 마십시오. 정품 인증을 사용 하지 않으면 모든 버전의 Windows Server가 180 일간 평가 모드로 작동 합니다. 

이후 버전의 Windows Server에서는이 문제가 해결 되었습니다.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>저장소 마이그레이션 서비스에서 전송 오류 CSV 다운로드 시간 초과

Windows 관리 센터 또는 PowerShell을 사용 하 여 전송 작업에 대 한 자세한 오류 전용 CSV 로그를 다운로드 하는 경우 오류 메시지가 표시 됩니다.

 >   전송 로그-방화벽에서 파일 공유를 사용할 수 있는지 확인 하세요. : 이 요청 작업이 net.tcp:/localhost: 28940/sms/service/1/transfer에서 구성 된 시간 제한 (00:01:00) 내에 회신을 받지 못했습니다. 이 작업에 할당 된 시간이 보다 긴 시간 제한의 일부일 수 있습니다. 서비스가 작업을 계속 처리 하 고 있거나 서비스에서 회신 메시지를 보낼 수 없기 때문일 수 있습니다. 채널/프록시를 IContextChannel로 캐스팅 하 고 OperationTimeout 속성을 설정 하 여 작업 시간 제한을 늘리고 서비스가 클라이언트에 연결할 수 있는지 확인 하세요.

이 문제는 저장소 마이그레이션 서비스에서 허용 하는 기본 1 분 제한 시간 내에 필터링 할 수 없는 너무 많은 전송 된 파일에 의해 발생 합니다. 

이 문제를 해결 하려면 다음을 수행 합니다.

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

5. 편집 메뉴에서 새로 만들기를 가리킨 후 DWORD 값을 클릭합니다. 
6. DWORD 이름에 "WcfOperationTimeoutInMinutes"를 입력 한 다음 ENTER 키를 누릅니다.
7. "WcfOperationTimeoutInMinutes"을 마우스 오른쪽 단추로 클릭 한 다음 수정을 클릭 합니다. 
8. 기본 데이터 상자에서 "10 진수"를 클릭 합니다.
9. 값 데이터 상자에 "10"을 입력 한 다음 확인을 클릭 합니다.
10. 레지스트리 편집기를 종료 합니다.
11. 오류 전용 CSV 파일 다운로드를 다시 시도 합니다. 

이후 버전의 Windows Server 2019에서이 동작을 변경 하려고 합니다.  

## <a name="cutover-fails-when-migrating-between-networks"></a>네트워크 간에 마이그레이션할 때의 가공선 실패

Azure IaaS 인스턴스와 같이 원본이 아닌 다른 네트워크에서를 실행 하는 대상 컴퓨터로 마이그레이션할 때 원본에서 고정 IP 주소를 사용 하는 경우에는 가공선이 완료 되지 않습니다. 

이 동작은 IP 주소를 통해 연결 하는 사용자, 응용 프로그램 및 스크립트에서 마이그레이션한 후 연결 문제를 방지 하기 위해 의도적으로 설계 되었습니다. IP 주소가 이전 원본 컴퓨터에서 새 대상 대상으로 이동 되 면 새 네트워크 서브넷 정보 및 DNS 및 WINS와 일치 하지 않습니다.

이 문제를 해결 하려면 동일한 네트워크에 있는 컴퓨터로 마이그레이션을 수행 합니다. 그런 다음 해당 컴퓨터를 새 네트워크로 이동 하 고 해당 IP 정보를 다시 할당 합니다. 예를 들어 Azure IaaS로 마이그레이션하는 경우 먼저 로컬 VM으로 마이그레이션한 후 Azure Migrate를 사용 하 여 VM을 Azure로 이동 합니다.  

이후 버전의 Windows 관리 센터에서이 문제가 해결 되었습니다. 이제 대상 서버의 네트워크 설정을 변경 하지 않는 마이그레이션을 지정할 수 있습니다. 업데이트 된 확장은 릴리스 시 여기에 나열 됩니다. 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>대상 프록시 및 자격 증명 관리 권한에 대 한 유효성 검사 경고

전송 작업의 유효성을 검사할 때 다음과 같은 경고가 표시 됩니다.

 > **자격 증명에는 관리 권한이 있습니다.**
 > 경고: 동작을 원격으로 사용할 수 없습니다.
 > **대상 프록시가 등록 되었습니다.**
 > 경고: 대상 프록시를 찾을 수 없습니다.

Windows Server 2019 대상 컴퓨터에 저장소 마이그레이션 서비스 프록시 서비스를 설치 하지 않았거나 대상 컴퓨터가 Windows Server 2016 또는 Windows Server 2012 r 2 인 경우이 동작은 의도적으로 설계 된 것입니다. 전송 성능을 크게 개선 하기 위해 프록시가 설치 된 Windows Server 2019 컴퓨터로 마이그레이션하는 것이 좋습니다.  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>특정 파일은 인벤토리 또는 전송 하지 않으며 오류 5 "액세스가 거부 되었습니다."

원본 컴퓨터에서 대상 컴퓨터로 파일을 인벤토리 또는 전송 하는 경우 사용자가 관리자 그룹 권한을 제거 하는 파일은 마이그레이션하지 못합니다. 저장소 마이그레이션 서비스 검사-프록시 디버그는 다음을 보여 줍니다.

  로그 이름:      Microsoft-Windows-StorageMigrationService-프록시/디버그 소스:        Microsoft-Windows-StorageMigrationService-프록시 날짜:          오전 2/26/2019 9:00:04 이벤트 ID:      1만 작업 범주: 없음 수준:         오류 키워드:      
  사용자:          네트워크 서비스 컴퓨터: srv1.contoso.com 설명:

  02/26/2019-09:00:04.860 [error] srv1에 대 \\한 전송 오류: com\public\indy.png: (5) 액세스가 거부 되었습니다.
스택 추적: StorageMigration. FileDirUtils. System.windows.forms.openfiledialog.openfile (String fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes) at StorageMigration. FileDirUtils... FileDirUtils 파일 (FileInfo 파일)에 있는 (FileInfo 파일 (FileInfo 파일))에 있습니다. StorageMigration () at FileTransfer () ()에 있는 InitializeSourceFileInfo ()를 (를) (으)로 변환 합니다. StorageMigration () [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs:: FileTransfer () :: Trtransfer:: 55]


이 문제는 저장소 마이그레이션 서비스에서 백업 권한이 호출 되지 않은 코드 오류로 인해 발생 합니다. 

이 문제를 해결 하려면 오 케 스트레이 터 컴퓨터에 [KB4490481 (OS 빌드 17763.404)를 Windows 업데이트](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) 설치 하 고 프록시 서비스가 설치 된 경우 대상 컴퓨터에 설치 합니다. 원본 마이그레이션 사용자 계정이 원본 컴퓨터 및 저장소 마이그레이션 서비스 orchestrator의 로컬 관리자 인지 확인 합니다. 대상 마이그레이션 사용자 계정이 대상 컴퓨터 및 저장소 마이그레이션 서비스 orchestrator의 로컬 관리자 인지 확인 합니다. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>저장소 마이그레이션 서비스를 사용 하 여 데이터를 사전 시드 하는 경우 DFSR 해시가 일치 하지 않음

저장소 마이그레이션 서비스를 사용 하 여 파일을 새 대상으로 전송 하는 경우, 해당 데이터를 미리 시드 된 복제 또는 DFSR 데이터베이스 복제를 통해 기존 DFSR 서버와 복제 하도록 DFS 복제 (DFSR)을 구성 합니다. 모든 파일은 해시를 experiemce 합니다. 불일치 및가 다시 복제 됩니다. SMS를 사용 하 여 전송 하 고 나면 데이터 스트림, 보안 스트림, 크기 및 특성이 모두 정확히 일치 하는 것으로 나타납니다. ICACLS 또는 DFSR 데이터베이스 복제 디버그 로그를 사용 하 여 파일을 검사 하면 다음과 같은 결과가 나타납니다.

원본 파일:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png/save D:AI (A;; FA;;; BA) (A;; 0) x1200a9;;D D) (A;; 0) x1301bf;;D U) (A; ID; FA;;;) BA) (A; ID; FA;;;) SY) (A; ID; 0x1200a9;;;) BU

대상 파일:

  icacls d:\test\thatcher.png/save D:AI (A;; FA;;; BA) (A;; 0) x1301bf;;D U) (A;; 0) x1200a9;;D D) (A; ID; FA;;;) BA) (A; ID; FA;;;) SY) (A; ID; 0x1200a9;;;) BU)**S:PAINO_ACCESS_CONTROL**

DFSR 디버그 로그:

  20190308 10:18:53.116 3948 DBCL 4045 [WARN] Dbcl:: IDTableImportUpdate 불일치 레코드가 발견 되었습니다. 

  로컬 ACL hash: 1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime: 20190308 18:09:44.876 FileSizeLow: 1131654 FileSizeHigh: 0 특성: 32 

  복제 ACL hash:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** LastWriteTime: 20190308 18:09:44.876 FileSizeLow: 1131654 FileSizeHigh: 0 특성: 32 

이 문제는 저장소 마이그레이션 서비스에서 SACL (보안 감사 Acl)을 설정 하는 데 사용 하는 라이브러리의 코드 오류로 인해 발생 합니다. Null이 아닌 SACL은 SACL이 비어 있을 때 실수로 설정 되며, DFSR이 해시 불일치를 올바르게 식별 하는 데 사용할 수 있습니다. 

이 문제를 해결 하려면 저장소 마이그레이션 서비스 대신 [dfsr 사전 시드 및 Dfsr 데이터베이스 복제 작업](../dfs-replication/preseed-dfsr-with-robocopy.md) 에 대해 Robocopy를 계속 사용 합니다. Microsoft는이 문제를 조사 하 고 있으며, 이후 버전의 Windows Server에서이 문제를 해결 하 고 Windows 업데이트 백 엔드가 가능 합니다. 

## <a name="error-404-when-downloading-csv-logs"></a>CSV 로그를 다운로드 하는 동안 오류 404 발생

전송 작업이 끝날 때 전송 또는 오류 로그를 다운로드 하려고 하면 다음과 같은 오류가 표시 됩니다.

  $jobname: 전송 로그: ajax 오류 404

Orchestrator 서버에서 "파일 및 프린터 공유 (SMB In)" 방화벽 규칙을 사용 하도록 설정 하지 않은 경우이 오류가 발생 합니다. Windows 관리 센터 파일 다운로드에는 연결 된 컴퓨터에서 포트 TCP/445 (SMB)가 필요 합니다.  

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Windows Server 2008 r 2에서 전송할 때 "모든 끝점에서 저장소를 전송할 수 없음" 오류

Windows Server 2008 R2 원본 컴퓨터에서 데이터를 전송 하려고 할 때 데이터를 전송 하지 않고 오류를 수신 합니다.  

  끝점에서 저장소를 전송할 수 없습니다.
0x9044

이 오류는 Windows Server 2008 R2 컴퓨터가 Windows 업데이트의 모든 중요 및 중요 업데이트를 사용 하 여 완전히 패치 되지 않은 경우에 발생 합니다. 저장소 마이그레이션 서비스와 관계 없이, 운영 체제에 최신 버전의 Windows Server에 대 한 보안 향상 기능이 포함 되어 있지 않기 때문에 보안을 위해 Windows Server 2008 R2 컴퓨터에 패치를 적용 하는 것이 좋습니다.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>"끝점에서 저장소를 전송 하지 못했습니다." 및 "원본 장치가 온라인 상태 인지 확인-액세스할 수 없습니다." 라는 오류가 발생 합니다.

원본 컴퓨터에서 데이터를 전송 하려고 하면 일부 또는 모든 공유가 전송 되지 않고 요약 오류가 발생 합니다.

   끝점에서 저장소를 전송할 수 없습니다.
0x9044

SMB 전송 세부 정보를 검사 하면 오류가 표시 됩니다.

   원본 장치가 온라인 상태 인지 확인 합니다. 액세스할 수 없습니다.

StorageMigrationService/Admin 이벤트 로그를 검사 하면 다음이 표시 됩니다.

   저장소를 전송할 수 없습니다.

   직함 Job1 ID:  
   상태: 실패 한 오류: 36931 오류 메시지: 

   지침 자세한 오류를 확인 하 고 전송 요구 사항이 충족 되었는지 확인 하십시오. 전송 작업에서 원본 및 대상 컴퓨터를 전송할 수 없습니다. 이는 방화벽 규칙 또는 권한 누락으로 인해 오 케 스트레이 터 컴퓨터가 원본 또는 대상 컴퓨터에 연결할 수 없기 때문일 수 있습니다.

StorageMigrationService-프록시/디버그 로그를 검사 하면 다음이 표시 됩니다.

   07/02/2019-13:35:57.231 [오류] 전송 유효성 검사에 실패 했습니다. ErrorCode 40961, 소스 끝점에 연결할 수 없거나, 소스 자격 증명이 잘못 되었거나, 인증 된 사용자에 게 액세스 권한이 없습니다.
StorageMigration ()에서 StorageMigration ()을 (를) 확인 합니다. TransferRequestHandler (FileTransferRequest fileTransferRequest, Guid operationId)를 확인 합니다.    [d:\os\src\base\dms\proxy\transfer\transferproxy\TransferRequestHandler.cs::

마이그레이션 계정에 SMB 공유에 대 한 읽기 이상의 권한이 없는 경우이 오류가 발생 합니다. 이 오류를 해결 하려면 원본 컴퓨터의 SMB 공유에 원본 마이그레이션 계정이 포함 된 보안 그룹을 추가 하 고 읽기, 변경 또는 모든 권한을 부여 합니다. 마이그레이션이 완료 된 후이 그룹을 제거할 수 있습니다.

## <a name="error-0x80005000-when-running-inventory"></a>인벤토리를 실행 하는 경우 오류 0x80005000

[KB4512534](https://support.microsoft.com/en-us/help/4512534/windows-10-update-kb4512534) 를 설치 하 고 인벤토리 실행을 시도한 후 인벤토리가 실패 하 고 오류가 발생 합니다.

  HRESULT의 예외: 0x80005000
  
  로그 이름:      Microsoft-Windows-StorageMigrationService/관리자 원본:        Microsoft-Windows-StorageMigrationService 날짜:          9/9/2019 5:21:42 PM 이벤트 ID:      2503 작업 범주: 없음 수준:         오류 키워드:      
  사용자:          네트워크 서비스 컴퓨터:      FS02. TailwindTraders.net 설명: 컴퓨터를 인벤토리에 만들지 못했습니다.
작업: foo2 ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b 상태: 실패 한 오류: 36934 오류 메시지: 모든 장치에 대 한 인벤토리가 실패 함 지침: 자세한 오류를 확인 하 고 인벤토리 요구 사항이 충족 되었는지 확인 하십시오. 작업에서 지정 된 원본 컴퓨터를 인벤토리에 만들지 못했습니다. 이는 방화벽 규칙 또는 권한 누락으로 인해 오 케 스트레이 터 컴퓨터가 네트워크를 통해 연결할 수 없기 때문일 수 있습니다.
  
  로그 이름:      Microsoft-Windows-StorageMigrationService/관리자 원본:        Microsoft-Windows-StorageMigrationService 날짜:          9/9/2019 5:21:42 PM 이벤트 ID:      2509 작업 범주: 없음 수준:         오류 키워드:      
  사용자:          네트워크 서비스 컴퓨터:      FS02. TailwindTraders.net 설명: 컴퓨터를 인벤토리에 만들지 못했습니다.
작업: foo2 컴퓨터: FS01. TailwindTraders.net 상태: 실패 한 오류:-2147463168 오류 메시지: 지침 자세한 오류를 확인 하 고 인벤토리 요구 사항이 충족 되었는지 확인 하십시오. 인벤토리에 지정 된 원본 컴퓨터의 모든 측면을 확인할 수 없습니다. 원본 또는 차단 된 방화벽 포트에 대 한 권한이 없거나 권한이 없기 때문일 수 있습니다.
  
이 오류는 'meghan@contoso.com' 등의 UPN (사용자 계정 이름) 형식으로 마이그레이션 자격 증명을 제공 하는 경우 저장소 마이그레이션 서비스의 코드 오류로 인해 발생 합니다. 저장소 마이그레이션 서비스 오 케 스트레이 터 서비스에서이 형식을 올바르게 구문 분석 하지 못했습니다. 그러면 KB4512534 및 19H1의 클러스터 마이그레이션 지원에 추가 된 도메인 조회에 실패 하 게 됩니다.

이 문제를 해결 하려면 ' Contoso\Meghan '과 같은 도메인 \ 사용자 형식으로 자격 증명을 제공 하십시오.

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>"ServiceError0x9006" 또는 "프록시를 현재 사용할 수 없습니다." 오류가 발생 합니다. Windows Server 장애 조치 (failover) 클러스터로 마이그레이션하는 경우

클러스터 된 파일 서버에 대해 데이터를 전송 하려고 하면 다음과 같은 오류가 표시 됩니다. 

   프록시 서비스가 설치 되어 실행 중인지 확인 한 후 다시 시도 하십시오. 프록시를 현재 사용할 수 없습니다.
0x9006 ServiceError0x9006, StorageMigration. UnregisterSmsProxyCommand

파일 서버 리소스가 원래 Windows Server 2019 클러스터 소유자 노드에서 새 노드로 이동 하 고 저장소 마이그레이션 서비스 프록시 기능이 해당 노드에 설치 되지 않은 경우이 오류가 발생 합니다.

한 가지 해결 방법으로, 전송 쌍을 처음 구성할 때 사용 중인 원래 소유자 클러스터 노드로 대상 파일 서버 리소스를 다시 이동 합니다.

대안으로 다음을 수행 합니다.

1. 클러스터의 모든 노드에 저장소 마이그레이션 서비스 프록시 기능을 설치 합니다.
2. Orchestrator 컴퓨터에서 다음 Storage Migration Service PowerShell 명령을 실행 합니다. 

   ```PowerShell
   Register-SMSProxy -ComputerName *destination server* -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>클러스터 노드에서 인벤토리를 실행 하는 동안 "Dll을 찾을 수 없습니다" 오류가 발생 함

Windows Server 2019 장애 조치 (failover) 클러스터 노드에 설치 된 Storage Migration Service orchestrator를 사용 하 여 인벤토리를 실행 하 고 Windows Server 장애 조치 (failover) 클러스터를 대상으로 하는 경우 파일 서버 원본을 일반적으로 사용 합니다.

    DLL not found
    [Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)   

이 문제를 해결 하려면 Storage Migration Service orchestrator를 실행 하는 서버에 "장애 조치 (Failover) 클러스터 관리 도구" (RSAT-클러스터링-Mgmt)를 설치 합니다. 


## <a name="see-also"></a>참조

- [Storage Migration Service 개요](overview.md)
