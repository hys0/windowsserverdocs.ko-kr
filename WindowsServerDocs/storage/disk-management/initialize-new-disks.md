---
title: "새 디스크 초기화"
description: "이 문서에는 새 디스크를 초기화하는 방법을 설명합니다."
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 587553746d45eceab654efd4d120038088d32991
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="initialize-new-disks"></a>새 디스크 초기화

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

> [!NOTE]
> **Backup Operators** 또는 **Administrators** 그룹의 구성원이어야 이 단계를 완료할 수 있습니다.

## <a name="to-initialize-new-disks"></a>새 디스크 초기화
1.  디스크 관리에서 초기화하고자 하는 디스크를 마우스 오른쪽 단추로 클릭하고 **디스크 초기화**를 클릭합니다.

2.  **디스크 초기화** 대화 상자에서 초기화할 디스크를 선택합니다. MBR(마스터 부트 레코드) 또는 GPT(GUID 파티션 테이블) 파티션 스타일을 선택할지 여부를 선택할 수 있습니다.

## <a name="additional-considerations"></a>추가 고려 사항

-   새 디스크가 **초기화되지 않음**으로 표시됩니다. 디스크를 사용하려면 그 전에 먼저 초기화해야 합니다. 디스크를 추가한 후 디스크 관리를 시작하면 디스크 초기화 마법사가 나타나 디스크를 초기화할 수 있습니다.

> [!NOTE]
> 새 디스크는 기본 디스크로 초기화됩니다.

