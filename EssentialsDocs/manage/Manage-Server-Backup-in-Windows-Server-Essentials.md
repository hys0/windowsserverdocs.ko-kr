---
title: Windows Server Essentials에서 서버 백업 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 0302d070-c58a-40f2-b56d-7e7842813d02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d792a03771ad406400877d73c0aa7ef1124adeb3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470588"
---
# <a name="manage-server-backup-in-windows-server-essentials"></a>Windows Server Essentials에서 서버 백업 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 다음 항목에는 Windows Server Essentials 대시보드를 사용하여 수행할 수 있는 일반적인 백업 작업에 대한 정보가 포함됩니다.

-   [선택해야 하는 백업](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_WhichBackup)

-   [서버 백업 설정 또는 사용자 지정](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)

-   [진행 중인 서버 백업 중지](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_2)

-   [원격으로 백업 관리](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_3)

-   [서버 백업 사용 안 함](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_4)

-   [서버 백업 설정에 대한 자세한 정보](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_5)

-   [서버에서 하드 드라이브 다시 분할](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_6)

-   [서버 백업에서 파일 및 폴더 복원](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_7)

##  <a name="which-backup-should-i-choose"></a><a name="BKMK_WhichBackup"></a>어떤 백업을 선택 해야 하나요?
 최근에 백업을 정상적으로 수행했으며 해당 백업에 중요한 데이터가 모두 포함되어 있는 경우에는 백업을 간단하게 선택할 수 있습니다. 이전 백업에서 서버나 컴퓨터로 복원하는 동안 복원할 양호한 백업을 선택하려면 약간의 조사와 절충이 필요할 수 있습니다.

#### <a name="to-choose-a-backup"></a>백업을 선택하려면

1.  파일 또는 폴더의 소유자를 확인하고 파일이나 폴더를 추가한 날짜와 시간을 기록해 둡니다. 이러한 날짜와 시간을 토대로 백업을 선택하게 됩니다.

2.  파일 및 폴더 복원 마법사의 **복원 옵션 선택** 페이지에서 **선택한 백업에서 복원(고급)** 을 클릭합니다.

3.  파일이나 폴더의 이전 또는 최신 버전을 복원할지에 따라 1단계에서 기록한 날짜와 시간에 가장 적합한 백업을 선택합니다.

4.  파일과 폴더를 대체 위치로 복원하고 파일 및 폴더의 소유자가 필요한 파일과 폴더를 원래 위치로 이동하게 하는 것이 좋습니다. 작업을 완료하면 대체 위치에 남아 있는 파일과 폴더를 삭제할 수 있습니다.

##  <a name="set-up-or-customize-server-backup"></a><a name="BKMK_1"></a>서버 백업 설정 또는 사용자 지정
 서버 백업은 설치 중에 자동으로 구성되지 않습니다. 매일 백업을 예약하여 서버와 해당 데이터를 자동으로 보호해야 합니다. 대부분 조직에서는 며칠 동안 생성된 데이터가 손실되면 안 되므로 매일 백업 계획을 유지 관리하는 것이 좋습니다. 자세한 내용은 [서버 백업 설정 또는 사용자 지정](Set-up-or-customize-server-backup.md)을 참조하세요.

##  <a name="stop-server-backup-in-progress"></a><a name="BKMK_2"></a>서버 백업 중지 진행 중
 서버 백업이 정기적으로 예약된 시간에 시작되거나 서버 백업을 수동으로 시작하는지에 관계없이 진행 중인 백업을 중지할 수 있습니다.

#### <a name="to-stop-a-backup-in-progress"></a>진행 중인 백업을 중지하려면

1.  대시보드를 엽니다.

2.  탐색 모음에서 **장치**를 클릭합니다.

3.  컴퓨터 목록에서 서버를 클릭하고 **작업** 창에서 **서버에 대한 백업 중지**를 클릭합니다.

4.  **예**를 클릭하여 작업을 확인합니다.

##  <a name="remotely-manage-your-backups"></a><a name="BKMK_3"></a>원격으로 백업 관리
 사무실을 비울 때 Windows Server Essentials 원격 웹 액세스를 통해 Windows Server Essentials 대시보드에 액세스하여 서버를 관리할 수 있습니다.

#### <a name="to-use-remote-web-access-to-manage-your-server"></a>원격 웹 액세스를 사용하여 서버를 관리하려면

1. 웹 브라우저를 엽니다.

2. 주소 상자에 Windows Server Essentials 도메인의 이름을 입력합니다.

3. 메시지가 표시되면 사용자 이름과 암호를 입력합니다.

4. 원격 웹 액세스에서 서버 이름을 클릭 하면 대시보드의 로그온 페이지가 표시 됩니다.

5. 관리자로 대시보드에 로그온하고 **장치**를 클릭합니다.

   원격 웹 액세스에 대 한 자세한 내용은 [원격 웹 액세스 개요](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Overview)를 참조 하세요.

