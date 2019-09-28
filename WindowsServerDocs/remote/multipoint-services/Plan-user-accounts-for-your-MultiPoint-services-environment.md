---
title: MultiPoint 서비스 환경에 대한 사용자 계정 계획
description: MultiPoint 서비스의 사용자 계정에 대 한 계획 정보
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d47be540-e891-47bd-85da-6df4bbf93b2f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 056c3b9773387cf00b40baf6f14e4e1f3583f6c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405010"
---
# <a name="plan-user-accounts-for-your-multipoint-services-environment"></a>MultiPoint 서비스 환경에 대한 사용자 계정 계획
MultiPoint 서비스에서 사용자 계정을 구현 하는 가장 좋은 방법은 배포의 규모와 복잡성에 따라 달라 집니다.  
  
-   **로컬 사용자 계정** -다중 서버를 실행 하는 소수의 컴퓨터를 포함 하는 소규모 배포의 경우에는 MultiPoint 서비스에서 만든 *로컬 사용자 계정을* 사용 하는 것이 가장 편리 합니다. 시스템을 사용 하는 각 사용자에 대해 개별 계정을 만들거나, 모든 사용자가 로그온 하는 데 사용할 수 있는 일반 계정을 만들 수 있습니다. MultiPoint 서비스 관리자는 다중 포인트 관리자를 사용 하 여 로컬 사용자 계정을 만들고 관리 합니다. 로컬 계정은 관리자 이거나, 제한 된 관리 권한 이거나, MultiPoint 서비스 데스크톱 또는 MultiPoint 관리자에 대 한 액세스 권한이 없는 일반 사용자 일 수 있습니다.  
  
