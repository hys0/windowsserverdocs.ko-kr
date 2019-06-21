---
title: 저장소 마이그레이션 서비스 질문과 대답 (FAQ)
description: 다른 서버에서 마이그레이션할 때 파일 전송에서 제외 됩니다와 같은 저장소 마이그레이션 서비스에 대 한 질문과 대답입니다.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 06/04/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 8f0f16f14ccf9099af8ff8bb8b27209c75c87cfc
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284464"
---
# <a name="storage-migration-service-frequently-asked-questions-faq"></a>저장소 마이그레이션 서비스 질문과 대답 (FAQ)

이 항목에서는 사용에 대 한 자주 묻는 질문과 대답 (Faq)를 포함 [저장소 마이그레이션 서비스](overview.md) 서버를 마이그레이션하려 합니다.

## <a name="excluded-files"></a> 전송에서 파일 및 프로그램으로 제외 되나요?

저장소 마이그레이션 서비스는 Windows 작업을 방해할 수 있음을 알고 있는 폴더나 파일 전송 되지 않습니다. 특히, 다음과 같습니다. 어떤 하거나 하지 않습니다 전송 대상 PreExistingData 폴더로 이동

- Windows에서 프로그램 파일, 프로그램 파일 (x86)를 프로그램 데이터를 사용자
- $Recycle.bin, 시스템 볼륨 정보, 재생기, Recycled $UpgDrv$, $SysReset, $Windows. ~ BT $Windows. ~ LS, Windows.old, 부팅, 복구, Documents and Settings
- pagefile.sys, hiberfil.sys, swapfile.sys, winpepge.sys, config.sys, bootsect.bak, bootmgr, bootnxt
- 파일 또는 대상에서 제외 된 폴더를 사용 하 여 충돌 하는 원본 서버의 폴더입니다. <br>예를 들어 원본에서 N:\Windows 폴더가 있으며 C:\에 매핑되 볼륨에서 대상에는 전송 가져올 없습니다-내용에 관계 없이-C:\Windows 시스템 폴더 대상에 방해 하기 때문에 있습니다.

## <a name="domain-migration"></a> 도메인 마이그레이션 지원 되나요?

저장소 마이그레이션 서비스 간의 Active Directory 도메인 마이그레이션 허용 하지 않습니다. 서버 간의 마이그레이션이 동일한 도메인에 대상 서버를 조인 항상 됩니다. Active Directory 포리스트의 다른 도메인에서 마이그레이션 자격 증명을 사용할 수 있습니다. 저장소 마이그레이션 서비스 작업 그룹 간 마이그레이션 지원지 않습니다.  

## <a name="cluster-support"></a> 원본 또는 대상으로 클러스터 지원 되나요?

저장소 마이그레이션 서비스 Windows Server 2019에는 클러스터 간의 마이그레이션 현재 하지 않습니다. 클러스터 지원 Storage Migration Service의 이후 릴리스에서 추가할 예정입니다.

## <a name="local-principals"></a> 로컬 그룹 및 로컬 사용자가 마이그레이션할?

저장소 마이그레이션 서비스는 로컬 사용자 또는 Windows Server 2019에서 로컬 그룹에 현재 마이그레이션할 하지 않습니다. 로컬 사용자 및 로컬 그룹 마이그레이션을 지원 저장소 마이그레이션 서비스의 향후 릴리스에서 추가할 예정입니다.

## <a name="domain-controller"></a> 도메인 컨트롤러 마이그레이션 지원

저장소 마이그레이션 서비스 Windows Server 2019에 도메인 컨트롤러를 현재 마이그레이션할 하지 않습니다. 둘 이상의 도메인 컨트롤러는 Active Directory 도메인에 있는으로 강등 하기 전에 도메인 컨트롤러 대 안으로 이동이 완료 된 후 대상을 승격 한 다음, 마이그레이션. 도메인 컨트롤러 마이그레이션 지원 Storage Migration Service의 이후 릴리스에서 추가할 예정입니다.

