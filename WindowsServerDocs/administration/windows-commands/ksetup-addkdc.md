---
title: ksetup:addkdc
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3e0d38bdec11618561ee4acaa32ffdd06695fab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868534"
---
# <a name="ksetupaddkdc"></a>ksetup:addkdc



지정된 된 Kerberos 영역에 대 한 키 배포 센터 (KDC) 주소를 추가합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /addkdc <RealmName> [<KDCName>] 
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<RealmName>|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 지정 됩니다. CONTOSO.COM 하며 기본 영역으로 표시 되 면 **ksetup** 실행 됩니다. 기타 KDC를 추가 하려고 하는이 영역에는 것입니다.|
|\<KDCName>|KDC 이름이 mitkdc.microsoft.com 같은 대/소문자 구분 정규화 된 도메인 이름으로 명시 됩니다. KDC 이름이 생략 된 경우 DNS가 Kdc를 찾습니다.|

## <a name="remarks"></a>설명

이러한 매핑은 레지스트리의 아래에 저장 됩니다 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**합니다. Kerberos 영역 구성 데이터를 여러 컴퓨터에 배포 하려면 사용 하는 대신 보안 구성 템플릿 스냅인 및 정책 배포를 사용 **ksetup** 개별 컴퓨터에서 명시적으로 합니다.

새 영역 설정을 사용할 컴퓨터를 다시 시작 해야 합니다.

컴퓨터에 대 한 기본 영역 이름을 확인 하거나 의도 한 대로이 명령에서 제대로 작동 하는지 확인 하려면를 실행 **ksetup** 명령 프롬프트에서 추가 KDC에 대 한 출력을 확인 합니다.

## <a name="BKMK_Examples"></a>예제

비 Windows KDC 서버 및 워크스테이션을 사용 해야 하는 영역을 구성 합니다.
```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```
로컬 컴퓨터 계정 암호를 설정 하려면 이전 명령과 같이 동일한 컴퓨터의 명령줄에서 Ksetup 도구를 실행 "p@sswrd1%?. 컴퓨터를 다시 시작 합니다.
```
Ksetup /setcomputerpassword p@sswrd1%
```

#### <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
-   [명령줄 구문 키](command-line-syntax-key.md)