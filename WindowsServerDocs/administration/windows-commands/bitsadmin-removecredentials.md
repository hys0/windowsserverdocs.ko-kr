---
title: bitsadmin removecredentials
description: Windows 명령 항목에 대 한 **bitsadmin removecredentials** -작업에서 자격 증명을 제거 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cbd65442ff0d74ec1179a49df5d4a94785f3dd25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822294"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

작업에서 자격 증명을 제거합니다.

**1.2 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /RemoveCredentials <Job> <Target> <Scheme>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|대상|서버 또는 프록시|
|Scheme|다음 중 하나일 수 있습니다.</br>-기본-사용자 이름 및 암호를을 텍스트로 서버 또는 프록시에 전송 되는 인증 체계입니다.</br>-다이제스트-문제에 대 한 서버 지정 데이터 문자열을 사용 하는 챌린지-응답 인증 체계입니다.</br>-NTLM-Windows 네트워크 환경에서 인증에 대 한 사용자의 자격 증명을 사용 하는 챌린지-응답 인증 체계를 합니다.</br>-NEGOTIATE-간편 하 고 보호 협상 프로토콜 (Snego)는 서버 또는 인증에 사용할 체계를 결정 하는 프록시를 사용 하 여 협상 하는 챌린지-응답 인증 체계 라고도 합니다. 이러한 예로는 Kerberos 프로토콜 및 NTLM이 있습니다.</br>-PASSPORT-멤버 사이트에 대 한 단일 로그온을 제공 하는 Microsoft에서 제공 하는 중앙 집중식된 인증 서비스입니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에서 자격 증명을 제거 *myDownloadJob*합니다.
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)