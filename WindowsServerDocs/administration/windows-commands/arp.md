---
title: arp
description: Windows 명령 항목에 대 한 **arp** -표시 하 고 IP 주소 및 해당 해결 된 물리적 주소를 저장 하는 데 주소 확인 프로토콜 (arp) 캐시의 항목을 수정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f7393c993601a5e1990cde3e6bc6763811062f4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435295"
---
# <a name="arp"></a>arp

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 하 고 주소 확인 프로토콜 (ARP) 캐시의 항목을 수정 합니다. Arp는 IP 주소 및 해당 해결 된 이더넷 또는 토큰 링 실제 주소를 저장 하는 데 사용 되는 하나 이상의 테이블을 포함 합니다. 컴퓨터에 설치 된 각 이더넷 또는 토큰 링 네트워크 어댑터에 대 한 별도 테이블이 있습니다. 매개 변수 없이 사용 **arp** 도움말 정보를 표시 합니다.
## <a name="syntax"></a>구문
```
arp [/a [<Inetaddr>] [/n <ifaceaddr>]] [/g [<Inetaddr>] [-n <ifaceaddr>]] [/d <Inetaddr> [<ifaceaddr>]] [/s <Inetaddr> <Etheraddr> [<ifaceaddr>]]
```
### <a name="parameters"></a>매개 변수

|                매개 변수                |                                                                                                                                                                                                                                                               설명                                                                                                                                                                                                                                                               |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /a [<Inetaddr>] [/n <ifaceaddr>]     | 모든 인터페이스에 대 한 현재 arp 캐시 테이블을 표시합니다. /N 매개 변수는 대 소문자를 구분 합니다.<br /><br />사용 하 여 특정 IP 주소에 대 한 arp 캐시 항목을 표시 하려면 **arp/a** 사용 하 여 합니다 *Inetaddr* 매개 변수를 여기서 *Inetaddr* IP 주소입니다. 하는 경우 *Inetaddr* 지정 하지 않으면 첫 번째 해당 인터페이스를 사용 합니다.<br /><br />특정 인터페이스에 대 한 arp 캐시 테이블을 표시 하려면 사용는 **n/***ifaceaddr* 와 함께에서 매개 변수를 **/a** 매개 변수 위치 *ifaceaddr* 는 IP 주소 인터페이스에 할당 합니다. |
|    /g [<Inetaddr>] [/n <ifaceaddr>]     |                                                                                                                                                                                                                                                          동일 **/a**합니다.                                                                                                                                                                                                                                                           |
|      [/d <Inetaddr> [<ifaceaddr>]       |                                                                                           특정 IP 주소를 가진 항목을 삭제 합니다. 여기서 *Inetaddr* IP 주소입니다.<br /><br />특정 인터페이스에 대 한 테이블에서 항목을 삭제 하려면 사용 합니다 *ifaceaddr* 매개 변수 위치 *ifaceaddr* 인터페이스에 할당 된 IP 주소입니다.<br /><br />모든 항목을 삭제 하려면 별표를 사용 하 여 (\*) 대신 와일드 카드 문자 *Inetaddr*합니다.                                                                                           |
| /s <Inetaddr> <Etheraddr> [<ifaceaddr>] |                                                                                                                     IP 주소를 확인 하 여 arp 캐시에 정적 항목을 추가 *Inetaddr* 실제 주소로 *Etheraddr*합니다.<br /><br />특정 인터페이스에 대 한 테이블에는 정적 arp 캐시 항목을 추가 하려면 사용 합니다 *ifaceaddr* 매개 변수 위치 *ifaceaddr* 인터페이스에 할당 된 IP 주소입니다.                                                                                                                     |
|                   /?                    |                                                                                                                                                                                                                                                  명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                   |

## <a name="remarks"></a>설명
- 에 대 한 IP 주소 *Inetaddr* 하 고 *ifaceaddr* 십진수 표기법으로 표현 됩니다.
- 실제 주소가 *Etheraddr* 16 진수 표기법으로 표현 되 고 (예: 00-AA-00-4F-2A-9C) 하이픈으로 구분 된 6 개의 바이트로 이루어져 있습니다.
- 추가 된 항목의 **/s** 매개 변수는 정적이 고 arp 캐시에서 만료 시간이 하지 않습니다. TCP/IP 프로토콜 중지 되 고 시작 하는 경우에 항목이 제거 됩니다. 정적 arp 영구 캐시 항목을 만들려면 해당 배치 **arp** 일괄 처리에서 명령 파일 및 예약 된 태스크를 사용 하 여 시작 배치 파일을 실행 합니다.
  ## <a name="BKMK_Examples"></a>예제
  모든 인터페이스에 대 한 arp 캐시 테이블을 표시 하려면 다음을 입력 합니다.
  ```
  arp /a
  ```
  IP 주소 10.0.0.99 할당 되는 인터페이스에 대 한 arp 캐시 테이블을 표시 하려면 다음을 입력 합니다.
  ```
  arp /a /n 10.0.0.99
  ```
  IP 주소 10.0.0.80 00-aa-00-4f-2a-9c로 확인 하는 실제 주소로 확인 되는 정적 arp 캐시 항목을 추가 하려면 다음을 입력 합니다.
  ```
  arp /s 10.0.0.80 00-AA-00-4F-2A-9C 
  ```
  ## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
