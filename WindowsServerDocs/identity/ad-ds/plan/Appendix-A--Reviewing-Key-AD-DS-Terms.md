---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: "부록 A 주요 광고 DS 조건 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ce7c0b639ded498b15200dfd594b3f34d6492dce
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>부록 a: 주요 AD DS 조건을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 단어 서비스에 대 한 Windows Server 2008 Active Directory 도메인 (AD DS)는 배포 프로세스와 관련이 있습니다.  
  
## <a name="active-directory-domain"></a>Active Directory 도메인  
관리 단위 관리 편의 위해 다음과 같은 몇 가지 기능을 그룹화 하는 컴퓨터가 네트워크에 다음과 같습니다.  
  
-   **전체 네트워크 사용자 id**합니다. 도메인에 있는 사용자 id 한 번 만들고 수 도메인이 있는 숲에 가입 하는 컴퓨터에서 참조 합니다. 도메인 구성 하는 도메인 컨트롤러 안전 하 게 사용자 계정 및 암호 또는 인증서를 등 사용자 자격 증명을 저장 합니다.  
  
-   **인증**합니다. 도메인 컨트롤러 사용자를 위한 인증 서비스를 제공합니다. 추가 인증 데이터, 사용자 그룹 구성원 같은 제공할 수도 있습니다. 관리자는 네트워크 리소스에 대 한 액세스를 제어 이러한 서비스를 사용할 수 있습니다.  
  
-   **관계 신뢰**합니다. 도메인 자동 양방향 신뢰를 사용 하 여 자신의 숲 속의 다른 도메인에 있는 사용자에 게 인증 서비스를 확장 합니다. 또한 도메인 숲 신뢰 또는 외부 수동으로 만든된 신뢰를 사용 하 여 인증 서비스 다른 숲 도메인에 있는 사용자를 확장합니다.  
  
-   **정책 관리**합니다. 도메인은 다시 사용 규칙 암호 복잡성 및 암호와 같은 관리 정책의 범위.  
  
-   **복제**합니다. 도메인 정의 디렉터리 밤나무 필요한 서비스를 제공 하기 위해 적절 한 이며 도메인 컨트롤러 간에 복제 하는 데이터를 제공 하는 파티션의 합니다. 이런 방법이으로 모든 도메인 컨트롤러 피어 도메인에 되며 단위로 관리 합니다.  
  
## <a name="active-directory-forest"></a>Active Directory 숲  
일반적인 논리 구조, 디렉터리 스키마 네트워크 구성에서 뿐만 아니라 자동, 양방향, 전이 신뢰 관계를 공유 하는 하나 이상의 Active Directory 도메인의 수집 합니다. 각 숲 디렉터리의 단일 인스턴스 이며 보안 경계 정의 됩니다.  
  
## <a name="active-directory-functional-level"></a>Active Directory 기능 수준  
설정 하는 광고 DS 고급 도메인 전체 또는 숲 전체 광고 DS 기능을 사용할 수 있습니다.  
  
## <a name="migration"></a>마이그레이션  
하는 프로세스에 유지 하거나 새 도메인에 액세스할 수 있도록 개체의 특성을 수정 하는 동안 개체 소스 도메인 대상 도메인 이동 합니다.  
  
## <a name="domain-restructure"></a>도메인 재구성  
마이그레이션 프로세스는 숲 속의 도메인 구조 변경 하는 방식입니다. 도메인 재구성은 통합 또는 도메인, 추가 포함 될 수 하 고 숲 간에 또는 숲에 내 장소 걸릴 수 있습니다.  
  
## <a name="domain-consolidation"></a>도메인 통합  
다른 도메인의 내용으로 해당 내용을 병합 하 여 광고 DS 도메인을 제거 하는 재구성 프로세스입니다.  
  
## <a name="domain-upgrade"></a>도메인 업그레이드  
디렉터리 서비스의 최신 버전으로 업그레이드 하는 도메인의 디렉터리 서비스 프로세스입니다. 운영 체제 모든 도메인 컨트롤러에서 업그레이드 하 고 해당 AD DS 기능 수준 시키는 포함 됩니다.  
  
## <a name="in-place-domain-upgrade"></a>즉시 도메인 업그레이드  
예를 들어 해당된 도메인에 있는 모든 도메인 컨트롤러의 운영 체제를 업그레이드 한, Windows Server 2008, Windows Server 2003 업그레이드 및 장소에 사용자 및 그룹을 등의 도메인 개체를 않고도 해당 되는 경우는 도메인의 기능 수준 발생 프로세스입니다.  
  
## <a name="forest-root-domain"></a>이렇게  
첫 번째 하는 도메인의 Active Directory 숲 속의 만들어집니다. 이 도메인 숲 루트 도메인으로 자동으로 지정 됩니다. 기반 Active Directory 숲 인프라를 제공합니다.  
  
## <a name="regional-domain"></a>지역 도메인  
복제 교통 최적화 하기 위해 한 지역에서 생성 되는 자녀가 도메인.  
  


