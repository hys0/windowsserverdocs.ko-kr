---
title: bdehdcfg
description: BitLocker 드라이브 암호화에 필요한 파티션이 있는 하드 드라이브를 준비 하는 bdehdcfg 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3bcc901847bb8d687d59bc3270dab39de0af8d60
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718565"
---
# <a name="bdehdcfg"></a>bdehdcfg

BitLocker 드라이브 암호화에 필요한 파티션이 있는 하드 드라이브를 준비합니다. BitLocker 설치 프로그램은 필요에 따라 드라이브를 준비 하 고 다시 분할할 수 있는 기능을 포함 하므로 대부분의 Windows 7 설치는이 도구를 사용할 필요가 없습니다.

> [!WARNING]
> 알려진된와 충돌 하는 **BitLocker로 보호 되지 않는 고정된 드라이브에 대 한 쓰기 액세스 거부** 그룹 정책 설정에 있는 **컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\BitLocker Drive 고정 데이터 드라이브**합니다.
>
>이 정책 설정을 사용 하는 경우 컴퓨터에서 bdehdcfg가 실행 되는 경우 다음과 같은 문제가 발생할 수 있습니다.
>
>- 려 할 때 시스템 드라이브에서 드라이브를 만들고 드라이브 축소 크기 성공적으로 감소 됩니다 및 원시 파티션 생성 됩니다. 그러나 원시 파티션에 포맷 되지 않습니다. 새 활성 드라이브를 포맷할 수 없습니다. 라는 오류 메시지가 표시 됩니다. BitLocker에 대 한 드라이브를 수동으로 준비 해야 할 수도 있습니다.
>
>- 시스템 드라이브를 만들려면 할당 되지 않은 공간을 사용 하려는 경우 원시 파티션 생성 됩니다. 그러나 원시 파티션에 포맷 되지 않습니다. 새 활성 드라이브를 포맷할 수 없습니다. 라는 오류 메시지가 표시 됩니다. BitLocker에 대 한 드라이브를 수동으로 준비 해야 할 수도 있습니다.
>
>- 시스템 드라이브에 기존 드라이브를 병합 하 려 할 때 시스템 드라이브를 만들려면 대상 드라이브에 필요한 부팅 파일을 복사 하는 도구 실패 합니다. 다음 오류 메시지가 표시 됩니다. BitLocker 설치에서 부팅 파일을 복사 하지 못했습니다. BitLocker에 대 한 드라이브를 수동으로 준비 해야 할 수도 있습니다.
>
>- 이 정책 설정은 시행 되는 경우 드라이브는 보호 되므로 하드 드라이브를 다시 분할 수 없습니다. 이전 버전의 Windows에서 조직에서 컴퓨터를 업그레이드 하는 경우 해당 컴퓨터는 단일 파티션으로 구성 된 컴퓨터에 정책 설정을 적용 하기 전에 필요한 BitLocker 시스템 파티션을 만들어야 합니다.

## <a name="syntax"></a>구문

```
bdehdcfg [–driveinfo <drive_letter>] [-target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}] [–newdriveletter] [–size <size_in_mb>] [-quiet]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |----------- |
| [bdehdcfg: driveinfo](bdehdcfg-driveinfo.md) | 지정 된 드라이브에서 드라이브 문자, 총 크기, 최대 여유 공간, 및 파티션의 파티션 특성을 표시 합니다. 유효한 파티션으로 나열 됩니다. 4 개의 주 또는 확장 된 파티션이 이미 존재 하는 경우에 할당 되지 않은 공간 나열 되지 않습니다. |
| [bdehdcfg: 대상](bdehdcfg-target.md) | 시스템 드라이브로 사용할 드라이브를의 부분을 정의 하 고 부분을 활성화 합니다. |
| [bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md) | 시스템 드라이브로 사용할 드라이브의 부분에 새 드라이브 문자를 할당 합니다. |
| [bdehdcfg: 크기](bdehdcfg-size.md) | 새 시스템 드라이브를 만들 때 시스템 파티션의 크기를 결정 합니다. |
| [bdehdcfg: quiet](bdehdcfg-quiet.md) | 명령줄 인터페이스에서 모든 동작 및 오류가 표시 되는 것을 방지 하 고 bdehdcfg가 후속 드라이브 준비 중에 발생할 수 있는 예/아니요 프롬프트에 대 한 예 대답을 사용 하도록 지시 합니다. |
| [bdehdcfg: 다시 시작](bdehdcfg-restart.md) | 드라이브를 준비 하는 완료 된 후 다시 시작 하는 컴퓨터에 지시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
