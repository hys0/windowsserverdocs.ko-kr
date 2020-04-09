---
title: bcdedit
description: 새 저장소를 만들고, 기존 저장소를 수정 하 고, 부팅 메뉴 매개 변수를 추가 하는 **bcdedit**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab2da47d-3aac-44a0-b7fd-bd9561d61553
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/27/2018
ms.openlocfilehash: f5bd39fa29dc99bba0d3600fc8609a355ffe540c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851076"
---
# <a name="bcdedit"></a>bcdedit

부팅 애플리케이션을 설명 하 고 부팅 애플리케이션 설정에 사용 되는 저장소를 제공 하는 부팅 구성 데이터 (BCD) 파일입니다. 개체와 저장소에는 요소는 효과적으로 Boot.ini를 대체 합니다.

BCDEdit는 BCD 저장소를 관리 하기 위한 명령줄 도구입니다. 다양 한 새 저장소 만들기를 포함 한 목적으로 사용할 수 있습니다, 그리고 추가, 수정 하 고 기존 저장소 부팅 메뉴 매개 변수 등입니다. BCDEdit 기본적으로 동일한 목적으로 사용 Bootcfg.exe 이전 버전의 Windows에서는 하지만 두 가지 주요 향상 기능:

- Bootcfg.exe 보다 더 광범위 한 부팅 매개 변수를 제공합니다.

- 스크립팅 지원을 향상 시켰습니다.

> [!NOTE]
> BCDEdit를 사용 하 여 BCD를 수정 하려면 관리자 권한이 필요 합니다.

BCDEdit 이후 버전의 Windows 및 Windows Vista의 부팅 구성을 편집 하는 기본 도구입니다. Windows Vista 배포는 %WINDIR%\System32 폴더에 포함 되어 있습니다.

BCDEdit 표준 데이터 형식에만 제한 되며 주로 BCD 변경 하는 단일 일반적인 작업을 수행 하도록 구성 되었습니다. 더 복잡 한 작업 또는 비표준 데이터 형식에 대 한 BCD Windows Management Instrumentation (WMI) 응용 프로그래밍 인터페이스 (API)를 사용 하 여 강력 하 고 유연한 사용자 지정 도구를 만들려고 하는 것이 좋습니다.

## <a name="syntax"></a>구문

```
BCDEdit /Command [<Argument1>] [<Argument2>] ...
```

### <a name="parameters"></a>매개 변수

### <a name="general-bcdedit-command-line-option"></a>일반 BCDEdit 명령줄 옵션

| 옵션 | 설명 |
| ------ | ----------- |
| /? | BCDEdit 명령 목록이 표시 됩니다. 사용 가능한 명령에 대 한 요약을 표시 인수 없이이 명령을 실행 합니다. 특정 명령에 대 한 자세한 도움말을 표시 하려면 실행 **bcdedit /?** `<command>`. 여기서 `<command>`는 검색 중인 명령 이름입니다. 예를 들어 **bcdedit /? createstore** Createstore 명령에 대 한 자세한 도움말을 표시 합니다. |

#### <a name="parameters-that-operate-on-a-store"></a>저장소에서 작동 하는 매개 변수

| 옵션 | 설명 |
| ------ | ----------- |
| /createstore | 새로운 빈 부팅 구성 데이터 저장소를 만듭니다. 만든된 저장소 시스템 저장소가 않습니다. |
| /export | 내보내기는 시스템의 내용을 파일에 저장합니다. 이 파일 시스템 저장소의 상태를 복원 하려면 나중에 사용할 수 있습니다. 이 명령은 시스템 저장소에 대해서만 유효합니다. |
| /import | 시스템 저장소의 상태를 사용 하 여 이전에 생성 된 백업 데이터 파일을 사용 하 여 복원 된 **/내보내기** 옵션입니다. 이 명령은 가져오기 수행 되기 전에 시스템 저장소에서 기존 항목을 삭제 합니다. 이 명령은 시스템 저장소에 대해서만 유효합니다. |
| /store | 이 옵션을 사용 하는 저장소를 지정 하려면 대부분 BCDedit 명령으로 사용할 수 있습니다. 이 옵션을 지정 하지 않으면 BCDEdit 시스템 저장소에서 작동 합니다. 실행의 **bcdedit /store** 자체로 명령은 실행와 같습니다는 **활성 bcdedit /enum** 명령입니다. |

#### <a name="parameters-that-operate-on-entries-in-a-store"></a>저장소의 항목에서 작동 하는 매개 변수

