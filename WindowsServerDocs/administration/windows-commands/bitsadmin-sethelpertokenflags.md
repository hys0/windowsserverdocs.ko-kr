---
title: bitsadmin sethelpertokenflags
description: BITS 전송 작업과 연결 된 도우미 토큰의 사용 플래그를 설정 하는 **bitsadmin sethelpertokenflags**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 77fac03dba2bb0686a98206405622e2eb398953e
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122971"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

BITS 전송 작업과 연결 된 [도우미 토큰](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs) 의 사용 플래그를 설정 합니다.

> [!NOTE]
> 이 명령은 BITS 3.0 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| flags | 가능한 도우미 토큰 값 (다음 포함)<ul><li>**0x0001.** 업로드 작업의 로컬 파일을 열고, 다운로드 작업의 임시 파일을 만들거나 이름을 바꾸거나, 업로드-회신 작업의 회신 파일을 만들거나 이름을 바꾸는 데 사용 됩니다.</li><li>**0x0002.** 서버 메시지 블록 (SMB) 업로드 또는 다운로드 작업의 원격 파일을 열거나 암시적 NTLM 또는 Kerberos 자격 증명에 대 한 프록시 챌린지 또는 HTTP 서버에 대 한 응답으로이 파일을 여는 데 사용 됩니다.</li></ul>HTTP를 통해 자격 증명을 전송 하려면 `/setcredentialsjob targetscheme null null` 를 호출 해야 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
