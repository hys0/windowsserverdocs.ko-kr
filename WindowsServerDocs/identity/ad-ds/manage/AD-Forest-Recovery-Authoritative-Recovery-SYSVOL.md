---
title: AD 포리스트 복구-SYSVOL의 신뢰할 수 있는 동기화
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adds
ms.openlocfilehash: 246a2ea589ee05110362cff99d50e93a0a18c2b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827004"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD 포리스트 복구-DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행 합니다.  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

SYSVOL의 정식 복원을 수행 하는 방법은 여러 가지입니다. 편집 하거나 수를 **msDFSR 옵션** 특성 또는 wbadmin – authsysvol를 사용 하 여 시스템 상태 복원을 수행 합니다. 시스템 상태 백업을 복원 하는 옵션 경우 (즉, 복원 하는 AD DS는 동일한 하드웨어 및 운영 체제 인스턴스로) wbadmin – authsysvol를 사용 하 여 하는 것은 간단 합니다. 완전 복구를 수행 해야 할 경우 편집 해야 하지만 합니다 **msDFSR 옵션** 특성입니다.  

편집 하 여 (DFSR을 사용 하 여이 복제) 하는 경우 SYSVOL의 신뢰할 수 있는 동기화를 수행 하려면 다음 단계를 사용 합니다 **msDFSR 옵션** 특성입니다. FRS를 사용 하 여 SYSVOL을 복제 하는 경우 참조 [290762 문서](https://go.microsoft.com/fwlink/?LinkId=148443)합니다.  

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행 하려면  

1. Active Directory 사용자 및 컴퓨터를 엽니다.  
2. 클릭 **뷰**를 선택한 후 **사용자, 연락처, 그룹 및 컴퓨터를 컨테이너로** 하 고 **고급 기능**합니다. 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 

3. 트리 보기에서 클릭 **도메인 컨트롤러**를 복원한 DC의 이름을 **DFSR LocalSettings**를 차례로 **도메인 시스템 볼륨**. 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  

4. 세부 정보 창에서 마우스 오른쪽 단추로 클릭 **SYSVOL 구독**, 클릭 **속성**를 클릭 하 고 **특성 편집기**합니다.  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 

5. 클릭 **msDFSR 옵션**, 클릭 **편집**, 유형 **1**를 클릭 하 고 **확인**  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 

6. 클릭 **확인** 특성 편집기를 닫습니다.  
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
