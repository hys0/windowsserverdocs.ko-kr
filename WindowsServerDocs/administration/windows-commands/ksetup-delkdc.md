---
title: ksetup delkdc
description: Kerberos 영역에 대 한 KDC (키 배포 센터) 이름의 인스턴스를 삭제 하는 ksetup delkdc 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d0477fd7317b0b9424fd6199cfde268c00dd1d6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926128"
---
# <a name="ksetup-delkdc"></a>ksetup delkdc

Kerberos 영역에 대 한 KDC (키 배포 센터) 이름의 인스턴스를 삭제 합니다.

매핑은 레지스트리에 저장 됩니다 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains` . 이 명령을 실행 한 후 KDC가 제거 되 고 더 이상 목록에 표시 되지 않도록 하는 것이 좋습니다.

> [!NOTE]
> 여러 컴퓨터에서 영역 구성 데이터를 제거 하려면 개별 컴퓨터에서 **ksetup** 명령을 명시적으로 사용 하는 대신 정책 배포와 함께 **보안 구성 템플릿** 스냅인을 사용 합니다.

## <a name="syntax"></a>구문

```
ksetup /delkdc <realmname> <KDCname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<realmname>` | CORP와 같은 대문자 DNS 이름을 지정 합니다. CONTOSO.COM. **Ksetup** 명령을 실행할 때 표시 되는 기본 영역이 며 KDC를 삭제 하려는 영역입니다. |
| `<KDCname>` | 대/소문자를 구분 하는 정규화 된 도메인 이름 (예: mitkdc.contoso.com)을 지정 합니다. |

### <a name="examples"></a>예

Windows 영역 및 비 Windows 영역 간의 모든 연결을 확인 하 고 제거할 항목을 확인 하려면 다음을 입력 합니다.

```
ksetup
```

연결을 제거 하려면 다음을 입력 합니다.

```
ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)

- [ksetup addkdc 명령](ksetup-addkdc.md)