---
title: bitsadmin setaclflag
description: ACL (액세스 제어 목록) 전파 플래그를 설정 하는 **bitsadmin setaclflag**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0aae550e94d04db518edccafb1d6bcf46d0320b
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123061"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

작업에 대 한 ACL (액세스 제어 목록) 전파 플래그를 설정 합니다. 플래그는 다운로드 하는 파일을 사용 하 여 소유자 및 ACL 정보를 유지 관리 하려는 경우를 의미 합니다. 예를 들어 파일을 사용 하 여 소유자와 그룹을 유지 하려면 **flags** 매개 변수를 `og`설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setaclflag <job> <flags>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| flags | 다음을 포함 하 여 하나 이상의 값을 지정 합니다.<ul><li>**o** -파일을 사용 하 여 소유자 정보를 복사 합니다.</li><li>**g** -파일을 사용 하 여 그룹 정보를 복사 합니다.</li><li>**d** -파일을 사용 하 여 DACL (임의 액세스 제어 목록) 정보를 복사 합니다.</li><li>**s** -파일이 포함 된 SACL (시스템 액세스 제어 목록) 정보를 복사 합니다.</li></ul> |

## <a name="remarks"></a>주의

/Setaclflag 스위치는 작업이 Windows (SMB) 공유에서 데이터를 다운로드 하는 경우 소유자 및 액세스 제어 목록 정보를 유지 관리 하는 데 사용 됩니다.

## <a name="examples"></a>예

다음 예제에서는 액세스 제어 목록 전파 플래그 이라는 작업에 대 한 *myDownloadJob* 다운로드 한 파일 소유자 및 그룹 정보를 유지 관리 합니다.

```
C:\>bitsadmin /setaclflags myDownloadJob og
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)&reg;'    