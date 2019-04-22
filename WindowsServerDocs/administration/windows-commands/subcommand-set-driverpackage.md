---
title: 하위 명령 집합 DriverPackage
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0513d3de2416f93f69b1e1cc286c38b12be94d15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818824"
---
# <a name="subcommand-set-driverpackage"></a>하위 명령: 집합 DriverPackage



이름 바꾸기 및/또는 사용 하거나 서버에 드라이버 패키지를 사용 하지 않도록 설정 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/ 서버:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름이 나 FQDN 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|[/DriverPackage:\<Name>]|수정 하는 드라이버 패키지의 현재 이름을 지정 합니다.|
|[/PackageId:\<ID>]|드라이버 패키지의 Windows 배포 서비스 ID를 지정합니다. 드라이버 패키지 이름으로 고유 하 게 식별할 수 없는 경우이 옵션을 지정 해야 합니다. 패키지에 대 한이 ID를 찾으려면 패키지가 드라이버 그룹을 클릭 합니다 (또는 **모든 패키지** 노드)에서 패키지를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다. 패키지 ID가 나열 된 **일반** 탭 합니다. 예: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}.|
|[/Name:\<새 이름 >]|드라이버 패키지에 대 한 새 이름을 지정합니다.|
|[/ 활성화: {예 | 아니요}|패키지를 사용 하지 않도록 설정 하거나 사용 합니다.|

## <a name="BKMK_examples"></a>예제

패키지에 대 한 설정을 변경 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)