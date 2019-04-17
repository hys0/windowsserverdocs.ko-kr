---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: "Adfs의 클레임에 ADFS 구성 목록 1.x"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fe99487d3a770547af36f69722b442d0e2cbb8b1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>검사: 구성 Adfs의 클레임에 ADFS 1.x

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-ad-fs-1x"></a>검사: 구성 Adfs의 클레임에 ADFS 1.x  
이 검사는 ADFS 1 전송한 클레임에 Windows Server 2012에서 Active Directory Federation Services \(AD FS\) Federation 서비스를 구성 하는 데 필요한는 작업이 포함 됩니다. *x* Federation 서비스입니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![Adfs의 클레임 소모](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: Adfs의 클레임에 ADFS 구성 1.x**  
  
||작업|참조|  
|-|--------|-------------|  
|![Adfs의 클레임 사용](media/icon_checkboxo.gif)|Windows Server 2012에서 ADFS 및 이전 버전의 ADFS, 간의 상호 운용성 계획 하 고 클레임 유형 이름 ID 대 한 자세한 내용을 알아보세요.|![Adfs의 클레임 소모](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 상호 운용성 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![Adfs의 클레임 사용](media/icon_checkboxo.gif)|Adfs의 이전 버전와 상호 작용할 수, 하기 전에 먼저 ADFS Federation 서비스에 클레임 공급자 신뢰를 만들어야 합니다. **참고:** ADFS 1 신뢰를 만들 수는 없습니다. *x* federation 메타 데이터를 사용 하 여 Federation 서비스입니다.<br /><br />절차를 사용 하 여 오른쪽에 있는 링크를 신뢰를 설정할 때 추가 클레임 공급자 신뢰 마법사 ADFS 1와 상호 작용 하려면이 신뢰를 설정 하려면 다음을 수행 해야 합니다. *x* Federation 서비스:<br /><br />1.에 **데이터 소스를 선택** 페이지 선택, **Enter 데이터의 사용에 대 한 보안을 수동으로 파티**합니다.<br />2.에 **프로필 선택** 페이지를 선택 하 고 **ADFS 1.0 및 1.1 프로필**합니다.<br />3.에 **구성 URL** 페이지의 **WS\ Federation 수동 URL**, 입력은 **Federation 서비스 endpoint URL** ADFS 1에에서 정의 된 대로 합니다. *x* 파트너의 서비스 Federation 합니다.<br />4.에 **구성 식별자** 페이지의 **클레임 공급자 신뢰 식별자**, 입력은 **Federation 서비스 URI** ADFS 1에에서 정의 된 대로 합니다. *x* 파트너의 서비스 Federation 합니다.|![Adfs의 클레임 소모](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[한 청구 공급자 신뢰 수동으로 만들](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)|  
|![Adfs의 클레임 사용](media/icon_checkboxo.gif)|이전에 만든 클레임 공급자 신뢰를 만들어야 합니다 클레임 규칙을는 Adfs에서 수신 되 고 클레임 창을 놓으면 필터링 또는 이름을 ID 클레임 형식으로 변환 1.x Federation 서비스 및 통과, 합니다.<br /><br />이름을 ID 클레임 입력을 통해 전달 된 필터링 또는 변환 때 사용할 수 다른 규칙 나 규칙 입력으로 이해 하 고 Windows Server 2012에서 ADFS Federation 서비스에서 사용할 수 있도록 합니다.|![Adfs의 클레임을 사용할](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 보내려면 규칙 1.x 호환 클레임](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![Adfs의 클레임 사용](media/icon_checkboxo.gif)|1 Adfs의 관리자에 게 문의 합니다. *x* Federation 서비스 관리자에 게 1 Adfs의 하 고 있습니다. *x* Federation 서비스 새로운 리소스 파트너 신뢰를 설정 합니다. 또한 관리자 해당 Federation 서비스 URI 제공 \ (Federation 서비스 properties\)에서 Federation 서비스 endpoint URL 및 내보낸 token\ 서명 인증서 파일 \ (와 공개 키 only\). 관리자는 보안을 설정 하려면이 항목 필요 합니다.|N\/A|  
  