## <a name="share-attributes"></a> 특성은 저장소 Migration Service를 통해 마이그레이션되지?

저장소 마이그레이션 서비스는 모든 플래그, 설정 및 SMB 공유의 보안을 마이그레이션합니다. 저장소 마이그레이션 서비스를 마이그레이션하는 플래그의 해당 목록에는 다음이 포함 됩니다.

    - 공유 상태
    - 가용성 유형
    - 공유 유형
    - 폴더 열거 모드 *(즉, 액세스 기반 열거 또는 ABE)*
    - 캐싱 모드
    - 임대 모드
    - Smb 인스턴스
    - CA 시간 제한
    - 동시 사용자 제한
    - 지속적으로 사용 가능한
    - 설명           
    - 데이터 암호화
    - Identity 원격
    - 인프라
    - 이름
    - Path
    - 범위
    - 범위 이름
    - 보안 설명자
    - 섀도 복사본
    - 특수
    - 임시

## <a name="move-db"></a> 저장소 마이그레이션 서비스 데이터베이스를 이동할 수 있나요?

저장소 마이그레이션 서비스에는 기본적으로 숨겨진된 c:\programdata\microsoft\storagemigrationservice 폴더에 설치 되어 있는 확장 가능한 저장소 엔진 (ESE) 데이터베이스를 사용 합니다. 작업 추가 되 고 전송을 완료 하 고 마이그레이션 후 중요 한 드라이브 공간을 사용할 수 있습니다이 데이터베이스가 더 커져서 수백만 개의 파일 작업을 삭제 하지 않는 경우. 데이터베이스를 이동 해야 하는 경우 다음 단계를 수행 합니다.

1. Orchestrator 컴퓨터의 "저장소 마이그레이션 서비스" 서비스를 중지 합니다.
2. 소유권을 `%programdata%/Microsoft/StorageMigrationService` 폴더
3. 공유를 통해 모든 권한을 가질 사용자 계정 및 모든 파일과 하위 폴더를 추가 합니다.
4. Orchestrator 컴퓨터의 다른 드라이브에 폴더를 이동 합니다.
5. 다음 레지스트리 REG_SZ 값을 설정 합니다.

    HKEY_Local_Machine\Software\Microsoft\SMS DatabasePath = *다른 볼륨에 새 데이터베이스 폴더의 경로를* 입니다. 
6. 시스템에 모든 파일 및 폴더의 하위 폴더에 모든 권한을 갖고 있는지 확인 합니다.
7. 사용자 고유의 계정 권한을 제거 합니다.
8. "저장소 마이그레이션 서비스" 서비스를 시작 합니다.

## <a name="non-windows"></a> Windows Server 이외의 원본에서 마이그레이션할 수 있나요?

Windows Server 2019에 제공 하는 저장소 마이그레이션 서비스 버전에서 Windows Server 2003 및 이후 운영 체제 마이그레이션 지원 합니다. Linux, Samba, NetApp, EMC, 또는 다른 SAN 및 NAS 저장소 장치에서 현재 마이그레이션할 수 없습니다. 저장소 마이그레이션 서비스, Linux Samba 지원 시작의 이후 버전에서이 허용 하도록 계획 합니다.

## <a name="previous-versions"></a> 이전 파일 버전을 마이그레이션할 수 있나요?

Windows Server 2019에 제공 하는 저장소 마이그레이션 서비스 버전으로 마이그레이션 (볼륨 섀도 복사본 서비스를 사용 하 여 만든) 파일의 이전 버전을 지원 하지 않습니다. 현재 버전에만 마이그레이션됩니다. 

## <a name="ntfs-refs"></a> REFS에 NTFS에서 마이그레이션할 수 있습니까?

