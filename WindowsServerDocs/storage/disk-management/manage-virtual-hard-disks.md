---
title: VHD(가상 하드 디스크) 관리
description: 이 문서에서는 가상 하드 디스크를 관리하는 방법을 설명합니다.
ms.date: 10/12/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6ffa7e9dc769b8d8c892d0af1ceae5246df62d3e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385813"
---
# <a name="manage-virtual-hard-disks-vhd"></a>VHD(가상 하드 디스크) 관리

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 디스크 관리를 통해 가상 하드 디스크를 만들고, 연결하고, 분리하는 방법을 설명합니다. VHD(가상 하드 디스크)는 탑재되고 나면 실제 하드 드라이브와 매우 동일하게 표시되고 작동하는 가상화된 하드 디스크 파일입니다. Hyper-V 가상 머신에서 가장 자주 사용됩니다. 

## <a name="viewing-vhds-in-disk-management"></a>디스크 관리에서 VHD 보기

디스크 관리에서 VHD는 실제 디스크처럼 표시됩니다. VHD는 연결되었을 때(시스템에서 사용 가능한 상태가 되었을 때) 파란색으로 표시됩니다. 분리되었을 때(사용 불가능한 상태일 때) 디스크 아이콘은 회색으로 변합니다.

## <a name="creating-a-vhd"></a>VHD 만들기

> [!NOTE]
> **Backup Operators** 또는 **Administrators** 그룹의 구성원이어야 이 단계를 완료할 수 있습니다.

**VHD를 만들려면**

1.  **작업** 메뉴에서 **VHD 만들기**를 선택합니다.

2.  **가상 하드 디스크 만들고 연결하기** 대화 상자에서 VHD 파일을 저장하고자 하는 실제 컴퓨터의 위치와 VHD의 크기 모두를 지정합니다.

3.  **가상 하드 디스크 형식**에서 **동적 확장** 또는 **고정 크기**를 선택한 다음, **확인**을 클릭합니다.

## <a name="attaching-and-detaching-a-vhd"></a>VHD 연결 및 분리

VHD(방금 만들었던 VHD 또는 이미 존재하는 또 다른 VHD)를 사용 가능한 상태로 만들기: 

1. **작업** 메뉴에서 **VHD 연결**을 선택합니다.

2. 정규화된 경로를 사용하여 VHD의 위치를 지정합니다.

사용할 수 없게 VHD를 분리하려면 다음을 수행합니다. 디스크를 마우스 오른쪽 단추로 클릭하고, **VHD 분리**를 선택한 다음, **확인**을 클릭합니다. VHD 분리는 VHD 또는 VHD에 저장된 어떠한 데이터도 삭제하지 않습니다.

## <a name="additional-considerations"></a>추가 고려 사항

-   VHD 위치를 지정하는 경로는 정규화된 경로여야 하며, \\Windows 디렉토리에 있을 수 없습니다.
-   VHD의 최소 크기는 3MB(메가바이트)입니다.
-   VHD는 기본 디스크만 될 수 있습니다.
-   VHD는 만들 때 초기화되고, 고정 크기가 큰 VHD를 만드는 데 시간이 걸릴 수 있기 때문입니다.
