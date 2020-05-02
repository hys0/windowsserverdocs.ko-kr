---
title: 퐁뒤
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2e3b64ff05ab9a539b7734f37b7515c6f9ef123
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725595"
---
# <a name="fondue"></a>퐁뒤

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Update 또는 그룹 정책에 의해 지정 된 다른 소스에서 필요한 파일을 다운로드 하 여 Windows 선택적 기능을 사용할 수 있습니다. 기능에 대 한 매니페스트 파일은 Windows 이미지에 이미 설치 되어 있어야 합니다. 
## <a name="syntax"></a>구문
```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootRequest}]
```
#### <a name="parameters"></a>매개 변수

|              매개 변수              |                                                                                                                                                                     설명                                                                                                                                                                     |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /enable-feature: <*feature_name*>   |                                                                               사용 하려는 Windows 선택적 기능의 이름을 지정 합니다. 명령줄 당 기능 중 하나에 사용할 수 있습니다. 여러 기능을 사용 하도록 설정 하려면 각 기능에 대해 fondue 사용 합니다.                                                                                |
|    /caller-name: <*program_name*>    |                                                                                 스크립트나 배치 파일에서 fondue 호출할 때 프로그램 또는 프로세스 이름을 지정 합니다. 이 옵션을 사용 하 여 오류가 발생 하는 경우 프로그램 이름을 SQM 보고서에 추가할 수 있습니다.                                                                                 |
| /hide-ux: {모든 & #124; rebootRequest} | 사용 하 여 **모든** Windows Update에 액세스 하는 진행률 및 사용 권한 요청을 포함 하 여 사용자에 게 모든 메시지를 숨기려면 합니다. 권한이 필요한 경우 작업이 실패 합니다.<p>사용 하 여 **rebootRequest** 만 메시지를 숨기려면 사용자 컴퓨터를 다시 부팅 수 있는 권한을 요청 합니다. 컨트롤 요청 다시 부팅 하는 스크립트가 있으면이 옵션을 사용 합니다. |

## <a name="examples"></a>예
Microsoft.NET Framework 3.5를 사용 하려면 다음을 입력 합니다.
```
fondue.exe /enable-feature:NETFX3
```
Microsoft.NET Framework 3.5를 사용 하려면 SQM 보고서에 프로그램 이름을 추가 하 고 유형 사용자에 게 메시지를 표시 하지:
```
fondue.exe /enable-feature:NETFX3 /caller-name:Admin.bat /hide-ux:all
```
## <a name="additional-references"></a>추가 참조
- - [명령줄 구문 키](command-line-syntax-key.md)
  ## <a name="see-also"></a>참고 항목
  [Microsoft .NET Framework 3.5 배포 고려 사항](https://go.microsoft.com/fwlink/?LinkId=248869)
