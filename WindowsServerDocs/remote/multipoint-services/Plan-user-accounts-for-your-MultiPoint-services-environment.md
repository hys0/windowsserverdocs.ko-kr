---
title: MultiPoint 서비스 환경에 대한 사용자 계정 계획
description: MultiPoint 서비스에서 사용자 계정에 대 한 계획 정보
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d47be540-e891-47bd-85da-6df4bbf93b2f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 02862c1a317dfe5deff75be4a80595c8dc8bc3f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864174"
---
# <a name="plan-user-accounts-for-your-multipoint-services-environment"></a>MultiPoint 서비스 환경에 대한 사용자 계정 계획
MultiPoint 서비스에서 사용자 계정을 구현 하는 가장 좋은 방법은 크기와 배포의 복잡성에 따라 달라 집니다.  
  
-   **로컬 사용자 계정을** -실행 중인 MultiPoind 몇 대의 컴퓨터만을 사용 하 여 소규모 배포에 대 한 서비스 및 사용자가 거의 볼 수 있습니다 하는 데 가장 편리한 *로컬 사용자 계정* MultiPoint 서비스에서 생성 된 합니다. 시스템을 사용 하거나 모든 사용자가 로그온 하는 데 사용할 수 있는 각 스테이션에 대 한 일반 계정 만들기가 각 사용자에 대 한 개별 계정을 만들 수 있습니다. MultiPoint 서비스 관리자가 만들고 다중 포인트 관리자를 사용 하 여 로컬 사용자 계정을 관리 합니다. 로컬 계정 관리자 권한을 제한, 다중 포인트 관리자 MultiPoint 서비스 데스크톱에 액세스할 수 없는 일반 사용자 관리자 일 수 있습니다.  
  
-   **도메인 계정을** -환경의 MultiPoint 서비스와 많은 사용자 들을 실행 하는 여러 컴퓨터에 있으면 아마도 있습니다 Active Directory 도메인 서비스를 설정 하는 것이 유용한 \(AD DS\) 도메인과 사용하여*도메인 사용자 계정을*, 도메인의 모든 스테이션에서 자신의 사용자 프로필 및 설정에 액세스할 수 있게 해 주는 합니다. 도메인 사용자 계정 도메인 관리자가 도메인 컨트롤러에서 생성 되어야 합니다.  
  
> [!NOTE]  
> 다음 섹션에서는 MultiPoint 서비스에서 로컬 사용자 계정에 대 한 구현 하는 시나리오를 설명 합니다. 도메인 사용자 계정을 사용 하는 경우 참조에서 "하나 이상의 MultiPoint 서버 도메인 네트워크 환경에서" 시나리오를 [예제 시나리오: MultiPoint 서비스 사용자 계정을](Example-scenarios--MultiPoint-Services-user-accounts.md)합니다.  
  
## <a name="planning-local-user-accounts"></a>로컬 사용자 계정 계획  
다음 섹션에서는 장점, 단점 및 개별 또는 공유 로컬 사용자 계정을 Windows MultiPoint 서비스 환경에서 구현 하는 여러 방법에 대 한 요구 사항을 고려 합니다.  
  
### <a name="use-individual-local-user-accounts"></a>개별 로컬 사용자 계정을 사용 하 여  
로컬 사용자 계정을 만들 때 방법은 다음 두 가지 옵션이 있습니다.  각 사용자 MultiPoint 서비스를 실행 하 고 각 사용자에 대 한 단일 계정을 만드는 특정 서버를 할당 합니다. 또는 Multipoint 서비스를 실행 하는 모든 컴퓨터에 모든 사용자에 대 한 로컬 사용자 계정을 만듭니다. 개별 사용자 계정을 구현 하는 가장 큰 장점은 경우 각 사용자가 데이터를 저장 하기 위한 개인 폴더를 포함 하는 자신의 Windows 데스크톱 환경 
  
시스템 관리 측면에서 특정 MultiPoint 서비스 컴퓨터에 사용자 지정 하기 더 편리할 수 있습니다. 예를 들어 5 개의 스테이션을 사용 하 여 두 MultiPoint 서버를 설정한 경우 다음 표에 나와 있는 대로 로컬 사용자 계정을 만들 수 있습니다.  
  
**표 1: MultiPoint 서비스를 실행 하는 특정 컴퓨터에 로컬 사용자 계정을 할당**  
  
|컴퓨터 A|컴퓨터 B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_06|  
|UserAccount_02|UserAccount_07|  
|UserAccount_03|UserAccount_08|  
|UserAccount_04|UserAccount_09|  
|UserAccount_05|UserAccount_10|  
  
이 시나리오에서는 각 사용자는 특정 컴퓨터에서 단일 계정을 갖습니다. 따라서 사람들에 게 1. 컴퓨터와 연결 된 모든 스테이션에서 자신의 계정에 로그온 컴퓨터는 수의 로컬 계정 그러나 컴퓨터 B와 반대로 연결 된 스테이션을 사용 하는 경우 이러한 사용자가 해당 계정에 액세스할 수 없습니다. 동일한 컴퓨터에 항상 연결 하 여 사용자 항상 찾을 파일에 액세스할이 방식의 장점은입니다.  
  