##  <a name="disable-server-backup"></a><a name="BKMK_4"></a>서버 백업 사용 안 함
 매일 백업을 예약하여 서버와 해당 데이터를 자동으로 보호해야 합니다. 대부분 조직에서는 며칠 동안 생성된 데이터가 손실되면 안 되므로 매일 백업 계획을 유지 관리하는 것이 좋습니다.

 서버 백업이 이미 구성되어 있는데 나중에 타사 애플리케이션을 사용하여 서버를 백업하려면 Windows Server Essentials 서버 백업을 사용하지 않도록 설정할 수 있습니다.

#### <a name="to-disable-server-backup"></a>서버 백업을 사용하지 않도록 설정하려면

1.  관리자 계정과 암호로 Windows Server Essentials 대시보드에 로그온합니다.

2.  **장치** 탭을 클릭하고 서버 이름을 클릭합니다.

3.  작업 창에서 **서버에 대한 백업 사용자 지정**을 클릭합니다.

    > [!NOTE]
    >  서버 백업 설정 마법사를 사용하여 서버 백업을 구성하고 나면 **서버에 대한 백업 사용자 지정** 작업이 표시됩니다. 서버 백업 설정에 대한 자세한 내용은 [서버 백업 설정 또는 사용자 지정](Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)을 참조하세요.

4.  서버 백업 사용자 지정 마법사가 나타납니다.

5.  **구성 옵션** 페이지에서 **서버 백업 사용 안 함**을 클릭합니다. 마법사의 지시를 따릅니다.

##  <a name="learn-more-about-setting-up-server-backup"></a><a name="BKMK_5"></a>서버 백업 설정에 대 한 자세한 정보
 서버 백업은 서버 설정 중에 사용하도록 설정되지 않습니다.

> [!NOTE]
>  서버 백업을 구성할 때 백업 대상 하드 드라이브로 사용할 외부 하드 드라이브 하나 이상을 서버에 연결해야 합니다.

###  <a name="backup-destination-drive"></a><a name="BKMK_Target"></a>백업 대상 드라이브
 백업에 여러 외부 스토리지 드라이브를 사용하고 온사이트 및 오프사이트 스토리지 위치 사이에서 드라이브를 순환할 수 있습니다. 이렇게 하면 하드웨어 온사이트에 물리적 손상이 발생할 경우 데이터를 복구하는 데 도움이 되므로 재해 대비 계획을 향상할 수 있습니다.

 서버 백업을 위한 스토리지 드라이브를 선택할 때 다음을 고려하세요.

-   데이터를 저장할 충분한 공간이 있는 드라이브를 선택합니다. 스토리지 드라이브에는 백업할 데이터 스토리지 용량의 2.5배 이상이 포함되어야 합니다. 또한 드라이브는 향후 서버 데이터 증가를 수용할 만큼 충분히 커야 합니다.

-   백업 대상 드라이브에 오프라인 드라이브가 들어 있으면 백업 구성에 실패합니다. 구성을 완료하려면 백업 대상을 선택할 때 오프라인 상태인 드라이브를 제외할 확인란을 선택 취소합니다.

-   이전 백업이 포함된 드라이브를 백업 대상으로 선택하면 마법사에서 이전 백업을 유지할지를 선택할 수 있습니다. 백업을 유지하면 드라이브가 포맷되지 않습니다.

-   외부 스토리지 드라이브를 다시 사용할 때 드라이브가 비어 있거나 필요하지 않은 데이터만 포함되어 있는지 확인합니다.

-   외부 스토리지 드라이브 제조업체의 웹 사이트를 방문하여 Windows Server Essentials를 실행하는 컴퓨터에서 백업 드라이브가 지원되는지 확인해야 합니다.

> [!CAUTION]
>  서버 백업 설정 마법사에서는 백업을 위해 스토리지 드라이브를 구성할 때 해당 드라이브를 포맷합니다.

### <a name="server-backup-schedule"></a>서버 백업 일정
 매일 백업을 예약하여 서버와 해당 데이터를 자동으로 보호해야 합니다. 대부분 조직에서는 며칠 동안 생성된 데이터가 손실되면 안 되므로 매일 백업 계획을 유지 관리하는 것이 좋습니다.

 Windows Server Essentials 서버 백업 설정 마법사를 사용하면 하루에 여러 번 서버 데이터를 백업하도록 선택할 수 있습니다. 마법사에서는 차등 기반 백업을 예약하므로 백업이 빠르게 실행되고 서버 성능에 큰 영향을 미치지 않습니다. 기본적으로 **서버 백업 설정**에서는 매일 오후 12시 및 11시에 백업이 실행되도록 예약합니다. 그러나 조직의 요구에 따라 백업 일정을 조정할 수 있습니다. 때때로 백업 계획의 유효성을 평가하고 필요에 따라 계획을 변경해야 합니다.

