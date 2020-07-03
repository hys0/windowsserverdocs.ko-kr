---
title: mount
description: NFS (네트워크 파일 시스템) 네트워크 공유를 탑재 하는 탑재 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 505094251ab6b0053cc3d46801ba5f6170201ecd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935720"
---
# <a name="mount"></a>mount

NFS (네트워크 파일 시스템) 네트워크 공유를 탑재 하는 명령줄 유틸리티입니다. 인수 또는 옵션 없이 사용할 경우 **탑재** 탑재 된 모든 NFS 파일 시스템에 대 한 정보를 표시 합니다.

> [!NOTE]
> 이 유틸리티는 **NFS 용 클라이언트** 를 설치한 경우에만 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
mount [-o <option>[...]] [-u:<username>] [-p:{<password> | *}] {\\<computername>\<sharename> | <computername>:/<sharename>} {<devicename> | *}
```

### <a name="parameters"></a>매개 변수

| 매개 변수  | 설명 |
| ---------- | ----------- |
| -o rsize =`<buffersize>` | (킬로바이트) 읽기 버퍼의 크기를 설정합니다. 허용 가능한 값은 1, 2, 4, 8, 16 및 32입니다. 기본값은 32KB입니다. |
| -o wsize =`<buffersize>` | (킬로바이트) 쓰기 버퍼의 크기를 설정합니다. 허용 가능한 값은 1, 2, 4, 8, 16 및 32입니다. 기본값은 32KB입니다. |
| -o 제한 시간 =`<seconds>` | 원격 프로시저 호출 (RPC)을 초 단위로 시간 제한 값을 설정합니다. 허용 가능한 값은 0.8, 0.9 및 1-60; 범위의 모든 정수 기본값은 0.8입니다. |
| -o 재시도 =`<number>` | 소프트 탑재에 대 한 재시도 횟수를 설정합니다. 허용 가능한 값은 1-10; 범위에 있는 정수 기본값은 1입니다. |
| -o mtype =`{soft|hard}` | NFS 공유에 대 한 탑재 유형을 설정 합니다. 기본적으로 Windows에서는 소프트 탑재를 사용 합니다. 연결 문제가 있는 경우 소프트 탑재 시간 제한이 더 쉬워집니다. 그러나 NFS 서버를 다시 부팅 하는 동안 i/o 중단을 줄이려면 하드 탑재를 사용 하는 것이 좋습니다.|
| -o anon | 익명 사용자로 탑재 합니다. |
| -o nolock | 잠금을 사용 하지 않도록 설정 (기본값은 **활성화**). |
| -o casesensitive | 강제로 서버 대/소문자 구분에 조회 파일입니다. |
| -o fileaccess =`<mode>` | NFS 공유에 만들어진 새 파일의 기본 사용 권한 모드를 지정 합니다. 지정 *모드* 형태로 세 자리 숫자로 *ogw*, 여기서 *o*, *g*, 및 *w* 는 각각 해당 파일의 소유자, 그룹 및 전 세계를 각각 부여 된 액세스를 나타내는 숫자입니다. 숫자는 다음을 포함 하 여 0-7 범위 내에 있어야 합니다.<ul><li>**0:** 액세스 권한 없음</li><li>**1:** x (실행 액세스)</li><li>**2:** w (쓰기 액세스)</li><li>**3:** wx (쓰기 및 실행 액세스)</li><li>**4:** r (읽기 액세스)</li><li>**5:** rx (읽기 및 실행 액세스)</li><li>**6:** rw (읽기 및 쓰기 권한)</li><li>**7:** rwx (읽기, 쓰기 및 실행 액세스)</li></ul> |
| -o lang =`{euc-jp|euc-tw|euc-kr|shift-jis|Big5|Ksc5601|Gb2312-80|Ansi)` | NFS 공유에서 구성할 언어 인코딩을 지정 합니다. 공유에서 한 언어만 사용할 수 있습니다. 이 값은 다음 값 중 하나를 포함할 수 있습니다.<ul><li>**euc-jp:** 일본어</li><li>**euc-hy 다음과 같이 합니다.** 중국어</li><li>**euc-kr:** 한국어</li><li>**shift-jis:** 일본어</li><li>**Big5:** 중국어</li><li>**Ksc5601:** 한국어</li><li>**Gb2312-80:** 중국어 간체</li><li>**Ansi:** ANSI 인코딩</li></ul> |
| 나무`<username>` | 공유를 마운트 하는 데 사용할 사용자 이름을 지정 합니다. *사용자 이름* 앞에 백슬래시 (*)가 없으면 *\** UNIX 사용자 이름으로 처리 됩니다. |
| ®`<password>` | 공유를 마운트 하는 데 사용할 암호입니다. 별표 (**&#42;**)를 사용 하는 경우 암호를 입력 하 라는 메시지가 표시 됩니다. |
| `<computername>` | NFS 서버의 이름을 지정 합니다. |
| `<sharename>` | 파일 시스템의 이름을 지정합니다. |
| `<devicename>` | 장치의 드라이브 문자와 이름을 지정 합니다. 별표 (**&#42;**)를 사용 하는 경우이 값은 사용 가능한 첫 번째 드라이버 문자를 나타냅니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
