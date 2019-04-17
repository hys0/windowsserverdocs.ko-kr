---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: "Adfs SSL 인증서 등록"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 12f544ad0d037c4ae7a9789238186b7ded311bdf
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Adfs SSL 인증서 등록

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Active Directory Federation Services \(AD FS\) federation 팜 각 federation 서버에서 Secure Socket 계층 \(SSL\) 서버 인증을 위한 인증서가 필요 합니다. 동일한 인증서 농장 각 federation 서버에서 사용할 수 있습니다. 인증서와 개인 키 사용할 수 있어야 합니다. 예를 들어,을 사용 하는 인증서 및 개인 키.pfx 파일의 Active Directory Federation Services 구성 마법사에 직접 파일을 가져올 수 있습니다. 이 SSL 인증서를 포함 해야 합니다.  
  
1.  제목 이름과 대체 주체 이름 fs.contoso.com 등 federation 서비스 이름에 있어야 합니다.  
  
2.  제목 다른 이름 값 있어야 **enterpriseregistration** 이 뒤에 조직에서 사용자 이름 \(UPN\) 접미사 예를 들어, **enterpriseregistration.corp.contoso.com**합니다.  
  
    > [!WARNING]  
    > 디바이스 등록 서비스 \(DRS\) Workplace Join에 대 한 사용 하려는 경우 대체 주체 이름을 지정 합니다.  
  
> [!IMPORTANT]  
> 조직에 사용 하 여 여러 UPN 접미사 DRS 사용 하려는 경우 각 접미사에 대 한 제목을 대체 이름 항목 SSL 인증서 있어야 합니다.  
  
## <a name="see-also"></a>참조 하십시오
[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[지침에 따라 Windows Server 2012 r 2 광고 FS 배포](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Federation 서버 농장 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