Windows Server 2019에 제공 하는 저장소 마이그레이션 서비스 버전은 NTFS에서 REFS 파일 시스템으로 마이그레이션 지원 하지 않습니다. NTFS 및 ReFS REFS NTFS에서 마이그레이션할 수 있습니다. 기본적으로 기능, 메타 데이터 및 NTFS에서 ReFS 중복 되지 않게 하는 다른 측면에서 많은 차이 때문입니다. ReFS는 응용 프로그램 워크 로드 파일 시스템의 일반 파일 시스템이 아닌로 제공 됩니다. 자세한 내용은 참조 하세요. [(ReFS) 복원 파일 시스템 개요](../refs/refs-overview.md)

## <a name="consolidate-servers"></a> 하나의 서버에 여러 서버 통합

Windows Server 2019에 제공 하는 저장소 마이그레이션 서비스 버전 여러 서버가 하나의 서버 통합을 지원 하지 않습니다. 통합의 예로 동일한 공유 이름을 가질 수 있는 세 가지 별도 소스 서버-마이그레이션 수 및 해당 경로 및 모든 중첩 되거나 충돌을 방지 하기 위해 공유를 가상화 하는 단일 새 서버로 로컬 파일 경로-에 다음 세 가지 모두 응답 이전 서버 이름과 IP 주소입니다. 저장소 마이그레이션 서비스의 향후 버전에서이 기능을 추가할 수 있습니다 했습니다.  

## <a name="optimize"></a> 인벤토리 및 전송 성능 최적화

저장소 마이그레이션 서비스를 다중 스레드 읽기 및 빠른 둘 다를 수 뿐만 아니라 완벽 한 데이터 정확성 부족 많은 파일 복사 도구와 함께 설계 했습니다 저장소 마이그레이션 서비스 프록시 서비스를 호출 하는 복사 엔진을 포함 합니다. 기본 구성을 많은 고객에 대 한 최적의 수, 하는 동안에 인벤토리 및 전송 하는 동안 SMS 성능 향상을 위해 가지가 있습니다.

- **대상 운영 체제에 대 한 Windows Server 2019를 사용 합니다.** Windows Server 2019 저장소 마이그레이션 서비스 프록시 서비스를 포함합니다. 이 기능을 설치 하 고 Windows Server 2019 대상으로 마이그레이션할 때 모든 전송을 직접 가시선 원본과 대상 간에으로 작동 합니다. 이 서비스 대상 컴퓨터가 Windows Server 2012 R2 또는 Windows Server 2016, 즉, 전송 더블 홉 있으며 훨씬 성능이 저하 됩니다 하는 경우는 오 케 스트레이 터에 전송 하는 동안 실행 됩니다. Windows Server 2012 R2 또는 Windows Server 2016 대상을 사용 하 여 실행 중인 여러 작업의 경우는 오 케 스트레이 터 병목이 될 수 있습니다. 

- **기본 전송 스레드를 변경 합니다.** 저장소 마이그레이션 서비스 프록시 서비스에서 지정된 된 작업을 동시에 8 개의 파일을 복사합니다. 10 진수 SMS 프록시를 실행 중인 모든 노드에서 다음 레지스트리 REG_DWORD 값 이름을 조정 하 여 동시 복사 스레드 수를 늘릴 수 있습니다.

    HKEY_Local_Machine\Software\Microsoft\SMSProxy   FileTransferThreadCount

   유효한 범위는 Windows Server 2019에 1 ~ 128입니다. 변경한 후 마이그레이션을에 참여 하는 모든 컴퓨터 저장소 마이그레이션 서비스 프록시 서비스에 다시 시작 해야 합니다. 이 설정을 사용할 때는 주의 더 높은 설정 추가 코어, 저장소 성능 및 네트워크 대역폭 필요할 수 있습니다. 너무 높게 설정 기본 설정에 비해 성능이 저하 될 수 있습니다. SMS의 이후 버전에 대 한 CPU, 메모리, 네트워크 및 저장소를 기준으로 스레드 설정을 자동으로 변경 하는 기능 예정 되어 있습니다.

