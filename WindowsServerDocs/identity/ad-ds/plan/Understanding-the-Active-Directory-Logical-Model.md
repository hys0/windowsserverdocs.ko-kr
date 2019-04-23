---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: Active Directory 논리 모델 이해
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e909d4e9c1fb26aa0f7cb97a7dc06192db5cc21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834274"
---
# <a name="understanding-the-active-directory-logical-model"></a>Active Directory 논리 모델 이해

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)에 대 한 논리 구조 디자인에서는 디렉터리의 컨테이너 간의 관계를 정의 합니다. 이러한 관계 권한 위임 등의 관리 요구 사항에 기반 할 수 있습니다 또는 복제를 제어 하는 등의 운영 요구 사항에 따라 정의 될 수 있습니다.  
  
Active Directory 논리 구조를 설계 하기 전에 Active Directory 논리 모델 이해 하는 것이 반드시 합니다. AD DS에 저장 하 고 디렉터리 사용 응용 프로그램에서 응용 프로그램별 데이터 뿐만 아니라 네트워크 리소스에 대 한 정보를 관리 하는 분산된 된 데이터베이스입니다. AD DS에는 계층적 포함 구조로 관리자를 요소 (예: 사용자, 컴퓨터 및 장치) 네트워크를 구성할 수 있습니다. 최상위 컨테이너인 포리스트입니다. 포리스트 내의 도메인 되며 도메인 내의 조직 구성 단위 (Ou). 이 인해 각 도메인 및 네트워크 토폴로지 내에서 필요한 도메인 컨트롤러 수와 같은 배포의 물리적 측면의 독립적 이기 때문에 논리적 모델을 호출 됩니다.  
  
## <a name="active-directory-forest"></a>Active Directory 포리스트  
포리스트 공통 논리 구조를 공유 하는 하나 이상의 Active Directory 도메인의 컬렉션인 경우 디렉터리 스키마 (클래스 및 특성 정의), 디렉터리 구성 (사이트 및 복제 정보) 및 글로벌 카탈로그 (포리스트 전체 검색 기능)입니다. 도메인이 동일한 포리스트에 양방향 전이적 트러스트 관계를 사용 하 여 자동으로 연결 됩니다.  
  
## <a name="active-directory-domain"></a>Active Directory 도메인  
도메인은 Active Directory 포리스트에서 파티션입니다. 데이터 분할 조직은 필요한 경우에 데이터를 복제할 수 있습니다. 이러한 방식으로 디렉터리는 사용 가능한 대역폭 제한 된 네트워크를 통해 전역으로 확장할 수 있습니다. 또한 도메인 지원 다른 코어의 수 등 관리와 관련 된 함수:  
  
-   네트워크 전체의 사용자 id입니다. 도메인은 사용자 id를 한 번 생성 되어 도메인 위치한 포리스트에 가입 된 컴퓨터에서 참조할 수 있습니다. 도메인을 구성 하는 도메인 컨트롤러는 사용자 계정 및 사용자 자격 증명 (예: 암호 또는 인증서)를 안전 하 게 저장 하는 데 사용 됩니다.  
  
-   인증 합니다. 도메인 컨트롤러는 사용자에 대 한 인증 서비스를 제공 하 고 네트워크의 리소스에 대 한 액세스 제어를 사용할 수 있는 사용자 그룹 멤버 자격 등의 추가 권한 부여 데이터를 제공 합니다.  
  
-   트러스트 관계입니다. 도메인은 트러스트를 사용 하 여 자신의 포리스트 외부 도메인의 사용자에 게 인증 서비스를 확장할 수 있습니다.  
  
-   복제 합니다. 도메인에 도메인 서비스를 제공 하도록 충분 한 데이터가 포함 되 고 다음 도메인 컨트롤러 간에 복제 하는 디렉터리의 파티션을 정의 합니다. 이러한 방식으로 모든 도메인 컨트롤러는 도메인의 피어 및 하나의 단위로 관리 됩니다.  
  
## <a name="active-directory-organizational-units"></a>Active Directory 조직 구성 단위  
Ou는 도메인 내에서 컨테이너의 계층 구조를 만드는 데 사용할 수 있습니다. Ou는 그룹 정책 적용 등 권한 위임을 관리 용도로 그룹 개체에 사용 됩니다. 제어 (OU 및 포함 된 개체) OU에 OU의 개체에 액세스 제어 목록 (Acl)에 의해 결정 됩니다. AD DS 개체의 많은 수의 관리를 용이 하 게 권한 위임의 개념을 지원 합니다. 위임을 통해 소유자는 다른 사용자 또는 그룹에 개체에 대해 전체 또는 제한 된 관리 권한의 전송할 수 있습니다. 관리 작업을 수행 하는 신뢰할 수 있는 사람들의 여러 개체의 많은 수의 관리를 배포할 수 있도록 위임은 중요 합니다.  
  


