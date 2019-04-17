---
title: "광고 숲 복구-제거 dc 메타 데이터를 청소"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adfs
ms.openlocfilehash: 3027c59b58801b44d20127e6bcf62dd7319708bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>광고 숲 복구-제거한 쓸 수 있는 도메인 컨트롤러의 메타 데이터를 청소 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
 메타 데이터 정리 DC 복제 시스템을 식별 하는 Active Directory 데이터를 제거 합니다.  
  
 다음 절차를 사용 하 여 AD DS 다시 설치 하 여 네트워크에 다시 추가 하려는 dc DC 개체를 삭제 합니다.  
  
 Active Directory 사이트 및 서비스를 포함 원격 서버 관리 도구 RSAT () Active Directory 사용자 및 컴퓨터 버전을 사용 하는 경우 메타 데이터 정리 DC 개체를 삭제 하면 자동으로 수행 됩니다.  
  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>도메인 컨트롤러 Active Directory 사용자 및 컴퓨터 사용 하 여 삭제  
 버전의 Active Directory 사용자 및 컴퓨터 또는 Active Directory 관리 센터에서 서버 관리 RSAT (원격 도구)를 사용 하면 메타 데이터 정리 DC 개체를 삭제 하면 자동으로 수행 됩니다. 서버 개체와 컴퓨터는도 자동으로 삭제 됩니다.  
  
 다른 방법으로 사용할 수 있습니다도 Active Directory 사이트 및 서비스에서 RSAT DC 개체를 삭제 하려면. Active Directory 사이트 및 서비스를 사용 하면 DC 개체의 삭제 하기 전에 관련된 서버 개체와 NTDS 설정 삭제 해야 합니다.  
  
 RSAT 다운로드 합니다.  

-   [Windows 10 대 한 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520)
  
-   [Windows 8 대 한 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=28972)  

-   [Windows 7 서비스 팩 1 (SP1)에 대 한 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=7887)  
  
-   [Windows Vista에 대 한 Microsoft 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=21090)  
  
 다음 절차는 실행 중 Windows Server 2016 년 2012, 2008 R2, 이나 dc 동일 합니다. 대상 DC 메타 데이터 정리 작업의 모든 버전의 Windows Server를 실행할 수 있습니다.  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>RSAT의 Active Directory 사용자 및 컴퓨터 사용 하는 도메인 컨트롤러 개체를 삭제 하려면  
  
1.  클릭 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  
2.  콘솔 트리에서 도메인 컨트롤러를 두 번 클릭 한 다음 두 번 클릭 하 고 **도메인 컨트롤러** 조직 단위 합니다.  
3.  마우스 오른쪽 단추로 클릭 한 다음 고 삭제 하려는 DC 세부 정보 창에서 **삭제**합니다. 
![삭제](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4.  클릭 **예** 삭제 확인 합니다. 선택는 **이 도메인 컨트롤러 영구적으로 오프 라인와 더 이상 Active Directory Domain Services 설치 마법사 (DCPROMO)를 사용 하 여 내릴 수** 확인란을 선택 하 고 클릭 **삭제**합니다.  
5.  DC 드 서버 되었으면 클릭 **예** 확인 하는 삭제 됩니다.  
  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
  
