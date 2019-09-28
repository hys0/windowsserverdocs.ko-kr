---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: 검사 목록-1. x AD FS에서 클레임을 사용 하도록 AD FS 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1c952abc0bca5eadbfc14f3eda54d05826d50294
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408484"
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>검사 목록: AD FS 1.x에서 클레임을 사용 하도록 AD FS 구성

  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-adfs1x"></a>검사 목록: AD FS 1.x에서 클레임을 사용 하도록 AD FS 구성  
이 검사 목록에는 AD FS 1에서 전송 하는 클레임을 사용 하기 위해 Windows Server 2012의 Active Directory Federation Services \(AD FS @ no__t-1 페더레이션 서비스를 구성 하는 데 필요한 작업이 포함 되어 있습니다. *x* 페더레이션 서비스입니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
@no__t-AD FS @ no__t 검사 목록에서 클레임을 사용 합니다. AD FS 1. x @ no__t에서 클레임을 사용 하도록 AD FS 구성  
  
||태스크|참조|  
|-|--------|-------------|  
|![AD FS에서 클레임을 사용합니다](media/icon_checkboxo.gif)|Windows Server 2012의 AD FS와 이전 버전의 AD FS에 대 한 상호 운용성을 계획 하 고 이름 ID 클레임 유형에 대해 자세히 알아보세요.|![ AD FS 1.x와의](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[상호 운용성에 대 한 AD FS 계획](https://technet.microsoft.com/library/ff678040.aspx) 의 클레임을 사용 합니다.|  
|![AD FS에서 클레임을 사용합니다](media/icon_checkboxo.gif)|이전 버전의 AD FS와 상호 운용 하려면 먼저 AD FS 페더레이션 서비스에서 클레임 공급자 트러스트를 만들어야 합니다. **참고:** AD FS 1을 사용 하 여 트러스트를 만들 수 없습니다. *x* 페더레이션 서비스 페더레이션 메타 데이터를 사용 합니다.<br /><br />오른쪽 링크의 절차를 사용 하 여 트러스트를 설정 하는 경우 클레임 공급자 트러스트 추가 마법사에서 다음을 수행 하 여 AD FS 1과 상호 운용 하도록이 트러스트를 설정 해야 합니다. *x* 페더레이션 서비스:<br /><br />1.  에 **데이터 원본 선택** 페이지에서 선택 **에서 신뢰 하는 방법에 대 한 데이터 입력 당사자 트러스트 수동으로**합니다.<br />2.  에 **프로필 선택** 페이지에서 **AD FS 1.0 및 1.1 프로필**합니다.<br />3.  **URL 구성** 페이지에서 **WS @ No__t-2federation Passive URL**아래에 AD FS 1에 정의 된 대로 **페더레이션 서비스 끝점 URL** 을 입력 합니다. 파트너의 *x* 페더레이션 서비스입니다.<br />4.  **식별자 구성** 페이지의 **클레임 공급자 트러스트 식별자**아래에 AD FS 1에 정의 된 대로 **페더레이션 서비스 URI** 를 입력 합니다. 파트너의 *x* 페더레이션 서비스입니다.|![에서 클레임을 사용](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[하 AD FS 클레임 공급자 트러스트를 수동으로 만듭니다](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md) .|  
|![AD FS에서 클레임을 사용합니다](media/icon_checkboxo.gif)|이전에 만든 클레임 공급자 트러스트에서 AD FS 1.x 페더레이션 서비스에서 들어오는 클레임을 가져와 이름 ID 클레임 유형으로 전달, 필터링 또는 변환 하는 클레임 규칙을 만들어야 합니다.<br /><br />이름 ID 클레임 유형이 필터링 또는 변환를 통해 전달 된 경우 사용할 수 있습니다 다른 규칙 또는 규칙에 대 한 입력으로 이해 및 Windows Server 2012의 AD FS 페더레이션 서비스에서 사용할 수 있도록 합니다.|@no__t에서 클레임을 사용 하 AD FS에서 클레임을 사용](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[하 여 AD FS 1. x 호환 클레임을 보내는 규칙을 만듭니다.](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![AD FS에서 클레임을 사용합니다](media/icon_checkboxo.gif)|AD FS 1의 관리자에 게 문의 하십시오. *x* 페더레이션 서비스 AD FS 1의 관리자가 있어야 합니다. *x* 페더레이션 서비스 새 리소스 파트너 트러스트를 설정 합니다. 또한 해당 관리자의 페더레이션 서비스 URI에 제공 \(페더레이션 서비스 속성에\), 페더레이션 서비스 끝점 URL 및 내보낸된 토큰\-서명 인증서 파일 \(공개 키만로\)합니다. 관리자가 이러한 항목이 트러스트를 설정 해야 합니다.|N\/A|  
  

