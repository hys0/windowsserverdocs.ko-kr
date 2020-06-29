---
title: Windows Server Essentials에서 서버 스토리지 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 1836682e-c7bb-4dd5-a2b5-6ff032693574
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cb6503c05f0dfc621758acb6da26cc90e658836d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470558"
---
# <a name="manage-server-storage-in-windows-server-essentials"></a>Windows Server Essentials에서 서버 스토리지 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Windows Server Essentials를 사용하면 대시보드의 **스토리지** 탭에 있는 **하드 드라이브** 페이지에서 모든 서버 스토리지(하드 드라이브 및 스토리지 공간 포함)를 관리할 수 있습니다.

 다음 항목에서는 서버 스토리지를 늘리고, 스토리지 공간을 이해 및 사용하고, 하드 드라이브를 관리하는 데 도움이 되는 정보를 제공합니다.

-   [대시보드를 사용하여 하드 드라이브 관리](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_1)

-   [서버의 스토리지 늘리기](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_2)

-   [하드 드라이브에서 확인 및 복구 수행](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_Check)

-   [하드 드라이브 포맷](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_3)

-   [새 하드 드라이브 추가](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4)

-   [저장소 공간 개요](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_5)

-   [스토리지 공간 만들기](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_6)

##  <a name="manage-hard-drives-using-the-dashboard"></a><a name="BKMK_1"></a>대시보드를 사용 하 여 하드 드라이브 관리
 Windows Server Essentials를 사용하면 대시보드를 통해 서버에 연결된 모든 하드 드라이브를 관리할 수 있습니다. 대시보드 **스토리지** 탭의 **하드 드라이브**에는 서버에서 데이터 및 서버 백업을 저장하는 데 사용할 수 있는 모든 하드 드라이브가 표시됩니다. 서버는 각 하드 드라이브에서 사용 가능한 공간을 모니터링하고 하드 드라이브 공간이 부족하면 경고를 표시합니다. **하드 드라이브** 탭에는 다음 정보가 표시됩니다.

- 각 하드 드라이브의 이름

- 각 하드 드라이브의 용량

- 각 하드 드라이브에서 사용한 공간 크기

- 각 하드 드라이브에서 사용 가능한 공간 크기

- 각 하드 드라이브의 상태. 상태가 비어 있으면 하드 드라이브가 제대로 작동하는 것입니다.

- 선택한 하드 드라이브가 실제 디스크 대신 스토리지 공간에 있는 경우 스토리지 풀, 스토리지 공간 및 하드 드라이브에 대한 모든 스토리지 스택 정보가 표시되는 세부 정보 창

  다음 표에서는 대시보드에서 사용할 수 있는 하드 드라이브 관리 작업 및 해당 설명을 보여 줍니다. 일부 작업은 하드 드라이브를 선택한 경우에만 표시됩니다.

### <a name="available-hard-drive-management-tasks"></a>사용 가능한 하드 드라이브 관리 작업

|작업 이름|설명|
|---------------|-----------------|
|**하드 드라이브 속성 보기**|저장소 풀과 저장소 공간을 만들고 관리할 수 있는 _HardDriveName_**속성** 페이지를 엽니다. 이 작업은 하드 드라이브를 선택한 경우에 표시됩니다. *HardDriveName* 속성 페이지의 **일반** 탭에는 다음과 같은 추가 작업이 포함됩니다.<br /><br /> -   **드라이브 정리**: 하드 드라이브에서 사용 하지 않는 파일을 정리할 수 있습니다 (이 작업은 Windows Server Essentials 에서만 사용할 수 있음).<br />-   **확인 및 복구**: 하드 드라이브에서 파일 시스템 오류를 확인 하 고 검색 된 오류를 자동으로 복구 하려고 합니다.<br /><br /> _HardDriveName_**속성** 페이지의 **섀도 복사본** 탭에서는 섀도 복사본을 사용 하도록 설정할 수 있습니다. 이 탭에는 섀도 복사본이 다음에 실행되도록 예약된 시간도 표시됩니다.|
|**스토리지 공간 관리**|**참고:** Windows Server Essentials의 경우이 작업은 기존 저장소 공간이 있는 경우에만 표시 됩니다.<br /><br /> 스토리지 풀과 스토리지 공간을 만들고 관리할 수 있는 **스토리지 공간** 제어판을 엽니다.|
|**스토리지 공간 만들기**|하나 이상의 하드 드라이브를 사용하여 스토리지 풀의 용량을 늘릴 수 있는 스토리지 공간 만들기 마법사를 엽니다.|
|**스토리지 풀 용량 늘리기**|**참고:** 이 작업은 선택한 하드 드라이브가 저장소 공간에 있는 경우에만 표시 됩니다.<br /><br /> 하나 이상의 하드 드라이브를 사용하여 스토리지 풀의 용량을 늘릴 수 있는 스토리지 풀 용량 늘리기 마법사를 엽니다.|

