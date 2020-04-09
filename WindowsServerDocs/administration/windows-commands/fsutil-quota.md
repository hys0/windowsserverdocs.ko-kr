---
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
title: Fsutil 할당량
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 4bb320d9192848cd7a6719c58bde4111798a799e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844216"
---
# <a name="fsutil-quota"></a>Fsutil 할당량
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

네트워크 기반 저장소를 보다 정확 하 게 제어할 수 있도록 NTFS 볼륨의 디스크 할당량을 관리 합니다.

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

### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                    설명                                                                                    |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    사용 안 함    |                                                         할당량 추적 및 지정된 된 볼륨에 적용 하는 사용 하지 않도록 설정 합니다.                                                          |
|    강제 적용    |                                                                   지정된 된 볼륨에 대 한 할당량 사용량을 적용합니다.                                                                   |
|    modify     |                                                              기존 디스크 할당량을 수정 하거나 새 할당량을 만듭니다.                                                              |
|     query     |                                                                            기존 디스크 할당량 나열 합니다.                                                                            |
|     추적     |                                                                    디스크에서 지정 된 볼륨에서 사용을 추적 합니다.                                                                     |
|  위반   | 시스템 및 애플리케이션 로그를 검색 하 고 할당량 위반이 검색 되었습니다 또는 사용자 할당량 임계값 또는 할당량 제한에 도달한 있는지를 나타내는 메시지가 표시 됩니다. |
| \<VolumePath > |                                  필수입니다. 드라이브 이름 뒤에 콜론 또는 GUID 형식에서 지정 **볼륨 {** <em>GUID</em> **}** 합니다.                                  |
| \<임계값 >  |                            경고가 발생 하는 제한 (바이트)을 설정 합니다. 이 매개 변수는에 대 한 필요는 **fsutil 할당량 수정** 명령입니다.                            |
|   \<제한 >    |                                허용 되는 최대 디스크 사용량 (바이트)을 설정 합니다. 이 매개 변수는에 대 한 필요는 **fsutil 할당량 수정** 명령입니다.                                |
|  \<사용자 이름 >  |                                      도메인 또는 사용자 이름을 지정합니다. 이 매개 변수는에 대 한 필요는 **fsutil 할당량 수정** 명령입니다.                                       |

## <a name="remarks"></a>주의

-   디스크 할당량은 볼륨 단위로 구현 되며, 하드 및 소프트 저장소 제한을 사용자 단위로 구현할 수 있도록 합니다.

-   새 사용자를 추가할 때마다 할당량 제한을 설정 하는 데 **fsutil quota** 를 사용 하는 write 스크립트를 사용 하거나, 할당량 한도를 자동으로 추적 하 고, 보고서로 컴파일한 후 자동으로 시스템 관리자에 게 전자 메일로 보낼 수 있습니다.

### <a name="examples"></a><a name="BKMK_examples"></a>예와
GUID, {928842df-5a01-11de-a85c-806e6f6e6963}를 사용 하 여 지정 된 디스크 볼륨에 대 한 기존 디스크 할당량을 나열 하려면 다음을 입력 합니다.

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

드라이브 문자를 지정 된 디스크 볼륨에 대 한 기존 디스크 할당량을 나열 하려면 **c:** , 유형:

```
Fsutil quota query C:
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


