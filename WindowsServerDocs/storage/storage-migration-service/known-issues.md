---
title: Storage Migration Service의 알려진 문제
description: 알려진된 문제 및 Microsoft 지원에 대 한 로그를 수집 하는 방법과 같은 저장소 마이그레이션 서비스에 대 한 문제 해결 지원 합니다.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 02/27/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: f5fefab2c1b7ba8b62ffd6734217eab9a13ae95e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888874"
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

Windows Server의 이후 릴리스에서이 문제를 해결 하려고 합니다. 통해 지원 사례를 여세요 [Microsoft 지원](https://support.microsoft.com) 요청을 백 포팅이 수정이 프로그램을 만들 수 있습니다.

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

대상 VM으로 마이그레이션하는 경우 Azure IaaS 인스턴스로 같이 원본 이외의 다른 네트워크에서 실행 중인 중단 완료 하지 못한 소스에서 고정 IP 주소를 사용 합니다. 

이 동작은 기본적으로 사용자, 응용 프로그램 및 IP 주소를 통해 연결 하는 스크립트에서 마이그레이션 후 연결 문제를 방지 하도록 합니다. 이전 원본 컴퓨터에서 새 대상 IP 주소로 이동 하면 새 네트워크 서브넷 정보, 아마도 DNS 및 WINS 일치 하지 않습니다.

이 문제를 해결 하려면, 동일한 네트워크에서 컴퓨터에는 마이그레이션을 수행 합니다. 그런 다음 해당 컴퓨터를 새 네트워크를 이동 하 고 해당 IP 정보를 다시 할당 합니다. 예를 들어, Azure IaaS로 마이그레이션하는 경우 먼저 로컬 VM에 마이그레이션한 다음 Azure에 VM을 이동 하려면 Azure Migrate를 사용 합니다.  

Windows Server 2019의 이후 릴리스에서이 문제를 수정 했습니다. 에서는 이제 있도록 대상 서버의 네트워크 설정을 변경 하지는 마이그레이션을 지정할 수 있습니다. 일반적인 월별 업데이트 주기의 일환으로 Windows Server 2019의 기존 버전에 대 한 업데이트를 출시 될 수 있습니다. 


## <a name="see-also"></a>참조

- [저장소 서비스 마이그레이션 개요](overview.md)