##  <a name="increase-storage-on-the-server"></a><a name="BKMK_2"></a>서버의 저장소 늘리기
 서버의 스토리지를 늘리기 위해 서버에 내부 하드 디스크를 더 추가할 수 있습니다. 내부 하드 디스크를 더 추가하려면 서버를 종료하고 내부 하드 디스크를 추가한 다음 서버를 다시 시작해야 합니다. 하드 디스크가 SCSI 컨트롤러에 연결되어 있는 경우 서버를 종료할 필요가 없습니다. 이 경우 서버가 실행되는 동안 하드 디스크를 연결할 수 있습니다.

 추가할 하드 디스크가 포맷되었는지 여부에 따라 다음 중 하나를 수행합니다.

-   **서식 지정** 내부 하드 디스크가 NTFS 또는 ReFS로 포맷 된 경우 서버에서 드라이브 문자를 할당 하 고 하드 디스크는 **하드 드라이브** 탭에 나타납니다. 이제 서버 폴더를 만들거나 새 하드 드라이브로 이동할 수 있습니다.

-   **포맷되지 않음** 내부 하드 디스크가 포맷되지 않은 경우 다음과 같은 경고가 나타납니다. 포맷되지 않은 하드 드라이브가 하나 이상 서버에 연결되어 있습니다. 다음 절차에 따라 하드 디스크를 포맷합니다.

#### <a name="to-format-the-hard-disk"></a>하드 디스크를 포맷하려면

1.  대시보드를 엽니다.

2.  탐색 창에서 경고 아이콘을 클릭 하 여 Windows Server Essentials에서 **경고 뷰어** 를 시작 하거나 Windows server Essentials의 **상태 모니터링** 탭을 시작 합니다.

3.  **경고 뷰어** 또는 **상태 모니터링** 탭에서 경고를 클릭한 다음 작업 창에서 **이 문제 해결**을 클릭합니다.

4.  지침에 따라 새 하드 드라이브 추가 마법사를 완료합니다.

###  <a name="to-clean-up-the-hard-drive"></a><a name="BKMK_Clean"></a>하드 드라이브를 정리 하려면

1.  대시보드를 엽니다.

2.  탐색 창에서 **스토리지**를 클릭한 다음 **하드 드라이브**를 클릭합니다.

3.  **하드 드라이브** 섹션에서 새로 추가된 하드 디스크에 할당된 드라이브 문자를 선택한 다음 작업 창에서 **하드 드라이브 속성 보기**를 클릭합니다.

4.  **<r \> 속성**의 **일반** 탭에서 **드라이브 정리**를 클릭 합니다.

##  <a name="perform-checks-and-repairs-on-hard-drives"></a><a name="BKMK_Check"></a>하드 드라이브에서 확인 및 복구 수행
 하드 드라이브 확인 및 복구 프로세스는 하드 드라이브에 저장된 파일 시스템의 상태를 확인합니다. 백업 파일이 저장된 볼륨에서 **chkdsk** 프로세스를 실행합니다. 하드 드라이브에서 확인 및 복구를 실행하여 다음과 같은 경고 문제를 해결할 수 있습니다.

