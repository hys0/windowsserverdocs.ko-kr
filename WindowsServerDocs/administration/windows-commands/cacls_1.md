---
title: cacls
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04b60bd852abdb55059efb96aec4c290361d6a74
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379950"
---
# <a name="cacls"></a>cacls

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 하거나 지정 된 파일에 대해 임의 액세스 제어 목록 (DACL)을 수정 합니다.  
## <a name="syntax"></a>구문  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
### <a name="parameters"></a>매개 변수  

|        매개 변수        |                                                                                            설명                                                                                             |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      \<filename\>       |                                                                            필수. 지정 된 파일의 Acl을 표시 합니다.                                                                             |
|           /t            |                                                          현재 디렉터리와 모든 하위 디렉터리에서 지정 된 파일의 Acl을 변경 합니다.                                                          |
|           /m            |                                                                          디렉터리에 탑재 된 볼륨의 Acl을 변경 합니다.                                                                           |
|           /l            |                                                                        대상 및 기호화 된 링크 자체에서 작동 합니다.                                                                         |
|         /s:sddl         |                                       Acl을 SDDL 문자열에 지정 된 대로 바꿉니다 ( **/e**, **/g**, **/r**, **/p**또는 **/d**와는 유효 하지 않음).                                        |
|           /e            |                                                                                 ACL을 바꾸지 않고 편집 합니다.                                                                                  |
|           /c            |                                                                                 액세스 거부 오류에서 계속 합니다.                                                                                  |
|    /g 사용자: \<perm @ no__t-1     |   사용자 액세스 권한을 지정 하는 권한 부여.<br /><br />권한에 대 한 유효한 값:<br /><br />-n-없음<br />-r-읽기<br />-w-쓰기<br />-c-변경 (쓰기)<br />-f-모든 권한   |
|      /r 사용자 [...]      |                                                                  지정 된 사용자의 액세스 권한을 취소할 (만 함께 사용할 **/e**).                                                                   |
| [/p 사용자: \<perm @ no__t-1 [...] | 지정 된 사용자의 액세스 권한을 바꿉니다.<br /><br />권한에 대 한 유효한 값:<br /><br />-n-없음<br />-r-읽기<br />-w-쓰기<br />-c-변경 (쓰기)<br />-f-모든 권한 |
|     [/p 사용자 [...]      |                                                                                    지정 된 사용자 액세스를 거부 합니다.                                                                                     |
|           /?            |                                                                                명령 프롬프트에 도움말을 표시합니다.                                                                                |

## <a name="remarks"></a>설명  
- 이 명령은 더 이상 사용 되지 않습니다. [Icacls](icacls.md) 를 대신 사용 하세요.  
- 다음 표를 사용 하 여 결과 해석 하 합니다.  


  |      출력       |                액세스 제어 항목 (ACE)에 적용 됩니다.                |
  |-------------------|---------------------------------------------------------------------|
  |        OI         |               개체 상속 합니다. 이 폴더 및 파일입니다.                |
  |        CI         |           컨테이너 상속 합니다. 이 폴더 및 하위 폴더입니다.            |
  |        IO         | 만 상속 합니다. ACE는 현재 파일/디렉터리에는 적용 되지 않습니다. |
  | 출력 메시지 없음 |                          이 폴더에만 합니다.                          |
  |     (OI) (CI)      |                 이 폴더, 하위 폴더 및 파일입니다.                 |
  |   (OI) (CI) IO)    |                     하위 폴더 및 파일만 합니다.                      |
  |     (CI) IO)      |                          하위 폴더만 합니다.                           |
  |     (OI) IO)      |                             파일에만 해당 합니다.                             |


- 와일드 카드를 사용할 수 있습니다 ( **?** 및 **\\ @ no__t-2**)를 지정 하 여 여러 파일을 지정 합니다.  
- 둘 이상의 사용자를 지정할 수 있습니다.  

#### <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
