---
ms.assetid: 407d5e81-c04c-4275-9ae9-35f65b4a371a
title: 글로벌 카탈로그 서버 배치 계획
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: aefed1a2ed0d346f75ad4d135f8c0ae314fd7fc7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820684"
---
# <a name="planning-global-catalog-server-placement"></a>글로벌 카탈로그 서버 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

글로벌 카탈로그 배치는 단일 도메인 포리스트가 있는 경우를 제외 하 고 계획 해야 합니다. 단일 도메인 포리스트의 모든 도메인 컨트롤러를 글로벌 카탈로그 서버로 구성 합니다. 포리스트의 유일한 도메인 디렉터리 파티션에 저장 하는 모든 도메인 컨트롤러를 하기 때문에 각 도메인 컨트롤러를 글로벌 카탈로그 서버로 구성 하지 않아도 모든 추가 디스크 공간 사용량, CPU 사용량 또는 복제 트래픽이 됩니다. 단일 도메인 포리스트의 모든 도메인 컨트롤러 가상 글로벌 카탈로그 서버로; 작동 즉, 모든 응답할 수 나 인증 서비스 요청 합니다. 단일 도메인 포리스트를 위한 특별 한이 상태는 의도적입니다. 인증 요청 경우 여러 도메인 사용자는 다른 도메인에 있는 유니버설 그룹의 멤버 수와 글로벌 카탈로그 서버에 연결 하는 것 필요 하지 않습니다. 그러나 전용 글로벌 카탈로그 서버로 지정 된 도메인 컨트롤러를 글로벌 카탈로그 포트 3268에 대 한 글로벌 카탈로그 쿼리에 응답할 수 있습니다. 이 시나리오에서는 관리를 단순화 하 고 일관 된 응답 하도록 모든 도메인 컨트롤러를 글로벌 카탈로그 서버로 지정 글로벌 카탈로그 쿼리에 응답할 수 컨트롤러는 도메인에 대 한 문제를 제거 합니다. 특히 사용자 든 Start\Search\For 사용자나 프린터 찾기를 사용 하 여 또는 유니버설 그룹을 확장, 글로벌 카탈로그에만 이러한 요청이 이동 합니다.  
  
다중 도메인 포리스트에서 글로벌 카탈로그 서버를 쉽게 사용자 로그온 요청 하 고 포리스트 전체 검색 합니다. 다음 그림에는 글로벌 카탈로그 서버를 필요로 하는 위치를 확인 하는 방법을 보여 줍니다.  
  
![gc 배치 계획](media/Planning-Global-Catalog-Server-Placement/8fc4777c-47b6-4ee7-b8ad-a04e7c5ee67f.gif)  
  
대부분의 경우에서 새 도메인 컨트롤러를 설치할 때 글로벌 카탈로그를 포함 하는 것이 좋습니다. 다음과 같은 예외가 적용 됩니다.  
  
- 제한 된 대역폭의 경우: 원격 사이트에 허브 사이트와 원격 사이트 간의 광역 네트워크 (WAN) 링크는 제한 하는 경우 사용할 수 있습니다 유니버설 그룹 구성원 자격 캐싱 원격 사이트에서 사이트에 사용자의 로그온 요구를 수용 하기 위해.  
- 인프라 작업 마스터 역할 비 호환성: 호스트 인프라 작업 도메인의 모든 도메인 컨트롤러는 글로벌 카탈로그 서버가 아니면 포리스트에 하나의 도메인에 도메인의 역할을 마스터 하는 도메인 컨트롤러에서 글로벌 카탈로그를 배치 하지 마십시오.  
  
## <a name="adding-global-catalog-servers-based-on-application-requirements"></a>응용 프로그램 요구 사항에 따라 추가 글로벌 카탈로그 서버

특정 응용 프로그램을 Microsoft Exchange, 메시지 큐 (MSMQ 라고도 함), 및 DCOM을 사용 하 여 응용 프로그램과 같은 잠재 WAN 링크를 통해 적절 한 응답을 제공 하지 않으며 따라서 낮은 쿼리를 제공 하기 위해 항상 사용 가능한 글로벌 카탈로그 인프라 필요 대기 시간입니다. 느린 WAN 링크를 통해 잘못 수행 하는 모든 응용 프로그램 위치 또는 위치에서 Microsoft Exchange Server를 요구 하는 여부 중인지 확인 합니다. WAN 링크를 통해 적절 한 응답을 전달 하지 않는 응용 프로그램이 포함 하는 위치, 글로벌 카탈로그 서버 쿼리 대기 시간을 줄이기 위해 위치에 배치 해야 합니다.  
  
