---
title: Storage Migration Service 질문과 대답 (FAQ)
description: 서버 간에 마이그레이션할 때 전송에서 제외 되는 파일을 비롯 하 여 저장소 마이그레이션 서비스에 대해 자주 묻는 질문과 대답입니다.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 08/19/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: b7a6dd37cfc054ead153d274ffa7f0d13844305e
ms.sourcegitcommit: 10331ff4f74bac50e208ba8ec8a63d10cfa768cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2020
ms.locfileid: "75953027"
---
# <a name="storage-migration-service-frequently-asked-questions-faq"></a>Storage Migration Service 질문과 대답 (FAQ)

이 항목에는 [Storage Migration Service](overview.md) 를 사용 하 여 서버를 마이그레이션하는 방법에 대 한 faq (질문과 대답)가 포함 되어 있습니다.

## <a name="what-files-and-folders-are-excluded-from-transfers"></a>전송에서 제외 되는 파일 및 폴더는 무엇입니까?

Storage Migration Service는 Windows 작업에 방해가 될 수 있는 파일 또는 폴더를 전송 하지 않습니다. 특히 대상의 PreExistingData 폴더로 전송 하거나 이동 하지 않는 항목은 다음과 같습니다.

- Windows, 프로그램 파일, 프로그램 파일 (x86), 프로그램 데이터, 사용자
- $Recycle. bin, Recycler, 재활용, 시스템 볼륨 정보, $UpgDrv $, $SysReset, $Windows $Windows BT,. ~ LS, Windows 이전, 부팅, 복구, 문서 및 설정
- 파일 시스템, hiberfil, 스왑 파일, winpepge.sys, config.sys, bootsect, bootmgr, bootnxt
- 대상에서 제외 된 폴더와 충돌 하는 원본 서버의 파일 또는 폴더입니다. <br>예를 들어 원본에 N:\Windows 폴더가 있는 경우이 폴더는 C:\에 매핑됩니다. 대상의 볼륨은 대상의 C:\Windows 시스템 폴더에 방해가 되기 때문에 포함 된 항목에 관계 없이 전송 되지 않습니다.

## <a name="are-domain-migrations-supported"></a>도메인 마이그레이션이 지원 되나요?

저장소 마이그레이션 서비스는 Active Directory 도메인 간의 마이그레이션을 허용 하지 않습니다. 서버 간 마이그레이션은 항상 대상 서버를 동일한 도메인에 가입 시킵니다. Active Directory 포리스트에서 다른 도메인의 마이그레이션 자격 증명을 사용할 수 있습니다. 저장소 마이그레이션 서비스는 작업 그룹 간의 마이그레이션을 지원 합니다.  

## <a name="are-clusters-supported-as-sources-or-destinations"></a>클러스터가 원본 또는 대상으로 지원 되나요?

