---
title: bitsadmin setsecurityflags
description: '**Bitsadmin setsecurityflags** 에 대 한 Windows 명령 항목-BITS에서 인증서 해지 목록을 확인 하 고, 특정 인증서 오류를 무시 하 고, 서버가 HTTP 요청을 리디렉션할 때 사용할 정책을 정의 하는 HTTP에 대 한 플래그를 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: acc5a64ef7c82b14e6815b6d51dda5ea4700dcad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380415"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags



비트 인증서 해지 목록 확인, 특정 인증서 오류를 무시 하 고 해야 하는 서버는 HTTP 요청을 리디렉션합니다 때 사용 하 여 정책을 정의 결정 하는 HTTP에 대 한 플래그를 설정 합니다. 값은 부호 없는 정수입니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetSecurityFlags <Job> <Value>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|값|주의 참조 하십시오.|

## <a name="remarks"></a>설명

**값** 매개 변수는 다음과 같은 알림 플래그 중 하나 이상을 포함할 수 있습니다.

|작업|이진 표현|
|------|---------------------|
|CRL 확인을 사용 하도록 설정|최하위 비트를 설정 합니다.|
|서버 인증서에 잘못 된 일반 이름 무시|오른쪽에서 두 번째 비트를 설정 합니다.|
|서버 인증서에 잘못 된 날짜를 무시 합니다.|오른쪽에서 세 번째 비트를 설정 합니다.|
|서버 인증서의 잘못 된 인증 기관 무시|오른쪽에서 네 번째 비트를 설정 합니다.|
|인증서를 잘못 사용 했습니다. 무시 합니다.|오른쪽에서 다섯 번째 비트를 설정 합니다.|
|리디렉션 정책|오른쪽에서 9에 11 비트에 의해 제어</br>0, 0, 0-리디렉션이 자동으로 허용 됩니다.</br>0, 0, 1-리디렉션이 발생 하면 IBackgroundCopyFile 인터페이스의 원격 이름이 업데이트 됩니다.</br>0, 1, 0 비트는 리디렉션이 발생 하면 작업에 실패 합니다.|
|HTTPS에서 HTTP 리디렉션을 허용합니다|오른쪽에서 12 비트를 설정 합니다.|

## <a name="BKMK_examples"></a>예와

명명 된 작업에 대 한 CRL 확인을 사용할 수 있도록 보안 플래그를 설정 하는 다음 예제에서는 *myJob*합니다.
```
C:\>bitsadmin /SetSecurityFlags myJob 0x0001
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)