반면에 다음 표에 설명 된 대로 MultiPoint 서비스를 실행 하는 모든 컴퓨터에서 개별 사용자 계정에 복제할 수 이기도 합니다.  
  
**표 2: MultiPoint 서비스를 실행 하는 모든 컴퓨터에서 사용자 계정 복제**  
  
|컴퓨터 A|컴퓨터 B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_01|  
|UserAccount_02|UserAccount_02|  
|UserAccount_03|UserAccount_03|  
|UserAccount_04|UserAccount_04|  
|UserAccount_05|UserAccount_05|  
  
이 방식의 장점은 사용자가 사용할 수 있는 모든 MultiPoint 서비스에서 로컬 사용자 계정입니다. 그러나 단점은 이러한 장점 보다 클 수 있습니다. 예를 들어, 사용자 이름 및 특정 사용자에 대 한 암호 인 두 컴퓨터 모두에서 동일 하 게 하는 경우에 계정은 서로 연결 되지 않습니다. 따라서 사용자가 자신의에 로그온 하거나 자신의 계정을 월요일에 컴퓨터 파일을 저장 하 고 그런 다음, 화요일에 컴퓨터 B에서 자신의 계정으로 로그온 자신이 됩니다 1. 또한 컴퓨터에서 이전에 저장 된 파일에 액세스할 수 관리 오버 헤드 및 저장소 요구 사항이 증가 여러 컴퓨터에서 사용자 계정에 복제 합니다.  
  
### <a name="use-generic-local-user-accounts"></a>일반 로컬 사용자 계정을 사용 하 여  
MultiPoint 서비스 시스템을 도메인에 연결 되지 않은 경우 각 사용자에 대 한 개별 계정을 만드는 각 스테이션에 대 한 제네릭 계정을 만들 수 있습니다. 예를 들어 MultiPoint 서비스를 실행 하는 컴퓨터가 두 대 있는 5 개의 스테이션은 각 컴퓨터에 연결 된 경우 다음 표에 나와 있는 것과 비슷한 사용자 계정을 만드는 결정할 수 있습니다.  
  
**표 3: 일반 사용자 계정, 스테이션 당 하나의 계정 만들기**  
  
|컴퓨터 A|컴퓨터 B|  
|--------------|--------------|  
|Computer_A-Station_01|Computer_B-Station_01|  
|Computer_A-Station_02|Computer_B-Station_02|  
|Computer_A-Station_03|Computer_B-Station_03|  
|Computer_A-Station_04|Computer_B-Station_04|  
|Computer_A-Station_05|Computer_B-Station_05|  
  
이 시나리오에서는 모든 스테이션 계정에 같은 암호를 일반 사용자 계정 이름 및 암호 제공 되며 모든 사용자에 게. 이 방식의 장점은 점 사용자 계정 관리의 오버 헤드가 있기 때문에 일반적으로 사용자에 비해 더 적은 스테이션 개별 계정을 사용 하는 경우에 보다 작은 수입니다. 또한 모든 서버에서 사용자 계정에 복제 하 여 생기는 오버 헤드가 제거 됩니다.  
  
또 다른 옵션 각 서버의 일반 계정을 만드는 것입니다. 모든 사용자는 동일한 계정으로, 서버에 로그온합니다. 이 위해 계정당 여러 세션을 설정 해야 합니다. 모든 서버에서 동일한 계정 이름 및 암호를 사용 하 여 자세한 단순화할 수 있습니다. 로그온을 한 계정 이름 및 서버의 모든 스테이션이 사용할 암호를 알면 사용자에 대 한 간단해 집니다. 이 시나리오에서는 모든 사용자를 볼 수 있는지 모든 사용자가 변경한 유의 해야 합니다. 예를 들어, 데스크톱에 파일로 저장 되는 경우 모든 사용자가 파일을 볼 수 있습니다.  
  
> [!IMPORTANT]  
> 사용자가 사용자 계정, 서버 당 하나씩 1 개 또는 스테이션 당 하나를 공유할 때 파일 – 파일도 내 문서에 저장 된-서버에 저장 되지 않는다는 사실을 개인을 이해 하는 것이 반드시 합니다. 사용자 계정을 사용 하 여 로그에 해당 파일에 대 한 액세스를 권한이 합니다. 사용자는 사용자는 하나의 스테이션에서 내 문서에 파일을 저장 하는 경우 스테이션 당 하나의 계정을 사용 하는 경우 다른 스테이션에서 해당 파일에 액세스를 하지 않습니다. 동일한 다른 MultiPoint 서비스 컴퓨터에 로그온 할 때 발생 합니다.  
  
모든 스테이션에서 해당 파일에 액세스할 수 있도록 파일 서버를 사용 하 여, 각 사용자 계정에 대 한 파일 공유 만들기 또는 USB 플래시 드라이브 또는 기타 개인 저장소 장치에 자신의 개인 문서를 저장 하는 사용자가 수 있습니다. MultiPoint 서비스에 대 한 사용자 계정이 공유 하는 경우에 개인 문서를 저장 하는 개별 사용자를 사용 하도록 설정 하는 개별 USB 플래시 드라이브.