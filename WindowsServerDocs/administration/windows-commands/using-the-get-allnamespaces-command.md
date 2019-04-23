---
title: Get AllNamespaces 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a907da52e773f85f0495681c21a55b3a8013e34e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889824"
---
# <a name="using-the-get-allnamespaces-command"></a>Get AllNamespaces 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
## <a name="parameters"></a>매개 변수
|매개 변수|Windows Server 2008|Windows Server 2008 R2|
|-------|------------|-------------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.||
|[/ ContentProvider:<name>]|만 지정 된 콘텐츠 공급자에 대 한 네임 스페이스를 표시합니다.||
|[/ 쇼: 클라이언트]|Windows Server 2008 에서만 지원 됩니다. 네임 스페이스에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.||
|[/details:Clients]|Windows Server 2008 r 2 에서만 지원 됩니다. 네임 스페이스에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.||
|[/ExcludedeletePending]|비활성화 된 모든 전송 목록에서 제외 됩니다.||
## <a name="BKMK_examples"></a>예제
모든 네임 스페이스를 보려면 다음을 입력 합니다.
```
wdsutil /Get-AllNamespaces
```
비활성화 된 작업을 제외한 모든 네임 스페이스를 보려면 다음을 입력 합니다.
-   Windows Server 2008
    ```
    wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:"MyContentProv" /Show:Clients /ExcludedeletePending
    ```
-   Windows Server 2008 R2
    ```
    wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:"MyContentProv" /details:Clients /ExcludedeletePending
    ```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[새 네임 스페이스 명령을 사용 하 여](using-the-new-namespace-command.md)
[제거 네임 스페이스 명령을 사용 하 여](using-the-remove-namespace-command.md)
[하위 명령: 시작 네임 스페이스](subcommand-start-namespace.md)