-   **도메인 계정** -환경에 MultiPoint 서비스와 많은 사용자를 실행 하는 여러 컴퓨터가 있는 경우 Active Directory Domain Services \(AD DS @ no__t-2 도메인을 설정 하 고 *도메인 사용자 계정을*사용 하는 것이 더 유용할 수 있습니다. 사용자가 도메인의 모든 스테이션에서 자신의 사용자 프로필 및 설정에 액세스할 수 있도록 합니다. 도메인 관리자가 도메인 컨트롤러에 도메인 사용자 계정을 만들어야 합니다.  
  
> [!NOTE]  
> 다음 섹션에서는 MultiPoint 서비스의 로컬 사용자 계정에 대해 구현할 수 있는 시나리오에 대해 설명 합니다. 도메인 사용자 계정을 사용 하는 경우 [Example 시나리오에서 "도메인 네트워크 환경에서 하나 이상의 MultiPoint server" 시나리오를 참조 하세요. MultiPoint 서비스 사용자 계정 @ no__t-0.  
  
## <a name="planning-local-user-accounts"></a>로컬 사용자 계정 계획  
다음 섹션에서는 Windows MultiPoint 서비스 환경에서 개별 또는 공유 로컬 사용자 계정을 구현 하는 여러 가지 방법에 대 한 장점, 단점 및 요구 사항을 고려 합니다.  
  
### <a name="use-individual-local-user-accounts"></a>개별 로컬 사용자 계정 사용  
로컬 사용자 계정을 만들 때 두 가지 방법으로 옵션을 사용할 수 있습니다.  MultiPoint 서비스를 실행 하는 특정 서버에 각 사용자를 할당 하 고 각 사용자에 대해 단일 계정을 만듭니다. 또는 Multipoint 서비스를 실행 하는 모든 컴퓨터에서 모든 사용자에 대 한 로컬 사용자 계정을 만듭니다. 개별 사용자 계정을 구현 하는 경우의 주요 이점은 각 사용자에 게 데이터를 저장 하기 위한 개인 폴더를 포함 하는 고유한 Windows 데스크톱 환경을 보유 하는 것입니다. 
  
시스템 관리 관점에서 특정 MultiPoint 서비스 컴퓨터에 사용자를 할당 하는 것이 더 편리할 수 있습니다. 예를 들어 각각 5 개의 스테이션을 포함 하는 두 개의 MultiPoint 서버가 있는 경우 다음 표에 설명 된 대로 로컬 사용자 계정을 만들 수 있습니다.  
  
**Table 1: MultiPoint 서비스를 실행 하는 특정 컴퓨터에 로컬 사용자 계정 할당 @ no__t-0  
  
|컴퓨터 A|컴퓨터 B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_06|  
|UserAccount_02|UserAccount_07|  
|UserAccount_03|UserAccount_08|  
|UserAccount_04|UserAccount_09|  
|UserAccount_05|UserAccount_10|  
  
이 시나리오에서 각 사용자는 특정 컴퓨터에서 단일 계정을 가집니다. 따라서 컴퓨터 A에 로컬 계정이 있는 모든 사용자는 컴퓨터 A에 연결 된 스테이션에서 자신의 계정 또는 자신의 계정에 로그온 할 수 있습니다. 그러나 이러한 사용자는 컴퓨터 B에 연결 된 스테이션을 사용 하는 경우 해당 계정에 액세스할 수 없으며 그 반대의 경우도 마찬가지입니다. 이 방법의 장점은 항상 동일한 컴퓨터에 연결 하 여 사용자가 항상 해당 파일을 찾아서 액세스할 수 있다는 것입니다.  
  
반면, 다음 표에 설명 된 것 처럼 MultiPoint 서비스를 실행 하는 모든 컴퓨터에서 개별 사용자 계정을 복제할 수 있습니다.  
  
** 표 2: MultiPoint 서비스를 실행 하는 모든 컴퓨터에서 사용자 계정 복제 @ no__t-0  
  
|컴퓨터 A|컴퓨터 B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_01|  
|UserAccount_02|UserAccount_02|  
|UserAccount_03|UserAccount_03|  
|UserAccount_04|UserAccount_04|  
|UserAccount_05|UserAccount_05|  
  
이 방법의 장점은 사용자가 사용 가능한 모든 MultiPoint 서비스에 대 한 로컬 사용자 계정을 보유 한다는 것입니다. 그러나 단점은이 이점 보다 클 수 있습니다. 예를 들어, 특정 사용자의 사용자 이름과 암호가 두 컴퓨터에서 동일 하더라도 계정은 서로 연결 되지 않습니다. 따라서 사용자가 월요일에 컴퓨터 A의 계정으로 로그온 하 고 파일을 저장 한 다음 화요일에 컴퓨터 B의 계정에 로그온 하면 컴퓨터 A에 이전에 저장 된 파일에 액세스할 수 없게 됩니다. 여러 컴퓨터에서 사용자 계정을 복제 하면 관리 오버 헤드 및 저장소 요구 사항이 증가 합니다.  
  
### <a name="use-generic-local-user-accounts"></a>일반 로컬 사용자 계정 사용  
MultiPoint 서비스 시스템이 도메인에 연결 되지 않은 상태에서 각 사용자에 대해 개별 계정을 만들지 않으려는 경우 각 스테이션에 대해 일반 계정을 만들 수 있습니다. 예를 들어 MultiPoint 서비스를 실행 하는 컴퓨터가 두 대 있고 각 컴퓨터에 5 개의 스테이션이 연결 되어 있는 경우 다음 표에 표시 된 것과 유사한 사용자 계정을 만들도록 결정할 수 있습니다.  
  
**Table 3: 일반 사용자 계정 만들기, 스테이션 마다 하나의 계정 @ no__t-0  
  
|컴퓨터 A|컴퓨터 B|  
|--------------|--------------|  
|Computer_A-Station_01|Computer_B-Station_01|  
|Computer_A-Station_02|Computer_B-Station_02|  
|Computer_A-Station_03|Computer_B-Station_03|  
|Computer_A-Station_04|Computer_B-Station_04|  
|Computer_A-Station_05|Computer_B-Station_05|  
  
이 시나리오에서는 모든 스테이션 계정에 동일한 암호가 있으며 모든 사용자가 암호와 일반 사용자 계정 이름을 모두 사용할 수 있습니다. 이 방법의 장점은 일반적으로 사용자 보다 많은 스테이션이 있으므로 사용자 계정을 관리 하는 오버 헤드가 개별 계정을 사용 하는 경우 보다 적을 가능성이 있습니다. 또한 모든 서버에서 사용자 계정을 복제 하 여 발생 하는 오버 헤드가 제거 됩니다.  
  
또 다른 옵션은 각 서버에서 일반 계정을 만드는 것입니다. 모든 사용자는 동일한 계정으로 서버에 로그온 합니다. 이를 허용 하려면 계정 마다 여러 세션을 사용 하도록 설정 해야 합니다. 모든 서버에서 동일한 계정 이름 및 암호를 사용 하 여 더 간소화할 수 있습니다. 이를 통해 사용자에 대 한 로그온을 간소화 합니다 .이 경우 서버에서 모든 스테이션을 사용할 계정 이름과 암호를 한 번만 알고 있으면 됩니다. 이 시나리오에서는 모든 사용자가 사용자가 수행 하는 변경 내용을 볼 수 있습니다. 예를 들어 파일이 바탕 화면에 저장 되는 경우 모든 사용자가 파일을 볼 수 있습니다.  
  
> [!IMPORTANT]  
> 사용자가 서버 당 하나 또는 스테이션 당 하나씩 사용자 계정을 공유 하는 경우, 서버에 저장 된 파일 (내 문서에 저장 된 파일)도 개인이 아닌 것을 이해 하는 것이 중요 합니다. 계정으로 로그온 하는 모든 사용자는 해당 파일에 액세스할 수 있습니다. 스테이션 당 한 계정을 사용 하는 경우 사용자가 한 스테이션의 내 문서에 파일을 저장 하면 사용자는 다른 스테이션의 해당 파일에 액세스할 수 없습니다. 다른 MultiPoint 서비스 컴퓨터에 로그온 하는 경우에도 마찬가지입니다.  
  
사용자가 모든 스테이션에서 파일에 액세스할 수 있도록 하려면 파일 서버를 사용 하거나, 각 사용자 계정에 대 한 파일 공유를 만들거나, 사용자가 USB 플래시 드라이브 또는 기타 개인 저장 장치에 개인 문서를 저장할 수 있도록 합니다. 개별 USB 플래시 드라이브를 사용 하면 개별 사용자가 MultiPoint 서비스에서 사용자 계정을 공유 하는 경우에도 개인 문서를 저장할 수 있습니다.