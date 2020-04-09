---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: Active Directory 논리 모델 이해
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cf2b997d601d42a47282df0ed95382e471233ff6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821616"
---
# <a name="understanding-the-active-directory-logical-model"></a>Active Directory 논리 모델 이해

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)에 대 한 논리 구조를 디자인 하는 데는 디렉터리의 컨테이너 간 관계를 정의 하는 작업이 포함 됩니다. 이러한 관계는 권한 위임과 같은 관리 요구 사항에 따라 달라 지 며, 복제를 제어 해야 하는 것과 같은 운영 요구 사항에 따라 정의 될 수 있습니다.  
  
Active Directory 논리 구조를 디자인 하기 전에 Active Directory 논리 모델을 이해 하는 것이 중요 합니다. AD DS는 디렉터리 지원 응용 프로그램의 응용 프로그램 관련 데이터 및 네트워크 리소스에 대 한 정보를 저장 하 고 관리 하는 분산 데이터베이스입니다. 관리자는 AD DS를 사용 하 여 네트워크 (예: 사용자, 컴퓨터 및 장치)의 요소를 계층적 포함 구조로 구성할 수 있습니다. 최상위 컨테이너는 포리스트입니다. 포리스트 내에서 도메인 이며 도메인 내에 Ou (조직 구성 단위)가 있습니다. 이를 논리적 모델 이라고 하며,이는 각 도메인 및 네트워크 토폴로지 내에 필요한 도메인 컨트롤러 수와 같은 배포의 물리적 측면에 독립적 이기 때문입니다.  
  
## <a name="active-directory-forest"></a>Active Directory 포리스트  
포리스트는 공통 논리 구조, 디렉터리 스키마 (클래스 및 특성 정의), 디렉터리 구성 (사이트 및 복제 정보) 및 글로벌 카탈로그 (포리스트 전체 검색 기능)를 공유 하는 하나 이상의 Active Directory 도메인 컬렉션입니다. 동일한 포리스트의 도메인은 양방향 전이적 트러스트 관계와 자동으로 연결 됩니다.  
  
## <a name="active-directory-domain"></a>Active Directory 도메인  
도메인은 Active Directory 포리스트의 파티션입니다. 데이터를 분할 하면 조직에서 필요한 경우에만 데이터를 복제할 수 있습니다. 이러한 방식으로 디렉터리는 사용 가능한 대역폭이 제한 된 네트워크를 통해 전역적으로 확장 될 수 있습니다. 또한 도메인은 다음과 같은 관리와 관련 된 다양 한 핵심 기능을 지원 합니다.  
  
-   네트워크 차원의 사용자 id입니다. 도메인을 사용 하면 사용자 id를 한 번 만들고 도메인이 있는 포리스트에 가입 된 모든 컴퓨터에서 참조할 수 있습니다. 도메인을 구성 하는 도메인 컨트롤러는 사용자 계정 및 사용자 자격 증명 (예: 암호 또는 인증서)을 안전 하 게 저장 하는 데 사용 됩니다.  
  
-   인증: 도메인 컨트롤러는 사용자에 대 한 인증 서비스를 제공 하 고, 네트워크의 리소스에 대 한 액세스를 제어 하는 데 사용할 수 있는 사용자 그룹 멤버 자격과 같은 추가 권한 부여 데이터를 제공 합니다.  
  
-   트러스트 관계. 도메인은 트러스트를 사용 하 여 자체 포리스트 외부의 도메인에 있는 사용자로 인증 서비스를 확장할 수 있습니다.  
  
-   복제. 도메인은 도메인 서비스를 제공 하기에 충분 한 데이터를 포함 하는 디렉터리의 파티션을 정의한 다음 도메인 컨트롤러 간에 복제 합니다. 이러한 방식으로 모든 도메인 컨트롤러는 도메인의 피어 이며 하나의 단위로 관리 됩니다.  
  
## <a name="active-directory-organizational-units"></a>Active Directory 조직 구성 단위  
Ou는 도메인 내의 컨테이너 계층 구조를 구성 하는 데 사용할 수 있습니다. Ou는 그룹 정책 또는 권한 위임의 응용 프로그램과 같은 관리 목적으로 개체를 그룹화 하는 데 사용 됩니다. Ou와 ou에 있는 개체에 대 한 Acl (액세스 제어 목록)에 의해 결정 됩니다. 다 수의 개체 관리를 용이 하 게 하기 위해 AD DS는 권한 위임의 개념을 지원 합니다. 위임을 통해 소유자는 개체에 대 한 전체 또는 제한 된 관리 권한을 다른 사용자 또는 그룹으로 전송할 수 있습니다. 위임은 관리 작업을 수행 하는 데 신뢰할 수 있는 많은 사용자에 게 많은 개체의 관리를 분산 하는 데 도움이 되기 때문에 중요 합니다.  
  


