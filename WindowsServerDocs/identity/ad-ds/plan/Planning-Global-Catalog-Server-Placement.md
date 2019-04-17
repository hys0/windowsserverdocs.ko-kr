---
ms.assetid: 407d5e81-c04c-4275-9ae9-35f65b4a371a
title: "드 서버 배치 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c32393640e929adf9681f511ed3707b85a3784db
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="planning-global-catalog-server-placement"></a>드 서버 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

글로벌 카탈로그 배치 단일 도메인 숲 하는 경우를 제외 하 고 계획 필요 합니다. 단일 도메인 숲에서 드 서버로 모든 도메인 컨트롤러를 구성 합니다. 모든 도메인 컨트롤러의 숲 속의 유일한 도메인 파티션을 저장을 하기 때문에 각 도메인 컨트롤러에 따라 글로벌 카탈로그 서버 구성 하지 않아도 모든 추가 디스크 공간 사용, cpu를 많이 사용 또는 복제 교통 됩니다. 단일 도메인 숲 모든 도메인 컨트롤러 역할을 가상 드 서버; 즉, 모든에 응답할 수 된 인증 또는 서비스 요청 합니다. 으로 설계 단일 도메인 숲에 대 한이 특별 한 상태가입니다. 인증 요청 여러 도메인 많고 사용자 다른 도메인에 있는 범용 그룹의 회원 될 수 있는 때 처럼 드 서버에 연결 하는 것을 요구 하지 않습니다. 그러나 3268 드 포트 드 쿼리에 드 서버로 지정 하는 도메인 컨트롤러만 응답할 수 있습니다. 이 시나리오 관리를 간소화 하 고 일관 된 응답을 얻으려면 모든 도메인 컨트롤러 서버 드로 지정 컨트롤러 드 쿼리에 응답할 수 있는 도메인에 대 한 관심사를 제거 합니다. 특히, 사용자는 언제 든 지 Start\Search\For 사람이 나 찾기 프린터를 사용 하 여 또는 그룹을 범용 확장을 이러한 요청 드에만 합니다.  
  
다중 도메인 숲에서 드 서버 쉽게 사용자의 로그온 요청 하 고 전체의 숲 검색 합니다. 다음 그림 있는 위치 필요 드 서버를 확인 하는 방법을 보여 줍니다.  
  
![Gc 배치 계획](media/Planning-Global-Catalog-Server-Placement/8fc4777c-47b6-4ee7-b8ad-a04e7c5ee67f.gif)  
  
대부분의 경우 새 도메인 컨트롤러를 설치할 때 드를 포함 하는 것이 좋습니다. 다음 예외 사항이 적용:  
  
-   제한 된 대역폭: 원격 사이트에 있는 경우 넓은 지역 (네트워크) 원격 사이트와 허브 현재 사이트 간의 연결이 제한, 사용할 수 있습니다 유니버설 그룹 구성원 캐싱 원격 사이트에서 해당 사이트에서 사용자의 로그온 요구에 맞게 합니다.  
  
-   Infrastructure 작업 역할 호환성 마스터: 도메인에 있는 모든 도메인 컨트롤러 서버 드 또는 숲은 하나만 도메인 하지 않으면 도메인에 있는 infrastructure 작업 마스터 역할 호스트 하는 도메인 컨트롤러에서 드 두지 않습니다.  
  
## <a name="adding-global-catalog-servers-based-on-application-requirements"></a>드 서버 응용 요구 사항에 따라 추가  
Microsoft Exchange, 메시지 큐 (라고도 MSMQ) DCOM를 사용 하 여 응용 프로그램 등의 특정 응용 프로그램 적절 한 응답 숨어 WAN 링크를 통해 제공 하지 않으며 낮은 받습니다 제공 하기 위해 항상 사용 가능한 드 인프라 따라서 필요 합니다. 느린 WAN 링크를 통해 잘못 수행 하는 모든 응용 프로그램에서 위치 또는 위치 Microsoft Exchange Server 필요한 지 여부 실행 중인지 확인 합니다. 위치에 적절 한 응답 WAN 링크를 통해 제공 하지 않는 응용 프로그램이 포함, 드 서버 받습니다 줄이기 위해 위치에 두어야 합니다.  
  
