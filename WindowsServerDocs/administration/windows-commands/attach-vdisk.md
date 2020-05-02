---
title: 연결 vdisk
description: 연결 vdisk 명령에 대 한 참조 항목으로, 호스트 컴퓨터에 로컬 하드 디스크 드라이브로 표시 되도록 VHD (가상 하드 디스크)를 연결 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91f988d1f84869874dbd0d6a25dce43ef5138066
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718905"
---
# <a name="attach-vdisk"></a>연결 vdisk

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

연결 (라고도 마운트 또는 표면) 가상 하드 디스크 (VHD) 로컬 하드 디스크 드라이브와 호스트 컴퓨터에 표시 되도록 합니다. VHD 연결 하면 디스크 파티션 및 파일 시스템 볼륨에 이미, VHD 내의 볼륨에 드라이브 문자를 할당 됩니다.

> [!IMPORTANT]
> 이 작업이 성공 하려면 VHD를 선택 하 고 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="syntax"></a>구문

```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| readonly | 읽기 전용으로 VHD를 연결 합니다. 모든 쓰기 작업 반환 된 오류입니다. |
| `sd=<SDDL string>` | VHD에 사용자 필터를 설정합니다. 필터 문자열 설명자 정의 SDDL (Security Language) 형식 이어야 합니다. 기본적으로 사용자 필터는 실제 디스크에서와 같은 액세스를 허용합니다. SDDL 문자열 복잡할 수 있지만 가장 간단한 형태로 액세스를 보호 하는 보안 설명자 라고 임의 액세스 제어 목록 (DACL). 다음 `D:<dacl_flags><string_ace1><string_ace2>`형식을 사용 합니다...`<string_acen>`<p>일반적인 DACL 플래그는:<ul><li>**입니다.** 액세스 허용</li><li>**4**. 액세스 거부</li></ul>일반 권한은 다음과 같습니다.<ul><li>**GA**. 모든 액세스</li><li>**GR**. 읽기 액세스</li><li> **GW**. 쓰기 액세스</li></ul>일반 사용자 계정에는<ul><li>**BA**. 기본 제공된 관리자</li><li>**AU**. 인증된 사용자</li><li>**공동**. 만든이 소유자</li><li>**WD**. 모든 사람</li></ul>예제:<ul><li>**D:P: (A;; GR;;; AU**. 인증 된 모든 사용자에 게 읽기 액세스 권한을 부여 합니다.</li><li>**D:P: (A;; GA;;; WD**. 모든 사용자에 게 모든 권한을 부여 합니다.</li></ul> |
| usefilesd | VHD에.vhd 파일의 보안 설명자를 사용 해야 함을 지정 합니다. 하는 경우는 **Usefilesd** 매개 변수를 지정 하지 않으면, VHD 명시적 보안 설명자가 있는 지정 되지 않은 경우는 **Sd** 매개 변수입니다. |
| noerr | 스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="examples"></a>예

읽기 전용으로 선택한 VHD를 연결 하려면 다음을 입력 합니다.

```
attach vdisk readonly
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [vdisk 선택](select-vdisk.md)

- [compact vdisk](compact-vdisk.md)

- [세부 정보 vdisk](detail-vdisk.md)

- [분리 vdisk](detach-vdisk.md)

- [vdisk 확장](expand-vdisk.md)

- [merge vdisk](merge-vdisk.md)

- [list](list_1.md)
