---
title: AD 포리스트 복구-krbtgt 암호 재설정
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adds
ms.openlocfilehash: 1ac0dcb9da1d10a417c128cb8498a5d8362d9a9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883744"
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>AD 포리스트 복구-krbtgt 암호 재설정

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

도메인에 대 한 krbtgt 암호를 재설정 하려면 다음 절차를 따르십시오. 다음 절차에는 읽기 전용 도메인 컨트롤러 (Rodc) 하지만 쓰기 가능한 Dc에 적용 됩니다.
  
> [!IMPORTANT]
> 포리스트 복구 하는 동안 온라인 Rodc를 복구 하려는 경우는 Rodc에 대 한 krbtgt 계정을 삭제 하지 마세요. RODC의 krbtgt 계정 형식 krbtgt_에 나열 됩니다*번호*합니다.
>
> Dc (예: passfilt.dll) 사용자 지정된 암호 필터를 사용 하는 경우 krbtgt 암호를 재설정 하려고 할 때 오류가 발생할 수 있습니다. 자세한 내용은 Microsoft 기술 자료를 참조 문제를 해결 하려면 포함 [2549833 문서](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833)합니다.
  
## <a name="to-reset-the-krbtgt-password"></a>Krbtgt 암호를 재설정 하려면  
  
1. 클릭 **시작**, 가리킨 **제어판**를 가리킵니다 **관리 도구**를 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다.
2. **보기**를 클릭한 다음 **고급 기능**을 클릭합니다.
3. 콘솔 트리에서 도메인 컨테이너를 두 번 클릭 한 다음 클릭 **사용자**합니다.
4. 세부 정보 창에서 마우스 오른쪽 단추로 클릭 합니다 **krbtgt** 사용자 계정 및 클릭 **암호 재설정**합니다.
   ![암호 재설정](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5. **암호만**새 암호를 입력 하 고에서 암호를 다시 입력 **암호 확인**를 클릭 하 고 **확인**. 시스템이 자동으로 지정 하는 암호의 독립적인 강력한 암호를 생성 하기 때문에 암호를 지정 하는 중요 하지 않습니다.
  
> [!NOTE]
> 이 작업을 두 번 수행 해야 합니다. Krbtgt 계정 암호 기록은 두 가지 두 개의 가장 최근 암호가 포함 되어 있습니다. 기록에서 이전 암호 효과적으로 삭제 하는 두 번의 암호를 재설정 하 여 방법이 있으면 되므로 다른 DC를 복제이 DC를 사용 하 여 이전 암호를 사용 하 여.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md) 
