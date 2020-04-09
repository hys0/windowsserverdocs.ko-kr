---
title: 연결 vdisk
description: '**연결 vdisk**에 대 한 Windows 명령 항목으로, 호스트 컴퓨터에 로컬 하드 디스크 드라이브로 표시 되도록 VHD (가상 하드 디스크)를 연결 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3a903ed231e34ac902ce10b5342f27e772ac89f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851266"
---
# <a name="attach-vdisk"></a>연결 vdisk

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

연결 (라고도 마운트 또는 표면) 가상 하드 디스크 (VHD) 로컬 하드 디스크 드라이브와 호스트 컴퓨터에 표시 되도록 합니다. VHD 연결 하면 디스크 파티션 및 파일 시스템 볼륨에 이미, VHD 내의 볼륨에 드라이브 문자를 할당 됩니다.

> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.

## <a name="syntax"></a>구문

```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| readonly | 읽기 전용으로 VHD를 연결 합니다. 모든 쓰기 작업 반환 된 오류입니다. |
| `sd=<SDDL string>` | VHD에 사용자 필터를 설정합니다. 필터 문자열 설명자 정의 SDDL (Security Language) 형식 이어야 합니다. 기본적으로 사용자 필터는 실제 디스크에서와 같은 액세스를 허용합니다. SDDL 문자열 복잡할 수 있지만 가장 간단한 형태로 액세스를 보호 하는 보안 설명자 라고 임의 액세스 제어 목록 (DACL). 다음 형식으로 되어 있습니다. `D:<dacl_flags><string_ace1><string_ace2>``<string_acen>`<p>일반적인 DACL 플래그는:<p>- **합니다**. 액세스 허용<p>- **D**. 액세스 거부<p>일반 권한은 다음과 같습니다.<p>- **GA** 모든 액세스<p>- **GR**. 읽기 액세스<p>**GW**를 - 합니다. 쓰기 액세스<p>일반 사용자 계정에는<p>- **BA**. 기본 제공된 관리자<p>- **AU**. 인증된 사용자<p>- **CO** 만든이 소유자<p>**WD**를 - 합니다. 모든 사용자<p>예제:<p>**D:P: (A;; GR;;; AU** 는 인증 된 모든 사용자에 게 읽기 액세스를 제공 합니다.<p>**D:P: (A;; GA;;; WD** 은 모든 사용자에 게 모든 권한을 부여 합니다. |
| usefilesd | VHD에.vhd 파일의 보안 설명자를 사용 해야 함을 지정 합니다. 하는 경우는 **Usefilesd** 매개 변수를 지정 하지 않으면, VHD 명시적 보안 설명자가 있는 지정 되지 않은 경우는 **Sd** 매개 변수입니다. |
| noerr | 스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="remarks"></a>주의

- VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

읽기 전용으로 선택한 VHD를 연결 하려면 다음을 입력 합니다.

```
attach vdisk readonly
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [compact vdisk](compact-vdisk.md)

- [세부 정보 vdisk](detail-vdisk.md)

- [분리 vdisk](detach-vdisk.md)

- [vdisk 확장](expand-vdisk.md)

- [merge vdisk](merge-vdisk.md)

- [vdisk 선택](select-vdisk.md)

- [은](list_1.md)
