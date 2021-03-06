---
ms.assetid: 407d5e81-c04c-4275-9ae9-35f65b4a371a
title: 글로벌 카탈로그 서버 배치 계획
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b424d758d98315ff63f05926880a23970f54e49c
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81623971"
---
# <a name="planning-global-catalog-server-placement"></a>글로벌 카탈로그 서버 배치 계획

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

글로벌 카탈로그 배치에는 단일 도메인 포리스트가 있는 경우를 제외 하 고 계획이 필요 합니다. 단일 도메인 포리스트에서 모든 도메인 컨트롤러를 글로벌 카탈로그 서버로 구성 합니다. 모든 도메인 컨트롤러는 포리스트에 유일한 도메인 디렉터리 파티션을 저장 하므로 각 도메인 컨트롤러를 글로벌 카탈로그 서버로 구성 하려면 추가 디스크 공간 사용, CPU 사용량 또는 복제 트래픽이 필요 하지 않습니다. 단일 도메인 포리스트에서 모든 도메인 컨트롤러는 가상 글로벌 카탈로그 서버 역할을 합니다. 즉, 모든 인증 또는 서비스 요청에 응답할 수 있습니다. 단일 도메인 포리스트에 대 한이 특수 조건은 의도적으로 설계 되었습니다. 여러 도메인이 있는 경우 처럼 인증 요청은 글로벌 카탈로그 서버에 연결할 필요가 없으며, 사용자는 다른 도메인에 있는 유니버설 그룹의 구성원이 될 수 있습니다. 그러나 글로벌 카탈로그 서버로 지정 된 도메인 컨트롤러만 글로벌 카탈로그 포트 3268에서 글로벌 카탈로그 쿼리에 응답할 수 있습니다. 이 시나리오에서 관리를 간소화 하 고 일관 된 응답을 보장 하기 위해 모든 도메인 컨트롤러를 글로벌 카탈로그 서버로 지정 하면 도메인 컨트롤러가 글로벌 카탈로그 쿼리에 응답할 수 있는 문제를 방지할 수 있습니다. 특히 사용자가 사용자에 게 start\search\\c\c\c\c\c\c\c\c\c\c\c\c\c\c\c\

다중 도메인 포리스트에서 글로벌 카탈로그 서버는 사용자 로그온 요청 및 포리스트 전체 검색을 용이 하 게 합니다. 다음 그림은 글로벌 카탈로그 서버를 필요로 하는 위치를 확인 하는 방법을 보여 줍니다.

![gc 배치 계획](media/Planning-Global-Catalog-Server-Placement/8fc4777c-47b6-4ee7-b8ad-a04e7c5ee67f.gif)

대부분의 경우 새 도메인 컨트롤러를 설치할 때 글로벌 카탈로그를 포함 하는 것이 좋습니다. 다음과 같은 예외가 있습니다.

- 제한 된 대역폭: 원격 사이트에서 원격 사이트와 허브 사이트 간의 WAN (광역 네트워크) 연결을 제한 하는 경우 원격 사이트에서 유니버설 그룹 구성원 자격 캐싱을 사용 하 여 사이트의 사용자에 대 한 로그온 요구를 수용할 수 있습니다.
- 인프라 작업 마스터 역할 비호환: 도메인의 모든 도메인 컨트롤러가 글로벌 카탈로그 서버 이거나 포리스트에 도메인이 하나만 있는 경우를 제외 하 고 도메인의 인프라 작업 마스터 역할을 호스트 하는 도메인 컨트롤러에 글로벌 카탈로그를 두지 않습니다.

## <a name="adding-global-catalog-servers-based-on-application-requirements"></a>응용 프로그램 요구 사항에 따라 글로벌 카탈로그 서버 추가

Microsoft Exchange, 메시지 큐 (MSMQ)와 같은 특정 응용 프로그램 및 DCOM을 사용 하는 응용 프로그램은 잠재적인 WAN 링크에 대 한 적절 한 응답을 제공 하지 않으므로 낮은 쿼리 대기 시간을 제공 하기 위해 항상 사용 가능한 글로벌 카탈로그 인프라가 필요 합니다. 저속 WAN 링크를 통해 성능이 저하 되는 응용 프로그램이 위치에서 실행 되 고 있는지 또는 위치에 Microsoft Exchange Server가 필요한 지 여부를 확인 합니다. WAN 링크를 통해 적절 한 응답을 제공 하지 않는 응용 프로그램이 위치에 포함 된 경우, 쿼리 대기 시간을 줄이기 위해 위치에 글로벌 카탈로그 서버를 배치 해야 합니다.

