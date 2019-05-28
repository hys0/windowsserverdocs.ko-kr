---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: AD FS 1.x와의 상호 운용성 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7a1082b873f65a9f98b25425a392b2c62de8ca22
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191007"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>AD FS 1.x와의 상호 운용성 계획

Active Directory Federation Services \(AD FS\) Windows Server® 2012를 실행 하는 페더레이션 서버는 AD FS 1.0 상호 운용할 수 있습니다 \(Windows Server 2003 R2와 함께 설치\) 페더레이션 서비스 및 AD FS 1.1 \(Windows Server 2008 또는 Windows Server 2008 R2와 함께 설치\) 페더레이션 서비스입니다. 다음과 같은 상호 운용성 조합이 지원됩니다.  
  
-   모든 AD FS 1입니다. *x* 페더레이션 서비스는 Windows Server 2012의 AD FS 페더레이션 서비스에서 사용할 수 있는 클레임을 전송할 수 있습니다. 자세한 내용은 참조 하세요. [검사 목록: AD FS에서 클레임을 사용 하도록 AD FS 구성 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)합니다.  
  
-   모든 AD FS 페더레이션 서비스 Windows Server 2012에서 AD FS 1을 보낼 수 있습니다. *x*\-AD FS 1에서 사용할 수 있는 호환 클레임. *x* 페더레이션 서비스입니다. 자세한 내용은 참조 하세요. [검사 목록: AD FS 1.x 페더레이션 서비스에 클레임을 보내도록 AD FS 구성](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)합니다.  
  
-   모든 AD FS 페더레이션 서비스 Windows Server 2012에서 AD FS 1을 보낼 수 있습니다. *x*\-AD FS 1을 실행 하는 하나 이상의 웹 서버에서 사용할 수 있는 호환 클레임. *x* 클레임\-인식 웹 에이전트입니다. 자세한 내용은 참조 하세요. [검사 목록: AD FS 1.x 클레임 인식 웹 에이전트에 대 한 클레임을 보내도록 AD FS 구성](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)합니다.  
  
> [!NOTE]  
> AD FS 지원 또는 AD FS 1와 상호 운용 되지 않습니다. *x* Windows NT 토큰 기반 웹 에이전트입니다.  
  
AD FS 1입니다. *x*\-호환 클레임은 Windows Server 2012의 AD FS 페더레이션 서비스에서 전송 하 고 AD FS 1에서 인식할 수 있는 클레임. *x* 페더레이션 서비스입니다. 있도록 AD FS 1. *x* 페더레이션 서비스 이름 식별자 클레임에서 보내는 AD FS 페더레이션 서비스를 사용할 수 있습니다 \(ID\) 클레임 유형을 전송 해야 합니다.  
  
## <a name="understanding-the-nameid-claim-type"></a>이름 ID 클레임 유형 이해  
이름 ID 클레임 유형은 AD FS 1.*x*에서 사용하는 ID 클레임 유형과 동일합니다. AD FS 1.*x*와 상호 운용하고자 하는 모든 경우에 사용해야 합니다. 이름 ID 클레임을 사용 하도록 설정 하거나 AD FS 1를 입력 합니다. *x* 페더레이션 서비스 또는 AD FS 1. *x* 클레임\-이러한 클레임은 다음 표의 이름 ID 형식 중 하나에 전송으로 Windows Server 2012에서 AD FS 보내는 클레임을 사용 하도록 인식 웹 에이전트입니다.  
  
|이름 ID 형식|해당 URI|  
|------------------|---------------------|  
|AD FS 1.*x* 메일 주소|http://schemas.xmlsoap.org/claims/EmailAddress|  
|AD FS 1.*x* 메일 UPN|http://schemas.xmlsoap.org/claims/UPN|  
|일반 이름|http://schemas.xmlsoap.org/claims/CommonName|  
|그룹|http://schemas.xmlsoap.org/claims/Group|  
  
적절한 형식의 이름 ID 클레임 하나만 보내야 합니다. 이 조건을 충족하는 경우 표에 설명된 제한 사항을 준수하는 다른 많은 클레임도 전송될 수 있습니다.  
  
> [!NOTE]  
> AD FS 1입니다. *x* 페더레이션 서비스는 Uniform Resource Identifier를 시작 하는 들어오는 클레임 유형만 해석할 수 있습니다 \(URI\) 의 http://schemas.xmlsoap.org/claims/합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
