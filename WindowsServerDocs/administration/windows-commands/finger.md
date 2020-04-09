---
title: finger
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78313fc4980b32e3aeb6d1611ef80d7eb6831fc1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844606"
---
# <a name="finger"></a>finger

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 원격 컴퓨터 (일반적으로 UNIX를 실행 하는 컴퓨터)에 있는 사용자 또는 사용자에 대 한 정보를 표시 합니다. 원격 컴퓨터의 형식 및 사용자 정보 표시의 출력을 지정합니다. 매개 변수 없이 사용 **손가락** 도움말을 표시 합니다. 
## <a name="syntax"></a>구문
```
finger [-l] [<User>] [@<Host>] [...]
```
#### <a name="parameters"></a>매개 변수

| 매개 변수 |                                                                            설명                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          긴 목록 형식으로 사용자 정보를 표시합니다.                                                           |
|  <User>   | 정보를 보려는 사용자를 지정 합니다. 생략 하면는 *사용자* 매개 변수를 **손가락** 지정된 된 컴퓨터의 모든 사용자에 대 한 정보를 표시 합니다. |
|  @<Host>  |        사용자 정보를 찾고 있는 핑거 서비스를 실행 하는 원격 컴퓨터를 지정 합니다. 컴퓨터 이름 또는 IP 주소를 지정할 수 있습니다.        |
|    /?     |                                                               명령 프롬프트에 도움말을 표시합니다.                                                                |

## <a name="remarks"></a>주의
User@Host 매개 변수를 여러 개 지정할 수 있습니다.
접두사를 지정 해야 **손가락** 슬래시 (/) 대신 하이픈 (-)와 매개 변수입니다.
이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 인터넷 프로토콜 (TCP/IP) 프로토콜을 설치 하는 경우에 사용할 수입니다.
Windows Server 2003 손가락 서비스를 제공 하지 않습니다.
## <a name="examples"></a><a name=BKMK_Examples></a>예와
컴퓨터 users.microsoft.com에 user1 계정에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
finger user1@users.microsoft.com
```
컴퓨터 users.microsoft.com에 모든 사용자에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>추가 참조
-   - [명령줄 구문 키](command-line-syntax-key.md)
