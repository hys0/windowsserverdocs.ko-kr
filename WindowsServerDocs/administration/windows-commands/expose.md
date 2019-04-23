---
title: 노출
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51cc744bc2b61862ed05ca2e7d0aaa8f70d38692
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886664"
---
# <a name="expose"></a>노출



드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|ShadowID|노출 하려는 섀도 복사본의 그림자 ID를 지정 합니다.|
|\<드라이브: >|드라이브 문자 (예를 들어 p:)으로 지정 된 섀도 복사본을 노출합니다.|
|\<Share>|지정 된 섀도 복사본 공유를 노출 합니다. (예를 들어 \\ \\ *MachineName*\)합니다.|
|\<MountPoint>|지정된 된 섀도 복사본이 탑재 지점 표시 (예를 들어 C:\shadowcopy\)합니다.|

## <a name="remarks"></a>설명

-   기존 별칭 또는 환경 변수 대신 사용할 수 있습니다 *ShadowID*합니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오.

## <a name="BKMK_examples"></a>예제

를 X 드라이브로 VSS_SHADOW_1 환경 변수와 연결 된 영구 섀도 복사본을 노출 하려면 다음을 입력 합니다.
```
expose %vss_shadow_1% x:
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)