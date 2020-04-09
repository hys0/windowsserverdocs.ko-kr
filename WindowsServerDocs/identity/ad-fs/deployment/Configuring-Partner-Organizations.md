---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: 파트너 조직 구성
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ac83d9754365f3ceea5b363af4df93862bdb59e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855496"
---
# <a name="configuring-partner-organizations"></a>파트너 조직 구성

Active Directory Federation Services \(AD FS\)에 새 파트너 조직을 배포 하려면 AD FS 설계에 따라 [검사 목록: 리소스 파트너 조직 구성](Checklist--Configuring-the-Resource-Partner-Organization.md) 또는 [검사 목록: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)의 작업을 완료 합니다.  
  
> [!NOTE]  
> 이러한 검사 목록 중 하나를 사용 하는 경우 새 파트너 조직을 설정 하기 위한 절차를 계속 하기 전에 먼저 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 에서 계정 파트너 또는 리소스 파트너 계획 지침에 대 한 참조를 읽어 보는 것이 좋습니다. 이러한 방식으로 검사 목록을 따라 하면 계정 파트너 또는 리소스 파트너 조직에 대 한 전체 AD FS 설계 및 배포 스토리를 보다 잘 이해할 수 있습니다.  
  
## <a name="about-account-partner-organizations"></a>계정 파트너 조직 정보  
계정 파트너는 AD FS – 지원 되는 특성 저장소에 사용자 계정을 실제로 저장 하는 페더레이션 트러스트 관계의 조직입니다. 계정 파트너는 사용자의 자격 증명을 수집 및 인증 하 고, 해당 사용자에 대 한 클레임을 작성 하 고, 보안 토큰에 클레임을 패키징하는 일을 담당 합니다. 그러면 페더레이션 트러스트를 통해 이러한 토큰을 제공 하 여 리소스 파트너 조직에 있는 웹\-기반 리소스에 액세스할 수 있습니다.  
  
즉, 계정 파트너는 계정\-쪽 페더레이션 서버에서 보안 토큰을 발급 하는 사용자의 조직을 나타냅니다. 계정 파트너 조직의 페더레이션 서버는 로컬 사용자를 인증 하 고 리소스 파트너가 권한 부여 결정을 내리는 데 사용 하는 보안 토큰을 만듭니다.  
  
특성 저장소와 관련 하 여 AD FS의 계정 파트너는 개념적으로 다른 포리스트에 있는 리소스에 대 한 액세스 권한이 필요한 단일 Active Directory 포리스트와 개념적으로 동일 합니다. 이 포리스트의 계정은 두 포리스트 간에 외부 트러스트 또는 포리스트 트러스트 관계가 존재 하는 경우와 사용자가 액세스 하려고 하는 리소스가 적절 한 권한 부여 권한으로 설정 된 경우에만 리소스 포리스트의 리소스에 액세스할 수 있습니다.  
  
## <a name="about-resource-partner-organizations"></a>리소스 파트너 조직 정보  
리소스 파트너는 웹 서버가 있는 AD FS 배포의 조직입니다. 리소스 파트너는 계정 파트너를 신뢰 하 여 사용자를 인증 합니다. 따라서 권한 부여 결정을 내리기 위해 리소스 파트너는 계정 파트너의 사용자가 제공 하는 보안 토큰에 패키지 된 클레임을 사용 합니다.  
  
즉, 리소스 파트너는 리소스\-쪽 페더레이션 서버에서 웹 서버를 보호 하 고 있는 조직을 나타냅니다. 리소스 파트너의 페더레이션 서버는 계정 파트너에 의해 생성 된 보안 토큰을 사용 하 여 리소스 파트너의 웹 서버에 대 한 권한 부여 결정을 내립니다.  
  
AD FS 리소스 역할을 하려면 리소스 파트너 조직의 웹 서버에 Windows Identity Foundation \(WIF\) 설치 되어 있어야 합니다. 그렇지 않으면 Active Directory Federation Services \(AD FS\) 인식 웹 에이전트 역할 서비스를 설치 해야 합니다.\- AD FS 리소스 역할을 하는 웹 서버는 웹\-browser\-기반 또는 웹\-service\-기반 응용 프로그램을 호스트할 수 있습니다.  