-   서버 백업의 하드 드라이브를 하나 이상 확인해야 합니다.

#### <a name="to-check-and-repair-hard-drives"></a>하드 드라이브를 확인 및 복구하려면

1.  대시보드를 엽니다.

2.  **서버 폴더 및 하드 드라이브**를 클릭한 다음 **하드 드라이브**를 클릭합니다.

3.  오류를 표시하는 하드 드라이브를 선택한 다음 **하드 드라이브 속성 보기**를 선택합니다.

4.  **확인 및 복구** 탭에서 **확인 및 복구**를 클릭합니다.

##  <a name="format-hard-drives"></a><a name="BKMK_3"></a>하드 드라이브 포맷
 서버에서 포맷되지 않은 내부 하드 드라이브가 검색되면 상태 경고가 표시되어 사용자에게 포맷 프로세스를 안내합니다. 새 하드 드라이브 추가 마법사에서는 하드 드라이브 포맷 과정을 안내하고 다음 방법 중 하나로 하드 드라이브를 구성할 수 있게 해줍니다.

1.  하드 드라이브를 포맷하고 하드 드라이브에 자동으로 드라이브를 만듭니다. 이 옵션을 선택하면 마법사 완료 시 NTFS 파일 시스템으로 포맷된 논리적 하드 드라이브 하나가 생성됩니다.

2.  하드 드라이브를 포맷하고 서버 백업을 위해 설정합니다. 이 옵션을 선택하면 서버 백업 설정 마법사가 시작되며 서버 백업 구성을 안내합니다.

3.  저장소 공간이 없는 경우 새 하드 드라이브를 사용 하 여 저장소 공간을 만듭니다. 스토리지 공간을 만들려면 하드 드라이브가 두 개 이상 있어야 합니다.

4.  스토리지 공간이 이미 있는 경우 새 하드 드라이브를 사용하여 스토리지 풀의 용량을 늘립니다. 이 옵션은 서버에 생성된 기존 스토리지 공간이 있는 경우에만 표시됩니다. 이 옵션을 선택하면 마법사가 이 하드 드라이브를 스토리지 풀에 추가합니다.

##  <a name="add-a-new-hard-drive"></a><a name="BKMK_4"></a>새 하드 드라이브 추가
 Windows Server Essentials를 실행하는 서버에 새 하드 디스크 드라이브를 연결하는 경우 다음 작업을 수행할 수 있습니다.

-   [새 하드 드라이브를 사용하여 서버 폴더 저장](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4a)

-   [새 하드 드라이브를 사용하여 서버 백업 저장](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4b)

-   [새 하드 드라이브를 사용하여 스토리지 풀 용량 늘리기](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4c)

###  <a name="use-the-new-hard-drive-to-store-server-folders"></a><a name="BKMK_4a"></a>새 하드 드라이브를 사용 하 여 서버 폴더 저장
 새 하드 드라이브를 사용하여 서버 폴더를 저장하려면 하드 드라이브에 새 서버 폴더를 추가하거나 기존 서버 폴더를 하드 드라이브로 이동할 수 있습니다.

##### <a name="to-store-server-folders"></a>서버 폴더를 저장하려면

1. 대시보드를 엽니다.

2. **저장소** 탭을 클릭한 다음 **서버 폴더**를 클릭합니다.

3. **서버 폴더 작업** 창에서 다음 중 하나를 수행합니다.

   1.  서버 폴더를 추가하려면 **폴더 추가**를 클릭합니다.

   2.  서버 폴더를 이동하려면 새 하드 드라이브로 이동할 폴더를 선택하고 **폴더 이동**을 클릭합니다.

   > [!NOTE]
   >  하드 드라이브를 찾아 폴더를 만들지 않고 서버 폴더 위치로 선택 하는 경우 **루트 디렉터리 (예: C: \\ , D: \\ )를 서버 폴더로 추가할 수 없다는 오류 메시지가 나타납니다. 새 폴더를 만들거나 루트 디렉터리 아래의 기존 폴더를 선택한 후 다시 시도**하십시오. 이 오류를 해결하려면 새로 추가한 하드 드라이브에 새 폴더를 만든 다음 서버 폴더를 저장할 위치로 새 폴더를 선택합니다.

