---
title: bitsadmin gethelpertokenflags
description: Windows 명령 항목에 대 한 **bitsadmin gethelpertokenflags** -BITS 전송 작업을 연관 된 도우미 토큰에 대 한 사용 플래그를 반환 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: e5665ed4670891dcbecd56215342f3d94e1ed753
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885794"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

에 대 한 사용 플래그를 반환 하는 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) BITS 전송 작업을 사용 하 여 연결 합니다.

**3.0 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetHelperTokenFlags <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

가능한 반환 값은 다음과 같습니다.

- 0x0001. 도우미 토큰 업로드 작업을 만들거나 다운로드 작업의 임시 파일 이름을 바꿀를 만들거나 업로드-회신 작업의 응답 파일 이름 바꾸기의 로컬 파일을 열에 사용 됩니다.
- 0x0002. 도우미 토큰에는 암시적 NTLM 또는 Kerberos에 대 한 HTTP 서버 또는 프록시 문제에 대 한 응답에서 자격 증명 또는 원격 서버 메시지 블록 (SMB) 업로드 파일을 열거나 다운로드 작업을 사용 됩니다. SetCredentialsJob TargetScheme NULL NULL 자격 증명 HTTP를 통해 보낼 수 있도록 호출 해야 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