> [!NOTE]  
> Read-only Rodc (도메인 컨트롤러)의 성공적으로 수준을 드 서버 상태를 올린 수 있습니다. 그러나 특정 디렉터리 사용 응용 프로그램 드 서버로 RODC 지원 하지 않습니다. 예를 들어, Microsoft Exchange server 없음 버전 Rodc 사용합니다. 그러나 Microsoft Exchange Server 쓸 수 있는 도메인 컨트롤러 사용할 수 있는 Rodc을 포함 하는 환경에서 작동 합니다. Exchange Server 2007를 효과적으로 Rodc 무시합니다. Exchange Server 2003 사용할 수 있는 도메인 컨트롤러에 구성 요소 Exchange 자동으로 검색 기본 상황에서 Rodc 무시 합니다. 변경 되지 Exchange Server 2003 읽기 전용 디렉터리 서버 인식 하도록 합니다. 따라서 강제로 Exchange Server 2003 서비스 및 관리 도구 Rodc 사용 하려고 예기치 않은 문제가 발생할 수 있습니다.  
  
## <a name="adding-global-catalog-servers-for-a-large-number-of-users"></a>많은 수의 사용자에 대 한 추가 드 서버  
드 서버 WAN 링크 오류가 발생할 경우 생산성 손실 되지 않도록 하려면 네트워크 WAN 링크 정체도 줄이기 위해 100 개 이상의 사용자를 포함 하는 모든 위치에 배치 합니다.  
  
## <a name="using-highly-available-bandwidth"></a>대역폭이 많이 사용 하 여  
글로벌 카탈로그 드 서버를 필요로 하는 응용 프로그램이 포함 되지 않는 100 미만의 사용자를 포함 하 고 100% Active Directory Domain Services (AD DS)에 사용할 수 있는 WAN 링크에서도 드 서버 포함 되어 있는 다른 위치에 연결 되어 있는 위치에 배치 필요가 없습니다. 이 경우에 사용자가 WAN 링크를 통해 드 서버에 액세스할 수 있습니다.  
  
로밍 사용자 위치에 처음으로 로그온 할 때마다 드 서버에 게 문의 해야 합니다. WAN 링크를 통해 로그온 시간이 허용 되지 않는 경우 글로벌 카탈로그 많은 로밍 사용자가 방문 하는 위치에 배치 합니다.  
  
## <a name="enabling-universal-group-membership-caching"></a>범용 그룹 구성원 캐싱 사용  
많은 수의 로밍 사용자 또는 드 서버를 필요로 하는 응용 프로그램을 포함 하지 않는 및 100 미만의 사용자를 포함 하는 위치, Windows Server 2008 실행 하 고 유니버설 그룹 구성원 캐시를 사용 하는 도메인 컨트롤러 배포할 수 있습니다. 드 서버 유니버설 그룹 구성원 캐싱는 사용할 수 있는 캐시에서 유니버설 그룹 정보 새로 수 있도록 도메인 컨트롤러에서 둘 이상의 복제 홉만 수행 되지 않았는지 확인 합니다. 그룹 캐싱 작동 유니버설 방법에 대 한 정보를 참조 the 글로벌 카탈로그 작동 방식 ([https://go.microsoft.com/fwlink/?LinkId=107063](https://go.microsoft.com/fwlink/?LinkId=107063)).  
  
드 서버와 도메인 컨트롤러 유니버설 그룹 캐싱 사용할 수 있는 장소 하려는 문서화에서 사용자를 지원 하도록 워크시트 참조 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))을 다운로드 < DICT__Job_ Aids_Designing_and_Deploying_Directory_and_Security_Services.zip>Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip</DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip>, and open Domain 컨트롤러 배치 (DSSTOPO_4.doc) 합니다. 이렇게 및 지역 도메인 배포할 때 드 서버를 필요한 위치에 대 한 정보를 참조 하십시오.  
  


