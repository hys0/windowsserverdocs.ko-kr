---
title: automount
description: 자동 탑재 기능을 사용 하거나 사용 하지 않도록 설정 하는 자동 탑재 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4635fc91-a477-4f17-8dcc-aa08854bfe45
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 897927c48a1ba2c2023e35ff1f4c93e6c33fb291
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923541"
---
# <a name="automount"></a>automount

적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

- [명령줄 구문 키](command-line-syntax-key.md)

> [!IMPORTANT]
> SAN(스토리지 영역 네트워크) 구성에서 자동 탑재를 비활성화하여 시스템에 표시되는 새 기본 볼륨에 드라이브 문자를 자동으로 탑재하거나 할당하지 않도록 합니다.

## <a name="syntax"></a>구문

자동 탑재 [{enable | disable | 스크럽}] [noerr]

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| enable | Windows 시스템에 추가 된 새 기본 및 동적 볼륨을 자동으로 탑재 하 고 드라이브 문자를 할당할 수 있게 합니다. |
| disable | Windows에서를 자동으로 시스템에 추가 된 새 기본 및 동적 볼륨을 탑재할 수 없습니다.<p>**참고**: 자동 탑재를 사용 하지 않도록 설정 하면 장애 조치 (failover) 클러스터가 구성 유효성 검사 마법사의 저장소 부분에 실패할 수 있습니다. |
| 삭제 | 볼륨 탑재 지점 디렉터리 및 시스템에서 더 이상 없는 볼륨에 대 한 레지스트리 설정을 제거 합니다. 이렇게 하면 볼륨을 자동으로 시스템에서 이전에 있던 및 시스템에 다시 추가 될 때 탑재 지점 볼륨에 이전 볼륨 않습니다. |
| noerr | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

자동 탑재 기능을 사용할 수 있는지를 확인 하려면 diskpart 명령 내에서 다음 명령을 입력 합니다.

```
automount
```

자동 탑재 기능을 사용 하려면 다음을 입력 합니다.

```
automount enable
```

자동 탑재 기능을 사용 하지 않으려면 다음을 입력 합니다.

```
automount disable
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [diskpart 명령](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc770877(v%3dws.11))
