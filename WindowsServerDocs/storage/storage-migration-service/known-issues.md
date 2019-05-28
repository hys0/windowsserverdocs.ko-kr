---
title: Storage Migration Service의 알려진 문제
description: 알려진된 문제 및 Microsoft 지원에 대 한 로그를 수집 하는 방법과 같은 저장소 마이그레이션 서비스에 대 한 문제 해결 지원 합니다.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 05/14/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: e1cfd2b0ea3bc4d7802cb4a6d2a8c1493d5511a1
ms.sourcegitcommit: 0099873d69bd23495d275d7bcb464594de09ee3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699693"
---
# <a name="storage-migration-service-known-issues"></a>Storage Migration Service의 알려진 문제

이 항목에서는 사용 하는 경우 알려진된 문제에 대 한 답변을 포함 [저장소 마이그레이션 서비스](overview.md) 서버를 마이그레이션하려 합니다.

## <a name="collecting-logs"></a> Microsoft 기술 지원 서비스를 사용 하 여 작업 하는 경우 로그 파일을 수집 하는 방법

저장소 마이그레이션 서비스 오 케 스트레이 터 서비스 및 프록시 서비스에 대 한 이벤트 로그를 포함합니다. Urchestrator 서버는 항상 두 이벤트 로그에 및 설치 하는 프록시 서비스를 사용 하 여 대상 서버는 프록시 로그를 포함 합니다. 이러한 로그는 아래에 있습니다.

- 응용 프로그램 및 서비스 로그 \ Microsoft \ Windows \ StorageMigrationService
- 응용 프로그램 및 서비스 로그 \ Microsoft \ Windows \ StorageMigrationService 프록시

