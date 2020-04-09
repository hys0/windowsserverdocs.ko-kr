---
title: vdisk 확장
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 272714372a35f7f205b5a2e70cb2f2669b3a0634
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844896"
---
# <a name="expand-vdisk"></a>vdisk 확장

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

VHD (가상 하드 디스크)를 지정한 크기로 확장 합니다.
> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.
> ## <a name="syntax"></a>구문
> ```
> expand vdisk maximum=<n>
> ```
> ### <a name="parameters"></a>매개 변수
> 
> |  매개 변수  |                      설명                      |
> |-------------|-------------------------------------------------------|
> | 최대값 =<n> | 메가바이트 (MB) 단위로 VHD에 대 한 새 크기를 지정합니다. |
> 
> ## <a name="remarks"></a>주의
> - VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하는 **vdisk를 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.
>   ## <a name="examples"></a><a name=BKMK_Examples></a>예와
>   선택한 VHD를 20GB로 확장 하려면 다음을 입력 합니다.
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>추가 참조
> - - [명령줄 구문 키](command-line-syntax-key.md)
> - [연결 vdisk](attach-vdisk.md)
> - [compact vdisk](compact-vdisk.md)

-   [분리 vdisk](detach-vdisk.md)
-   [세부 정보 vdisk](detail-vdisk.md)
-   [Merge vdisk](merge-vdisk.md)
-   [vdisk 선택](select-vdisk.md)
-   [list_1](list_1.md)
