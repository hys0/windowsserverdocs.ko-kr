---
title: 'ksetup: delkdc'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b918f8c2fa0ec09c2aae77517a0ee2c9e77ce2dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375142"
---
# <a name="ksetupdelkdc"></a>ksetup: delkdc



Kerberos 영역에 대 한 KDC (키 배포 센터) 이름의 인스턴스를 삭제 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /delkdc <RealmName> <KDCName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|@no__t 0RealmName >|영역 이름은 CORP와 같은 대문자 DNS 이름으로 명시 됩니다. CONTOSO.COM는 **ksetup** 가 실행 될 때 기본 영역으로 나열 됩니다. 이 영역에서 다른 KDC를 삭제 하려고 합니다.|
|@no__t 0KDCName >|KDC 이름은 대/소문자를 구분 하지 않고 정규화 된 도메인 이름 (예: mitkdc.contoso.com)으로 명시 됩니다.|

## <a name="remarks"></a>설명

이러한 매핑은 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains**의 레지스트리에 저장 됩니다. 여러 컴퓨터에서 영역 구성 데이터를 제거 하려면 개별 컴퓨터에서 명시적으로 **ksetup** 를 사용 하는 대신 보안 구성 템플릿 스냅인 및 정책 배포를 사용 합니다.

Windows 2000 Server SP1 (서비스 팩 1) 및 이전 버전을 실행 하는 컴퓨터에서 컴퓨터를 다시 시작 해야 변경 된 영역 설정 구성이 사용 됩니다.

컴퓨터의 기본 영역 이름을 확인 하거나이 명령이 의도 한 대로 작동 하는지 확인 하려면 명령 프롬프트에서 **ksetup** 를 실행 하 고 제거 된 KDC가 목록에 없는지 확인 합니다.

## <a name="BKMK_Examples"></a>예와

이 컴퓨터에 대 한 보안 요구 사항이 변경 되어 Windows 영역 및 비 Windows 영역 간의 링크를 제거 해야 합니다. 먼저 기존 연결의 출력을 제거 하 고 생성 하는 연결을 결정 합니다.
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