| 매개 변수 | 설명 |
| ------ | ----------- |
| /copy | 동일한 시스템 저장소에 지정 된 부팅 항목의 복사본을 만듭니다. |
| 만들기 / | 부팅 구성 데이터 저장소에 새 항목을 만듭니다. 잘 알려진 식별자를 지정 하면 **/응용 프로그램**, **상속 /** , 및 **/device** 매개 변수를 지정할 수 없습니다. 식별자가 지정 된 열 또는 하지 잘 알려져 있는 경우는 **/응용 프로그램**, **상속 /** , 또는 **/device** 옵션을 지정 해야 합니다. |
| /delete | 지정된 된 항목에서 요소를 삭제합니다. |

#### <a name="parameters-that-operate-on-entry-options"></a>항목 옵션에서 작동 하는 매개 변수

| 매개 변수 | 설명 |
| ------ | ----------- |
| /deletevalue | 부팅 항목에서 지정된 된 요소를 삭제합니다. |
| 설정 / | 항목 옵션 값을 설정합니다. |

#### <a name="parameters-that-control-output"></a>출력을 제어 하는 매개 변수

| 매개 변수 | 설명 |
| ------ | ----------- |
| /enum | 저장소에 항목을 나열 합니다. **/enum** 옵션은 실행 되므로 BCEdit의 기본값은 **bcdedit** 매개 변수 없이 명령을 실행 중에 해당 하는 **활성 bcdedit /enum** 명령. |
| /v | 자세한 정보 표시 모드입니다. 일반적으로 잘 알려진 항목 식별자는 간단한 줄임 양식으로 표시 됩니다. 지정 **/v** 명령줄 옵션을 전체에서 모든 식별자를 표시 합니다. 실행 되는 **bcdedit /v** 자체로 명령은 실행와 같습니다는 **bcdedit /enum 활성 /v** 명령 합니다. |

#### <a name="parameters-that-control-the-boot-manager"></a>부팅 관리자를 제어 하는 매개 변수

| 매개 변수 | 설명 |
| ------ | ----------- |
| /bootsequence | 다음 부팅에 사용할 일회성 표시 순서를 지정 합니다. 이 명령은 비슷합니다는 **포함** 옵션, 그 다음에는 컴퓨터에만 사용 됩니다 점을 제외 하 고 시작 합니다. 그런 다음 컴퓨터 원래 표시 순서 되돌아갑니다. |
| /default | 부팅 관리자 제한 시간을 선택 하는 기본 항목을 지정 합니다. |
| 포함 | 부팅 관리자에서 사용자에 게 부팅 매개 변수를 표시할 때 사용 하는 표시 순서를 지정 합니다. |
| /timeout | (초)을 부팅 관리자가 기본 항목을 선택 하기 전에 대기할 시간을 지정 합니다. |
| /toolsdisplayorder | 표시할 때 사용 하 여 부팅 관리자 표시 순서를 지정 된 **도구** 메뉴. |

#### <a name="parameters-that-control-emergency-management-services"></a>응급 관리 서비스를 제어 하는 매개 변수

| 매개 변수 | 설명 |
| ------ | ----------- |
| /bootems | 지정된 된 항목에 대 한 관리 EMS (응급 서비스)를 사용 하지 않도록 설정 하거나 사용 합니다. |
| /ems | 지정 된 운영 체제 부팅 항목에 대해 EMS를 사용 하지 않도록 설정 하거나 사용 합니다. |
| /emssettings | 컴퓨터에 대 한 전역 EMS 설정을 설정합니다. **/emssettings** 모든 특정 부팅 항목에 대해 EMS를 사용 하지 않도록 설정 하거나 설정 하지 않습니다. |

#### <a name="parameters-that-control-debugging"></a>디버깅을 제어 하는 매개 변수

| 매개 변수 | 설명 |
| ------ | ----------- |
| /bootdebug | 사용 하거나 지정 된 부팅 항목에 대 한 부팅 디버거를 사용 하지 않도록 설정 합니다. 이 명령은 모든 부팅 항목에 대해 제대로 작동 해도 부팅 애플리케이션에만 효과적입니다. |
| /dbgsettings | 지정 하거나 시스템에 대 한 전역 디버거 설정을 표시 합니다. 이 명령은 enablepose를 수행 하지 않습니다. 개별 전역 디버거 설정을 설정 하려면 **bcdedit/set** `<dbgsettings> <type> <value>` 명령을 사용 합니다. |
| /debug | 사용 하거나 지정 된 부팅 항목에 대 한 커널 디버거를 사용 하지 않도록 설정 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

BCDEdit를 사용 하는 방법에 대 한 예제는 [Bcdedit 옵션 참조](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference) 문서를 참조 하세요.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
