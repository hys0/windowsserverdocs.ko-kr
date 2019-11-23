---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: 검사 목록-1. x AD FS에서 클레임을 사용 하도록 AD FS 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f91944333da9ce4c1d78bbbf7b3652f1118e1f08
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408493"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>검사 목록: AD FS 1.x 페더레이션 서비스에 대한 클레임을 보내도록 AD FS 구성

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>검사 목록: AD FS 1.x 페더레이션 서비스 클레임을 보내도록 AD FS 구성  
이 검사 목록에는 페더레이션 서비스 1에서 이해할 수 있는 클레임을 전송 하기 위해 Windows Server 2012\) AD FS AD FS Active Directory Federation Services \(를 구성 하는 데 필요한 작업이 포함 되어 있습니다. *x* 페더레이션 서비스입니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
클레임을 보내도록 AD FS 구성 ![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: AD FS 1.x에 클레임을 보내도록 AD FS 구성 페더레이션 서비스**  
  
||태스크|참고자료|  
|-|--------|-------------|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|Windows Server 2012의 AD FS와 이전 버전의 AD FS에 대 한 상호 운용성을 계획 하 고 이름 ID 클레임 유형에 대해 자세히 알아보세요.|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x와의 상호 운용성을 위한 클레임 계획](https://technet.microsoft.com/library/ff678040.aspx) 을 보내도록 AD FS 구성 ![|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|이전 버전의 AD FS와의 상호 운용성을 실현 하려면 먼저 AD FS 1에 페더레이션 서비스 AD FS에서 신뢰 당사자 트러스트를 만들어야 합니다. *x* 페더레이션 서비스입니다. **참고:** AD FS 1을 사용 하 여 트러스트를 만들 수 없습니다. *x* 페더레이션 서비스 페더레이션 메타 데이터를 사용 합니다.<br /><br />오른쪽 링크의 절차를 사용 하 여 트러스트를 설정 하는 경우 신뢰 당사자 트러스트 추가 마법사에서 다음을 수행 하 여 AD FS 1과 상호 운용 하도록이 트러스트를 설정 해야 합니다. *x* 페더레이션 서비스:<br /><br />1. **데이터 원본 선택** 페이지에서 **신뢰 당사자 트러스트에 대 한 데이터를 수동으로 입력**을 선택 합니다.<br />2. **프로필 선택** 페이지에서 **AD FS 1.0 및 1.1 프로필**을 선택 합니다.<br />3. **URL 구성** 페이지의 **WS\-페더레이션 수동 URL**아래에서 AD FS 1에 정의 된 **페더레이션 서비스 끝점 URL** 을 입력 합니다. 파트너의 *x* 페더레이션 서비스입니다.<br />4. **식별자 구성** 페이지의 **신뢰 부분 신뢰 식별자**에 AD FS 1에 정의 된 대로 **페더레이션 서비스 URI** 를 입력 합니다. 파트너의 *x* 페더레이션 서비스입니다.|클레임을 보내도록 AD FS 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[신뢰 당사자 트러스트를 수동으로 만듭니다](../../ad-fs/operations/Create-a-Relying-Party-Trust.md) .|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|이전에 만든 신뢰 당사자 트러스트에서 특성 저장소에서 추출 된 들어오는 클레임을 사용 하 여 AD FS 1에서 이해 하 고 사용할 수 있는 이름 ID 클레임 형식으로 전달, 필터링 또는 변환 하는 클레임 규칙을 만들어야 합니다. *x* 페더레이션 서비스입니다. **참고:** 이 규칙을 만들기 전에이 규칙을 만들려는 클레임 규칙 집합에 먼저 Lightweight Directory Access Protocol을 추출 하는 그 앞에 오는 하는 규칙이 있는지 확인 \(LDAP\) 특성 저장소에서 특성 클레임입니다. 이 클레임은 AD FS 1을 보내기 위해 만든 규칙의 입력으로 사용 됩니다. *x*\-호환 클레임입니다. LDAP 특성을 추출 하는 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [LDAP 특성을 클레임으로 보내기 위한 규칙을 만드는](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)합니다.|클레임을 보내도록 AD FS 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.X 호환 클레임을 보내는 규칙을 만듭니다.](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|AD FS 1의 관리자에 게 문의 하십시오. *x* 페더레이션 서비스 AD FS 1의 관리자가 있어야 합니다. *x* 페더레이션 서비스 새 계정 파트너 트러스트를 설정 합니다. 또한 해당 관리자의 페더레이션 서비스 URI에 제공 \(페더레이션 서비스 속성에\), WS\-페더레이션 수동 끝점 URL \(페더레이션 서비스 끝점 URL\), 및 내보낸된 토큰\-서명 인증서 파일 \(공개 키만로\)합니다. 해당 관리자가 이러한 항목을 트러스트를 설정 해야 합니다.|N\/A|  
  