4. 지시에 따라 마법사를 완료합니다.

   서버 폴더를 이동하는 방법에 대한 자세한 내용은 [Add or move a server folder](Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)을 참조하세요.

###  <a name="use-the-new-hard-drive-to-store-server-backups"></a><a name="BKMK_4b"></a>새 하드 드라이브를 사용 하 여 서버 백업 저장
 새로 추가한 하드 드라이브를 사용하여 서버 백업을 저장할 수 있습니다.

##### <a name="to-store-server-backups"></a>서버 백업을 저장하려면

1. 대시보드를 엽니다.

2. **장치** 탭을 클릭하고 목록 창에서 서버를 선택한 다음 작업 창에서 다음 중 하나를 수행합니다.

   1. 서버에 서버 백업이 구성되어 있지 않은 경우 **서버 백업 설정**을 클릭합니다.

   2. 서버에 서버 백업이 구성되어 있는 경우 **서버 백업 사용자 지정**을 클릭합니다.

      서버 백업 설정 마법사가 나타납니다.

3. **백업 대상 선택** 페이지에서 새 하드 드라이브를 백업 대상으로 선택합니다.

4. 지시에 따라 마법사를 완료합니다.

###  <a name="use-the-new-hard-drive-to-increase-storage-pool-capacity"></a><a name="BKMK_4c"></a>새 하드 드라이브를 사용 하 여 저장소 풀 용량 늘리기
 스토리지 풀 용량이 부족하면 스토리지 풀 용량 늘리기 마법사를 통해 스토리지 풀에 새 하드 드라이브를 추가하여 스토리지 풀 용량을 늘릴 수 있다는 경고가 나타납니다.

> [!NOTE]
>  이 절차는 서버에 스토리지 풀을 만든 경우에만 수행할 수 있습니다.

##### <a name="to-increase-storage-pool-capacity"></a>스토리지 풀 용량을 늘리려면

1.  대시보드를 엽니다.

2.  **스토리지** 탭을 클릭한 다음, **하드 드라이브**를 클릭합니다.

3.  용량 부족을 표시하는 드라이브를 선택합니다.

4.  작업 창에서 **저장소 풀 용량 늘리기**를 선택합니다. 스토리지 풀 용량 늘리기 마법사가 나타납니다.

5.  지시에 따라 마법사를 완료합니다.

##  <a name="storage-spaces-overview"></a><a name="BKMK_5"></a>저장소 공간 개요
 스토리지 공간을 사용하여 스토리지 풀에 디스크를 그룹화할 수 있습니다. 그런 다음 풀 용량을 사용하여 스토리지 공간을 만들 수 있습니다. 스토리지 공간은 대시보드의 **하드 드라이브** 탭에 표시되는 가상 드라이브입니다. 다른 드라이브 처럼 저장소 공간을 사용할 수 있으므로 파일을 쉽게 사용할 수 있습니다. 풀 용량이 부족한 경우 큰 스토리지 공간을 만들고 스토리지 풀에 드라이브를 더 추가할 수 있습니다. 저장소 풀에 둘 이상의 디스크가 있는 경우 드라이브 오류의 영향을 받지 않는 양방향 미러를 사용 하 여 저장소 공간을 만들거나, 3 방향 미러 저장소 공간을 만드는 경우 두 드라이브가 실패할 수도 있습니다.

 스토리지 공간을 만들려면 Windows가 설치된 드라이브 외에 하나 이상의 추가 드라이브만 있으면 됩니다. 이러한 드라이브는 내부 또는 외부 하드 드라이브이거나 SSD(반도체 드라이브)일 수 있습니다. USB, SATA 및 SAS 드라이브를 포함하여 다양한 종류의 드라이브를 스토리지 공간에 사용할 수 있습니다.

