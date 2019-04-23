---
title: 기본 볼륨 축소
description: 이 문서에서는 기본 볼륨을 축소하는 방법을 설명합니다.
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e54632b78fd67a65b51147323565130881d8d81b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885334"
---
# <a name="shrink-a-basic-volume"></a>기본 볼륨 축소

> **적용 대상:** Windows 10, Windows 8.1, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

주 파티션과 논리 드라이브를 동일한 디스크의 연속된 인접한 공간으로 축소하여 이러한 주 파티션과 논리 드라이브에 사용되는 공간을 줄일 수 있습니다. 예를 들어 추가 파티션이 필요하지만 추가 디스크가 없는 경우 기존 파티션을 볼륨 끝부터 축소하여 할당되지 않은 새 공간을 만든 다음 이 공간을 새 파티션에 사용할 수 있습니다. 축소 작업은 특정 파일 형식의 존재 여부에 따라 차단될 수 있습니다. 자세한 내용은 [추가 고려 사항](#addcon)을 참조하세요. 

파티션을 축소할 때 일반 파일은 디스크에 자동적으로 재배치되고, 디스크에 할당되지 않은 공간이 새로 만들어집니다. 파티션을 축소하기 위해 디스크를 다시 포맷할 필요는 없습니다.

> [!CAUTION]
> 파티션이 데이터(데이터베이스 파일 등)를 포함한 원시 파티션(즉, 파일 시스템이 없는 파티션)인 경우 파티션 축소로 인해 데이터가 손상될 수 있습니다.

## <a name="shrinking-a-basic-volume"></a>기본 볼륨 축소

-   [Windows 인터페이스를 사용 하 여](#BKMK_WINUI)
-   [명령줄을 사용 하 여](#BKMK_CMD)

> [!NOTE]
> **Backup Operators** 또는 **Administrators** 그룹의 구성원이어야 이 단계를 완료할 수 있습니다.

<a id="BKMK_WINUI"></a>
#### <a name="to-shrink-a-basic-volume-using-the-windows-interface"></a>Windows 인터페이스를 사용하여 기본 볼륨 축소

1.  디스크 관리자에서 축소하고자 하는 기본 볼륨을 마우스 오른쪽 단추로 클릭합니다.

2.  **볼륨 축소**를 클릭합니다.

3.  화면상의 지침을 따릅니다.

<br />

> [!NOTE]
> 파일 시스템이 없거나 NTFS 파일 시스템을 사용하는 기본 볼륨만을 축소할 수 있습니다.

<a id="BKMK_CMD"></a>
#### <a name="to-shrink-a-basic-volume-using-a-command-line"></a>명령줄을 사용하여 기본 볼륨 축소

1.  명령 프롬프트를 열고 `diskpart`를 입력합니다.

2.  **DISKPART** 프롬프트에서 `list volume`을 입력합니다. 축소하고자 하는 단순 볼륨의 번호를 메모합니다.

3.  **DISKPART** 프롬프트에서 `select volume <volumenumber>`을 입력합니다. 축소하고자 하는 단순 볼륨의 *volumenumber*를 선택합니다.

4.  **DISKPART** 프롬프트에서 `shrink [desired=<desiredsize>] [minimum=<minimumsize>]`을 입력합니다. 선택한 볼륨을 가급적 *desiredsize* 메가바이트(MB)로 축소합니다. 또는 *desiredsize*가 너무 큰 경우 *minimumsize*로 축소합니다.

<br />

| 값 | 설명|
|---|---|
| <p>**볼륨 목록**</p> | <p>모든 디스크에 기본 및 동적 볼륨 목록을 표시합니다.</p>|
| <p>**볼륨 선택**</p> | <p>볼륨 번호가 <em>volumenumber</em>인 지정된 볼륨을 선택하고 포커스를 설정합니다. 지정된 볼륨이 없는 경우 **select** 명령이 포커스가 설정된 현재 볼륨 목록을 표시합니다. 번호, 드라이브 문자 또는 탑재 지점 경로로 볼륨을 지정할 수 있습니다. 기본 디스크에서 볼륨을 선택하면 해당 파티션에도 포커스를 설정합니다.</p> |
| <p>**shrink**</p> | <p>포커스가 설정된 볼륨을 축소하여 할당되지 않은 공간을 만듭니다. 데이터는 손실되지 않습니다. 파티션에 이동할 수 없는 파일(페이지 파일 또는 섀도 복사본 저장 영역 등)이 포함된 경우 볼륨은 이동할 수 없는 파일이 있는 지점으로 축소됩니다. |
| <p>**desired=** <em>desiredsize</em></p> | <p>현재 파티션에 복구할 공간 크기(MB, 메가바이트)입니다.</p> |
| <p>**minimum=** <em>minimumsize</em></p> | <p>현재 파티션에 복구할 최소 공간 크기(MB, 메가바이트)입니다. 원하는 크기 또는 최소 크기를 지정하지 않은 경우 명령은 가능한 최대 공간의 양을 확보합니다.</p> 

<a id="addcon"></a>

## <a name="additional-considerations"></a>추가 고려 사항

-   파티션을 축소할 때 특정 파일(예: 페이징 파일 또는 섀도 복사본 저장 영역)은 자동으로 재배치될 수 없습니다. 또한 이동할 수 없는 파일이 있는 지점을 넘어서까지 할당된 공간을 줄일 수 없습니다. 축소 작업이 실패하는 경우 이동할 수 없는 파일을 식별하는 이벤트 259에 대한 응용 프로그램 로그를 확인합니다. 축소 작업을 차단하는 파일과 연결된 클러스터를 알고 있는 경우 명령 프롬프트에서 **fsutil** 명령을 사용할 수도 있습니다(**fsutil volume querycluster /?** 를 입력하여 사용). **querycluster** 매개 변수를 입력하면 명령 출력은 축소 작업을 완료하지 못하도록 하는 이동할 수 없는 파일을 식별합니다.
경우에 따라 파일을 일시적으로 재배치할 수 있습니다. 예를 들어 파티션을 더 축소해야 하는 경우 제어판을 사용하여 페이징 파일 또는 저장된 섀도 복사본을 다른 디스크로 이동하고, 저장된 섀도 복사본을 삭제하고, 볼륨을 축소한 다음 페이징 파일을 다시 디스크로 이동할 수 있습니다. 동적 불량 클러스터 다시 매핑을 통해 감지된 불량 클러스터의 수가 너무 많은 경우 파티션을 축소할 수 없습니다. 이러한 경우 데이터를 이동하고 디스크를 교체하는 것을 고려해야 합니다.

-  블록 수준 복사를 사용하여 데이터를 전송하면 안 됩니다. 불량 섹터 테이블까지 복사되고, 새 디스크가 정상인 섹터까지 동일하게 불량으로 처리합니다.

-   원시 파티션(파일 시스템이 없는 파티션) 또는 NTFS 파일 시스템을 사용하는 파티션의 주 파티션과 논리 드라이브를 축소할 수 있습니다.

## <a name="see-also"></a>관련 항목

-   [기본 볼륨 관리](manage-basic-volumes.md)