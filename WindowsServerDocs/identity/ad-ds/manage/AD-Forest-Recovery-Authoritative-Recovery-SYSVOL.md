---
title: AD 포리스트 복구-SYSVOL의 신뢰할 수 있는 동기화
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adds
ms.openlocfilehash: 4c797c98fc8d41621954077ebf470f1f52604cf7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824306"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD 포리스트 복구-DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화 수행  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

SYSVOL의 정식 복원을 수행 하는 방법에는 여러 가지가 있습니다. **Msdfsr 옵션** 특성을 편집 하거나 wbadmin – authsysvol을 사용 하 여 시스템 상태 복원을 수행할 수 있습니다. 시스템 상태 백업을 복원 하는 옵션이 있는 경우 (즉, 동일한 하드웨어 및 운영 체제 인스턴스에 AD DS 복원 하는 경우) wbadmin – authsysvol을 사용 하는 것이 더 간단 합니다. 그러나 완전 복원을 수행 해야 하는 경우에는 **Msdfsr 옵션** 특성을 편집 해야 합니다.  

다음 단계를 사용 하 여 **Msdfsr 옵션** 특성을 편집 하 여 SYSVOL의 신뢰할 수 있는 동기화 (DFSR을 사용 하 여 복제 된 경우)를 수행 합니다. FRS를 사용 하 여 SYSVOL을 복제 하는 경우 [문서 290762](https://go.microsoft.com/fwlink/?LinkId=148443)을 참조 하세요.  

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행 하려면  

1. Active Directory 사용자 및 컴퓨터를 엽니다.  
2. **보기**를 클릭 하 고 **사용자, 연락처, 그룹 및 컴퓨터를 컨테이너** 및 **고급 기능**으로 선택 합니다. 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 

3. 트리 뷰에서 **도메인 컨트롤러**, 복원한 DC 이름, **DFSR-LocalSettings**, **도메인 시스템 볼륨**을 차례로 클릭 합니다. 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  

4. 세부 정보 창에서 **SYSVOL 구독**을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 **특성 편집기**를 클릭 합니다.  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 

5. **Msdfsr-옵션**을 클릭 하 고 **편집**을 클릭 한 다음 **1**을 입력 하 고 **확인** 을 클릭 합니다.  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 

6. **확인** 을 클릭 하 여 특성 편집기를 닫습니다.  
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
