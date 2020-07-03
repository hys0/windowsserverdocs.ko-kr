---
title: verbose
description: 지정 된 명령에 대 한 자세한 정보 출력을 표시 하는 자세한 정보에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 079e441ba4a932e23493e7e37fbe36cab4c4971f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935241"
---
# <a name="verbose"></a>verbose

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