오프 라인 보기에 대 한 이러한 로그를 수집 하거나 Microsoft 지원에 보낼 경우에 오픈 소스 GitHub에서 사용할 수 있는 PowerShell 스크립트:

 [저장소 마이그레이션 서비스 도우미](https://aka.ms/smslogs) 

사용량에 대 한 추가 정보를 검토 합니다.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>저장소 마이그레이션 서비스 표시 되지 않습니다 Windows Admin Center Windows Server 2019를 관리 하지 않는 한

Windows Admin Center 1809 버전을 사용 하 여 Windows Server 2019 orchestrator 관리를 저장소 마이그레이션 서비스에 대 한 도구 옵션이 표시 하지 않습니다. 

Windows Admin Center Storage Migration Service 확장이 버전 바인딩된만 Windows Server 2019 버전 1809 또는 이후 운영 체제를 관리 하도록 됩니다. 이전 Windows Server 운영 체제 또는 참가자 미리 보기 관리를 사용 하는 경우이 도구는 표시 되지 않습니다. 이 동작은 의도된 것입니다. 

를 해결 하려면 사용 하거나 Windows Server 2019 빌드 1809 이상으로 업그레이드 합니다.

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>저장소 마이그레이션 서비스 중단에 고정 IP를 선택할 수 있습니다 하지 않습니다.

Windows Admin Center 확장 중단 단계에 도달 하는 저장소 마이그레이션 서비스의 0.57 버전을 사용 하는 경우 고정 IP 주소를 선택할 수 없습니다. DHCP를 사용 하도록 강제 됩니다.

Windows Admin Center이 문제를 해결 하려면 아래에서 확인 **설정을** > **확장** 를 업데이트 된 버전 저장소 마이그레이션 서비스 0.57.2 경고가 설치에 사용할 수 있습니다. Windows 관리 센터에 대 한 사용자 브라우저 탭을 다시 시작 해야 합니다.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>"대상 컴퓨터에서 토큰 필터 정책에 대 한 액세스가 거부 되었습니다" 오류와 함께 저장소 마이그레이션 서비스 중단 유효성 검사 실패

단독형 유효성 검사를 실행 하면 오류가 "실패 합니다. 액세스 토큰 필터 정책 대상 컴퓨터에 대해 거부 되었습니다. " 이 원본 및 대상 컴퓨터에 대 한 올바른 로컬 관리자 자격 증명을 제공 하는 경우에 발생 합니다.

이 문제를 Windows Server 2019에 코드 결함 때문일 수 있습니다. 저장소 마이그레이션 서비스 Orchestrator와 대상 컴퓨터를 사용할 때 문제가 발생 합니다.

이 문제를 해결 하려면 원하는 마이그레이션 대상으로 하지 않은 Windows Server 2019 컴퓨터 저장소 마이그레이션 서비스를 설치 하 고 Windows Admin Center 사용 하 여 해당 서버에 연결할 마이그레이션을 수행 합니다.

Windows Server의 이후 릴리스에서이 문제를 해결 있을 것입니다. 통해 지원 사례를 여세요 [Microsoft 지원](https://support.microsoft.com) 요청을 백 포팅이 수정이 프로그램을 만들 수 있습니다.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-edition"></a>저장소 마이그레이션 서비스 Windows Server 2019 Evaluation edition에 포함 되지 않습니다.

에 연결할 Windows Admin Center 사용 하는 경우는 [Windows Server 2019 평가 릴리스](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 저장소 마이그레이션 서비스를 관리 하는 옵션이 없습니다. 저장소 마이그레이션 서비스 역할 및 기능에 포함 되지 않습니다.

이 문제는 Windows Server 2019의 평가 미디어에서 서비스 문제로 인해 발생 합니다. 

이 문제를 해결 하려면 일반 정품, MSDN, OEM 또는 볼륨 라이선스 버전의 Windows Server 2019를 설치 하 고 활성화 하지 마십시오. 활성화 하지 않고 모든 버전의 Windows Server는 180 일 평가 모드에서 작동합니다. 

Windows Server 2019의 이후 릴리스에서이 문제를 수정 했습니다.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>저장소 마이그레이션 서비스에서 전송 오류가 CSV 다운로드 시간이

전송 작업 자세한 오류 전용 CSV 로그를 다운로드 하려면 Windows Admin Center 또는 PowerShell 사용 하는 경우 오류가 발생 합니다.

 >   전송 로그-방화벽에서 허용 되는 파일 공유를 확인 하세요. : Net.tcp://localhost에 보낸이 요청 작업이: 28940/sms/service/1/전송 구성된 된 시간 제한 내에 회신을 받지 못했습니다 (00: 01:00). 이 작업에 할당 된 시간이 보다 긴 시간 제한의 일부 되었을 수 있습니다. 이 없거나 서비스 회신 메시지를 보낼 수 없습니다. 서비스가 아직 작업을 처리 하기 때문에 수 있습니다. 채널/프록시를 IContextChannel로 캐스팅 하 고 OperationTimeout 속성을 설정) (에서 작업 시간 제한 증가 고려 하 고 서비스 클라이언트에 연결할 수 있는지 확인 하세요.

이 문제는 매우 많은 수의 저장소 마이그레이션 서비스에서 허용 되는 기본 1 분 시간 제한에서 필터링 할 수 없는 전송된 파일 때문일 수 있습니다. 

이 문제를 해결 하려면:

1. Orchestrator 컴퓨터의 편집 된 *%SYSTEMROOT%\SMS\Microsoft.StorageMigration.Service.exe.config* Notepad.exe를 사용 하 여 10 분에서 1 분 기본값으로 "sendTimeout" 변경 하려면 파일

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Orchestrator 컴퓨터의 "저장소 마이그레이션 서비스" 서비스를 다시 시작 합니다. 
3. 오 케 스트레이 터 컴퓨터에 Regedit.exe를 시작 합니다.
4. 다음 레지스트리 하위 키를 찾아 클릭합니다. 

   `HKEY_LOCAL_MACHINE\\Software\\Microsoft\\SMSPowershell`

5. 편집 메뉴에서 새로 만들기를 가리킨 후 DWORD 값을 클릭합니다. 
6. DWORD의 이름을 "WcfOperationTimeoutInMinutes"를 입력 하 고 enter 키를 누릅니다.
7. "WcfOperationTimeoutInMinutes"를 마우스 오른쪽 단추로 클릭 하 고 수정을 클릭 합니다. 
8. 기본 데이터 상자에 "Decimal"를 클릭 합니다.
9. 값 데이터 상자에 "10"을 입력 하 고 확인을 클릭 합니다.
10. 레지스트리 편집기를 종료 합니다.
11. 오류 전용 CSV 파일을 다시 다운로드 하려고 시도 합니다. 

Windows Server 2019의 이후 릴리스에서이 동작을 변경 하려고 합니다.  

## <a name="cutover-fails-when-migrating-between-networks"></a>네트워크 간에 마이그레이션하는 경우 중단 실패

Azure IaaS 인스턴스로 같이 원본 이외의 다른 네트워크에서 실행 하는 대상 컴퓨터를 마이그레이션하는 경우 컷 오버 완료 하지 못한 소스에서 고정 IP 주소를 사용 합니다. 

이 동작은 기본적으로 사용자, 응용 프로그램 및 IP 주소를 통해 연결 하는 스크립트에서 마이그레이션 후 연결 문제를 방지 하도록 합니다. 이전 원본 컴퓨터에서 새 대상 IP 주소로 이동 하면 새 네트워크 서브넷 정보, 아마도 DNS 및 WINS 일치 하지 않습니다.

이 문제를 해결 하려면, 동일한 네트워크에서 컴퓨터에는 마이그레이션을 수행 합니다. 그런 다음 해당 컴퓨터를 새 네트워크를 이동 하 고 해당 IP 정보를 다시 할당 합니다. 예를 들어, Azure IaaS로 마이그레이션하는 경우 먼저 로컬 VM에 마이그레이션한 다음 Azure에 VM을 이동 하려면 Azure Migrate를 사용 합니다.  

Windows Admin Center 이후 릴리스에서이 문제를 수정 했습니다. 에서는 이제 있도록 대상 서버의 네트워크 설정을 변경 하지는 마이그레이션을 지정할 수 있습니다. 업데이트 된 확장 릴리스되면 여기 나열 됩니다. 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>대상 프록시 및 자격 증명 관리 권한에 대 한 유효성 검사 경고

전송 작업의 유효성을 검사 하는 경우 다음과 같은 경고가 표시 됩니다.

 > **자격 증명 관리 권한이 없습니다.**
 > 경고: 작업 원격으로 사용할 수 없습니다.
 > **대상 프록시 등록 됩니다.**
 > 경고: 대상 프록시를 찾을 수 없습니다.

때문 컴퓨터가 Windows Server 2016 또는 Windows Server 2012 R2 또는 Windows Server 2019 대상 컴퓨터 저장소 마이그레이션 서비스 프록시 서비스를 설치 하지 않은 경우이 동작은 의도적인 것입니다. 크게 향상 된 전송 성능에 대 한 설치 된 프록시를 사용 하 여 Windows Server 2019 컴퓨터로 마이그레이션하는 것이 좋습니다.  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>특정 파일 인벤토리 하지 않거나 전송, 오류 5 "액세스 거부 되었습니다."

인벤토리 또는 원본에서 대상 컴퓨터에 파일을 전송 하는 경우 파일을 사용자가 관리자 그룹 권한을 제거 하는 데는 마이그레이션에 실패 합니다. 저장소 마이그레이션 서비스 프록시 디버그 검사를 보여 줍니다.

  로그 이름:      Microsoft-Windows-StorageMigrationService-프록시/디버그 소스:        Microsoft-Windows-StorageMigrationService-Proxy Date:          2019/26/2 일 오전 9시: 04 이벤트 ID:      10000 작업 범주: None 수준:         오류 키워드:      
  사용자:          네트워크 서비스 컴퓨터: srv1.contoso.com 설명:

  02/26/2019-09:00:04.860 [Erro] Transfer error for \\srv1.contoso.com\public\indy.png: (5) 액세스가 거부 되었습니다.
Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile (문자열 fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes)에서 스택 추적: Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile (FileInfo 파일)에서 Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile (문자열 경로) Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer()에서 Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo() Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer() [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs::TryTransfer::55]


이 문제는 백업 권한이 호출 되지 않은 중인 저장소 마이그레이션 서비스에 코드 결함 때문일 수 있습니다. 

이 문제를 해결 하려면 설치 [Windows 업데이트 2019 년 4 월 2 일-KB4490481 (OS 빌드 17763.404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) 오 케 스트레이 터 컴퓨터에서 프록시 서비스가 설치 되 고 있는 경우 대상 컴퓨터에 있습니다. 원본 마이그레이션 사용자 계정에 원본 컴퓨터 및 저장소 마이그레이션 서비스 오 케 스트레이 터에서 로컬 관리자 인지 확인 합니다. 대상 마이그레이션 사용자 계정을 대상 컴퓨터 및 저장소 마이그레이션 서비스 오 케 스트레이 터에서 로컬 관리자 인지 확인 합니다. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>저장소 마이그레이션 서비스를 사용 하 여 데이터를 미리 시드하고 때 DFSR 해시가 일치 하지 않습니다

파일을 전송 하는 새 대상 Storage Migration Service를 사용 하는 경우 다음 presseded 복제 또는 복제, DFSR 데이터베이스를 모든 파일 experiemce 해시를 통해 기존 DFSR 서버를 사용 하 여 해당 데이터를 복제 하려면 DFS 복제 (DFSR) 구성 일치 하지 않습니다 되며 다시 복제 합니다. 데이터 스트림, 보안 스트림, 크기 및 SMS를 사용 하 여 전송 합니다 완벽 하 게 일치 시킬 표시 하는 모든 특성. 검사 ICACLS 사용 하 여 파일 또는 DFSR 데이터베이스 복제 디버그 로그 표시 됩니다.

소스 파일:

  icacls d:\test\Source:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png D:AI(A;;FA;;;BA)(A;;0x1200a9;;;DD)(A;;0x1301bf;;;DU)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)

대상 파일:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png D:AI(A;;FA;;;BA)(A;;0x1301bf;;;DU)(A;;0x1200a9;;;DD)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)**S:PAINO_ACCESS_CONTROL**

DFSR 디버그 로그:

  20190308 10:18:53.116 3948 DBCL 4045 [경고] DBClone::IDTableImportUpdate 불일치 레코드를 찾을 수 있습니다. 

  Local ACL hash:1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime:20190308 18:09:44.876 FileSizeLow:1131654 FileSizeHigh:0 Attributes:32 

  ACL 해시를 복제 합니다.**DDC4FCE4 DDF329C4-977CED6D F4D72A5B** LastWriteTime:20190308 18:09:44.876 FileSizeLow:1131654 FileSizeHigh:0 특성: 32 

이 문제는 보안 감사 Acl (SACL)를 설정 하는 저장소 마이그레이션 서비스에서 사용 하는 라이브러리의 코드 결함으로 발생 합니다. Null이 아닌 SACL SACL 해시가 일치 하지 않습니다를 올바르게 식별 하는 DFSR 선행 비어 있는 경우에 의도 하지 않게 설정 됩니다. 

이 문제를 해결 하려면,에 대 한 Robocopy를 사용 하 여 계속 [사전 시드가 DFSR 및 복제 작업 하는 DFSR 데이터베이스](../dfs-replication/preseed-dfsr-with-robocopy.md) Storage Migration Service를 대신 합니다. 이 문제를 조사 하 고 Windows Server 및 Windows 업데이트 하는 백 포팅의 이후 버전에서는이 문제를 해결 하려면. 

## <a name="error-404-when-downloading-csv-logs"></a>CSV를 다운로드할 때 404 오류 로그

전송 작업의 끝에 전송 또는 오류 로그를 다운로드 하려고 시도할 때, 오류가 발생 합니다.

  $jobname: 로그 전송: ajax 오류 404

오 케 스트레이 터 서버의 "파일 및 프린터 공유 (Smb-in)" 방화벽 규칙을 설정 하지 않은 경우이 오류가 예상 됩니다. Windows Admin Center 파일 다운로드에는 포트 445 TCP / (SMB) 연결 된 컴퓨터에 필요합니다.  

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transfering-from-windows-server-2008-r2"></a>오류 "수 없습니다 저장소에서 전송 끝점" 때 Windows Server 2008 R2에서 전송

Windows Server 2008 R2 원본 컴퓨터에서 데이터를 전송 하는 동안, 데이터 trasnfers 없습니다 하며 오류가 발생 합니다.  

  끝점 중 하나에서 저장소를 전송할 수 없습니다.
0x9044

Windows Server 2008 R2 컴퓨터 되지 않습니다 Windows Update에서 모든 필수 및 중요 업데이트를 사용 하 여 완전히 패치 된 경우이 오류가 예상 됩니다. 저장소 마이그레이션 서비스에 관계 없이 항상 좋습니다 보안상의 이유로 Windows Server 2008 R2 컴퓨터를 패치 해당 운영 체제는 최신 버전의 Windows Server의 향상 된 보안 기능을 포함 하지 않습니다.

## <a name="see-also"></a>참조

- [저장소 서비스 마이그레이션 개요](overview.md)