> [!NOTE]
> Rodc (읽기 전용 도메인 컨트롤러)를 글로벌 카탈로그 서버 상태에 성공적으로 승격할 수 있습니다. 그러나 특정 디렉터리 사용 응용 프로그램은 글로벌 카탈로그 서버로 RODC를 지원할 수 없습니다. 예를 들어 어떤 버전의 Microsoft Exchange Server는 Rodc를 사용 하지 않습니다. 그러나 사용할 수 있는 쓰기 가능한 도메인 컨트롤러가 있는 경우 Microsoft Exchange Server는 Rodc를 포함 하는 환경에서 작동 합니다. Exchange Server 2007는 Rodc를 효과적으로 무시 합니다. Exchange Server 2003는 Exchange 구성 요소가 사용 가능한 도메인 컨트롤러를 자동으로 검색 하는 기본 조건에서 Rodc도 무시 합니다. 읽기 전용 디렉터리 서버를 인식할 수 있도록 Exchange Server 2003가 변경 되지 않았습니다. 따라서 Exchange Server 2003 서비스 및 관리 도구에서 Rodc를 사용 하도록 강제 하려고 하면 예기치 않은 동작이 발생할 수 있습니다.

## <a name="adding-global-catalog-servers-for-a-large-number-of-users"></a>여러 사용자에 대 한 글로벌 카탈로그 서버 추가

네트워크 WAN 링크의 정체를 줄이고 WAN 링크에 오류가 발생 하는 경우 생산성 손실을 방지 하기 위해 100 명 이상의 사용자가 포함 된 모든 위치에 글로벌 카탈로그 서버를 추가 합니다.

## <a name="using-highly-available-bandwidth"></a>항상 사용 가능한 대역폭 사용

글로벌 카탈로그 서버를 필요로 하는 응용 프로그램이 포함 되지 않은 위치에는 글로벌 카탈로그를 배치 하지 않아도 되 고, 100 명 미만의 사용자를 포함 하며, Active Directory Domain Services (AD DS)에서 사용할 수 있는 100% 인 WAN 링크로 글로벌 카탈로그 서버를 포함 하는 다른 위치에도 연결할 수 있습니다. 이 경우 사용자는 WAN 링크를 통해 글로벌 카탈로그 서버에 액세스할 수 있습니다.

로밍 사용자는 모든 위치에서 처음 로그온 할 때마다 글로벌 카탈로그 서버에 연결 해야 합니다. WAN 링크를 통한 로그온 시간이 허용 되지 않는 경우 많은 수의 로밍 사용자가 방문 하는 위치에 글로벌 카탈로그를 배치 합니다.

## <a name="enabling-universal-group-membership-caching"></a>유니버설 그룹 구성원 자격 캐싱 사용

100 미만의 사용자를 포함 하 고 글로벌 카탈로그 서버를 필요로 하는 많은 수의 로밍 사용자 또는 응용 프로그램을 포함 하지 않는 위치의 경우 Windows Server 2008를 실행 하는 도메인 컨트롤러를 배포 하 고 유니버설 그룹 멤버 자격 캐싱을 사용 하도록 설정할 수 있습니다. 글로벌 카탈로그 서버가 유니버설 그룹 멤버 자격 캐싱이 설정 된 도메인 컨트롤러에서 둘 이상의 복제 홉이 아닌지 확인 하 여 캐시의 유니버설 그룹 정보를 새로 고칠 수 있도록 합니다. 유니버설 그룹 캐싱이 작동 하는 방법에 대 한 자세한 내용은 [글로벌 카탈로그 작동 방법](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737410(v=ws.10))문서를 참조 하세요.

유니버설 그룹 캐싱을 사용 하도록 설정 된 글로벌 카탈로그 서버와 도메인 컨트롤러를 배치할 계획을 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://microsoft.com/download/details.aspx?id=9608)을 참조 하 고, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services을 다운로드 하 고, 도메인 컨트롤러 배치 (DSSTOPO_4)를 엽니다. 포리스트 루트 도메인 및 지역 도메인을 배포할 때 글로벌 카탈로그 서버를 배치 해야 하는 위치에 대 한 정보를 참조 하세요.
