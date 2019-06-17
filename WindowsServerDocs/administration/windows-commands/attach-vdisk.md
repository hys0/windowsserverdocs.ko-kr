---
title: vdisk를 연결 합니다.
description: Windows 명령 항목에 대 한 **vdisk를 연결** -연결 (라고도 마운트 또는 표면) 가상 하드 디스크 (VHD) 로컬 하드 디스크 드라이브와 호스트 컴퓨터에 표시 되도록 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb33d040ce0b2a7a9d06951a7e80251a0d0da614
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435222"
---
# <a name="attach-vdisk"></a>vdisk를 연결 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

연결 (라고도 마운트 또는 표면) 가상 하드 디스크 (VHD) 로컬 하드 디스크 드라이브와 호스트 컴퓨터에 표시 되도록 합니다. VHD 연결 하면 디스크 파티션 및 파일 시스템 볼륨에 이미, VHD 내의 볼륨에 드라이브 문자를 할당 됩니다.
> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.

## <a name="syntax"></a>구문
```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```
### <a name="parameters"></a>매개 변수

|    매개 변수     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     읽기 전용     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             읽기 전용으로 VHD를 연결합니다. 모든 쓰기 작업 반환 된 오류입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| sd=<SDDL string> | VHD에 사용자 필터를 설정합니다. 필터 문자열 설명자 정의 SDDL (Security Language) 형식 이어야 합니다. 기본적으로 사용자 필터는 실제 디스크에서와 같은 액세스를 허용합니다.<br /><br />SDDL 문자열 복잡할 수 있지만 가장 간단한 형태로 액세스를 보호 하는 보안 설명자 라고 임의 액세스 제어 목록 (DACL). 폼입니다. D:<dacl_flags><string_ace1><string_ace2>... <string_acen><br /><br />일반적인 DACL 플래그는:<br /><br />-    **** 액세스 허용<br />-   **D** 액세스 거부<br /><br />일반 권한은 다음과 같습니다.<br /><br />-   **GA** 대 한 모든 액세스<br />-   **GR** 읽기 액세스<br />-   **GW** 쓰기 액세스<br /><br />일반 사용자 계정에는<br /><br />-   **BA** 기본 제공 된 관리자<br />-   **AU** 인증 된 사용자<br />-   **CO** Creator owner<br />-   **WD** -모든 사용자<br /><br />예를 들면 다음과 같습니다.<br /><br />**D:P:(A;; GR;; AU** 모든 인증 된 사용자에 대 한 읽기 액세스를 제공 합니다.<br /><br />**D:P:(A;; GA;; WD** everyone에 게 완전 한 액세스 |
|    usefilesd     |                                                                                                                                                                                                                                                                                                                                                                                          VHD에.vhd 파일의 보안 설명자를 사용 해야 함을 지정 합니다. 하는 경우는 **Usefilesd** 매개 변수를 지정 하지 않으면, VHD 명시적 보안 설명자가 있는 지정 되지 않은 경우는 **Sd** 매개 변수입니다.                                                                                                                                                                                                                                                                                                                                                                                          |
|      noerr       |                                                                                                                                                                                                                                                                                                                                                                                                           스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.                                                                                                                                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>설명
- VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.
  ## <a name="BKMK_Examples"></a>예제
  읽기 전용으로 선택한 VHD를 연결 하려면 다음을 입력 합니다.
  ```
  attach vdisk readonly
  ```
  ## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
- [vdisk를 압축 합니다.](compact-vdisk.md)

- [세부 vdisk](detail-vdisk.md)
- [Vdisk를 분리 합니다.](detach-vdisk.md)
- [vdisk를 확장 합니다.](expand-vdisk.md)
- [Vdisk를 병합 합니다.](merge-vdisk.md)
- [vdisk를 선택 합니다.](select-vdisk.md)
- [list_1](list_1.md)