> [!NOTE]
>  Windows Server Essentials의 기본 설치에서 서버는 매주 한 번 조각 모음을 자동으로 수행하도록 구성됩니다. 따라서 타사 이미징 소프트웨어를 사용할 경우 기본 백업보다 큰 백업이 만들어질 수 있습니다. 서버에서 정기적으로 조각 모음을 수행할 필요가 없으면 다음 단계에 따라 조각 모음 일정을 끌 수 있습니다.
>
> 1. Windows 키 +W를 눌러 **검색**을 엽니다.
>    2. 검색 텍스트 상자에 **Defragment**를 입력합니다.
>    3. 결과 섹션에서 **드라이브 조각 모음 및 최적화**를 클릭합니다.
>    4. **드라이브 최적화** 페이지에서 드라이브를 선택하고 **설정 변경**을 클릭합니다.
>    5. **최적화 일정** 창에서 **예약 실행(권장)** 확인란을 선택 취소한 후 **확인**을 클릭하여 변경 내용을 저장합니다.

### <a name="items-to-be-backed-up"></a>백업할 항목
 기본적으로 모든 운영 체제 파일 및 폴더가 백업을 위해 선택됩니다. 서버에 있는 모든 하드 디스크, 파일 및 폴더를 백업하도록 선택하거나 백업할 개별 하드 디스크, 파일 또는 폴더만 선택할 수 있습니다. 백업을 위해 항목을 추가하거나 제거하려면 다음의 하나를 수행합니다.

-   서버 백업에 데이터 드라이브를 포함하려면 옆에 있는 확인란을 선택합니다.

-   서버 백업에서 데이터 드라이브를 제외하려면 옆에 있는 확인란의 선택을 취소합니다.

> [!NOTE]
>  백업에서 **운영 체제** 항목을 제외하려면 먼저 **시스템 백업(권장)** 확인란을 선택 취소해야 합니다.

 서버 백업에 사용할 백업 하드 디스크 공간의 크기를 최소화하려고 유용하거나 특히 중요한 것으로 간주하지 않는 파일이 포함된 모든 폴더를 제외하려고 할 수 있습니다.

 예를 들어 많은 하드 드라이브 공간을 사용하는 녹화된 TV 프로그램이 포함된 폴더가 있을 수 있습니다. 일반적으로 이러한 프로그램을 시청한 이후에는 삭제하므로 이러한 파일을 백업하지 않도록 선택할 수 있습니다. 또는 유지하지 않으려는 임시 파일이 포함된 폴더가 있을 수 있습니다.

##  <a name="repartition-a-hard-drive-on-the-server"></a><a name="BKMK_6"></a>서버에서 하드 드라이브 다시 분할
 Windows Server Essentials 서버에서 포맷되지 않은 내부 하드 디스크 드라이브가 발견되면 새 하드 드라이브 추가 마법사의 링크가 포함된 상태 경고가 표시됩니다. 새 하드 드라이브 추가 마법사에서 하드 드라이브를 포맷하기 위한 다양한 옵션을 안내합니다. 마법사가 완료되면 드라이브 크기에 따라 포맷된 논리적 하드 드라이브 하나 이상이 하드 드라이브에서 생성되고 NTFS로 포맷됩니다.

 하드 디스크 드라이브를 다시 분할해야 하면 다음 지침을 따르세요.

#### <a name="to-repartition-a-hard-disk-drive"></a>하드 디스크 드라이브를 다시 분할하려면

1.  **시작** 화면에서 **관리 도구**를 클릭하고 **컴퓨터 관리**를 두 번 클릭합니다.

2.  컴퓨터 관리에서 **스토리지**를 클릭하고 **디스크 관리**를 두 번 클릭합니다.

3.  다시 분할할 드라이브를 마우스 오른쪽 단추로 클릭하고 **볼륨 삭제**, **예**를 차례로 클릭합니다.

    > [!NOTE]
    >  하드 디스크 드라이브에서 각 파티션에 대해 이 단계를 반복합니다.

4.  **할당되지 않은** 하드 디스크 드라이브를 마우스 오른쪽 단추로 클릭하고 **새 단순 볼륨**을 클릭합니다.

5.  새 단순 볼륨 마법사에서 16TB(16,000,000MB) 이하인 볼륨을 만들고 포맷합니다.

    > [!NOTE]
    >  하드 디스크 드라이브에서 모든 할당되지 않은 공간이 사용될 때까지 이 단계를 반복합니다.

##  <a name="restore-files-and-folders-from-a-server-backup"></a><a name="BKMK_7"></a>서버 백업에서 파일 및 폴더 복원
 서버 백업에서 개별 파일과 폴더를 찾아서 복원할 수 있습니다.

#### <a name="to-restore-files-and-folders-from-a-server-backup"></a>서버 백업에서 파일 및 폴더를 복원하려면

1.  대시보드를 열고 **장치** 탭을 클릭합니다.

2.  서버 이름을 클릭하고 **작업** 창에서 **서버에 대한 파일 또는 폴더 복원**을 클릭합니다.

3.  파일 또는 폴더 복원 마법사가 열립니다. 마법사의 지침에 따라 파일이나 폴더를 복원합니다.

## <a name="additional-references"></a>추가 참조

-   [백업 및 복원 관리](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)

-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)
