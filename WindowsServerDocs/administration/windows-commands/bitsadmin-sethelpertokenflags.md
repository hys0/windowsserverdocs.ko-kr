---
title: bitsadmin sethelpertokenflags
description: '**Bitsadmin sethelpertokenflags** 에 대 한 Windows 명령 항목-BITS 전송 작업과 연결 된 도우미 토큰의 사용 플래그를 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 6047c63677fac3311634ababb675be5301b7f3b5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380578"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

BITS 전송 작업과 연결 된 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) 의 사용 플래그를 설정 합니다.

**BITS 3.0 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID입니다.|
|Flags|가능한 값은 다음과 같습니다. 0x0001 @ no__t-0이 도우미 토큰은 업로드 작업의 로컬 파일을 열고, 다운로드 작업의 임시 파일을 만들거나 이름을 바꾸거나, 업로드-회신 작업의 회신 파일을 만들거나 이름을 바꾸는 데 사용 됩니다. 0x0002 @ no__t-0 도우미 토큰은 SMB (서버 메시지 블록) 업로드 또는 다운로드 작업의 원격 파일을 열거나 암시적 NTLM 또는 Kerberos 자격 증명에 대 한 HTTP 서버 또는 프록시 챌린지에 대 한 응답으로 사용 됩니다. HTTP를 통해 자격 증명을 전송할 수 있도록 하려면 @ no__t-0 @ no__t-1을 호출 해야 합니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