- **코어 및 메모리를 추가 합니다.**  오 케 스트레이 터를 원본과 대상 컴퓨터에 있는 두 개 이상의 프로세서 코어 또는 두 개의 Vcpu를 더 크게 도움을 줄 수 인벤토리 및 전송 성능을 FileTransferThreadCount (위)를 함께 사용 하면 특히 것이 좋습니다. 일반적인 Office 형식 보다 큰 파일을 전송 하는 경우 (기가바이트 이상)에서 기본 2GB 최소값 보다 더 많은 메모리 전송 성능이 향상 됩니다.

- **여러 작업을 만듭니다.** 인벤토리를 전송 하기 위해 직렬 방식으로 각 서버에 연결 된 여러 서버 소스를 사용 하 여 작업을 만들 때 중단 하 고 있습니다. 즉, 각 서버가 다른 서버를 시작 하기 전에 해당 단계를 완료 해야 합니다. 더 많은 서버를 병렬로 실행 하려면 단순히 서버가 하나만 포함 된 각 작업을 사용 하 여 여러 작업을 만듭니다. SMS 의미는 단일 오 케 스트레이 터 대부분의 Windows Server 2019 대상 컴퓨터를 병렬화 할 수 작업을 동시에 실행 하는 100으로 지원 합니다. 대상 컴퓨터는 Windows Server 2016 또는 Windows Server 2012 R2 SMS 프록시 서비스를 대상에서 실행 하지 않고는 오 케 스트레이 터 해야 수행할 모든 전송 자체 경우 여러 병렬 작업을 실행 하는 것을 권장 하지 않습니다 고 될 것을 병목 상태입니다. 서버에서 단일 작업 내에서 병렬로 실행 하는 기능에는 SMS의 이후 버전에서 추가 예정 기능입니다.

- **RDMA 네트워크를 사용 하 여 SMB 3을 사용 합니다.** Windows Server 2012 또는 이후 원본 컴퓨터에서 SMB 3.x SMB 다이렉트 모드를 지원 및 RDMA 네트워킹에서 전송 하는 경우 합니다. RDMA 이동 전송의 대부분의 CPU 비용 Cpu 마더보드에서 온 보 딩 NIC 프로세서 대기 시간 및 서버 CPU 사용률 감소 합니다. 또한 RDMA 네트워크 ROCE 등 iWARP는 일반적으로 일반 TCP/이더넷, 25, 50 및 인터페이스당 100gb 속도 포함 하 여 보다 실질적으로 더 높은 대역폭을 차지 합니다. 일반적으로 SMB 다이렉트를 사용 하는 저장소 자체까지 네트워크에서 전송 속도 제한 이동 합니다.   

- **3 SMB 다중 채널을 사용 합니다.** Windows Server 2012 또는 이후 원본 컴퓨터를 전송 하는 경우 SMB 3.x 지원 다중 채널 복사본 크게 향상 시킬 수 있는 파일 복사 성능을입니다. 이 기능은 원본 및 대상으로 자동으로 작동 합니다.

   - 여러 네트워크 어댑터
   - 수신 RSS (수신측 배율)를 지 원하는 하나 이상의 네트워크 어댑터
   - NIC 팀을 사용 하 여 구성 된 더 많은 네트워크 어댑터 중 하나
   - RDMA를 지원하는 하나 이상의 네트워크 어댑터

- **드라이버를 업데이트 합니다.** 적절 하 게 설치 최신 공급 업체 저장소와 엔클로저 펌웨어 및 드라이버, 최신 공급 업체 HBA 드라이버, 최신 공급 업체 BIOS/UEFI 펌웨어, 최신 공급 업체 네트워크 드라이버 및 최신 마더보드 칩셋 드라이버 원본, 대상 및 오 케 스트레이 터 서버입니다. 필요에 따라 노드를 다시 시작합니다. 공유 저장소 및 네트워킹 하드웨어 구성은 하드웨어 공급업체 설명서를 참조하세요.

