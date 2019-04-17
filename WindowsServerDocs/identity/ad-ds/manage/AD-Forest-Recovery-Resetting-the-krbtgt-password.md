---
title: "광고 숲 복구-krbtgt 암호 다시 설정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.technology: identity-adfs
ms.openlocfilehash: 445fa18503e26d04e20a61cfe652424f78631abe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>광고 숲 복구-krbtgt 암호 다시 설정 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 다음 절차 도메인에 대 한 krbtgt 암호 다시 설정 합니다. 다음 절차 읽기 전용 Rodc (도메인 컨트롤러) 있지만 쓰기 Dc 적용 됩니다.  
  
> [!IMPORTANT]
>  숲 복구 하는 동안 온라인 Rodc 복구 하려는 경우는 Rodc에 대 한 krbtgt 계정 삭제 하지 않습니다. 가 rodc krbtgt 계정이 형식 krbtgt_에 나열*번호*합니다.  
>   
>  Dc (예: passfilt.dll) 사용자 지정 된 암호 필터를 사용 하는 경우 krbtgt 암호 재설정을 시도 하면 오류가 발생할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 참조 한 해결 방법을 포함 하 여 [2549833 문서](https://support.microsoft.com/kb/2549833) (https://support.microsoft.com/kb/2549833).  
  
## <a name="to-reset-the-krbtgt-password"></a>Krbtgt 암호 다시 설정  
  
1.  클릭 **시작**, 가리킨 **제어판**, 가리킨 **관리 도구**을 차례로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다.  
2.  2.  클릭 **보기**을 차례로 클릭 하 고 **고급 기능**합니다.  
3.  콘솔 트리에서 도메인 컨트롤러를 두 번 클릭 한 다음 클릭 **사용자**합니다.  
4.  세부 정보 창에서 마우스 오른쪽 단추로 클릭는 **krbtgt** 사용자 계정 및 클릭 **암호 재설정**합니다.  
![암호 다시 설정](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)
5.  **새 암호**, 새 암호를 입력에서 암호를 다시 입력 **암호 확인**을 차례로 클릭 하 고 **확인**합니다. 시스템 강력한 암호를 자동으로 독립적으로 지정 하는 암호를 생성 하기 때문 사용자 지정 하는 암호가 중요 한 하지 않습니다.  
  
    > [!NOTE]
    >  두 번이 작업을 수행 해야 합니다. Krbtgt 계정의 암호 기억은 두 가지 두 개의 최신 암호 포함 됩니다. 기록에서 기존 암호 효과적으로 삭제 하는 두 번 암호를 재설정 하 여 방법은 없습니다 되므로 다른 DC 됩니다 복제할이 DC 이전 암호를 사용 하 여.  
 
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md) 
  
