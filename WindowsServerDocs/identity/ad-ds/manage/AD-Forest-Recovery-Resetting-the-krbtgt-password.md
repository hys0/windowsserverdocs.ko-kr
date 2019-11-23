---
title: AD 포리스트 복구-krbtgt 암호 다시 설정
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adds
ms.openlocfilehash: 14dd09c6177d473547a67e1d79e9714f0a7a29b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390297"
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>AD 포리스트 복구-krbtgt 암호 다시 설정

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

도메인에 대 한 krbtgt 암호를 다시 설정 하려면 다음 절차를 따르십시오. 다음 절차에서는 Rodc (읽기 전용 도메인 컨트롤러)가 아닌 쓰기 가능한 Dc를 적용 합니다.
  
> [!IMPORTANT]
> 포리스트를 복구 하는 동안 Rodc online을 복구 하려는 경우에는 Rodc에 대 한 krbtgt 계정을 삭제 하지 마십시오. RODC에 대 한 krbtgt 계정이 krbtgt_*번호*형식으로 나열 됩니다.
>
> DC에서 사용자 지정 된 암호 필터 (예: passfilt)를 사용 하는 경우 krbtgt 암호를 다시 설정 하려고 하면 오류가 발생할 수 있습니다. 해결 방법에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 2549833](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833)를 참조 하십시오.
  
## <a name="to-reset-the-krbtgt-password"></a>Krbtgt 암호를 다시 설정 하려면  
  
1. **시작**을 클릭 하 고 **제어판**, **관리 도구**를 차례로 가리킨 다음 **사용자 및 컴퓨터 Active Directory**를 클릭 합니다.
2. **보기**를 클릭한 다음 **고급 기능**을 클릭합니다.
3. 콘솔 트리에서 도메인 컨테이너를 두 번 클릭 한 다음 **사용자**를 클릭 합니다.
4. 세부 정보 창에서 **krbtgt** 사용자 계정을 마우스 오른쪽 단추로 클릭 하 고 **암호 다시 설정**을 클릭 합니다.
   암호를 다시 설정 ![](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5. **새 암호**에서 새 암호를 입력 하 고 암호 **확인**에 암호를 다시 입력 한 다음 **확인**을 클릭 합니다. 지정 하는 암호는 시스템에서 사용자가 지정한 암호와 독립적인 강력한 암호를 자동으로 생성 하기 때문에 중요 하지 않습니다.
  
> [!NOTE]
> 이 작업을 두 번 수행 해야 합니다. Krbtgt 계정에 대 한 암호 기록은 2입니다. 즉, 두 개의 최신 암호를 포함 합니다. 암호를 두 번 다시 설정 하면 기록에서 이전 암호가 효과적으로 제거 되므로 다른 DC가 이전 암호를 사용 하 여이 DC로 복제할 방법이 없습니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md) 
