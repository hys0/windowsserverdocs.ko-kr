---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: "Adfs의 상호 운용성 계획 1.x"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f287261ce6cb56e40385ef4de922045153819a23
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Adfs의 상호 운용성 계획 1.x

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모두 ADFS 1.0와 상호 작용할 수의 Active Directory Federation Services \(AD FS\) federation 서버® Windows Server 2012를 실행 \ (Windows Server 2003 R2\ 함께 설치) Federation 서비스 및 ADFS 1.1 \ (Windows Server 2008 또는 Windows Server 2008 R2\ 설치) Federation 서비스입니다. 다음 상호 운용성 조합을 지원 됩니다.  
  
-   모든 ADFS 1입니다. *x* Federation 서비스는 ADFS Federation 서비스 Windows Server 2012에서 사용할 수 있는 클레임 보낼 수 있습니다. 자세한 내용은 참조 [검사: Adfs의 소모 청구 발생 시에도 ADFS 구성 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)합니다.  
  
-   모든 ADFS Federation 서비스 Windows Server 2012에서 ADFS 1 보낼 수 있습니다. *x*ADFS 1 사용할 수 있는 \-compatible 청구 합니다. *x* Federation 서비스입니다. 자세한 내용은 참조 [검사: 클레임 ADFS 전송 ADFS 구성 1.x Federation 서비스](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)합니다.  
  
-   모든 ADFS Federation 서비스 Windows Server 2012에서 ADFS 1 보낼 수 있습니다. *x*ADFS 1 실행 하는 하나 이상의 웹 서버에서 사용할 수 있는 \-compatible 청구 합니다. *x* claims\ 인식 웹 에이전트 합니다. 자세한 내용은 참조 [검사: 클레임 ADFS 전송 ADFS 구성 1.x 클레임 인식 웹 에이전트](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)합니다.  
  
> [!NOTE]  
> ADFS 지원 되지 않거나 1 Adfs와 상호 작용 합니다. *x* 토큰 기반 웹 에이전트 Windows NT 합니다.  
  
ADFS 1입니다. *x*\-compatible 클레임은 청구 된 ADFS Federation 서비스 Windows Server 2012에서에서 보내고 ADFS 1 인식할 수 있습니다. *x* Federation 서비스입니다. 되도록 ADFS 1. *x* Federation 서비스 ADFS Federation 서비스는 사용자가 전송 청구를 사용할 수 있는 이름 식별자 \(ID\) 클레임 유형 전송 해야 합니다.  
  
## <a name="understanding-the-name-id-claim-type"></a>이해 이름을 ID 클레임 유형  
이름을 ID 클레임 유형은 id 클레임에 해당 하는 해당 ADFS 1 입력 합니다. *x* uses. ADFS 1와 상호 작용 언제 사용 해야 합니다. *x*. 이름을 ID 클레임 사용 하거나 ADFS 1를 입력 합니다. *x* Federation 서비스 또는 ADFS 1. *x* claims\ 인식 웹 에이전트 다음 표에 있는 ID 이름 형식은 중 하나에 전송 될 이러한으로 ADFS Windows Server 2012에서 보내는 클레임을 사용할 수 있습니다.  
  
|ID 이름 형식|해당 URI|  
|------------------|---------------------|  
|ADFS 1입니다. *x* 메일 주소|http://schemas.xmlsoap.org/claims/EmailAddress|  
|ADFS 1입니다. *x* UPN 메일|http://schemas.xmlsoap.org/claims/UPN|  
|일반 이름|http://schemas.xmlsoap.org/claims/CommonName|  
|그룹|http://schemas.xmlsoap.org/claims/Group|  
  
적절 한 형식 하나만 이름을 ID 클레임 전송 해야 합니다. 이 조건을 충족 하는 경우 가정 표에 설명 제한 사항을 준수 하 고 다른 여러 청구도 전송 수 있습니다.  
  
> [!NOTE]  
> ADFS 1입니다. *x* Federation 서비스의 http://schemas.xmlsoap.org/claims/ Uniform 리소스 식별자 \(URI\)로 시작 하는 수신 클레임 유형 해석 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
