---
title: ksetup:delkdc
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e2fa065ca60338b04cc8718e199805cc494c908
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814564"
---
# <a name="ksetupdelkdc"></a>ksetup:delkdc



Kerberos 영역에 대 한 키 배포 센터 (KDC) 이름의 인스턴스를 삭제합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /delkdc <RealmName> <KDCName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<RealmName>|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 지정 됩니다. CONTOSO.COM 하며 기본 영역으로 표시 되 면 **ksetup** 실행 됩니다. 다른 KDC를 삭제 하려고 하는이 영역에는 것입니다.|
|\<KDCName>|KDC 이름이 mitkdc.contoso.com 같은 대/소문자 정규화 된 도메인 이름으로 명시 됩니다.|

## <a name="remarks"></a>설명

이러한 매핑은의 레지스트리에 저장 됩니다 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**합니다. 여러 컴퓨터에서 구성 데이터 영역을 제거 하려면 대신 보안 구성 템플릿 스냅인 및 정책 배포를 사용 **ksetup** 개별 컴퓨터에서 명시적으로 합니다.

서비스 팩 1 (SP1) 및 이전 버전의 Windows 2000 Server를 실행 하는 컴퓨터에서 컴퓨터를 다시 시작 해야 변경 된 영역 설정 구성이 사용 됩니다.

컴퓨터에 대 한 기본 영역 이름을 확인 하거나 의도 한 대로이 명령에서 제대로 작동 하는지 확인 하려면를 실행 **ksetup** 명령 프롬프트에서 제거 된 KDC 목록에 없는 경우를 확인 합니다.

## <a name="BKMK_Examples"></a>예제

이 컴퓨터에 대 한 보안 요구 사항을 변경 Windows 영역 및 비 Windows 영역 간의 링크를 제거 해야 합니다. 먼저, 제거 하 고 기존 연결의 출력을 생성 하는 연결을 확인 합니다.
```
ksetup
```
다음 명령을 사용 하 여 연결을 제거 합니다.
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

#### <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)