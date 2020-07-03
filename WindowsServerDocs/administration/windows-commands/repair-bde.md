---
title: repair-bde
description: '* * * *에 대 한 참조 문서'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2ba82708acd9c5830e2dc8a09cd804ade342066
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935641"
---
# <a name="repair-bde"></a>repair-bde



액세스에 암호화 된 데이터가 심각 하 게 손상된 된 하드 디스크 드라이브는 BitLocker를 사용 하 여 암호화 된 경우. Repair-bde는 드라이브의 중요 한 부분을 다시 생성할 수와 올바른 복구 암호 또는 복구 키가 데이터를 해독 하는 데 사용으로 복구 가능한 데이터를 복원 합니다. 드라이브에 BitLocker 메타 데이터 데이터 손상 된 경우 복구 암호 또는 복구 키 외에도 백업 키 패키지를 제공할 수 있어야 합니다. 이 키 패키지 경우는 백업 Active Directory 도메인 서비스 (AD DS)에서 AD DS 백업에 대 한 기본 설정을 사용 합니다. 이 키 패키지 하 고 복구 암호 또는 복구 키를 디스크에서 손상 된 경우 BitLocker 보호 드라이브의 일부를 해독할 수 있습니다. 각 키 패키지는 해당 드라이브 식별자를가지고 있는 드라이브에 대해서만 작동 합니다. 사용할 수는 [Active Directory에 대 한 BitLocker 복구 암호 뷰어](https://technet.microsoft.com/library/dd875531(v=ws.10).aspx) AD DS에서이 키 패키지를 얻을 수 있습니다.

> [!NOTE]
> BitLocker 복구 암호 뷰어는 Windows Server 2012에서 서버 관리를 사용 하 여 설치할 수 있는 선택적 관리 기능 중 하나로 포함 됩니다.

Repair-bde 명령줄 도구에는 다음과 같은 제한이 있습니다.
-   복구 bde 암호화 또는 암호 해독 프로세스 동안 실패 한 드라이브를 복구할 수 없습니다.
-   복구 bde를 드라이브에 있는 모든 암호화 경우 다음 드라이브에 완벽 하 게 암호화 되어 있다고 가정 합니다.



## <a name="syntax"></a>구문

```
repair-bde <InputVolume> <OutputVolumeorImage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<InputVolume>|복구 하고자 하는 BitLocker로 암호화 된 드라이브의 드라이브 문자를 식별 합니다. 드라이브 문자는 콜론; 있어야 합니다. 예를 들어: **c:** 합니다.|
|\<OutputVolumeorImage>|복구 된 드라이브의 콘텐츠를 저장 하는 드라이브를 식별 합니다. 출력 드라이브에 대 한 모든 정보를 덮어씁니다.|
|-날짜별|볼륨의 잠금을 해제 하는 데 사용 해야 하는 복구 키의 위치를 식별 합니다. 이 명령으로도 지정할 수 있습니다 **-recoverykey**합니다.|
|-rp|볼륨의 잠금을 해제 하는 데 사용 해야 하는 숫자로 된 복구 암호를 식별 합니다. 이 명령으로도 지정할 수 있습니다 **-recoverypassword**합니다.|
|-pw|볼륨의 잠금을 해제 하는 데 사용 해야 하는 암호를 식별 합니다. 이 명령으로도 지정할 수 있습니다 **-암호**|
|-kp|볼륨의 잠금을 해제 하는 데 사용할 수 있는 복구 키 패키지를 식별 합니다. 이 명령으로도 지정할 수 있습니다 **-keypackage**합니다.|
|-lf|Repair-bde 오류, 경고 및 정보 메시지를 저장할 파일의 경로를 지정 합니다. 이 명령으로도 지정할 수 있습니다 **-로그 파일**합니다.|
|-f|볼륨을 잠글 수 없습니다 경우에 분리 되도록 합니다. 이 명령으로도 지정할 수 있습니다 **-강제로**합니다.|
|-? 또는 /?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

키 패키지의 경로를 지정 하지 않으면 **복구 bde** 키 패키지에 대 한 드라이브를 검색 합니다. 그러나 하드 드라이브가 손상 된 경우, **복구 bde** 패키지를 찾을 수 없으며 경로 제공 하 라는 메시지가 나타납니다.

## <a name="examples"></a>예

C 드라이브를 복구 하 고 드라이브 F에 저장 된 복구 키 파일 (Recoverykey.bek)을 사용 하 여 C 드라이브에서 D 드라이브에 콘텐츠를 쓰고이 시도의 결과를 Z 드라이브의 로그 파일 (log.txt)에 기록 합니다.
```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```
을 사용 하 여 C 드라이브를 복구 하 고 지정 된 48 자리 복구 암호를 사용 하 여 D 드라이브에 C 드라이브에 콘텐츠를 기록 합니다. 각 블록을 구분 하이픈으로 6 자리 숫자의 8 개 블록에 복구 암호를 입력 해야 합니다.
```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```
C 드라이브를 강제로 분리 한 다음 드라이브 F에 저장 된 복구 키 패키지 및 복구 키 파일 (Recoverykey.bek)을 사용 하 여 c 드라이브에 c 드라이브에 콘텐츠를 기록 합니다.
```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```
C 드라이브를 복구 하 고 C 드라이브에서 D 드라이브에 콘텐츠를 쓴 다음, 메시지가 표시 되 면 C: 드라이브의 잠금을 해제 하는 암호를 입력 해야 합니다.
```
repair-bde C: D: -pw
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)