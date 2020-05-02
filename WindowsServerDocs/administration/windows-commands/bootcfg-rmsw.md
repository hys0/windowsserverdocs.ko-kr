---
title: bootcfg rmsw
description: 지정 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 제거 하는 bootcfg rmsw 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41c9819fb3d669b24a5918077bef960869625a15
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708911"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 제거합니다.

## <a name="syntax"></a>구문

```
bootcfg /rmsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는 `<user>` `<domain>\<user>`로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| /mm | 지정 된 위치에서 /maxmem 옵션과 관련 된 최대 메모리 값을 제거 `<osentrylinenum>`합니다. 운영 체제에서 사용할 수 있는 RAM의 최대 크기를 지정 하는 /maxmem 옵션입니다. |
| /bv | 지정 된 위치에서 /basevideo 옵션 제거 `<osentrylinenum>`합니다. /Basevideo 옵션 설치 비디오 드라이버에 대 한 표준 VGA 모드를 사용 하 여 운영 체제에 지시 합니다. |
| /so | 지정 된 위치에서 동안 옵션을 제거 `<osentrylinenum>`합니다. 운영 체제가 로드 되는 디바이스 드라이버의 이름을 표시 하도록 지시 하는 동안 옵션입니다. |
| /ng | 지정 된 위치에서 /noguiboot 옵션 제거 `<osentrylinenum>`합니다. /Noguiboot 옵션에는 진행률 표시줄은 CTRL + ALT + DEL 로그온 프롬프트 앞에 나타나는 비활성화 합니다. |
| `/id <osentrylinenum>` | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

**Bootcfg/rmsw** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /rmsw /mm 64 /id 2
bootcfg /rmsw /so /id 3
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /rmsw /ng /id 2
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
