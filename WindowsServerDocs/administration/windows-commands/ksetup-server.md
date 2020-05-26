---
title: ksetup 서버
description: Ksetup 서버 명령에 대 한 참조 항목으로, Windows 운영 체제를 실행 하는 컴퓨터의 이름을 지정할 수 있으므로 ksetup 명령의 변경 내용은 대상 컴퓨터를 업데이트 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e39a3fbef4b99848d2a90c81007c526597c77275
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817523"
---
# <a name="ksetup-server"></a>ksetup 서버

Windows 운영 체제를 실행 하는 컴퓨터의 이름을 지정할 수 있으므로 **ksetup** 명령에 의해 변경 된 내용은 대상 컴퓨터를 업데이트 합니다.

대상 서버 이름은의 레지스트리에 저장 됩니다 `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos` . **Ksetup** 명령을 실행 하면이 항목이 보고 되지 않습니다.

> [!IMPORTANT]
> 대상 서버 이름을 제거할 수 있는 방법은 없습니다. 대신 로컬 컴퓨터 이름 (기본값)으로 다시 변경할 수 있습니다.

## <a name="syntax"></a>구문

```
ksetup /server <servername>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<servername>` | 구성이 적용 되는 전체 컴퓨터 이름 (예: *IPops897.corp.contoso.com*)을 지정 합니다.<p>불완전 하 게 정규화 된 도메인 컴퓨터 이름이 지정 된 경우 명령이 실패 합니다. |

### <a name="examples"></a>예

Contoso 도메인에 연결 된 *IPops897* 컴퓨터에서 **ksetup** 구성을 적용 하려면 다음을 입력 합니다.

```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)
