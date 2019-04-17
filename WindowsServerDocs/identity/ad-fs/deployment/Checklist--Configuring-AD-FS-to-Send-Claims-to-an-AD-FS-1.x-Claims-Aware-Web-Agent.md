---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: "Federation 서버를 배포"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32675aa7fb8c7b928bcf80a4d1072fe5eab7cd61
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>구성 클레임은 ADFS 1.x 클레임 인식 웹 에이전트를 보내려면 ADFS 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>구성 클레임 ADFS 1.x claims\ 인식 웹 에이전트를 보내려면 ADFS 검사:  
이 검사는 Windows Server 2012 ADFS 1 실행 하는 웹 서버에서 호스트 하는 응용 프로그램에 의해 인식할 수 있는 클레임 보낼 수의 Active Directory Federation Services \(AD FS\) Federation 서비스 구성 하는 데 필요한는 작업이 포함 됩니다. *x* claims\ 인식 웹 에이전트 합니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![클레임 보내려면 ADFS 구성](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 클레임 ADFS 1.x claims\ 인식 웹 에이전트를 보내려면 ADFS 구성**  
  
||작업|참조|  
|-|--------|-------------|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|Adfs의 이전 버전의 Windows Server 2012 ADFS 간의 상호 운용성 계획 하 고 클레임 유형 이름 ID 대 한 자세한 내용을 알아보세요.|![클레임 보내려면 ADFS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 상호 운용성 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|이미 완료 하는 경우 링크를 통해 오른쪽 먼저 ADFS 1과 Windows Server 2012에서 ADFS Federation 서비스 신뢰 파티 신뢰를 만듭니다. *x* Federation 서비스입니다.|[구성 클레임은 ADFS 1.x Federation 서비스에 전송 ADFS 검사:](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|이전 ADFS 1 하 여 호스팅된 응용 프로그램과 상호 작용을 얻을 수 있습니다. *x* claims\ 인식 웹 에이전트 먼저 만들어야 ADFS Federation 서비스에서 신뢰 파티 신뢰 ADFS 1 Windows Server 2012에서 합니다. *x* claims\ 인식 웹 에이전트 합니다. **참고:** 이 신뢰 ADFS Federation 서비스를 작성 하는 새 추가 **응용 프로그램** 하 고 ADFS 1.x Federation 서비스 \ (**Federation Service\\Trust Policy\\My Organization\\Application**\). ADFS 해당 없기 때문에이 신뢰 파티 신뢰 필요는 **응용 프로그램** 노드 snap\에는 자체에 있습니다. 그러나 여전히 있어야 보안 채널 응용 프로그램을 합니다.<br /><br />절차를 사용 하 여 오른쪽에 있는 링크를 신뢰를 설정할 때 추가 의존 파티 신뢰 마법사에서 ADFS 1와 상호 작용 하려면이 신뢰를 설정 하려면 다음을 수행 해야 합니다. *x* claims\ 인식 웹 에이전트:<br /><br />1.에 **데이터 소스를 선택** 페이지 선택, **Enter 데이터의 사용에 대 한 보안을 수동으로 파티**합니다.<br />2.에 **프로필 선택** 페이지를 선택 하 고 **ADFS 1.0 및 1.1 프로필**합니다.<br />3.에 **구성 URL** 페이지의 **WS\ Federation 수동 URL**, 종류의 **응용 프로그램 URL** ADFS 1에에서 정의 된 대로 합니다. *x* 파트너의 서비스 Federation 합니다.<br />4.에 **구성 식별자** 페이지의 **Relying 일부 신뢰 식별자**, 입력은 **응용 프로그램 URL** ADFS 1에에서 정의 된 대로 합니다. *x* claims\ 인식 웹 에이전트|![클레임 보내려면 ADFS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[필요로 하 파티 신뢰 수동으로 만들](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|관리자 ADFS 1 실행 하는 웹 서버에 게 문의 합니다. *x* 인식 claims\ 에이전트 웹와 관련 된 claims\ 인식 응용 프로그램 토큰과 편집 관리자에 게 해당 \ (인터넷 정보 서비스 \(IIS\)\) 지점 웹 에이전트 ADFS Federation 서비스에에서 기본 웹 사이트 아래에서.<br /><br />예를 들어 교체 *myresourcefederationserver* 태그에 `<fs>https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>`유효한 ADFS federation 서버 이름으로 토큰과의 합니다.<br /><br />이 필요한 응용 프로그램 및 ADFS 1.x claims\ 인식 웹 에이전트 Windows Server 2012에서 ADFS Federation 서비스에서 전송 클레임을 사용할 수 있습니다.|N\/A|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|이전에 만든 신뢰 파티 신뢰에서 클레임 특성 스토어에서 추출 된 들어오는 클레임 수행 하 고 통과, 필터링 되거나 이름 ID로 변환는 규칙 주장 유형을 이해 하 고 AD에서 사용할 수 있는 만들 필요가 FS 1. *x* claims\ 인식 웹 에이전트 합니다. **참고:** 이 규칙을 만들기 전에이 규칙 만드는 클레임 규칙 집합 먼저 LDAP(Lightweight Directory Access Protocol) \(LDAP\) 특성 클레임 특성 스토어에서 추출 하 하기 전에 함께 제공 되는 규칙에 있는지 확인 합니다. 이 청구 ADFS 1 전송 하기 위해 만든 규칙 입력으로 사용 됩니다. *x*\-compatible 청구 합니다. LDAP 특성 추출 하 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [규칙 클레임으로 전송 LDAP 특성을 만들어](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)합니다.|![클레임 보내려면 ADFS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 보내려면 규칙 1.x 호환 클레임](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

