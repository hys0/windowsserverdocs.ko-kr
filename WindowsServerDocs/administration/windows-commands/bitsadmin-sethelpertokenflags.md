---
title: bitsadmin sethelpertokenflags
description: Windows 명령 항목에 대 한 **bitsadmin sethelpertokenflags** -BITS 전송 작업을 연관 된 도우미 토큰에 대 한 사용 플래그를 설정 합니다.
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
ms.openlocfilehash: cc9652afe73476041aa42e64671885bfc1af9628
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813864"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

에 대 한 사용 플래그를 설정 합니다는 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) BITS 전송 작업을 사용 하 여 연결 합니다.

**3.0 및 이전 비트**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID입니다.|
|Flags|가능한 값은 다음과 같습니다. 0x0001&mdash;는 도우미 토큰을 사용 하 업로드 작업의 로컬 파일을 엽니다 만들거나 다운로드 작업의 임시 파일 이름 바꾸기로 또는 만들거나 업로드-회신 작업의 응답 파일의 이름을 바꿉니다. 0x0002&mdash;도우미 토큰 원격 서버 메시지 블록 (SMB) 업로드 파일을 열거나 작업을 다운로드 하는 데 사용 됩니다 또는 암시적 NTLM 또는 Kerberos에 대 한 HTTP 서버 또는 프록시 문제에 대 한 응답에서 자격 증명입니다. 호출 해야 합니다 `/SetCredentialsJob TargetScheme NULL NULL` HTTP를 통해 보낼 수 있는 자격 증명을 허용 하도록 합니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
