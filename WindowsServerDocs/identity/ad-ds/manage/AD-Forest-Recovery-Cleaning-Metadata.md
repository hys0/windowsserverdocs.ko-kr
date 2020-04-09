---
title: AD 포리스트 복구-제거 된 dc의 메타 데이터 정리
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adds
ms.openlocfilehash: b9ba00939ccb2ee747501733fb9654edb4c8132e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824256"
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>AD 포리스트 복구-제거 된 쓰기 가능 도메인 컨트롤러의 메타 데이터 정리

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

메타 데이터 정리는 DC를 식별 하는 Active Directory 데이터를 복제 시스템에 제거 합니다.  

다음 절차를 사용 하 여 AD DS을 다시 설치 하 여 네트워크에 다시 추가할 dc의 DC 개체를 삭제 합니다.  
  
Active Directory 사용자 및 컴퓨터 버전을 사용 하거나 RSAT (원격 서버 관리 도구)에 포함 된 Active Directory 사이트 및 서비스를 사용 하는 경우 DC 개체를 삭제 하면 메타 데이터 정리가 자동으로 수행 됩니다.  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Active Directory 사용자 및 컴퓨터를 사용 하 여 도메인 컨트롤러 삭제

Active Directory 사용자 및 컴퓨터 버전을 사용 하거나 RSAT (원격 서버 관리 도구)에서 Active Directory 관리 센터 하면 DC 개체를 삭제할 때 메타 데이터 정리가 자동으로 수행 됩니다. 서버 개체와 컴퓨터 개체도 자동으로 삭제 됩니다.  

또는 RSAT의 Active Directory 사이트와 서비스를 사용 하 여 DC 개체를 삭제할 수도 있습니다. Active Directory 사이트와 서비스를 사용 하는 경우에는 연결 된 서버 개체 및 NTDS 설정 개체를 삭제 해야 DC 개체를 삭제할 수 있습니다.  

RSAT를 설치 하는 방법에 대 한 자세한 내용은 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)문서를 참조 하세요.
  
다음 절차는 Windows Server 2016, 2012, 2008 R2 또는 2008을 실행 하는 Dc에 대해 동일 합니다. 메타 데이터 정리 작업의 대상 DC는 모든 버전의 Windows Server를 실행할 수 있습니다.  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>RSAT에서 Active Directory 사용자 및 컴퓨터를 사용 하 여 도메인 컨트롤러 개체를 삭제 하려면  
  
1. **시작**, **관리 도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다.  
2. 콘솔 트리에서 도메인 컨테이너를 두 번 클릭 한 다음 **도메인 컨트롤러** OU (조직 구성 단위)를 두 번 클릭 합니다.  
3. 세부 정보 창에서 삭제 하려는 DC를 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 클릭 합니다.
   ![삭제](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4. **예**를 클릭하여 삭제를 확인합니다. **이 도메인 컨트롤러가 영구적으로 오프 라인 상태이 고 Active Directory Domain Services 설치 마법사 (DCPROMO) 확인란을 사용 하 여 더 이상 수준을 내릴 수 없습니다** . 확인란을 선택 하 고 **삭제**를 클릭 합니다.  
5. DC가 글로벌 카탈로그 서버인 경우 **예** 를 클릭 하 여 삭제를 확인 합니다.  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
