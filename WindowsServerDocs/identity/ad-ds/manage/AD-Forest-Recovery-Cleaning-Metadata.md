---
title: AD 포리스트 복구-제거 dc의 메타 데이터를 정리 합니다.
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adds
ms.openlocfilehash: b71cab51a362a96ab6071e5eed3cf31c4421041c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843044"
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>AD 포리스트 복구-제거 쓰기 가능한 도메인 컨트롤러의 메타 데이터를 정리 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

메타 데이터 정리 DC가 복제 시스템을 식별 하는 Active Directory 데이터를 제거 합니다.  

AD DS를 다시 설치 하 여 네트워크에 다시 추가 하려고 하는 Dc에 대 한 DC 개체를 삭제 하려면 다음 절차를 따르십시오.  
  
Active Directory 사용자 및 컴퓨터의 버전을 사용 하는 경우 Active Directory 사이트 및 서비스는 원격 서버 관리 도구 (RSAT)를 포함 된 DC 개체를 삭제할 때 메타 데이터 정리 자동으로 수행 됩니다.  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Active Directory 사용자 및 컴퓨터를 사용 하 여 도메인 컨트롤러를 삭제 합니다.

Active Directory 사용자 및 컴퓨터 또는 원격 서버 관리 도구 (RSAT)을의 Active Directory 관리 센터의 버전을 사용 하면 메타 데이터 정리는 DC 개체를 삭제할 때 자동으로 수행 됩니다. 서버 개체 및 컴퓨터 개체는도 자동으로 삭제 됩니다.  

대신 사용할 수도 있습니다 Active Directory 사이트 및 서비스 rsat에서 DC 개체를 삭제 하려면. Active Directory 사이트 및 서비스를 사용 하면 DC 개체를 삭제 하려면 먼저 연결 된 server 개체 및 NTDS 설정 개체를 삭제 해야 합니다.  

RSAT를 설치 하는 것에 대 한 자세한 문서를 참조 [원격 서버 관리 도구](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)합니다.
  
다음 절차 중 Windows Server 2016, 2012, 2008 R2 또는 2008을 실행 하는 Dc에 대 한 동일 합니다. 대상 DC 메타 데이터 정리 작업의 모든 버전의 Windows Server를 실행할 수 있습니다.  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>RSAT에서 Active Directory 사용자 및 컴퓨터를 사용 하 여 도메인 컨트롤러 개체를 삭제 하려면  
  
1. **시작**, **관리 도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다.  
2. 콘솔 트리에서 도메인 컨테이너를 차례로 두 번 클릭 합니다 **도메인 컨트롤러** 조직 구성 단위 (OU).  
3. 세부 정보 창에서 삭제 하 고 클릭 하려는 DC를 마우스 오른쪽 단추로 **삭제**합니다.
   ![Delete](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4. **예**를 클릭하여 삭제를 확인합니다. 선택 된 **이 도메인 컨트롤러 영구적으로 오프 라인 상태 이며 더 이상 Active Directory Domain Services 설치 마법사 (DCPROMO)를 사용 하 여 강등 수** 확인란을 클릭 **삭제**합니다.  
5. DC는 글로벌 카탈로그 서버를 클릭 **예** 확인 삭제 합니다.  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