> [!NOTE]  
> 글로벌 카탈로그 서버 상태를 읽기 전용 도메인 컨트롤러 (Rodc)을 성공적으로 승격할 수 있습니다. 그러나 특정 디렉터리 사용 응용 프로그램은 글로벌 카탈로그 서버로 RODC를 지원할 수 없습니다. 예를 들어, Microsoft Exchange Server의 버전이 Rodc를 사용합니다. 그러나 Microsoft Exchange Server는 사용할 수 있는 쓰기 가능한 도메인 컨트롤러와 Rodc를 포함 하는 환경에서 작동 합니다. Exchange Server 2007에는 효과적으로 Rodc는 무시합니다. 또한 Exchange Server 2003 사용 가능한 도메인 컨트롤러에 Exchange 구성 요소 자동으로 검색 하는 기본 조건에서 Rodc를 무시 합니다. 읽기 전용 디렉터리 서버를 인식 하도록 Exchange Server 2003으로 변경 된 내용이 없습니다. 따라서 Exchange Server 2003 서비스 및 관리 도구 Rodc를 강제 적용 하는 동안 예기치 않은 동작이 발생할 수 있습니다.  
  
## <a name="adding-global-catalog-servers-for-a-large-number-of-users"></a>많은 수의 사용자에 대 한 글로벌 카탈로그 서버를 추가합니다.

네트워크의 WAN 링크의 혼잡을 줄이고 WAN 링크 오류 발생 시 생산성 손실을 방지 하기 위해 100 개가 넘는 사용자를 포함 하는 모든 위치에서 글로벌 카탈로그 서버를 배치 합니다.  
  
## <a name="using-highly-available-bandwidth"></a>항상 사용 가능한 대역폭을 사용 하 여

글로벌 카탈로그 서버를 필요로 하는 응용 프로그램을 다루지 않습니다 100 개 미만의 사용자를 포함 하 고 100%는 WAN 링크로 글로벌 카탈로그 서버를 포함 하는 다른 위치에 연결 된 위치에 글로벌 카탈로그를 추가할 필요가 없습니다를 Active Directory Domain Services (AD DS)에 대 한 장식 합니다. 이 경우 사용자는 WAN 링크를 통해 글로벌 카탈로그 서버를 액세스할 수 있습니다.  
  
로밍 사용자는 모든 위치에서 처음으로 로그온 할 때마다 글로벌 카탈로그 서버를 연결 해야 합니다. WAN 링크를 통해 로그온에 허용 되지 않는 경우 글로벌 카탈로그는 다양 한 로밍 사용자가 방문한 위치에 배치 합니다.  
  
## <a name="enabling-universal-group-membership-caching"></a>유니버설 그룹 구성원 자격 캐싱을 사용 하도록 설정

100 대 미만의 사용자를 포함 하 고 많은 수의 로밍 사용자 또는 글로벌 카탈로그 서버를 필요로 하는 응용 프로그램을 포함 하지 않는 위치에 대 한 Windows Server 2008을 실행 하 고 유니버설 그룹 멤버 자격을 사용 하도록 설정 하는 도메인 컨트롤러를 배포할 수 있습니다. 캐싱. 글로벌 카탈로그 서버 유니버설 그룹 구성원 자격 캐싱을 사용 되는 캐시에서 유니버설 그룹 정보를 새로 고칠 수 있도록 도메인 컨트롤러에서 둘 이상의 복제 홉 되지 않았는지 확인 합니다. 어떻게 유니버설 그룹 캐싱 동작에 대 한 자세한 문서를 참조 [전역 카탈로그의 작동 방식](https://go.microsoft.com/fwlink/?LinkId=107063)합니다.  
  
유니버설 그룹 캐싱을 사용 하도록 설정 된 도메인 컨트롤러와 글로벌 카탈로그 서버를 배치 하려는 위치를 문서화 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_ 다운로드 Designing_and_Deploying_Directory_and_Security_Services.zip, 및 open 도메인 컨트롤러 배치 (DSSTOPO_4.doc). 포리스트 루트 도메인 및 지역 도메인 배포 하는 경우 글로벌 카탈로그 서버를 배치 해야 하는 위치에 대 한 정보를 참조 하세요.  
