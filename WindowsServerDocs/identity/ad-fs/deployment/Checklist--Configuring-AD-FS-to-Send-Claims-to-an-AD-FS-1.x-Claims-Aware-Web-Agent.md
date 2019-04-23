---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: 페더레이션 서버 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32675aa7fb8c7b928bcf80a4d1072fe5eab7cd61
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864084"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>검사 목록: AD FS 1.x 클레임 인식 웹 에이전트에 대 한 클레임을 보내도록 AD FS를 구성 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-claims-aware-web-agent"></a>검사 목록: AD FS 1.x 클레임에 클레임을 보내도록 AD FS 구성\-인식 웹 에이전트  
이 검사 목록에는 Active Directory Federation Services를 구성 하는 데 필요한 작업이 포함 \(AD FS\) 에서 호스트 되는 응용 프로그램에서 인식할 수 있는 클레임을 보내도록 Windows Server 2012의 페더레이션 서비스는 웹 서버를 AD FS 1을 실행 합니다. *x* 클레임\-인식 웹 에이전트입니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
![클레임을 보내도록 AD FS 구성](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: AD FS 1.x 클레임에 클레임을 보내도록 AD FS 구성\-인식 웹 에이전트**  
  
||태스크|참조|  
|-|--------|-------------|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|Windows Server 2012의 AD FS 및 AD FS의 이전 버전 간의 상호 운용성 계획 하 고 클레임 유형 이름이 ID에 대 한 자세히 알아봅니다.|![클레임을 보내도록 AD FS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS와의 상호 운용성에 대 한 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|아직 수행 하는 경우는 Windows Server 2012에서 AD FS 페더레이션 서비스 및 AD FS 1 간에 신뢰 당사자 트러스트를 만들려면 먼저 오른쪽의 링크를 사용 합니다. *x* 페더레이션 서비스입니다.|[검사 목록: AD FS 1.x 페더레이션 서비스에 클레임을 보내도록 AD FS를 구성 합니다.](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|전에 AD FS 1에서 호스트 되는 응용 프로그램의 상호 운용성을 높일 수 있습니다. *x* 클레임\-인식 웹 에이전트를 먼저 만들어야 AD FS 페더레이션 서비스에서 신뢰 당사자 트러스트에 Windows Server 2012 AD FS 1에 있습니다. *x* 클레임\-인식 웹 에이전트입니다. **참고:** AD FS 페더레이션 서비스에이 트러스트를 만드는 것과 같습니다 새로 추가 하는 **응용 프로그램** AD fs 페더레이션 서비스 1.x \( **페더레이션 서비스\\트러스트 정책\\ 내 조직\\응용 프로그램**\)합니다. AD FS에 해당 하는 없기 때문에이 신뢰 당사자 트러스트는 필요한 **응용 프로그램** 노드 자체 스냅인에서\-에 있습니다. 그러나 여전히 있어야 응용 프로그램에 보안 채널입니다.<br /><br />오른쪽에 대 한 링크의 절차를 사용 하 여 트러스트를 설정한 경우에 신뢰 당사자 트러스트 추가 마법사는 AD FS 1와 상호 운용 하도록이 트러스트를 설정 하려면 다음을 수행 해야 합니다. *x* 클레임\-인식 웹 에이전트:<br /><br />1.  에 **데이터 원본 선택** 페이지에서 선택 **에서 신뢰 하는 방법에 대 한 데이터 입력 당사자 트러스트 수동으로**합니다.<br />2.  에 **프로필 선택** 페이지에서 **AD FS 1.0 및 1.1 프로필**합니다.<br />3.  에 **URL 구성** 페이지의 **WS\-페더레이션 수동 URL**, 형식 합니다 **응용 프로그램 URL** AD FS 1에에서 정의 된 대로. *x* 파트너의 페더레이션 서비스입니다.<br />4.  에 **식별자 구성** 페이지의 **신뢰 부분 신뢰 식별자**, 형식 합니다 **응용 프로그램 URL** AD FS 1에에서 정의 된 대로. *x* 클레임\-인식 웹 에이전트|![클레임을 보내도록 AD FS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[는 수동으로 신뢰 당사자 트러스트 만들기](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|AD FS 1을 실행 하는 웹 서버의 관리자에 게 문의 합니다. *x* 클레임\-인식 웹 에이전트와 클레임과 연결 된 web.config 파일을 편집 하는 관리자가\-인식 응용 프로그램 \(인터넷 정보의 기본 웹 사이트 아래의 서비스 \(IIS\) \) 웹 에이전트는 AD FS 페더레이션 서비스를 가리키도록 합니다.<br /><br />예를 들어 교체 *myresourcefederationserver* 태그에서 `<fs> https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>` 유효한 AD FS 페더레이션 서버 이름으로 web.config 파일의입니다.<br /><br />이 응용 프로그램 및 AD FS 1.x 클레임에 대 한 필요한\-인식 웹 에이전트를 Windows Server 2012의 AD FS 페더레이션 서비스에서 전송 된 클레임을 사용할 수 있습니다.|N\/A|  
|![클레임을 보내도록 AD FS 구성](media/icon_checkboxo.gif)|특성 저장소에서 추출 된 들어오는 클레임 하 고 통과, 필터링 하거나 이름 ID 클레임 유형을 이해 하 고에서 사용할 수 있는로 변환 하는 클레임 규칙을 만들 수 있는 이전에 만든 신뢰 당사자 트러스트에는 AD FS 1입니다. *x* 클레임\-인식 웹 에이전트입니다. **참고:** 이 규칙을 만들기 전에이 규칙을 만들려는 클레임 규칙 집합에 먼저 Lightweight Directory Access Protocol을 추출 하는 규칙이 있는지 확인 하십시오 \(LDAP\) 특성 저장소에서 특성 클레임입니다. 이 클레임을 AD FS 1 보내기 위해 만든 규칙에 대 한 입력으로 사용 됩니다. *x*\-호환 클레임입니다. LDAP 특성을 추출 하는 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [LDAP 특성을 클레임으로 보내기 위한 규칙을 만드는](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)합니다.|![클레임을 보내도록 AD FS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS를 보내도록 규칙을 만들 1.x 호환 클레임](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

