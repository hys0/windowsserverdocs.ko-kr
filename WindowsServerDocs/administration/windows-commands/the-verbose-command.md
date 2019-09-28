---
title: Verbose 명령
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c7ecc2bb3578b578060694c95833fd32674db10
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369907"
---
# <a name="the-verbose-command"></a>Verbose 명령



지정 된 명령에 대 한 자세한 정보 출력을 표시합니다. 사용할 수 있습니다 **/verbose** 실행 하는 다른 WDSUTIL 명령을 사용 합니다. 지정 해야 하는 참고 **/verbose** 및 **진행률/** 바로 뒤 **WDSUTIL**합니다.

## <a name="syntax"></a>구문

```
WDSUTIL /verbose <commands>
```

## <a name="examples"></a>예

자동 추가 데이터베이스에서 승인 된 컴퓨터를 삭제 하 고 자세한 정보 출력을 표시 하려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```