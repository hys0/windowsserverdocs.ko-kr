---
title: bcdboot
description: '**Bcdboot** 의 Windows 명령 항목-시스템 파티션을 빠르게 설정 하거나 시스템 파티션에 있는 부팅 환경을 복구 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c0f505180a503617335cc9575fea3d346bbe02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383443"
---
# <a name="bcdboot"></a>bcdboot



시스템 파티션을 신속 하 게 설정 하거나 시스템 파티션에 있는 부팅 환경을 복구를 수 있습니다. 시스템 파티션은 빈 파티션이 간단한 집합 데이터 BCD (부팅 구성) 파일을 복사 하 여 설정 됩니다.

BCDboot 및이 명령을 사용 하는 방법의 예제를 찾을 수 있는 위치에 대 한 정보를 포함 하 여 BCDboot에 대 한 자세한 내용은 참조는 [BCDboot 명령줄 옵션](https://technet.microsoft.com/library/hh824874.aspx) 항목입니다.

## <a name="syntax"></a>구문

```
bcdboot <source> [/l] [/s]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|원본|부팅 환경 파일을 복사 하기 위한 원본으로 사용 하 여 Windows 디렉터리의 위치를 지정 합니다.|
|/l|로캘을 지정 합니다. 기본 로캘은 영어 (미국)입니다.|
|/s|시스템 파티션의 볼륨 문자를 지정합니다. 기본값은 시스템 파티션을 펌웨어에서 식별 합니다.|

## <a name="BKMK_examples"></a>예와

이 명령을 사용 하는 방법의 자세한 예제는 참조는 [BCDboot 명령줄 옵션](https://technet.microsoft.com/library/hh824874.aspx) 항목입니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)