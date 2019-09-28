---
title: bitsadmin setcredentials
description: '**Bitsadmin setcredentials** 에 대 한 Windows 명령 항목-작업에 자격 증명을 추가 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70ac9a01a2e713b5a2fb881f327a52552a6bbec6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380716"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

작업에 자격 증명을 추가 합니다.

**BITS 1.2 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetCredentials <Job> <Target> <Scheme> <Username> <Password>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|대상|서버 또는 프록시|
|Scheme|다음 중 하나일 수 있습니다.</br>-BASIC-사용자 이름과 암호가 일반 텍스트로 서버나 프록시로 전송 되는 인증 체계입니다.</br>-다이제스트-챌린지에 대해 서버 지정 데이터 문자열을 사용 하는 챌린지-응답 인증 체계입니다.</br>-NTLM-Windows 네트워크 환경에서 인증을 위해 사용자의 자격 증명을 사용 하는 챌린지-응답 인증 체계입니다.</br>-NEGOTIATE (단순 및 보호 된 협상 프로토콜 (Snego)이 라고도 함)는 인증에 사용할 체계를 결정 하기 위해 서버 또는 프록시와 협상 하는 챌린지-응답 인증 체계입니다. 이러한 예로는 Kerberos 프로토콜 및 NTLM이 있습니다.</br>-PASSPORT-Microsoft에서 제공 하는 중앙 집중식 인증 서비스로, 구성원 사이트에 대 한 단일 로그온을 제공 합니다.|
|Username|제공 된 자격 증명의 이름입니다.|
|암호|제공 된 *사용자 이름과* 연결 된 암호입니다.|

## <a name="BKMK_examples"></a>예와

다음 예에서는 이름이 *Mydownloadjob*인 작업에 자격 증명을 추가 합니다.
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC Edward Password20
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)