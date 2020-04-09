---
title: 'ksetup: changepassword'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68b14388ff3c33458873b494c8d5a770b44f7545
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841786"
---
# <a name="ksetupchangepassword"></a>ksetup: changepassword



키 배포 센터 (KDC) 암호 (kpasswd) 값을 사용 하 여 로그온 한 사용자의 암호를 변경 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<OldPasswd >|로그온 한 사용자의 기존 암호를 명시 합니다.|
|\<NewPasswd >|로그온 한 사용자의 새 암호를 명시 합니다.|

## <a name="remarks"></a>주의

이 명령은 KDC password (kpasswd) 값을 사용 하 여 로그온 한 사용자의 암호를 변경 합니다. **Ksetup/** kpasswd 명령을 실행 하 여 출력에 설정 된 경우이를 표시 합니다.

사용자의 새 암호는이 컴퓨터에 설정 된 모든 암호 요구 사항을 충족 해야 합니다.

사용자 계정이 현재 도메인에 없는 경우 시스템은 사용자 계정이 있는 도메인 이름을 입력 하도록 요청 합니다.

다음 로그온 할 때 암호 변경을 강제로 적용 하려면이 명령을 사용 하 여 별표 (*)를 사용할 수 있으므로 사용자에 게 새 암호를 입력 하 라는 메시지가 표시 됩니다.

명령의 출력은 성공 또는 실패 상태를 알려 줍니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

이 도메인에서 현재이 컴퓨터에 로그온 한 사용자의 암호를 변경 합니다.
```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```
Contoso 도메인에 현재 로그온 되어 있는 사용자의 암호를 변경 합니다.
```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```
다음 로그온 할 때 현재 로그온 한 사용자가 암호를 변경 하도록 강제 합니다.
```
ksetup /changepassword Pas$w0rd *
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)