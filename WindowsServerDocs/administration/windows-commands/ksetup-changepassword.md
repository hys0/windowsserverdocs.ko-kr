---
title: ksetup:changepassword
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f629c6c7930777583df38f5af900ed380ec60f9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878534"
---
# <a name="ksetupchangepassword"></a>ksetup:changepassword



로그온 한 사용자의 암호를 변경 하려면 키 배포 센터 (KDC) 암호 (kpasswd) 값을 사용 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<OldPasswd>|로그온 한 사용자의 기존 암호를 알려 줍니다.|
|\<NewPasswd>|사용자의 새 암호 로그인을 명시합니다.|

## <a name="remarks"></a>설명

이 명령은 KDC 암호 (kpasswd) 값을 사용 하 여 로그온 한 사용자의 암호를 변경 합니다. kpasswd 경우 설정, 실행 하 여 출력에 표시 되는 **ksetup /dumpstate** 명령입니다.

사용자의 새 암호는이 컴퓨터에 설정 된 모든 암호 요구 사항을 충족 해야 합니다.

현재 도메인에서 사용자 계정이 없으면 사용자 계정이 있는 도메인 이름을 제공 하는 시스템이 묻습니다.

강제로 다음 로그온 시 암호를 변경 하려는 경우이 명령은 새 암호를 묻는 메시지가 사용자 있으므로 별표 (*)를 사용할 수 있습니다.

명령의 출력을 사용 하면 성공 또는 실패 상태의 알려줍니다.

## <a name="BKMK_Examples"></a>예제

이 도메인에서이 컴퓨터에 현재 로그온 한 사용자의 암호를 변경 합니다.
```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```
Contoso 도메인에 현재 로그온 한 사용자의 암호를 변경 합니다.
```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```
다음 로그온 시 암호를 변경 하려면 현재 로그온된 한 사용자를 강제 합니다.
```
ksetup /changepassword Pas$w0rd *
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)