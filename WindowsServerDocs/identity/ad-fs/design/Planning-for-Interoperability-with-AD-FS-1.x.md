---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: AD FS 1.x와의 상호 운용성 계획
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0bbf64a7bf110e3d73084dd047c84b2b83be8d9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858616"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>AD FS 1.x와의 상호 운용성 계획

Windows server&reg; 2012를 실행 하는 Active Directory Federation Services \(AD FS\) 페더레이션 서버는 windows server 2003 R2 AD FS \(과 함께 설치 된\) 1.0 페더레이션 서비스 및 Windows server 2008 또는 Windows Server 2008 R2 AD FS \(과 함께 설치 된\) 1.1 페더레이션 서비스와 상호 운용할 수 있습니다. 다음과 같은 상호 운용성 조합이 지원됩니다.  

-   모든 AD FS 1입니다. *x* 페더레이션 서비스 Windows Server 2012의 AD FS 페더레이션 서비스에서 사용할 수 있는 클레임을 보낼 수 있습니다. 자세한 내용은 [검사 목록: AD FS 1.x에서 클레임을 사용 하도록 AD FS 구성](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)을 참조 하세요.  

-   Windows Server 2012의 모든 AD FS 페더레이션 서비스 AD FS 1을 보낼 수 있습니다. *x*\-AD FS 1에서 사용할 수 있는 호환 클레임입니다. *x* 페더레이션 서비스입니다. 자세한 내용은 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)를 참조하세요.  

-   Windows Server 2012의 모든 AD FS 페더레이션 서비스 AD FS 1을 보낼 수 있습니다. AD FS 1을 실행 하는 하나 이상의 웹 서버에서 사용할 수 있는 *x*\-호환 클레임입니다. *x* 클레임\-인식 웹 에이전트입니다. 자세한 내용은 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)를 참조하세요.  

> [!NOTE]  
> AD FS은 AD FS 1을 지원 하거나 상호 운용 하지 않습니다. *x* Windows NT 토큰 기반 웹 에이전트.  

AD FS 1입니다. *x*\-호환 클레임은 Windows Server 2012에서 AD FS 페더레이션 서비스에서 전송 하 고 AD FS 1로 인식할 수 있는 클레임입니다. *x* 페더레이션 서비스입니다. AD FS 1입니다. *x* 페더레이션 서비스는 AD FS 페더레이션 서비스 보내는 클레임을 사용할 수 있으며, 이름 식별자 \(ID\) 클레임 유형을 전송 해야 합니다.  

## <a name="understanding-the-name-id-claim-type"></a>이름 ID 클레임 유형 이해  
이름 ID 클레임 유형은 AD FS 1.*x* 에서 사용하는 ID 클레임 유형과 동일합니다. AD FS 1.*x*와 상호 운용하고자 하는 모든 경우에 사용해야 합니다. 이름 ID 클레임 유형은 AD FS 1을 사용 하도록 설정 합니다. *x* 페더레이션 서비스 또는 AD FS 1. *x* 클레임\-인식 웹 에이전트는 다음 표의 이름 ID 형식 중 하나로 전송 되는 경우 Windows Server 2012 전송에서 AD FS 하는 클레임을 사용 합니다.  


|      이름 ID 형식       |               해당 URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* 메일 주소 | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* 메일 UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        일반 이름        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           그룹           |    http://schemas.xmlsoap.org/claims/Group     |

적절한 형식의 이름 ID 클레임 하나만 보내야 합니다. 이 조건을 충족하는 경우 표에 설명된 제한 사항을 준수하는 다른 많은 클레임도 전송될 수 있습니다.  

> [!NOTE]  
> AD FS 1입니다. *x* 페더레이션 서비스는 http://schemas.xmlsoap.org/claims/의 URI\) \(Uniform resource Identifier로 시작 하는 들어오는 클레임 유형만 해석할 수 있습니다.  

## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
