---
title: "ADFS 2.0 federation server를 마이그레이션해야"
description: "Windows Server 2012 r 2에는 ADFS 서버에 정보를 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a3e8e444f715fe2ae0f0ccd858d90e8664be00c
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2017
---
# <a name="verify-the-ad-fs-20-migration-to-windows-server-2012-r2"></a>AD 확인 FS 2.0 마이그레이션을 Windows Server 2012 r 2

Federation 서버에 농장의 운영, 있는지 확인 다음 절차를 사용할 수 사용자 Active Directory Federation 서비스 (ADFS) 팜 Windows Server 2012 r 2에 동일한 서버 마이그레이션을 완료 되 면 즉, 모든 클라이언트 동일한 네트워크에 federtation 서버에 연결할 수 있습니다.  
  
회원 **사용자**, **백업 운영자**, **고급 사용자**, **관리자** 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.
  
### <a name="to-verify-that-a-federation-server-is-operational"></a>Federation 서버가 작동 하는지 확인 하려면  
  
1.  브라우저 창 열기 및 주소 표시줄에 federation 서버 이름 입력 한 다음 사용 하 여 추가 `federationmetadata/2007-06/federationmetadata.xml` federation 서비스 메타 데이터 끝점 찾아볼 수 있습니다. 예를 들어, `https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml` 합니다.  
  
브라우저 창에서 없이 SSL 오류나 경고 federation 서버 메타 데이터를 볼 수를 하는 경우 해당 federation 서버 작동있지 않습니다.  
  
2.  ADFS 로그인 페이지를 찾아볼 수 있습니다 (federation 서비스 이름이 추가 된 `adfs/ls/idpinitiatedsignon.htm`예를 들어, `https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm`).  이 페이지를 표시는 ADFS 로그인 도메인 관리자 자격 증명으로 로그인 할 수 있습니다.  
  
> [!IMPORTANT]
>  Federation 서비스 이름 추가 하 여 federation 서버 역할 신뢰 하 여 브라우저 설정을 구성 하 않도록 (예를 들어, `https://fs.contoso.com`) 브라우저의 로컬 인트라넷 영역 합니다.  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 r 2 Active Directory Federation Services 역할 서비스 마이그레이션을](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [광고 FS Federation 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)  
 [마이그레이션 광고 FS Federation 서버](migrate-ad-fs-fed-server-r2.md)   
 [AD FS Federation 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
