---
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
title: Fsutil 할당량
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 1e844d73348ee31f309f44895831ded9a2e6365c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439064"
---
# <a name="fsutil-quota"></a>Fsutil 할당량
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

네트워크 기반 저장소 보다 자세하게 제어할 수 있도록 NTFS 볼륨의 디스크 할당량을 관리 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil quota [disable] <VolumePath>
fsutil quota [enforce] <VolumePath>
fsutil quota [modify] <VolumePath> <Threshold> <Limit> <UserName>
fsutil quota [query] <VolumePath>
fsutil quota [track] <VolumePath>
fsutil quota [violations]
```

## <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                    설명                                                                                    |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    사용 안 함    |                                                         할당량 추적 및 지정된 된 볼륨에 적용 하는 사용 하지 않도록 설정 합니다.                                                          |
|    강제 적용    |                                                                   지정된 된 볼륨에 대 한 할당량 사용량을 적용합니다.                                                                   |
|    modify     |                                                              기존 디스크 할당량을 수정 하거나 새 할당량을 만듭니다.                                                              |
|     쿼리     |                                                                            기존 디스크 할당량 나열 합니다.                                                                            |
|     추적     |                                                                    디스크에서 지정 된 볼륨에서 사용을 추적 합니다.                                                                     |
|  위반   | 시스템 및 응용 프로그램 로그를 검색 하 고 할당량 위반이 검색 되었습니다 또는 사용자 할당량 임계값 또는 할당량 제한에 도달한 있는지를 나타내는 메시지가 표시 됩니다. |
| \<VolumePath> |                                  필수. 드라이브 이름 뒤에 콜론 또는 GUID 형식에서 지정 **볼륨 {** <em>GUID</em> **}** 합니다.                                  |
| \<Threshold>  |                            경고가 발생 하는 바이트 단위로 제한을 설정 합니다. 이 매개 변수는에 대 한 필요는 **fsutil 할당량 수정** 명령입니다.                            |
|   \<Limit>    |                                허용 된 최대 디스크 사용량 (바이트)를 설정합니다. 이 매개 변수는에 대 한 필요는 **fsutil 할당량 수정** 명령입니다.                                |
|  \<UserName>  |                                      도메인 또는 사용자 이름을 지정합니다. 이 매개 변수는에 대 한 필요는 **fsutil 할당량 수정** 명령입니다.                                       |

## <a name="remarks"></a>설명

-   볼륨 단위로 디스크 할당량은 구현 및 사용자별으로 구현 되도록 할 두 가지 하드 및 소프트 저장소 제한을 사용 합니다.

-   사용 하는 스크립트를 작성을 사용할 수 있습니다 **fsutil 할당량** 보고서로 컴파일하여 및 자동으로 시스템 관리자가 전자 메일을 보낼 새 사용자를 추가할 때마다 할당량 한도 설정 또는 할당량 한도 자동으로 추적 합니다.

### <a name="BKMK_examples"></a>예제
{928842df-5a01-11de-a85c-806e6f6e6963} GUID를 가진 지정 된 디스크 볼륨에 대 한 기존 디스크 할당량을 나열 하려면 다음을 입력 합니다.

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

드라이브 문자를 지정 된 디스크 볼륨에 대 한 기존 디스크 할당량을 나열 하려면 **c:** , 유형:

```
Fsutil quota query C:
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


