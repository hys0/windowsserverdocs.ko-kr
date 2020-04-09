---
title: bitsadmin sethelpertokenflags
description: BITS 전송 작업과 연결 된 도우미 토큰의 사용 플래그를 설정 하는 bitsadmin sethelpertokenflags에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: c644e82026cfc1d62f3fb5d20e3925002b871036
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849496"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

BITS 전송 작업과 연결 된 [도우미 토큰](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) 의 사용 플래그를 설정 합니다.

**BITS 3.0 및 이전 버전**: 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID입니다.|
|Flags|가능한 값은 다음과 같습니다. 0x0001&mdash;는 도우미 토큰을 사용 하 여 업로드 작업의 로컬 파일을 열거나, 다운로드 작업의 임시 파일을 만들거나 이름을 바꾸거나, 업로드-회신 작업의 회신 파일을 만들거나 이름을 바꿉니다. 0x0002&mdash;도우미 토큰은 SMB (서버 메시지 블록) 업로드 또는 다운로드 작업의 원격 파일을 열거나 암시적 NTLM 또는 Kerberos 자격 증명에 대 한 프록시 챌린지 또는 HTTP 서버에 대 한 응답으로이를 사용 합니다. HTTP를 통해 자격 증명을 전송할 수 있도록 `/SetCredentialsJob TargetScheme NULL NULL` 를 호출 해야 합니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