- **고성능 처리를 사용 하도록 설정 합니다.** 서버의 BIOS/UEFI 설정이 고성능을 지원하는지 확인합니다(예: C-상태 사용 안 함, QPI 속도 설정, NUMA 사용, 가장 높은 메모리 주파수 설정 등). Windows Server의 전원 관리 고성능으로 설정 되었는지 확인 합니다. 필요에 따라 다시 시작합니다. 마이그레이션을 완료 한 후이 적절 한 상태를 반환할 것을 잊지 마세요. 

- **하드웨어 튜닝** 검토 합니다 [성능 튜닝 지침에 대 한 Windows Server 2016](https://docs.microsoft.com/windows-server/administration/performance-tuning/) 튜닝 오 케 스트레이 터 및 Windows Server 2019를 실행 하는 대상 컴퓨터 및 Windows Server 2016에 대 한 합니다. 합니다 [네트워크 하위 시스템 성능 튜닝](https://docs.microsoft.com/windows-server/networking/technologies/network-subsystem/net-sub-performance-tuning-nics) 섹션에 특히 중요 한 정보가 포함 되어 있습니다.

- **더 빠른 저장소를 사용 합니다.** 원본 컴퓨터 저장소 속도 업그레이드 하기 어려울 수 있지만, 대상 저장소는 쓰기 IO 성능 속도 만큼 빠르게 전송에서 없는 불필요 한 병목 상태가 있는지 확인 하기 위해 원본이 읽기 IO 성능으로 이상 확인 해야 합니다. 대상 VM 인 경우, 적어도 마이그레이션에서는 실행 되도록 하이퍼바이저 호스트에서 가장 빠른 저장소 계층의 같은 플래시 계층 또는 미러된 전체 플래시 또는 하이브리드 공간을 활용 하 여 저장소 공간 다이렉트 HCI 클러스터를 사용 하 여 합니다. SMS 마이그레이션이 완료 되었을 때 VM 실시간으로 마이그레이션할 수 있습니다 느린 계층 또는 호스트 합니다.

- **바이러스 백신 업데이트 합니다.** 항상 원본 및 대상을 실행 하는 최소 성능 오버 헤드를 확인 하도록 바이러스 백신 소프트웨어의 최신 패치 버전을 확인 합니다. 테스트를 수행할 수 있습니다 *일시적으로* 인벤토리 또는 원본 및 대상 서버에서 마이그레이션 중인 폴더의 검색을 제외 합니다. 전송 성능이 향상 됩니다 지침은 또는 바이러스 백신 소프트웨어의 업데이트 된 버전 또는 예상 되는 성능 저하의 설명에 대 한 바이러스 백신 소프트웨어 공급 업체에 문의 합니다.

## <a name="give-feedback"></a> 의견을 보고 버그를 제출 하거나 지원 하나요?

저장소 마이그레이션 서비스 의견:

- Windows 10, "는 기능 제안"를 클릭 하 고 "저장소 마이그레이션"의 "Windows server" 범주와 하위 지정에 포함 된 피드백 허브 도구 사용
- 사용 된 [Windows Server UserVoice](https://windowsserver.uservoice.com) 사이트
- 메일 주소 smsfeed@microsoft.com

파일 버그:

- Windows 10에서 "문제 보고"를 클릭 하 고 "저장소 마이그레이션"의 "Windows server" 범주와 하위 지정의 피드백 허브 도구 사용
- 통해 지원 사례를 열어야 [Microsoft 지원](https://support.microsoft.com)

지원을 받으려면:

 - 에 질문을 게시 합니다 [Windows Server 기술 커뮤니티](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)
 - 에 게시 된 [Windows Server 2019 Technet 포럼](https://social.technet.microsoft.com/Forums/en-US/home?forum=ws2019&filter=alltypes&sort=lastpostdesc) 
 - 통해 지원 사례를 열어야 [Microsoft 지원](https://support.microsoft.com)


## <a name="see-also"></a>참조

- [저장소 서비스 마이그레이션 개요](overview.md)
