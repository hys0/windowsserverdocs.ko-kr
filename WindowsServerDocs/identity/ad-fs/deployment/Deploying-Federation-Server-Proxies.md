---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: 페더레이션 서버 프록시 배포
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c6af319283de72963691ae3e91c3db5992bdec72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408402"
---
# <a name="deploying-federation-server-proxies"></a>페더레이션 서버 프록시 배포

Active Directory Federation Services \(AD FS\)에서 페더레이션 서버 프록시를 배포 하려면 [검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)에서 각 작업을 완료 합니다.  
  
> [!NOTE]  
> 이 검사 목록을 사용 하는 경우 서버를 구성 하는 절차를 시작 하기 전에 먼저 [Windows server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 에서 페더레이션 서버 프록시 계획 지침에 대 한 참조를 읽어 보는 것이 좋습니다. 검사 목록에 따라 페더레이션 서버 프록시에 대 한 디자인 및 배포 프로세스를 보다 잘 이해할 수가 있습니다.  
  
## <a name="about-federation-server-proxies"></a>페더레이션 서버 프록시 정보  
페더레이션 서버 프록시는 프록시 역할을 수행 하도록 수동으로 구성 된 Windows Server® 2012 및 AD FS 소프트웨어를 실행 하는 컴퓨터입니다. 조직에서 페더레이션 서버 프록시를 사용하여 인터넷 클라이언트와 회사 네트워크의 방화벽으로 보호된 페더레이션 서버 간에 중간 서비스를 제공할 수 있습니다.  
  
> [!NOTE]  
> 페더레이션 서버와 페더레이션 서버 프록시 역할은 동일한 컴퓨터에 설치할 수 없지만 페더레이션 서버는 페더레이션 서버 프록시 기능을 수행할 수 있습니다. 자세한 내용은 [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)를 참조하세요.  
  
Windows Server® 2012 컴퓨터에 AD FS 소프트웨어를 설치 하 고 프록시 역할을 수행 하도록 구성 하는 작업은 해당 컴퓨터에 페더레이션 서버 프록시를 제공 합니다.  
  

