---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: "Adfs의 클레임에 ADFS 구성 목록 1.x"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdfd06a28f8ccaa04014024a235cd19512adb181
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>구성 클레임은 ADFS 1.x Federation 서비스에 전송 ADFS 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>검사: 구성 클레임 ADFS 보내려면 ADFS 1.x Federation 서비스  
이 검사는 Windows Server 2012 ADFS 1 이해할 수 있는 클레임 보낼 수의 Active Directory Federation Services \(AD FS\) Federation 서비스 구성 하는 데 필요한는 작업이 포함 됩니다. *x* Federation 서비스입니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![클레임 보내려면 ADFS 구성](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 클레임 ADFS 보내려면 ADFS 구성 1.x Federation 서비스**  
  
||작업|참조|  
|-|--------|-------------|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|Adfs의 이전 버전의 Windows Server 2012 ADFS 간의 상호 운용성 계획 하 고 클레임 유형 이름 ID 대 한 자세한 내용을 알아보세요.|![클레임 보내려면 ADFS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 상호 운용성 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|Adfs의 이전 버전의 상호 운용성을 실현 하기 전에 먼저 ADFS 1에 ADFS Federation 서비스에서 신뢰 파티 보안을 만들어야 합니다. *x* Federation 서비스입니다. **참고:** ADFS 1 신뢰를 만들 수는 없습니다. *x* federation 메타 데이터를 사용 하 여 Federation 서비스입니다.<br /><br />절차를 사용 하 여 오른쪽에 있는 링크를 신뢰를 설정할 때 추가 의존 파티 신뢰 마법사에서 ADFS 1와 상호 작용 하려면이 신뢰를 설정 하려면 다음을 수행 해야 합니다. *x* Federation 서비스:<br /><br />1.에 **데이터 소스를 선택** 페이지 선택, **Enter 데이터의 사용에 대 한 보안을 수동으로 파티**합니다.<br />2.에 **프로필 선택** 페이지를 선택 하 고 **ADFS 1.0 및 1.1 프로필**합니다.<br />3.에 **구성 URL** 페이지의 **WS\ Federation 수동 URL**, 입력은 **Federation 서비스 endpoint URL** ADFS 1에에서 정의 된 대로 합니다. *x* 파트너의 서비스 Federation 합니다.<br />4.에 **구성 식별자** 페이지의 **Relying 일부 신뢰 식별자**, 입력은 **Federation 서비스 URI** ADFS 1에에서 정의 된 대로 합니다. *x* 파트너의 서비스 Federation 합니다.|![클레임 보내려면 ADFS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[필요로 하 파티 신뢰 수동으로 만들](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|이전에 만든 신뢰 파티 신뢰에서 특성 스토어에서 추출 된 들어오는 클레임 수행 하 고 통과, 필터링 되거나 이름 ID로 변환는 규칙 클레임 이해 하 고 AD에서 사용할 수 있는 유형 클레임 만들어야 FS 1. *x* Federation 서비스입니다. **참고:** 이 규칙을 만들기 전에이 규칙 만드는 클레임 규칙 집합 먼저 LDAP(Lightweight Directory Access Protocol) \(LDAP\) 특성 클레임 특성 스토어에서 추출 하 하기 전에 함께 제공 되는 규칙에 있는지 확인 합니다. 이 청구 ADFS 1 전송 하기 위해 만든 규칙 입력으로 사용 됩니다. *x*\-compatible 청구 합니다. LDAP 특성 추출 하 규칙을 만드는 방법에 대 한 자세한 내용은 참조 [규칙 클레임으로 전송 LDAP 특성을 만들어](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)합니다.|![클레임 보내려면 ADFS 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 보내려면 규칙 1.x 호환 클레임](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![클레임 보내려면 ADFS 구성](media/icon_checkboxo.gif)|1 Adfs의 관리자에 게 문의 합니다. *x* Federation 서비스 관리자에 게 1 Adfs의 하 고 있습니다. *x* Federation 서비스 새 계정 파트너 신뢰를 설정 합니다. 또한 관리자 해당 Federation 서비스 URI 제공 \ (Federation 서비스 properties\)에서 WS\ Federation 수동 끝점 URL \ (Federation 서비스 끝점 URL\), 내보낸 token\ 서명 인증서 파일 및 \ (와 공개 키 only\). 해당 관리자는 보안을 설정 하려면이 항목 필요 합니다.|N\/A|  
  

