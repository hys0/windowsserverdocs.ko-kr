---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: "Active Directory 논리 모델을 이해합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0f8cdc4789d1b3008f3b53104e5517d4ef1e65b9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="understanding-the-active-directory-logical-model"></a>Active Directory 논리 모델을 이해합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)에 대 한 논리 구조 디자인 디렉터리에 컨테이너 간의 관계 정의 포함 됩니다. 이러한 관계 기관, 위임 등 관리 요구 사항에 따라 될 수도 있습니다 또는 복제 제어 필요 등 작동 요구 사항에 따라 지정할 수 있습니다.  
  
Active Directory 논리 구조를 디자인 하기 전에는 Active Directory 논리 모델을 파악 하는 것이 중요 합니다. AD DS는 분산된 데이터베이스 저장 하 고 디렉터리 사용 응용 프로그램에서 특정 응용 프로그램 데이터 뿐만 아니라 네트워크 리소스에 대 한 정보를 관리 합니다. AD DS 계층 포함 구조도 구성 요소 (예: 사용자가, 컴퓨터 및 디바이스) 네트워크 관리자 수 있습니다. 최상위 컨테이너 숲입니다. 숲 내 도메인, 및 도메인 내 조직 (Ou). 이 각 도메인 및 네트워크 토폴로지에서 필요한 도메인 컨트롤러의 수와 같은 배포의 실제 측면 독립적인 있기 때문에 논리 모델을 라고 합니다.  
  
## <a name="active-directory-forest"></a>Active Directory 숲  
한 숲은 일반적인 논리 구조 공유 하는 하나 이상의 Active Directory 도메인 집합이 디렉터리 스키마 (클래스 및 특성 정의), 디렉터리 구성 (사이트와 복제 정보)와 드 (숲 검색 기능). 동일한 숲 속의 도메인 양방향, 전이 신뢰 관계를 자동으로 연결 됩니다.  
  
## <a name="active-directory-domain"></a>Active Directory 도메인  
도메인 된 Active Directory 숲 속의 파티션을입니다. 필요한 경우에 데이터 복제 수 있도록 데이터 분할 됩니다. 이런 방법이으로 디렉터리 대역폭이 제한 된 네트워크를 통해 전 세계 확장할 수 있습니다. 또한 도메인 지원 다양 한 다른 core 등 관리와 관련 된 기능:  
  
-   전체 네트워크 사용자 id 합니다. 도메인을 한 번 만들고 도메인이 있는 숲 연결 된 컴퓨터에서 참조 사용자 id를 허용 합니다. 도메인 구성 하는 도메인 컨트롤러 안전 하 게 사용자 계정 및 (예: 암호 또는 인증서) 사용자 자격 증명을 저장 하는 데 사용 합니다.  
  
-   인증 합니다. 도메인 컨트롤러 사용자를 위한 인증 서비스를 제공 및 네트워크 리소스에 대 한 액세스를 제어 하는 데 사용할 수 있는 사용자 그룹 구성원 같은 추가 인증 데이터를 제공 합니다.  
  
-   관계 신뢰 합니다. 도메인 신뢰를 사용 하 여 자신의 숲 밖에 도메인에 있는 사용자에 게 인증 서비스를 확장할 수 있습니다.  
  
-   복제 합니다. 도메인은 도메인 서비스를 제공 하기 위해 충분 한 데이터가 포함 된 후 도메인 컨트롤러 사이 복제 디렉터리의 파티션을 정의 됩니다. 이런 방법으로 모든 도메인 컨트롤러 피어 도메인에 되며는 하나의 단위로 관리 합니다.  
  
## <a name="active-directory-organizational-units"></a>Active Directory 조직  
Ou는 도메인 내 컨테이너 계층을 사용할 수 있습니다. Ou 개체를 그룹화 기관의 위임 그룹 정책 응용 프로그램 등 관리를 위해 사용 됩니다. (OU 및 제어 포함 된 개체)는 액세스 제어 (Acl 목록) OU의 개체와 OU에서에 따라 결정 됩니다. 많은 수의 개체 관리를 위해 AD DS 위임 기관의 개념을 지원 합니다. 소유자 위임을 사용 하 여 다른 사용자 또는 그룹에 개체 대 한 전체 또는 제한 된 관리 제어를 전송할 수 있습니다. 신뢰할 수 있는 관리 작업을 수행 하는 사람들의 숫자를 통해 많은 수의 개체의 관리를 배포 하는 데 도움이 되므로 위임이 중요 합니다.  
  


