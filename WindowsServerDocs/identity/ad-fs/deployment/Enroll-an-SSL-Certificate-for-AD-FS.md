---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: AD FS용 SSL 인증서 등록
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: efa7c7aee848a5bbb68d3ce7140e135d37c2161d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408366"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>AD FS용 SSL 인증서 등록

Active Directory Federation Services \(AD FS @ no__t-1에는 페더레이션 서버 팜의 각 페더레이션 서버에서 보안 소켓 계층 \(SSL @ no__t 서버 인증에 대 한 인증서가 필요 합니다. 팜의 각 페더레이션 서버에서 동일한 인증서를 사용할 수 있습니다. 인증서와 해당 프라이빗 키는 모두 사용할 수 있는 상태여야 합니다. 예를 들어 .pfx 파일에 인증서와 해당 프라이빗 키가 있는 경우 AD FS(Active Directory Federation Services) 구성 마법사에 직접 파일을 가져올 수 있습니다. 이 SSL 인증서에는 다음 사항이 포함되어 있어야 합니다.  
  
1.  주체 이름과 주체 대체 이름에는 fs.contoso.com와 같은 페더레이션 서비스 이름이 포함 되어야 합니다.  
  
2.  주체 대체 이름에는 **enterpriseregistration** 값을 포함 해야 하며, 그 다음에는 조직의 사용자 계정 이름 \(upn @ no__t-2 접미사 (예: **enterpriseregistration.corp.contoso.com**)가 포함 되어야 합니다.  
  
    > [!WARNING]  
    > 장치 등록 서비스를 사용 하도록 설정 하려는 경우 주체 대체 이름을 지정 \(DRS @ no__t-1 Workplace Join.  
  
> [!IMPORTANT]  
> 조직에서 여러 UPN 접미사를 사용 하는 경우 DRS를 사용 하도록 설정 하려는 경우 SSL 인증서에는 각 접미사에 대 한 주체 대체 이름 항목이 포함 되어야 합니다.  
  
## <a name="see-also"></a>관련 항목
[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  

