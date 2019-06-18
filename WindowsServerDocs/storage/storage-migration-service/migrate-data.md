---
title: 저장소 마이그레이션 서비스를 사용 하 여 파일 서버 마이그레이션
description: 검색 엔진 결과 대 한 항목의 간략 한 설명
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 879a87d4383d07e37227ecf6fffa5d002a77bbc0
ms.sourcegitcommit: 214e827934e7b3e8987e9e0ab2cf00047d332c89
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67153321"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>저장소 마이그레이션 서비스를 사용 하 여 서버 마이그레이션

이 항목의 파일 및 구성 및 사용 하 여 다른 서버를 포함 하 여 서버를 마이그레이션하는 방법에 설명 [저장소 마이그레이션 서비스](overview.md) 및 Windows Admin Center. 서비스를 설치 하 고 모든 필요한 방화벽 포트를 연 후에 세 가지 단계를 수행 마이그레이션: 서버 인벤토리 데이터를 전송 하 고 새 서버로 이동 합니다.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>0 단계: 저장소 마이그레이션 서비스를 설치 하 고 방화벽 포트를 확인 합니다.

시작 하기 전에 Storage Migration Service를 설치 하 고 필요한 방화벽 포트가 열려 있는지 확인 합니다.

1. 확인 합니다 [저장소 마이그레이션 서비스 요구 사항](overview.md#requirements) 하 고 설치 [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) PC 또는 관리 서버를 아직 없는 경우에 합니다.
2. Windows Admin Center Windows Server 2019를 실행 하는 오 케 스트레이 터 서버에 연결 합니다. <br>이 서버에 저장소 마이그레이션 서비스를 설치 하 고 마이그레이션을 관리 하는 데 것입니다. 서버가 하나만으로 마이그레이션하는 경우에 Windows Server 2019 실행으로 대상 서버를 사용할 수 있습니다. 모든 다중 서버 마이그레이션에 대 한 별도 오케스트레이션 서버를 사용 하는 것이 좋습니다.
1. 로 이동 **서버 관리자** (Windows Admin Center)에서 > **Storage Migration Service** 선택한 **설치** 저장소 마이그레이션 서비스 및 해당 필수 구성 요소를 설치 하려면 (그림 1에 표시 됨).
    ![설치 단추를 표시 하는 저장소 마이그레이션 서비스 페이지의 스크린샷](media/migrate/install.png) **그림 1: 저장소 마이그레이션 서비스를 설치합니다.**
1. Windows Server 2019를 실행 하는 모든 대상 서버에 저장소 마이그레이션 서비스 프록시를 설치 합니다. 이 대상 서버에 설치 하는 경우 전송 속도를 두 배로 만듭니다. <br>이렇게 하려면 Windows Admin Center 대상 서버에 연결 하 고 이동 **서버 관리자** (Windows Admin Center)에서 > **역할 및 기능**선택, **저장소 마이그레이션 서비스 프록시**를 선택한 후 **설치**합니다.
1. 모든 원본 서버 및 Windows Admin Center Windows Server 2012 R2 또는 Windows Server 2016을 실행 하는 대상 서버의 각 서버에 연결로 이동 **서버 관리자** (Windows Admin Center)에서 > **방화벽**   >  **들어오는 규칙**, 다음과 같은 규칙이 설정 되어 있는지 확인 합니다.
    - 파일 및 프린터 공유(SMB-In)
    - Netlogon 서비스 (Np-in)
    - Windows Management Instrumentation (Dcom-in)
    - WMI(Windows Management Instrumentation)(WMI-In)

   > [!NOTE]
   > 타사 방화벽을 사용 하는 경우 열려는 인바운드 포트 범위는 TCP/445 (SMB), TCP/135 (RPC/DCOM endpoint mapper) 및 TCP 1025-65535 (RPC/DCOM 사용 후 삭제 포트). 저장소 마이그레이션 서비스 포트는 TCP/28940 (오 케 스트레이 터) 및 TCP/28941 (프록시)입니다.

1. Orchestrator 서버를 사용 하 여 마이그레이션을 관리 하 고 이벤트 또는 로그를 전송할 데이터를 다운로드 하려는 경우 해당 서버의 파일 및 프린터 공유 (Smb-in) 방화벽 규칙 활성화 되어 있는지 확인 합니다.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>1단계: 마이그레이션할 파악 서버 작업 및 인벤토리 만들기

이 단계에서는 마이그레이션 후 해당 파일에 구성 정보를 수집할를 스캔 하는 서버를 지정 합니다.

1. 선택 **새 작업**, 작업 이름 및 선택한 **확인**합니다.
1. 에 **자격 증명 입력** 페이지에서 마이그레이션하려는 서버에서 작업을 선택 하는 관리자 자격 증명을 입력 합니다 **다음**합니다.
1. 선택 **장치 추가**는 원본 서버 이름을 입력 하 고 선택한 **확인**합니다. <br>인벤토리 할 모든 서버에 대해이 단계를 반복 합니다.
1. 선택 **검사 시작**합니다.<br>페이지 업데이트 검색이 완료 되 면 표시 됩니다.
    ![검색할 준비 서버를 보여 주는 스크린 샷](media/migrate/inventory.png) **그림 2: 서버 인벤토리 만들기**
1. 공유, 구성, 네트워크 어댑터 및 인벤토리에 포함 된 볼륨을 검토 하려면 각 서버를 선택 합니다. <br><br>저장소 마이그레이션 서비스는이 릴리스에서 Windows 시스템 폴더에 있는 모든 공유에 대 한 경고를 볼 수 있습니다 Windows 작업을 방해할 수 있음을 알고 있는 폴더나 파일 전송 되지 않습니다. 전송 단계에서 이러한 공유를 건너뛰기 해야 합니다. 자세한 내용은 참조 하세요. [전송에서 파일 및 폴더 제외 된](faq.md#excluded-files)합니다.
1. 선택 **다음** 데이터 전송으로 이동 합니다.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>2단계: 대상 서버에 이전 서버에서 데이터를 전송

이 단계에서는 대상 서버에 넣을 위치를 지정한 후 데이터를 전송 합니다.

1. 에 **데이터 전송** > **자격 증명을 입력** 페이지에서, 마이그레이션할 대상 서버에서 작동 한 다음 선택 하는 관리자 자격 증명을 입력 **다음**.
2. 에 **대상 장치 및 매핑을 추가** 페이지에서 첫 번째 원본 서버가 나열 됩니다. 마이그레이션하고 선택 하려는 서버 이름을 입력 **장치의 검색**합니다.
3. 매핑할 원본 볼륨 대상 볼륨 선택을 취소 합니다 **포함** 모든 공유에 대 한 확인란을 선택 하지 않을 (비롯 한 모든 관리 공유는 Windows 시스템 폴더에 있는)를 전송 하 고 선택한 **다음** .
   ![원본 서버 및 볼륨 및 공유를 보여 주는 스크린 샷 및 이러한에서는 전송할 대상](media/migrate/transfer.png) **그림 3: 원본 서버 및 해당 저장소는 전송했습니다**
4. 대상 서버 및 모든 더 많은 원본 서버에 대 한 매핑을 추가 하 고 선택한 **다음**합니다.
5. 필요에 따라 전송 설정을 조정 하 고 선택한 **다음**합니다.
6. 선택 **유효성 검사** 선택한 후 **다음**합니다.
7. 선택 **전송을 시작** 데이터 전송을 시작 합니다.<br>처음을 이전에서는 이동 기존 파일 대상 위치에서 백업 폴더로 합니다. 후속 전송에 기본적으로 새로 고칠 예정 대상 첫 번째 백업 없이 합니다. <br>또한 Storage Migration Service는 지능적 공유 겹치는 다루는-동일한 작업에서 두 번 같은 폴더에 복사 되지 않습니다.
8. 전송이 완료 되 면 모든 것이 제대로 전송 되었는지 확인 하려면 대상 서버를 확인 합니다. 선택 **오류 로그만** 전송 하지 않은 파일의 로그를 다운로드 하려는 경우.

   > [!NOTE]
   > 전송의 감사 내역을 유지 하거나 작업에서 둘 이상의 전송을 수행, 클릭 하려는 **전송 로그** CSV 복사본을 저장 합니다. 모든 후속 전송에는 이전 실행의 데이터베이스 정보를 덮어씁니다. 

이 시점에서 세 가지 옵션이 있습니다.

- **다음 단계로 이동**를 원본 서버의 id를 채택 하는 대상 서버를 통해 잘라내기 합니다.
- **마이그레이션 완료는 것이 좋습니다** 원본 서버를 identities를 통해 수행 하지 않고 있습니다.
- **다시 전송**, 마지막 전송 이후 업데이트 된 파일만 복사 합니다.

Azure 사용 하 여 파일을 동기화 하는 것이 목표인 경우 설정할 수 있습니다 Azure File Sync를 사용 하 여 대상 서버, 파일을 전송할 대상 서버를 통해 절감 후 또는 (참조 [Azure File Sync 배포 계획](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)).

## <a name="step-3-optionally-cut-over-to-the-new-servers"></a>3단계: 필요에 따라 새 서버로 이동

이 단계에서는으로 전환 하기 원본 서버에서 대상 서버에 컴퓨터 이름과 IP 주소를 대상 서버로 이동 합니다. 이 단계를 완료 한 후 앱과 사용자 이름 및 서버에서 마이그레이션된 주소를 통해 새 서버에 액세스 합니다.

 1. 로 이동 하는 경우 Windows Admin Center 마이그레이션 작업을 벗어난 했습니다 **서버 관리자** > **Storage Migration Service** 를 선택한 다음을 완료 하는 작업입니다. 
 1. 에 **를 새 서버로 전환할** > **자격 증명을 입력** 페이지에서 **다음** 이전에 입력 한 자격 증명을 사용 합니다.
 1. 에 **중단 구성** 페이지에서 각 원본 장치의 설정을 인수 하는 네트워크 어댑터를 지정 합니다. 이 IP 주소는 중단의 일부로 대상에 소스에서 이동합니다.
 1. 어떤 사용할 IP 주소를 원본 서버에 대 한 중단 이동 후 대상에 해당 주소를 지정 합니다. DHCP 또는 고정 주소를 사용할 수 있습니다. 정적 주소를 사용 하는 경우 기존 서브넷와 동일 하거나 중단 하지 못합니다 새 서브넷 이어야 합니다.
    ![원본 서버 IP 주소 및 컴퓨터 이름 및 항목을 보여 주는 스크린 샷 컷 오버 후으로 대체 될 하겠습니다](media/migrate/cutover.png)
    **그림 4: 원본 서버 및 네트워크 구성이 대상으로 이동 하는 방법**
 1. 대상 서버는 해당 이름을 후 원본 서버 이름을 바꾸는 방법을 지정 합니다. 임의로 생성 된 이름을 사용 하거나 직접 입력 수 있습니다. 선택한 **다음**합니다.
 1. 선택 **다음** 에 **cutover 설정을 조정** 페이지입니다.
 1. 선택 **유효성 검사** 에 **유효성 검사 원본 및 대상 장치** 페이지를 선택한 후 **다음**합니다.
 1. 중단을 수행 하려면 준비 된 경우 선택 **중단 시작**합니다. <br>사용자 및 앱 이름과 주소는 이동 하 고 서버를 다시 시작 여러 번 각각 하는 동안 중단 될 수 있지만 수이 고, 그렇지는 마이그레이션에서 영향을 받는 없습니다. 기간 컷 오버는 Active Directory 및 DNS 복제 시간 뿐만 아니라 서버 다시 시작 하는 방법에 따라 달라 집니다.

## <a name="see-also"></a>참조

- [저장소 서비스 마이그레이션 개요](overview.md)
- [저장소 마이그레이션 서비스 질문과 대답 (FAQ)](faq.md)
- [Azure File Sync 배포 계획](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)
