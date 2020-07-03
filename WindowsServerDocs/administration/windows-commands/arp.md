---
title: arp
description: Arp 명령에 대 한 참조 문서로, IP 주소 및 해당 IP 주소를 저장 하는 데 사용 되는 arp (주소 확인 프로토콜) 캐시의 항목을 표시 하 고 수정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41f9ebde5faa3eda99402aa86a0aef5e55b42eba
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924005"
---
# <a name="arp"></a>arp

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ARP (주소 확인 프로토콜) 캐시에 있는 항목을 표시 하 고 수정 합니다. ARP 캐시에는 IP 주소 및 확인 된 이더넷 또는 토큰 링 실제 주소를 저장 하는 데 사용 되는 테이블이 하나 이상 포함 되어 있습니다. 컴퓨터에 설치 된 각 이더넷 또는 토큰 링 네트워크 어댑터에 대 한 별도 테이블이 있습니다. 매개 변수 없이 사용 **arp** 도움말 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
arp [/a [<inetaddr>] [/n <ifaceaddr>]] [/g [<inetaddr>] [-n <ifaceaddr>]] [/d <inetaddr> [<ifaceaddr>]] [/s <inetaddr> <etheraddr> [<ifaceaddr>]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[/a [<inetaddr>] [/n <ifaceaddr>]` | 모든 인터페이스에 대 한 현재 arp 캐시 테이블을 표시 합니다. **/N** 매개 변수는 대/소문자를 구분 합니다. 특정 IP 주소에 대 한 arp 캐시 항목을 표시 하려면 **inetaddr** 매개 변수와 함께 **arp/a** 를 사용 합니다. 여기서 **inetaddr** 는 IP 주소입니다. **Inetaddr** 를 지정 하지 않으면 첫 번째 적용 가능한 인터페이스가 사용 됩니다. 특정 인터페이스에 대 한 arp 캐시 테이블을 표시 하려면 **/n ifaceaddr** 매개 변수를 **/a** 매개 변수와 함께 사용 합니다. 여기서 **inetaddr** 는 인터페이스에 할당 된 IP 주소입니다. |
| `[/g [<inetaddr>] [/n <ifaceaddr>]` | 동일 **/a**합니다. |
| `[/d <inetaddr> [<ifaceaddr>]` | 특정 IP 주소를 사용 하 여 항목을 삭제 합니다. 여기서 **inetaddr** 는 ip 주소입니다. 특정 인터페이스에 대 한 테이블에서 항목을 삭제 하려면 **ifaceaddr** 매개 변수를 사용 합니다. 여기서 **ifaceaddr** 는 인터페이스에 할당 된 IP 주소입니다. 모든 항목을 삭제 하려면 **inetaddr**대신 별표 (*) 와일드 카드 문자를 사용 합니다. |
| `[/s <inetaddr> <etheraddr> [<ifaceaddr>]` | IP 주소 **inetaddr** 를 확인 하는 arp 캐시에 정적 항목을 추가 합니다. **etheraddr**. 정적 arp 캐시 항목을 특정 인터페이스에 대 한 테이블에 추가 하려면 **ifaceaddr** 매개 변수를 사용 합니다. 여기서 **ifaceaddr** 는 인터페이스에 할당 된 IP 주소입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="remarks"></a>설명

- **Inetaddr** 및 **ifaceaddr** 에 대 한 IP 주소는 점으로 구분 된 10 진수 표기법으로 표현 됩니다.

- **Etheraddr** 의 실제 주소는 16 진수 표기법으로 표현 되 고 하이픈으로 구분 된 6 바이트로 구성 됩니다 (예: 00-AA-00-4F-9C).

- **/S** 매개 변수를 사용 하 여 추가한 항목은 정적 이며 arp 캐시 시간이 초과 되지 않습니다. TCP/IP 프로토콜 중지 되 고 시작 하는 경우에 항목이 제거 됩니다. 영구 정적 arp 캐시 항목을 만들려면 적절 한 **arp** 명령을 배치 파일에 배치 하 고 예약 된 작업을 사용 하 여 시작 시 배치 파일을 실행 합니다.

## <a name="examples"></a>예

모든 인터페이스에 대 한 arp 캐시 테이블을 표시 하려면 다음을 입력 합니다.

```
arp /a
```

IP 주소가 *10.0.0.99*할당 된 인터페이스에 대 한 arp 캐시 테이블을 표시 하려면 다음을 입력 합니다.

```
arp /a /n 10.0.0.99
```

*10.0.0.80* IP 주소를 확인 하는 고정 arp 캐시 항목을 추가 하려면 *다음을 입력*합니다.

```
arp /s 10.0.0.80 00-AA-00-4F-2A-9C
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
