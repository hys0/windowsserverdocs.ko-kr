---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: 부록 A-주요 AD DS 용어 검토
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ad8c1cf769c0c2a22e2d55f7bd2d111095410afe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822866"
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>부록 A: 주요 AD DS 용어 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음은 Windows Server 2008 Active Directory Domain Services (AD DS) 배포 프로세스와 관련 된 용어입니다.  
  
## <a name="active-directory-domain"></a>Active Directory 도메인  
관리 편의성을 위해 다음을 비롯 한 여러 기능을 그룹화 하는 컴퓨터 네트워크의 관리 단위입니다.  
  
-   **네트워크 차원의 사용자 id**입니다. 도메인에서 사용자 id를 한 번 만든 다음 도메인이 있는 포리스트에 가입 된 모든 컴퓨터에서 참조할 수 있습니다. 도메인을 구성 하는 도메인 컨트롤러는 사용자 계정 및 사용자 자격 증명 (예: 암호 또는 인증서)을 안전 하 게 저장 합니다.  
  
-   **인증**: 도메인 컨트롤러는 사용자에 대 한 인증 서비스를 제공 합니다. 또한 사용자 그룹 멤버 자격과 같은 추가 권한 부여 데이터를 제공 합니다. 관리자는 이러한 서비스를 사용 하 여 네트워크에 있는 리소스에 대 한 액세스를 제어할 수 있습니다.  
  
-   **트러스트 관계**. 도메인은 자동 양방향 트러스트를 사용 하 여 자체 포리스트의 다른 도메인에 있는 사용자로 인증 서비스를 확장 합니다. 또한 도메인은 포리스트 트러스트 또는 수동으로 만든 외부 트러스트를 통해 다른 포리스트에 있는 도메인의 사용자로 인증 서비스를 확장 합니다.  
  
-   **정책 관리**. 도메인은 암호 복잡성 및 암호 재사용 규칙과 같은 관리 정책의 범위입니다.  
  
-   **복제**. 도메인은 필요한 서비스를 제공 하기에 적합 하 고 도메인 컨트롤러 간에 복제 되는 데이터를 제공 하는 디렉터리 트리의 파티션을 정의 합니다. 이러한 방식으로 모든 도메인 컨트롤러는 도메인의 피어 이며 하나의 단위로 관리 됩니다.  
  
## <a name="active-directory-forest"></a>Active Directory 포리스트  
공통 논리 구조, 디렉터리 스키마 및 네트워크 구성 뿐 아니라 자동, 양방향 전이적 트러스트 관계를 공유 하는 하나 이상의 Active Directory 도메인 컬렉션입니다. 각 포리스트는 디렉터리의 단일 인스턴스이며 보안 경계를 정의 합니다.  
  
## <a name="active-directory-functional-level"></a>Active Directory 기능 수준  
고급 도메인 전체 또는 포리스트 전체 AD DS 기능을 사용 하도록 설정 하는 AD DS 설정입니다.  
  
## <a name="migration"></a>마이그레이션  
개체를 원본 도메인에서 대상 도메인으로 이동 하는 동시에 개체의 특징을 유지 하거나 수정 하 여 새 도메인에서 액세스할 수 있도록 하는 프로세스입니다.  
  
## <a name="domain-restructure"></a>도메인 재구성  
포리스트의 도메인 구조 변경을 포함 하는 마이그레이션 프로세스입니다. 도메인 재구성은 도메인의 통합 또는 추가를 포함할 수 있으며 포리스트 또는 포리스트 내에서 수행 될 수 있습니다.  
  
## <a name="domain-consolidation"></a>도메인 통합  
콘텐츠를 다른 도메인의 내용과 병합 하 여 AD DS 도메인 제거를 포함 하는 구조 변경 프로세스입니다.  
  
## <a name="domain-upgrade"></a>도메인 업그레이드  
도메인의 디렉터리 서비스를 디렉터리 서비스의 이후 버전으로 업그레이드 하는 프로세스입니다. 여기에는 모든 도메인 컨트롤러에서 운영 체제를 업그레이드 하 고 해당 되는 경우 AD DS 기능 수준을 올리는 작업이 포함 됩니다.  
  
## <a name="in-place-domain-upgrade"></a>내부 도메인 업그레이드  
지정 된 도메인에 있는 모든 도메인 컨트롤러의 운영 체제를 업그레이드 하는 프로세스입니다. 예를 들어 Windows Server 2003을 Windows Server 2008로 업그레이드 하 고 도메인의 기능 수준 (해당 하는 경우)을 발생 시키고, 도메인 개체 (예: 사용자 및 그룹)는 그대로 둡니다.  
  
## <a name="forest-root-domain"></a>포리스트 루트 도메인  
Active Directory 포리스트에서 만든 첫 번째 도메인입니다. 이 도메인은 자동으로 포리스트 루트 도메인으로 지정 됩니다. Active Directory 포리스트 인프라의 토대를 제공 합니다.  
  
## <a name="regional-domain"></a>지역 도메인  
복제 트래픽을 최적화 하기 위해 지리적 지역에 생성 되는 자식 도메인입니다.  
  


