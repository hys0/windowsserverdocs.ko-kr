---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: 검사 목록-AD FS에서 클레임을 사용 하도록 AD FS 구성 1.x
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bd4c436c806074f63bf51f497429532d7be32f75
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192409"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>검사 목록: AD FS 1.x 페더레이션 서비스에 클레임을 보내도록 AD FS를 구성 합니다.

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>검사 목록: AD FS에 대 한 클레임을 보내도록 AD FS 구성 1.x 페더레이션 서비스  
이 검사 목록에는 Active Directory Federation Services를 구성 하는 데 필요한 작업이 포함 \(AD FS\) AD FS 1에서 인식할 수 있는 클레임을 보내도록 Windows Server 2012의 페더레이션 서비스. *x* 페더레이션 서비스입니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
![클레임을 보내도록 AD FS 구성](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: AD FS에 대 한 클레임을 보내도록 AD FS 구성 1.x 페더레이션 서비스**  
  
||태스크|참조|  
|-|--------|-------------|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|Windows Server 2012의 AD FS 및 AD FS의 이전 버전 간의 상호 운용성 계획 하 고 클레임 유형 이름이 ID에 대 한 자세히 알아봅니다.|![클레임을 보내도록 AD FS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS와의 상호 운용성에 대 한 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|이전 버전의 AD FS와의 상호 운용성을 실현 하기 전에 AD FS 1에 AD FS 페더레이션 서비스에서 신뢰 당사자 트러스트를 먼저 만들어야 합니다. *x* 페더레이션 서비스입니다. **참고:** AD FS 1 트러스트를 만들 수 없습니다. *x* 페더레이션 메타 데이터를 사용 하 여 페더레이션 서비스입니다.<br /><br />오른쪽에 대 한 링크의 절차를 사용 하 여 트러스트를 설정한 경우에 신뢰 당사자 트러스트 추가 마법사는 AD FS 1와 상호 운용 하도록이 트러스트를 설정 하려면 다음을 수행 해야 합니다. *x* 페더레이션 서비스:<br /><br />1.  에 **데이터 원본 선택** 페이지에서 선택 **에서 신뢰 하는 방법에 대 한 데이터 입력 당사자 트러스트 수동으로**합니다.<br />2.  에 **프로필 선택** 페이지에서 **AD FS 1.0 및 1.1 프로필**합니다.<br />3.  에 **URL 구성** 페이지의 **WS\-페더레이션 수동 URL**, 형식 합니다 **페더레이션 서비스 끝점 URL** AD FS 1에에서 정의 된 대로. *x* 파트너의 페더레이션 서비스입니다.<br />4.  에 **식별자 구성** 페이지의 **신뢰 부분 신뢰 식별자**, 형식 합니다 **페더레이션 서비스 URI** AD FS 1에에서 정의 된 대로. *x* 파트너의 페더레이션 서비스입니다.|![클레임을 보내도록 AD FS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[는 수동으로 신뢰 당사자 트러스트 만들기](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|클레임은 특성 저장소에서 추출 된 들어오는 클레임을 통과, 필터링 또는 이름이 ID로 변환 하는 규칙 클레임 유형을 이해 하 고 AD에서 사용할 수 있는 이전에 만든 신뢰 당사자 트러스트에서 만들어야 FS 1입니다. *x* 페더레이션 서비스입니다. **참고:** 이 규칙을 만들기 전에이 규칙을 만들려는 클레임 규칙 집합에 먼저 Lightweight Directory Access Protocol을 추출 하는 규칙이 있는지 확인 하십시오 \(LDAP\) 특성 저장소에서 특성 클레임입니다. 이 클레임을 AD FS 1 보내기 위해 만든 규칙에 대 한 입력으로 사용 됩니다. *x*\-호환 클레임입니다. LDAP 특성을 추출 하는 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [LDAP 특성을 클레임으로 보내기 위한 규칙을 만드는](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)합니다.|![클레임을 보내도록 AD FS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS를 보내도록 규칙을 만들 1.x 호환 클레임](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|AD FS 1의 관리자에 게 문의 합니다. *x* 페더레이션 서비스 및 AD FS 1의 관리자가. *x* 페더레이션 서비스가 새 계정 파트너 트러스트를 설정 합니다. 또한 해당 관리자의 페더레이션 서비스 URI에 제공 \(페더레이션 서비스 속성에\), WS\-페더레이션 수동 끝점 URL \(페더레이션 서비스 끝점 URL\), 및 내보낸된 토큰\-서명 인증서 파일 \(공개 키만로\)합니다. 해당 관리자가 이러한 항목을 트러스트를 설정 해야 합니다.|N\/A|  
  

