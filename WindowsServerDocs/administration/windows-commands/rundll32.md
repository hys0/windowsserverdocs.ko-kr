---
title: rundll32
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46d9cd64-8186-4cd4-a500-44700340fe81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 391607f6e744fe88a60cb556067cf2699eee25f5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835436"
---
# <a name="rundll32"></a>rundll32



로드 하 고 32 비트 동적 연결 라이브러리 (Dll)를 실행 합니다. Rundll32에 대 한 구성 가능한 설정이 없습니다. 실행 하면 특정 DLL에 대 한 도움말 정보가 제공 됩니다는 **rundll32** 명령입니다.

실행 해야는 **rundll32** 상승된 된 명령 프롬프트에서 명령을 합니다. 관리자 권한 명령 프롬프트를 열려면 **시작**, 를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 를 클릭 하 고 **관리자 권한으로 실행**합니다.

## <a name="syntax"></a>구문

```
Rundll32 <DLLname>
```

## <a name="commands"></a>Commands

|매개 변수|설명|
|---------|-----------|
|[Rundll32.exe printui.dll, PrintUIEntry](rundll32-printui.md)|프린터 사용자 인터페이스를 표시합니다.|

## <a name="remarks"></a>주의

Rundll32.exe는 Rundll32.exe에 의해 호출 되도록 명시적으로 작성 된 DLL 에서만 함수를 호출할 수 있습니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