> [!NOTE]
>  Windows Server Essentials를 실행 하는 서버에서 저장소 공간을 구성 하는 경우 **데이터 정리** 옵션을 사용 하 여 공장 기본 설정을 수행할 수 없습니다. 이 문제를 해결하려면 먼저 스토리지 공간을 제거한 다음 **데이터 정리** 옵션을 사용하여 공장 기본 설정으로 복원을 수행합니다.

 스토리지 공간에 대한 자세한 내용은 [스토리지 공간 FAQ(질문과 대답)](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)를 참조하세요.

##  <a name="create-a-storage-space"></a><a name="BKMK_6"></a>저장소 공간 만들기
 서버에서 스토리지 공간 작업을 시작하려면 다음과 같은 최소 요구 사항을 충족해야 합니다.

-   Windows Server Essentials를 실행하는 서버를 부팅 드라이브뿐 아니라 추가 실제 드라이브에 연결해야 하며, 드라이브에서 볼륨을 호스트하면 안 되고 10GB의 최소 용량이 있어야 합니다. 스토리지 풀을 만들려면 실제 드라이브 하나가 필요합니다. 복원 미러 스토리지 공간을 만들려면 최소 두 개의 실제 드라이브가 필요합니다.

-   패리티 또는 양방향 미러링을 통한 복원 기능이 있는 스토리지 공간을 만들려면 최소 두 개의 실제 드라이브가 필요합니다.

> [!NOTE]
>  Windows Server Essentials를 실행 하는 서버에서 저장소 공간을 구성 하는 경우 **데이터 정리** 옵션을 사용 하 여 공장 기본 설정을 수행할 수 없습니다. 이 문제를 해결하려면 먼저 스토리지 공간을 제거한 다음 **데이터 정리** 옵션을 사용하여 공장 기본 설정으로 복원을 수행합니다.

#### <a name="to-create-a-storage-space-in-windows-server-essentials"></a>Windows Server Essentials에서 저장소 공간을 만들려면

1. 스토리지 공간을 사용하여 그룹화하려는 모든 드라이브를 Windows Server Essentials 실행 서버에 추가하거나 연결합니다.

2. 대시보드에서 **고급: 스토리지 공간 관리**를 클릭합니다.

3. **새 풀 및 저장소 공간 만들기**를 클릭합니다.

4. 새 저장소 공간에 추가할 드라이브를 선택하고 **풀 만들기**를 클릭합니다.

5. 드라이브에 이름 및 문자를 지정하고 레이아웃을 선택합니다. **양방향 미러**, **3방향 미러** 및 **패리티**는 저장소 공간에 있는 파일을 드라이브 오류로부터 보호할 수 있습니다.

6. 저장소 공간이 도달할 수 있는 최대 크기를 입력하고 **저장소 공간 만들기**를 클릭합니다.

   Windows Server Essentials에서 대시보드의 저장소 공간 만들기 마법사를 사용 하 여 양방향 미러된 저장소 공간을 만들 수 있습니다.

#### <a name="to-create-a-storage-space-in-windows-server-essentials"></a>Windows Server Essentials에서 저장소 공간을 만들려면

1. 스토리지 공간을 사용하여 그룹화하려는 모든 드라이브를 Windows Server Essentials 실행 서버에 추가하거나 연결합니다.

2. 대시보드에서 **스토리지 공간 관리**를 클릭합니다. 스토리지 공간 만들기 마법사가 나타납니다.

3. 지시에 따라 마법사를 완료합니다.

   스토리지 풀 용량을 늘리는 방법에 대한 자세한 내용은 [Use the new hard drive to increase storage pool capacity](Manage-Server-Storage-in-Windows-Server-Essentials.md#BKMK_4c)를 참조하세요.

## <a name="additional-references"></a>추가 참조

-   [서버 폴더 관리](Manage-Server-Folders-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)

-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
