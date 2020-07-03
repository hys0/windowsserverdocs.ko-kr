---
title: bootcfg addsw
description: 지정 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가 하는 bootcfg addsw 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9d54c2cfdf898e1162d804220ae6dbb4a446fc5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926357"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가합니다.

## <a name="syntax"></a>구문

```
bootcfg /addsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm <maximumram>] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>매개 변수

| 용어 | 정의 |
| ---- | ---------- |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain>\<user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| `/mm <maximumram>` | 운영 체제에서 사용할 수 있는 (메가바이트) ram, 최대 크기를 지정 합니다. 32mb 보다 크거나 같은 값 이어야 합니다. |
| /bv | 추가 **/basevideo** 옵션을 지정 된 `<osentrylinenum>`, 운영 체제가 설치 된 비디오 드라이버에 대 한 표준 VGA 모드를 사용 하도록 지시 합니다. |
| /so | 지정 된에 **/sos** 옵션을 추가 하 여 `<osentrylinenum>` 운영 체제를 로드 하는 동안 장치 드라이버 이름을 표시 하도록 지시 합니다. |
| /ng | 추가 **/noguiboot** 옵션을 지정 된 `<osentrylinenum>`, CTRL + ALT + DEL 로그온 프롬프트 앞에 나타나는 진행률 표시줄을 사용 하지 않도록 설정 합니다. |
| `/id <osentrylinenum>` | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

**Bootcfg/addsw** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /addsw /mm 64 /id 2
bootcfg /addsw /so /id 3
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /addsw /ng /id 2
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
