---
title: tpmtool
description: Windows 명령 항목 tpmtool-에 대 한 신뢰할 수 있는 플랫폼 모듈에 대 한 정보를 가져옵니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: d2939b693c3f9bd8d0d8c8e1fefdd5d8f892e4c9
ms.sourcegitcommit: 3582c38d87f23cc54467d63bf00c29ef07cdb7c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2019
ms.locfileid: "65517196"
---
>[!IMPORTANT]
>일부 정보는 상업용으로 출시되기 전에 상당 부분 수정될 수 있는 시험판 제품과 관련이 있습니다. Microsoft는 여기에 제공된 정보에 대해 명시적 또는 묵시적 보증을 하지 않습니다.

# <a name="tpmtool"></a>tpmtool

이 유틸리티에 대 한 정보를 가져오는 데 사용할 수는 [모듈 TPM (Trusted Platform)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)합니다.

이 명령을 사용하는 방법의 예는 [예](#tpmtool_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|getdeviceinformation|TPM의 기본 정보를 표시합니다.|
|gatherlogs [출력 디렉터리 경로]|TPM 로그를 수집 하 고 지정된 된 디렉터리에 배치 합니다. 기본적으로 현재 디렉터리에 배치 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="tpmtool_examples"></a>예제

TPM의 기본 정보를 표시 하려면 다음을 입력 합니다.
```
tpmtool getdeviceinformation
```
TPM 로그를 수집 하 고 형식 현재 디렉터리에 배치 합니다.
```
tpmtool gatherlogs
```
TPM 로그를 수집 하 고 고 `C:\Users\Public`, 유형:
```
tpmtool gatherlogs C:\Users\Public
```
