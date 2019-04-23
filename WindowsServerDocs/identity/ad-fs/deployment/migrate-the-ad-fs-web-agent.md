---
title: AD FS 웹 에이전트 마이그레이션
description: Windows Server 2012로 AD FS 웹 에이전트에서 정보를 제공합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 945a5f4cf0e6c491479b095671ff5e77416c6fa3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877594"
---
# <a name="migrate-the-ad-fs-web-agent"></a>AD FS 웹 에이전트 마이그레이션

마이그레이션하려면 AD FS 1.1 Windows 토큰 기반 에이전트 또는 AD FS 1.1 클레임 인식 에이전트를 Windows Server 2008 R2 나 Windows Server 2012, Windows Server 2008에 설치 된 에이전트 중 하나를 호스트 하는 컴퓨터의 운영 체제의 전체 업그레이드를 수행 합니다. Windows Server 2012로 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요. 추가 구성은 필요하지 않습니다.  
  
> [!IMPORTANT]
>  마이그레이션된 AD FS 1.1 Windows 토큰 기반 에이전트는 Windows Server 2008 R2 또는 Windows Server 2008과 함께 설치된 AD FS 1.1 페더레이션 서비스에서만 작동합니다. 자세한 내용은 [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)를 참조하세요.  
>   
>  마이그레이션된 AD FS 1.1 클레임 인식 웹 에이전트는 다음에서 작동합니다.  
>   
>  -   Windows Server 2008 R2 또는 Windows Server 2008과 함께 설치된 AD FS 1.1 페더레이션 서비스  
> -   Windows Server 2008 R2 또는 Windows Server 2008에 설치된 AD FS 2.0 페더레이션 서비스  
> -   Windows Server 2012를 사용 하 여 설치 된 AD FS 페더레이션 서비스  
>   
>  자세한 내용은 [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)를 참조하세요.  
  
  
## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)