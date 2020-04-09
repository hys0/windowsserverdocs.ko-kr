---
title: auditpol
description: Windows 명령 항목-에 대 한 **정보를 표시**하 고 감사 정책을 조작 하는 함수를 수행 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00365b0e46b8bff761cf991dbdbd09d8f5e9c687
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851136"
---
# <a name="auditpol"></a>auditpol

에 대 한 정보를 표시 하 고 감사 정책을 조작 하는 함수를 수행 합니다.

이 명령을 사용할 수 있는 방법을 예제를 보려면 각 항목의 예 섹션을 참조 하십시오.

## <a name="syntax"></a>구문

```
auditpol command [<sub-command><options>]
```

#### <a name="parameters"></a>매개 변수

| 하위 명령 | 설명 |
| ----------- | ----------- |
| /get | 현재 감사 정책을 표시합니다. 자세한 내용은 [auditpol get](auditpol-get.md) 구문 및 옵션을 참조 하세요. |
| 설정 / | 감사 정책을 설정합니다. 자세한 내용은 구문 및 옵션에 대 한 [auditpol 집합](auditpol-set.md) 을 참조 하세요. |
| /list | 선택할 수 있는 정책 요소를 표시합니다. 자세한 내용은 구문 및 옵션에 대 한 [auditpol list](auditpol-list.md) 를 참조 하세요. |
| 백업 / | 감사 정책 파일에 저장 합니다. 자세한 내용은 구문 및 옵션에 대 한 [auditpol backup](auditpol-backup.md) 을 참조 하세요. |
| /restore | 감사 정책을 auditpol /backup을 사용 하 여 이전에 만든 파일에서 복원 합니다. 자세한 내용은 구문 및 옵션에 대 한 [auditpol 복원](auditpol-restore.md) 을 참조 하세요. |
| / 지우기 | 감사 정책을 지웁니다. 자세한 내용은 참조는 [auditpol clear](auditpol-clear.md) 구문 및 옵션 합니다. |
| /remove | 사용자 단위 감사 정책 설정을 모두 제거 하 고 모든 시스템 감사 정책 설정을 사용 하지 않도록 설정 합니다. 자세한 내용은 참조는 [auditpol remove](auditpol-remove.md) 구문 및 옵션 합니다. |
| /resourceSACL | 전역 리소스 시스템 액세스 제어 목록 (Sacl)를 구성합니다. **참고:** Windows 7 및 Windows Server 2008 r 2에만 적용 됩니다. 자세한 내용은 [Auditpol Sourceacl](auditpol-resourcesacl.md)을 참조 하세요. |
| /?| 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>주의

감사 정책 명령줄 도구를 사용할 수 있습니다.

- 설정 및 시스템 감사 정책을 쿼리 합니다.

- 설정 하 고는 사용자 단위 감사 정책을 쿼리 합니다.

- 설정 하 고 감사 옵션을 쿼리 합니다.

- 설정 하 고 감사 정책에 대 한 액세스를 위임 하는 데 사용 되는 보안 설명자를 쿼리 합니다.

- 보고서 또는 쉼표로 구분 된 값 (CSV) 텍스트 파일에 감사 정책을를 백업 합니다.

- CSV 텍스트 파일에서 감사 정책을 로드 합니다.

- 전역 리소스 Sacl을 구성 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)