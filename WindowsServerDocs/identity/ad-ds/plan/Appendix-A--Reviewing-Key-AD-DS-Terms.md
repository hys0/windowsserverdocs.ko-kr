---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: 부록 A-주요 AD DS 용어 검토
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5434db4124c471c613f159dec28e27dee70e7086
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852024"
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>부록 a: 주요 AD DS 용어 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 용어는 Windows Server 2008 Active Directory Domain Services (AD DS)에 대 한 배포 프로세스에 관련이 있습니다.  
  
## <a name="active-directory-domain"></a>Active Directory 도메인  
관리 단위 관리 편의 위해 다음을 비롯 한 여러 기능을 그룹화 하는 컴퓨터 네트워크에:  
  
-   **네트워크 전체의 사용자 id**합니다. 도메인에서 사용자 id는 작성 한 번 및 도메인 위치한 포리스트에 연결 되는 모든 컴퓨터에서 참조 됩니다. 도메인을 구성 하는 도메인 컨트롤러 안전 하 게 사용자 계정 및 암호 또는 인증서와 같은 사용자 자격 증명을 저장 합니다.  
  
-   **인증**: 도메인 컨트롤러는 사용자에 대 한 인증 서비스를 제공합니다. 사용자 그룹 멤버 자격 등의 추가 권한 부여 데이터를 제공할 수도 있습니다. 관리자 이러한 서비스를 사용 하 여 네트워크의 리소스에 대 한 액세스를 제어할 수 있습니다.  
  
-   **트러스트 관계**합니다. 도메인 자동 양방향 트러스트를 사용 하 여 자신의 포리스트의 다른 도메인의 사용자에 게 인증 서비스를 확장 합니다. 도메인은도 수동으로 만든된 외부 트러스트 또는 포리스트 트러스트를 사용 하 여 다른 포리스트에 있는 도메인에서 사용자에 게 인증 서비스를 확장 합니다.  
  
-   **정책 관리**합니다. 도메인 암호 복잡성 및 암호 다시 사용 규칙 같은 관리 정책의 범위를입니다.  
  
-   **복제**. 도메인 파티션에 필요한 서비스를 제공 하는 데 적합 이며 도메인 컨트롤러 간에 복제 되는 데이터를 제공 하는 디렉터리 트리를 정의 합니다. 이러한 방식으로 모든 도메인 컨트롤러는 도메인의 피어 및 하나의 단위로 관리 되는 합니다.  
  
## <a name="active-directory-forest"></a>Active Directory 포리스트  
공통 논리 구조, 디렉터리 스키마에 네트워크 구성 뿐만 아니라 자동, 양방향 전이적 트러스트 관계를 공유 하는 하나 이상의 Active Directory 도메인의 컬렉션입니다. 각 포리스트는 디렉터리의 단일 인스턴스 및 보안 경계를 정의 합니다.  
  
## <a name="active-directory-functional-level"></a>Active Directory 기능 수준  
설정 하는 AD DS 고급 전체 도메인 또는 포리스트 전체 AD DS 기능을 사용할 수 있습니다.  
  
## <a name="migration"></a>마이그레이션  
원본 도메인에서 유지 하거나 새 도메인에 액세스할 수 있도록 하는 개체의 특성을 수정 하는 동안 대상 도메인에 개체를 이동 하는 프로세스입니다.  
  
## <a name="domain-restructure"></a>도메인 구조 변경  
마이그레이션 프로세스는 포리스트의 도메인 구조 변경 하는 방식입니다. 통합 또는 도메인의 추가 도메인 구조 변경 될 수 있습니다 하 고 포리스트 간에 또는 포리스트 내의 위치 걸릴 수 있습니다.  
  
## <a name="domain-consolidation"></a>도메인 통합  
다른 도메인의 콘텐츠를 사용 하 여 해당 콘텐츠를 병합 하 여 AD DS 도메인을 제거 하는 재구성 프로세스입니다.  
  
## <a name="domain-upgrade"></a>도메인 업그레이드  
도메인의 디렉터리 서비스 디렉터리 서비스의 최신 버전으로 업그레이드 하는 프로세스입니다. 모든 도메인 컨트롤러에서 운영 체제를 업그레이드 하 고 해당 하는 경우 AD DS 기능 수준을 올리는 포함 됩니다.  
  
## <a name="in-place-domain-upgrade"></a>전체 도메인 업그레이드  
예를 들어 지정된 된 된 도메인의 모든 도메인 컨트롤러의 운영 체제를 업그레이드, Windows Server 2008, Windows Server 2003 업그레이드 및 사용자와 같은 도메인 개체를 그대로 유지 하면서 해당 하는 경우 도메인 기능 수준은 발생 시키는 프로세스 및 그룹을 진행에서 합니다.  
  
## <a name="forest-root-domain"></a>포리스트 루트 도메인  
Active Directory 포리스트에서 만든 첫 번째 도메인. 이 도메인은 포리스트 루트 도메인으로 자동 지정 됩니다. Active Directory 포리스트 인프라에 대 한 기초를 제공합니다.  
  
## <a name="regional-domain"></a>지역 도메인  
복제 트래픽을 최적화 하는 지리적 영역에서 만든 자식 도메인입니다.  
  


