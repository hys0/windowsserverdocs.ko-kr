---
title: change port
description: MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 나열 하거나 변경 하는 변경 포트에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39273382038edb7709f2d99baea8090d71df3a57
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848076"
---
# <a name="change-port"></a>change port

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

나열 하거나 MS-DOS 애플리케이션과 호환 되도록 COM 포트 매핑을 변경 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문

```
change port [<PortX>=<PortY| /d <PortX| /query]
```

### <a name="parameters"></a>매개 변수


|    매개 변수    |              설명               |
|-----------------|----------------------------------------|
| <PortX>=<PortY> | COM <*Portx*>를 <*폰* 에 매핑합니다> |
|   /d <PortX>    | COM <*Portx*>에 대 한 매핑을 삭제 합니다. |
|     / 쿼리      | 현재 포트 매핑을 표시 합니다. |
|       /?        | 명령 프롬프트에서 도움말을 표시 합니다. |

## <a name="remarks"></a>주의

- 대부분의 MS-DOS 애플리케이션 COM4 직렬 포트를 통해 c o m 1만 지원합니다. **포트 변경** 명령 직렬 포트에 액세스 하는 포트 번호가 큰 COM을 지원 하지 않는 응용 프로그램을 허용 하는 다른 포트 번호를 직렬 포트에 매핑합니다. 다시 매핑은 현재 세션에 대해서만 작동 하며 세션에서 로그 오프 한 다음 다시 로그온 하는 경우에는 유지 되지 않습니다.

- 사용 하 여 **포트 변경** 대 한 현재 매핑을 사용할 수 있는 COM 포트를 표시 하려면 매개 변수 없이 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

- COM12 c o m 1을 사용 하기 위해 MS-DOS-기반 애플리케이션을 매핑하려면 다음을 입력 합니다.
  ```
  change port com12=com1
  ```
- 현재 매핑된 포트를 표시 하려면 다음을 입력 합니다.
  ```
  change port /query
  ```

### <a name="additional-references"></a>추가 참조
- - [명령줄 구문 키](command-line-syntax-key.md)
- [change](change.md)
- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
