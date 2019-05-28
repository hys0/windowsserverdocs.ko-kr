---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: 파트너 조직 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3d7389ce806a5e3aebf4fe166b10e5262df0be8a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192241"
---
# <a name="configuring-partner-organizations"></a>파트너 조직 구성

Active Directory Federation Services에서 새 파트너 조직 배포할 \(AD FS\)에서 작업을 완료 [검사 목록: Configuring the Resource Partner Organization](Checklist--Configuring-the-Resource-Partner-Organization.md) 또는 [검사 목록: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)AD FS 디자인에 따라 합니다.  
  
> [!NOTE]  
> 이러한 검사 목록 중 하나를 사용 하는 경우 좋습니다 계정 파트너나 리소스 파트너에 대 한 지침 계획에 대 한 참조를 먼저 확인 하는 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 을 계속 하기 전에 새 파트너 조직을 설정 하기 위한 절차입니다. 이러한 방식으로 검사를 다음 계정 파트너나 리소스 파트너 조직에 대 한 모든 AD FS 디자인 및 배포 정보를 더 잘 이해를 제공 하는 데 도움이 됩니다.  
  
## <a name="about-account-partner-organizations"></a>계정 파트너 조직에 대 한  
계정 파트너 조직의 AD FS – 지원 되는 특성 저장소에 사용자 계정을 실제로 저장 하는 페더레이션 트러스트 관계의 경우 계정 파트너를 수집 및 사용자의 자격 증명을 인증 하 고, 해당 사용자에 대 한 클레임을 구축 하 고 보안 토큰에 클레임을 패키징 담당 합니다. 이러한 토큰은 웹에 액세스할 수 있도록 페더레이션 트러스트를 통해 제시 될 수 있습니다\-리소스 파트너 조직에 있는 리소스를 기반으로 합니다.  
  
즉, 계정 파트너 조직을 나타냅니다. 사용자에 대해 계정\-쪽 페더레이션 서버는 보안 토큰을 발급 합니다. 계정 파트너 조직의 페더레이션 서버는 로컬 사용자를 인증 하 고 권한 부여 결정을 내리는 리소스 파트너를 사용 하는 보안 토큰을 만듭니다.  
  
특성 저장소와 관련 하 여 AD FS의 계정 파트너는 물리적으로 다른 포리스트에 있는 리소스에 대 한 액세스를 해야 하는 계정이 Active Directory 포리스트가 개념적와 같습니다. 이 포리스트의 계정에에서는 외부 트러스트 또는 포리스트 트러스트 두 포리스트 간에 관계가 존재 하 고 적절 한 권한 부여를 사용 하 여 사용자 액세스를 시도 하는 리소스를 설정한 경우에 리소스 포리스트의 리소스에 액세스할 수 있습니다. 사용 권한입니다.  
  
## <a name="about-resource-partner-organizations"></a>리소스 파트너 조직에 대 한  
리소스 파트너는 웹 서버가 있는 AD FS 배포에는 조직입니다. 리소스 파트너 사용자를 인증 하는 계정 파트너를 신뢰 합니다. 따라서 권한 부여 결정을 리소스 파트너는 계정 파트너의 사용자에 게 제공 되는 보안 토큰에 패키지 된 클레임을 사용 합니다.  
  
리소스 파트너 리소스에서 해당 웹 서버를 보호 하는 조직을 나타냅니다. 즉,\-쪽 페더레이션 서버입니다. 리소스 파트너 페더레이션 서버는 계정 파트너 리소스 파트너에 웹 서버에 대 한 권한 부여 결정에 의해 생성 되는 보안 토큰을 사용 합니다.  
  
AD FS 리소스로 작동 하려면 리소스 파트너 조직의 웹 서버 있어야 Windows Identity Foundation \(WIF\) 설치 되어 있거나 Active Directory Federation Services \(AD FS\) 1.x 클레임\-인식 웹 에이전트 역할 서비스를 설치 합니다. 웹 서버는 AD FS 리소스 하거나 웹을 호스트할 수 있습니다 하는 대로 작동\-브라우저\-기반 또는 웹\-서비스\-기반 응용 프로그램입니다.  