Storage Migration Service는 누적 업데이트 [KB4513534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 또는 후속 업데이트를 설치한 후 클러스터에서로의 마이그레이션을 지원 합니다. 여기에는 장치 통합을 위해 원본 클러스터에서 대상 클러스터로 마이그레이션하는 것 뿐만 아니라 독립 실행형 원본 서버에서 대상 클러스터로 마이그레이션하는 작업이 포함 됩니다. 

## <a name="do-local-groups-and-local-users-migrate"></a>로컬 그룹 및 로컬 사용자를 마이그레이션해야 하나요?

Storage Migration Service는 누적 업데이트 [KB4513534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 또는 후속 업데이트를 설치한 후 로컬 사용자 및 그룹의 마이그레이션을 지원 합니다. 

## <a name="is-domain-controller-migration-supported"></a>도메인 컨트롤러 마이그레이션이 지원 되나요?

저장소 마이그레이션 서비스는 현재 Windows Server 2019에서 도메인 컨트롤러를 마이그레이션하지 않습니다. 한 가지 해결 방법으로, Active Directory 도메인에 도메인 컨트롤러가 두 개 이상 있는 한 도메인 컨트롤러를 마이그레이션한 후에 도메인 컨트롤러의 수준을 내린 후 이동이 완료 되 면 대상의 수준을 올립니다. 도메인 컨트롤러 원본 또는 대상을 마이그레이션하도록 선택 하는 경우에는 이동할 수 없습니다. 에서 도메인 컨트롤러로 마이그레이션할 때는 사용자 및 그룹을 마이그레이션하지 않아야 합니다.

## <a name="what-attributes-are-migrated-by-the-storage-migration-service"></a>저장소 마이그레이션 서비스에서 마이그레이션되는 특성은 무엇 인가요?

Storage Migration Service는 SMB 공유의 모든 플래그, 설정 및 보안을 마이그레이션합니다. 저장소 마이그레이션 서비스에서 마이그레이션하는 플래그 목록에는 다음이 포함 됩니다.

    - 공유 상태
    - 가용성 유형
    - 공유 유형
    - 폴더 열거 모드 *(즉, Access 기반 열거 또는 ABE)*
    - 캐싱 모드
    - 임대 모드
    - Smb 인스턴스
    - CA 제한 시간
    - 동시 사용자 제한
    - 지속적으로 사용 가능
    - 설명           
    - 데이터 암호화
    - Id 원격
    - 인프라
    - Name(이름)
    - 경로
    - Scoped
    - 범위 이름
    - 보안 설명자
    - 섀도 복사본
    - 특수
    - 임시

## <a name="can-i-consolidate-multiple-servers-into-one-server"></a>여러 서버를 하나의 서버로 통합할 수 있나요?

Windows Server 2019에 제공 된 Storage Migration Service 버전은 여러 서버를 하나의 서버로 통합 하는 기능을 지원 하지 않습니다. 통합의 예는 서로 다른 세 원본 서버를 마이그레이션하는 것입니다 .이 경우 중복 또는 충돌을 방지 하기 위해 해당 경로 및 공유를 가상화 한 단일 새 서버에 공유 이름 및 로컬 파일 경로가 동일 합니다. 이전 서버 이름 및 IP 주소입니다. 그러나 단일 클러스터에서 독립 실행형 서버를 여러 파일 서버 리소스로 마이그레이션할 수 있습니다. 

## <a name="can-i-migrate-from-sources-other-than-windows-server"></a>Windows Server 이외의 원본에서 마이그레이션할 수 있나요?

Storage Migration Service는 누적 업데이트 [KB4513534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 또는 후속 업데이트를 설치한 후에 Samba Linux 서버에서의 마이그레이션을 지원 합니다. 지원 되는 Samba 버전 및 Linux 배포판의 목록에 대 한 요구 사항을 참조 하세요.

## <a name="can-i-migrate-previous-file-versions"></a>이전 파일 버전을 마이그레이션할 수 있나요?

Windows Server 2019에 제공 된 Storage Migration Service 버전은 파일의 이전 버전 (볼륨 섀도 복사본 서비스를 사용 하 여 만든) 마이그레이션을 지원 하지 않습니다. 현재 버전만 마이그레이션됩니다. 

## <a name="optimizing-inventory-and-transfer-performance"></a>인벤토리 및 전송 성능 최적화

Storage Migration Service는 저장소 마이그레이션 서비스 프록시 서비스 라고 하는 다중 스레드 읽기 및 복사 엔진을 포함 하며,이 엔진은 많은 파일 복사 도구에서 완벽 한 데이터 충실도를 제공 하는 것 외에도 신속 하 게 사용할 수 있도록 설계 되었습니다. 기본 구성은 많은 고객에 게 가장 적합 하지만 인벤토리 및 전송 중에 SMS 성능을 향상 시킬 수 있는 방법이 있습니다.

- **대상 운영 체제에 Windows Server 2019를 사용 합니다.** Windows Server 2019에는 저장소 마이그레이션 서비스 프록시 서비스가 포함 되어 있습니다. 이 기능을 설치 하 고 Windows Server 2019 대상으로 마이그레이션하는 경우 모든 전송은 원본 및 대상 간의 직접적인 시야로 작동 합니다. 대상 컴퓨터가 Windows Server 2012 R2 또는 Windows Server 2016 인 경우이 서비스는 전송 하는 동안 orchestrator에서 실행 되며,이는 이중 홉을 전송 하 고 훨씬 더 느립니다. Windows Server 2012 R2 또는 Windows Server 2016 대상으로 실행 되는 여러 작업이 있는 경우 오 케 스트레이 터가 병목 상태가 됩니다. 

- **기본 전송 스레드를 변경 합니다.** 저장소 마이그레이션 서비스 프록시 서비스는 지정 된 작업에서 동시에 8 개의 파일을 복사 합니다. 저장소 마이그레이션 서비스 프록시를 실행 하는 모든 노드에서 다음 레지스트리 REG_DWORD 값 이름을 10 진수로 조정 하 여 동시 복사 스레드 수를 늘릴 수 있습니다.

    HKEY_Local_Machine \Software\Microsoft\SMSProxy
    
    FileTransferThreadCount

   Windows Server 2019에서 유효한 범위는 1 ~ 128입니다. 변경한 후에는 마이그레이션에 참여 하는 모든 컴퓨터에서 Storage Migration Service 프록시 서비스를 다시 시작 해야 합니다. 이 설정에서는 주의를 기울여야 합니다. 더 높게 설정 하려면 추가 코어, 저장소 성능 및 네트워크 대역폭이 필요할 수 있습니다. 너무 높게 설정 하면 기본 설정에 비해 성능이 저하 될 수 있습니다.

- **코어 및 메모리를 추가 합니다.**  원본, orchestrator 및 대상 컴퓨터에 두 개 이상의 프로세서 코어가 있거나 두 개의 vCPUs가 있는 것이 좋습니다. 특히 FileTransferThreadCount (위)와 함께 사용 하는 경우 인벤토리 및 전송 성능을 크게 지원할 수 있습니다. 일반적인 사무실 형식 (기가바이트 이상) 보다 큰 파일을 전송 하는 경우 전송 성능은 기본 2GB 최소값 보다 많은 메모리를 활용 합니다.

- **여러 작업을 만듭니다.** 여러 서버 소스가 포함 된 작업을 만들 때 각 서버는 인벤토리, 전송 및 사용을 위해 일련의 방식으로 연결 됩니다. 즉, 각 서버는 다른 서버를 시작 하기 전에 해당 단계를 완료 해야 합니다. 더 많은 서버를 병렬로 실행 하려면 각 작업에 하나의 서버만 포함 된 여러 작업을 만들면 됩니다. SMS는 동시에 실행 되는 최대 100의 작업을 지원 합니다. 즉, 단일 orchestrator에서 많은 Windows Server 2019 대상 컴퓨터를 병렬화 할 수 있습니다. 대상 컴퓨터가 대상 컴퓨터에서 실행 되 고 있지 않고 Windows Server 2016 또는 Windows Server 2012 r 2 인 경우 여러 병렬 작업을 실행 하지 않는 것이 좋습니다. 오 케 스트레이 터는 모든 전송 작업을 수행 해야 하며 상태가. 서버를 단일 작업 내에서 병렬로 실행 하는 기능은 이후 버전의 SMS에서 추가할 계획입니다.

- **RDMA 네트워크에서 SMB 3을 사용 합니다.** Windows Server 2012 이상 원본 컴퓨터에서 전송 하는 경우 SMB 3.x는 SMB 직접 모드와 RDMA 네트워킹을 지원 합니다. RDMA는 마더보드 Cpu에서 온보드 NIC 프로세서로 전송 되는 대부분의 CPU 비용을 이동 하 여 대기 시간 및 서버 CPU 사용률을 줄입니다. 또한 ROCE 및 iWARP와 같은 RDMA 네트워크는 일반적으로 25, 50 및 인터페이스당 100Gb 속도를 포함 하 여 일반적인 TCP/IP 보다 훨씬 더 높은 대역폭을 갖습니다. 일반적으로 SMB 다이렉트를 사용 하면 네트워크에서 저장소 자체로 전송 속도 제한을 이동 합니다.   

- **SMB 3 다중 채널을 사용 합니다.** Windows Server 2012 이상 원본 컴퓨터에서 전송 하는 경우 SMB 3.x는 파일 복사 성능을 크게 향상 시킬 수 있는 다중 채널 복사본을 지원 합니다. 이 기능은 원본 및 대상 모두에 게 자동으로 적용 됩니다.

   - 여러 네트워크 어댑터
   - RSS (수신측 배율)를 지 원하는 하나 이상의 네트워크 어댑터
   - NIC 팀을 사용 하 여 구성 된 네트워크 어댑터 중 하나
   - RDMA를 지원하는 하나 이상의 네트워크 어댑터

- **드라이버를 업데이트 합니다.** 필요에 따라 원본, 대상 및 오 케 스트레이 터 서버에 최신 공급 업체 저장소와 엔클로저 펌웨어 및 드라이버, 최신 공급 업체 HBA 드라이버, 최신 공급 업체 BIOS/UEFI 펌웨어, 최신 공급 업체 네트워크 드라이버 및 최신 마더보드 칩셋 드라이버를 설치 합니다. 필요에 따라 노드를 다시 시작합니다. 공유 저장소 및 네트워킹 하드웨어 구성은 하드웨어 공급업체 설명서를 참조하세요.

- **고성능 처리를 사용 합니다.** 서버의 BIOS/UEFI 설정이 고성능을 지원하는지 확인합니다(예: C-상태 사용 안 함, QPI 속도 설정, NUMA 사용, 가장 높은 메모리 주파수 설정 등). Windows Server의 전원 관리가 고성능으로 설정 되어 있는지 확인 합니다. 필요에 따라 다시 시작합니다. 마이그레이션을 완료 한 후에는 이러한 상태를 적절 한 상태로 되돌리는 것을 잊지 마세요. 

- **하드웨어 조정** Windows server 2019 및 Windows Server 2016를 실행 하는 orchestrator 및 대상 컴퓨터를 튜닝 하기 위해 [Windows server 2016에 대 한 성능 조정 지침](https://docs.microsoft.com/windows-server/administration/performance-tuning/) 을 검토 합니다. [네트워크 하위 시스템 성능 튜닝](https://docs.microsoft.com/windows-server/networking/technologies/network-subsystem/net-sub-performance-tuning-nics) 섹션에는 특히 중요 한 정보가 포함 되어 있습니다.

- **더 빠른 저장소를 사용 합니다.** 원본 컴퓨터 저장소 속도를 업그레이드 하는 것이 어려울 수 있지만 전송에서 불필요 한 병목 현상이 발생 하지 않도록 하기 위해 원본에서 읽기 IO 성능에 있기 때문에 대상 저장소가 적어도 쓰기 IO 성능 보다 빨라야 합니다. 대상이 VM 인 경우 최소한 마이그레이션의 경우에는 최소한 하이퍼바이저 호스트의 가장 빠른 저장소 계층에서 실행 해야 합니다. 예를 들어, 미러된 모든 플래시 또는 하이브리드 공간을 활용 하는 스토리지 공간 다이렉트 HCI 클러스터를 사용 합니다. SMS 마이그레이션이 완료 되 면 VM을 느린 계층 또는 호스트로 실시간 마이그레이션할 수 있습니다.

- **바이러스 백신을 업데이트 합니다.** 항상 원본 및 대상에서 최신 패치 버전의 바이러스 백신 소프트웨어를 실행 하 고 있는지 확인 하 여 성능 오버 헤드를 최소화 합니다. 테스트로 원본 서버와 대상 서버에서 인벤토리 또는 마이그레이션 중인 폴더의 검색을 *일시적으로* 제외할 수 있습니다. 전송 성능이 향상 되 면 바이러스 백신 소프트웨어 공급 업체에 문의 하거나 업데이트 된 버전의 바이러스 백신 소프트웨어 또는 예상 되는 성능 저하에 대 한 설명을 참조 하십시오.

## <a name="can-i-migrate-from-ntfs-to-refs"></a>NTFS에서 REFS로 마이그레이션할 수 있나요?

Windows Server 2019에 제공 된 Storage Migration Service 버전은 NTFS에서 REFS 파일 시스템으로의 마이그레이션을 지원 하지 않습니다. NTFS에서 NTFS로, REFS에서 refs로 마이그레이션할 수 있습니다. 이는 기능, 메타 데이터 및 ReFS가 NTFS에서 중복 되지 않는 다른 측면에서 많은 차이점이 있기 때문에 의도 된 것입니다. ReFS는 일반 파일 시스템이 아닌 응용 프로그램 작업 파일 시스템으로 사용 됩니다. 자세한 내용은 [ReFS (복원 파일 시스템) 개요](../refs/refs-overview.md) 를 참조 하세요. 

## <a name="can-i-move-the-storage-migration-service-database"></a>Storage Migration Service 데이터베이스를 이동할 수 있나요?

Storage Migration Service는 기본적으로 hidden c:\programdata\microsoft\storagemigrationservice 폴더에 설치 된 ESE (extensible Storage engine) 데이터베이스를 사용 합니다. 이 데이터베이스는 작업이 추가 되 고 전송이 완료 되 면 증가 하며, 작업을 삭제 하지 않을 경우 수백만 개의 파일을 마이그레이션한 후에는 상당한 드라이브 공간을 사용할 수 있습니다. 데이터베이스를 이동 해야 하는 경우 다음 단계를 수행 합니다.

1. Orchestrator 컴퓨터에서 "Storage Migration Service" 서비스를 중지 합니다.
2. `%programdata%/Microsoft/StorageMigrationService` 폴더의 소유권 가져오기
3. 해당 공유 및 모든 파일 및 하위 폴더에 대 한 모든 권한을 보유 하는 사용자 계정을 추가 합니다.
4. Orchestrator 컴퓨터의 다른 드라이브로 폴더를 이동 합니다.
5. 다음 레지스트리 REG_SZ 값을 설정 합니다.

    HKEY_Local_Machine \Software\Microsoft\SMS DatabasePath = *다른 볼륨의 새 데이터베이스 폴더에* 대 한 경로입니다. 
6. 시스템에 해당 폴더의 모든 파일 및 하위 폴더에 대 한 모든 권한이 있는지 확인 합니다.
7. 자신의 계정 사용 권한을 제거 합니다.
8. "Storage Migration Service" 서비스를 시작 합니다.

## <a name="give-feedback"></a>사용자 의견을 제공 하거나, 버그를 제공 하거나, 지원을 받을 수 있는 옵션은 무엇 인가요?

Storage Migration Service에 대 한 피드백을 제공 하려면:

- Windows 10에 포함 된 피드백 허브 도구를 사용 하 여 "기능 제안"을 클릭 하 고 "Windows Server" 범주 및 "저장소 마이그레이션"의 하위 범주를 지정 합니다.
- [Windows Server UserVoice](https://windowsserver.uservoice.com) 사이트 사용
- 메일 smsfeed@microsoft.com

파일 버그:

- Windows 10에 포함 된 피드백 허브 도구를 사용 하 여 "문제 보고"를 클릭 하 고 "Windows Server" 범주 및 "저장소 마이그레이션"의 하위 범주를 지정 합니다.
- [Microsoft 지원](https://support.microsoft.com) 를 통해 지원 사례를 엽니다.

지원 받기:

 - [Windows Server 기술 커뮤니티](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server) 에 질문을 게시 합니다.
 - [Windows Server 2019 Technet 포럼](https://social.technet.microsoft.com/Forums/en-US/home?forum=ws2019&filter=alltypes&sort=lastpostdesc) 에 게시 
 - [Microsoft 지원](https://support.microsoft.com) 를 통해 지원 사례를 엽니다.

## <a name="see-also"></a>참고 항목

- [Storage Migration Service 개요](overview.md)
