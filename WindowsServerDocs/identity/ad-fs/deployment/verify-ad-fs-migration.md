---
title: AD FS 2.0 페더레이션 서버 마이그레이션
description: AD FS 서버를 Windows Server 2012 R2로 마이그레이션하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a3e8e444f715fe2ae0f0ccd858d90e8664be00c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877774"
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>확인 된 AD FS 2.0 Windows Server 2012 R2 마이그레이션

팜에 페더레이션 서버 작동; 지 확인 하려면 다음 절차를 사용할 수 Windows Server 2012 R2로 Active Directory Federation Service (AD FS) 팜의 동일한 서버 마이그레이션을 완료 하면, 즉, 동일한 네트워크에 있는 모든 클라이언트가 federtation 서버를 연결할 수 있습니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터에 대한 **Users**, **Backup Operators**, **Power Users**, **Administrators** 또는 이에 상응하는 구성원 자격이 필요합니다.
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>페더레이션 서버가 작동하는지 확인하려면  
  
1.  브라우저 창을 열고 주소 표시줄에 페더레이션 서버 이름을 입력 하 고 추가 `federationmetadata/2007-06/federationmetadata.xml` 를 페더레이션 서비스 메타 데이터 끝점으로 이동 합니다. 예를 들어 `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` 합니다.  
  
브라우저 창에서 SSL 오류 또는 경고 없이 페더레이션 서버 메타데이터를 볼 수 있는 경우 페더레이션 서버가 작동하는 것입니다.  
  
2.  AD FS 로그인 페이지로 이동할 수도 있습니다(페더레이션 서비스 이름 뒤에 `adfs/ls/idpinitiatedsignon.htm` 추가, 예: `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`).  도메인 관리자 자격 증명으로 로그인할 수 있는 AD FS 로그인 페이지가 표시됩니다.  
  
> [!IMPORTANT]
>  브라우저의 로컬 인트라넷 영역에 페더레이션 서비스 이름(예: `https://fs.contoso.com`)을 추가하여 페더레이션 서버 역할을 신뢰하도록 브라우저 설정을 구성해야 합니다.  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)  
 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)   
 [AD FS 페더레이션 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
