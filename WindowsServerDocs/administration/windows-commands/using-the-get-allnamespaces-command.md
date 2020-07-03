---
title: get AllNamespaces 스페이스
description: 서버에 있는 모든 네임 스페이스에 대 한 정보를 표시 하는 get AllNamespaces 스페이스에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de44d659657a8d6df10c0f2ea7b7fb2a670b7f88
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935050"
---
# <a name="get-allnamespaces"></a>get AllNamespaces 스페이스

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 모든 네임 스페이스에 대 한 정보를 표시합니다.

## <a name="syntax"></a>구문
Windows Server 2008:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 R2:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/details:Clients] [/ExcludedeletePending]
```
### <a name="parameters"></a>매개 변수

|         매개 변수         |                                                                               Windows Server 2008                                                                               | Windows Server 2008 R2 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|  [/ 서버:<Server name>]  | 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다. |                        |
| [/ ContentProvider:<name>] |                                                        만 지정 된 콘텐츠 공급자에 대 한 네임 스페이스를 표시합니다.                                                         |                        |
|      [/ 쇼: 클라이언트]      |                            Windows Server 2008 에서만 지원 됩니다. 네임 스페이스에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.                             |                        |
|    [/세부 정보: 클라이언트]     |                           Windows Server 2008 r 2 에서만 지원 됩니다. 네임 스페이스에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.                           |                        |
|  [/ExcludedeletePending]  |                                                              비활성화 된 모든 전송 목록에서 제외 됩니다.                                                              |                        |

## <a name="examples"></a>예
모든 네임 스페이스를 보려면 다음을 입력 합니다.
```
wdsutil /Get-AllNamespaces
```
비활성화 된 작업을 제외한 모든 네임 스페이스를 보려면 다음을 입력 합니다.
- Windows Server 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /details:Clients /ExcludedeletePending
  ```
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md) 
   [새 네임 스페이스 명령을](using-the-new-namespace-command.md) 
   사용 하 여 [네임 스페이스 제거 명령을](using-the-remove-namespace-command.md) 
   사용 하 여 [하위 명령: 시작-네임 스페이스](subcommand-start-namespace.md)
