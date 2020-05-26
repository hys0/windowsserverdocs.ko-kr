---
title: ksetup getenctypeattr
description: 도메인에 대 한 암호화 유형 특성을 검색 하는 ksetup getenctypeattr 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2acead4ff1179002303c18d4feff262080203a28
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817703"
---
# <a name="ksetup-getenctypeattr"></a>ksetup getenctypeattr

도메인에 대 한 암호화 유형 특성을 검색 합니다. 성공 또는 실패 완료 시 상태 메시지가 표시 됩니다.

**Klist** 명령을 실행 하 고 출력을 확인 하 여 Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 볼 수 있습니다. 명령을 실행 하 여 도메인을 연결 하 고 사용 하도록 설정할 수 있습니다 `ksetup /domain <domainname>` .

## <a name="syntax"></a>구문

```
ksetup /getenctypeattr <domainname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<domainname>` | 연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다. |

### <a name="examples"></a>예

도메인에 대 한 암호화 유형 특성을 확인 하려면 다음을 입력 합니다.

```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [klist 명령](klist.md)

- [ksetup 명령](ksetup.md)

- [ksetup 도메인 명령](ksetup-domain.md)

- [ksetup addenctypeattr 명령](ksetup-addenctypeattr.md)

- [ksetup setenctypeattr 명령](ksetup-setenctypeattr.md)

- [ksetup delenctypeattr 명령](ksetup-delenctypeattr.md)
