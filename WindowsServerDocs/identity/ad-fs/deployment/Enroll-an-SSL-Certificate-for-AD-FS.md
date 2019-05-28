---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: AD FS용 SSL 인증서 등록
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e80927f2670614d2949f4e67cc158319f05c5fa0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192146"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS용 SSL 인증서 등록

Active Directory Federation Services \(AD FS\) Secure Socket Layer 인증서가 필요 \(SSL\) 페더레이션 서버 팜의 각 페더레이션 서버의 서버 인증. 팜의 각 페더레이션 서버에 동일한 인증서를 사용할 수 있습니다. 인증서와 해당 개인 키는 모두 사용할 수 있는 상태여야 합니다. 예를 들어 .pfx 파일에 인증서와 해당 개인 키가 있는 경우 AD FS(Active Directory Federation Services) 구성 마법사에 직접 파일을 가져올 수 있습니다. 이 SSL 인증서에는 다음 사항이 포함되어 있어야 합니다.  
  
1.  주체 이름과 주체 대체 이름에는 fs.contoso.com과 같은 페더레이션 서비스 이름에 포함 해야 합니다.  
  
2.  주체 대체 이름 값을 포함 해야 합니다 **enterpriseregistration** 는 사용자 계정 이름 뒤 \(UPN\) 예를 들어 사용자 조직의 접미사  **enterpriseregistration.corp.contoso.com**합니다.  
  
    > [!WARNING]  
    > Device Registration Service를 사용 하도록 설정 하려는 경우 주체 대체 이름 지정 \(DRS\) 작업 공간 연결에 대 한 합니다.  
  
> [!IMPORTANT]  
> 조직에서 여러 UPN 접미사를 사용 하 고 DRS를 사용 하도록 설정 하려는 경우 SSL 인증서에 각 접미사에 대 한 주체 대체 이름 항목이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목
[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

