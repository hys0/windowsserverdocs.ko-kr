---
title: ksetup addkdc
description: 지정 된 Kerberos 영역에 대 한 KDC (키 배포 센터) 주소를 광고 하는 ksetup addkdc 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e51279166bf60196d12f877506d3228b78c4a711
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818093"
---
# <a name="ksetup-addkdc"></a>ksetup addkdc

지정 된 Kerberos 영역에 대 한 키 배포 센터 (KDC) 주소를 추가 합니다.

매핑은 레지스트리에 저장 되며, **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains** 에서 컴퓨터를 다시 시작 해야 새 영역 설정이 사용 됩니다.

> [!NOTE]
> Kerberos 영역 구성 데이터를 여러 컴퓨터에 배포 하려면 개별 컴퓨터에서 명시적으로 **보안 구성 템플릿** 스냅인 및 정책 배포를 사용 해야 합니다. 이 명령은 사용할 수 없습니다.

## <a name="syntax"></a>구문

```
ksetup /addkdc <realmname> [<KDCname>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<realmname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM. 이 값은 **ksetup** 가 실행 되는 경우에도 기본 영역으로 나타나고 다른 KDC를 추가 하려는 영역입니다. |
| `<KDCname>` | 대/소문자를 구분 하지 않고 정규화 된 도메인 이름 (예: mitkdc.contoso.com)을 지정 합니다. KDC 이름이 생략 되 면 DNS는 Kdc를 찾습니다. |

### <a name="examples"></a>예

비 Windows KDC 서버와 워크스테이션에서 사용 해야 하는 영역을 구성 하려면 다음을 입력 합니다.

```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

이전 예제와 동일한 컴퓨터에서 로컬 컴퓨터 계정 암호 를%로 설정 하 p@sswrd1 고 컴퓨터를 다시 시작 하려면 다음을 입력 합니다.

```
ksetup /setcomputerpassword p@sswrd1%
```

컴퓨터의 기본 영역 이름을 확인 하거나이 명령이 의도 한 대로 작동 하는지 확인 하려면 다음을 입력 합니다.

```
ksetup
```
레지스트리를 확인 하 여 매핑이 의도 한 대로 발생 했는지 확인 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup setcomputerpassword 명령](ksetup-setcomputerpassword.md)
