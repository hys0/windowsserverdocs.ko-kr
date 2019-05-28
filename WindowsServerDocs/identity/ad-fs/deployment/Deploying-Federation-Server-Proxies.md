---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: 페더레이션 서버 프록시 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 02311522ee229eeaf0b27ce8d39090a9529b99ae
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192204"
---
# <a name="deploying-federation-server-proxies"></a>페더레이션 서버 프록시 배포

Active Directory Federation Services에서 페더레이션 서버 프록시를 배포 하려면 \(AD FS\), 각 작업의 완료 [검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)합니다.  
  
> [!NOTE]  
> 이 검사를 사용 하는 경우 계획 지침에서 페더레이션 서버 프록시에 대 한 참조를 먼저 읽는 것이 좋습니다 합니다 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 서버를 구성 하는 절차를 시작 하기 전에 합니다. 다음 검사 목록을 서버 프록시 페더레이션에 대 한 디자인 및 배포 프로세스에 대 한 더 나은 이해를 제공 합니다.  
  
## <a name="about-federation-server-proxies"></a>페더레이션 서버 프록시에 대 한  
페더레이션 서버 프록시는 프록시 역할을 수동으로 구성 된 Windows Server® 2012 및 AD FS 소프트웨어를 실행 하는 컴퓨터입니다. 조직에서 페더레이션 서버 프록시를 사용하여 인터넷 클라이언트와 회사 네트워크의 방화벽으로 보호된 페더레이션 서버 간에 중간 서비스를 제공할 수 있습니다.  
  
> [!NOTE]  
> 동일한 컴퓨터에 페더레이션 서버 및 페더레이션 서버 프록시 역할을 설치할 수 없습니다, 있지만 페더레이션 서버가 페더레이션 서버 프록시 기능을 수행할 수 있습니다. 자세한 내용은 [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)를 참조하세요.  
  
Windows Server® 2012 컴퓨터에서 AD FS 소프트웨어를 설치 하 고 프록시 역할에서을 제공 하도록 구성 하면 해당 컴퓨터가 페더레이션 서버 프록시입니다.  
  

