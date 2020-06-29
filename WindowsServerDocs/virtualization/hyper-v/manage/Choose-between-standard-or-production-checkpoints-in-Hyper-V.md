---
title: Hyper-v에서 표준 또는 프로덕션 검사점 중에서 선택
description: 표준 또는 프로덕션 검사점을 사용 하도록 가상 컴퓨터를 구성 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 92bb573b-03b7-470e-b72e-e35edf52b349
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 4e5e3d2d81f9ee1b7cbb4a60a1ade2c218d1e769
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474290"
---
# <a name="choose-between-standard-or-production-checkpoints-in-hyper-v"></a>Hyper-v에서 표준 또는 프로덕션 검사점 중에서 선택

>적용 대상: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019


Windows Server 2016 및 Windows 10 이상에서는 각 가상 머신에 대한 표준 및 프로덕션 검사점 간에 선택할 수 있습니다. 프로덕션 검사점은 새 가상 컴퓨터에 대 한 기본값입니다.

- 프로덕션 검사점은 모든 프로덕션 작업에 대해 완전히 지원 되는 방식으로 나중에 복원할 수 있는 가상 머신의 이미지 "지정 시간"입니다. 이는 저장된 상태 기술을 사용하는 대신 검사점을 만드는 게스트 내 백업 기술을 사용하여 수행됩니다.

- 표준 검사점 실행 중인 가상 머신의 상태, 데이터 및 하드웨어 구성을 캡처하고 용도로 개발 및 테스트 시나리오에서 사용합니다. 문제를 해결할 수 있도록 특정 상태 또는 조건 실행 중인 가상 머신을 다시 만들어야 할 경우 표준 검사점 유용할 수 있습니다.

  ## <a name="change-checkpoints-to-production-or-standard-checkpoints"></a>프로덕션 또는 표준 검사점 검사점 변경

1.  **Hyper-v 관리자**, 가상 머신을 마우스 오른쪽 단추로 클릭하고 클릭 **설정을**합니다.

2.  아래는 **관리** 섹션에서 **검사점**합니다.

3.  프로덕션 검사점 또는 표준 검사점 중 하나를 선택합니다.

    프로덕션 검사점을 선택 하면 경우 프로덕션 검사점을 수행할 수 없습니다 호스트 표준 검사점을 수행 해야 하는지 여부를 지정할 수 있습니다. 이 확인란의 선택을 취소 하 고 프로덕션 검사점을 가져올 수 없으므로, 검사점이 없거나 수행 됩니다.

4.  다른 위치에는 검사점 구성 파일을 저장 하려는 경우 변경에 **검사점 파일 위치** 섹션입니다.

5.  클릭 **적용** 변경 내용을 저장 합니다. 완료 되 면 클릭 **확인** 대화 상자를 닫습니다.

> [!NOTE]
> **프로덕션 검사점** 만 Active Directory Domain Services 역할 (도메인 컨트롤러) 또는 Active Directory LDS(Lightweight Directory Services) 역할을 실행 하는 게스트에서 지원 됩니다.

## <a name="additional-references"></a>추가 참조

-   [프로덕션 검사점](../What-s-new-in-Hyper-V-on-Windows.md#production-checkpoints-new)

-   [검사점 사용 또는 사용 안 함](Enable-or-disable-checkpoints-in-Hyper-V.md)



